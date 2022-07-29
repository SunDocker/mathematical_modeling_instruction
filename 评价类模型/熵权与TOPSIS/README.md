## 2 熵权与TOPSIS

### 2.1 熵权法

> 主要是用来确定某一个指标的**权重**的，依据的原理是指标的**变异程度**越小，所反映的信息量也越少，其对应的权值也应该越低

<img src="README.assets/image-20220725103607608.png" alt="image-20220725103607608" style="zoom:67%;" />

- 如果出现了负数，要重新标准化到**非负区间**

  > 当然如果有0的话，ln那一项直接让它为0即可，使用`np.nansum`可以做到

- X是矩阵，m个要评价的对象，n个评价指标，目标是要求这组数据应该有的**权重**

  > 注意，**一列**是一个**评价指标**的所有取值

  > 这组数据应该已经**正向化**过了，并且最好将其标准化/归一到[0, 1]内，就是用图中的公式

- p~ij~是**概率矩阵**

- 在数据归一化中，**越大越好**的用第一种（min-max归一化/规约化）

  > 如果没有提前正向化，越小越好的还需要用1减去min-amx归一化的结果，这样就转化成了**越大越好**的

- 图中那个n和k是评价指标的个数，写得可以说是很不标准了

Python代码实现：

```python
def entropy_weight(data):
    # 假设data已经正向化过了
    data = np.array(data)
    print(data)
    # 归一化
    data = (data - data.min(axis=0)) / (data.max(axis=0) - data.min(axis=0))
    print(data)
    # 概率矩阵
    p = data / data.sum(axis=0)
    # 信息熵
    E = - np.nansum(p * np.log(p), axis=0) / np.log(len(data[0]))
    # 熵权
    return (1 - E) / (1 - E).sum()
```

### 2.2 TOPSIS分析

TOPSIS的想法就是，通过一定的计算，评估方案系统中任何一个方案**距离理想最优解和最劣解的综合距离**。如果一个方案距离理想最优解越近，距离最劣解越远，我们就有理由认为这个方案更好。

那理想最优解和最劣解又是什么呢？很简单，理想最优解就是该理想最优方案的**各指标值都取到系统中评价指标的最优值**，最劣解就是该理想最劣方案的各指标值都取到系统中评价指标的最劣值。

<img src="README.assets/image-20220725110406086.png" alt="image-20220725110406086" style="zoom:67%;" />

> 与层次分析法对比，TOPSIS方法是**自底向上**的
>
> TOPSIS是先有每个**方案**的各项**准则**指标，然后对指标数据进行**预处理**，每个方案的各项指标构成一个行向量，再把行向量堆起来，从而形成了下面提到的**评分矩阵Z**（注意这个时候还没涉及到**权重**）

#### 2.2.1 数据预处理

> TOPSIS分析法的第一步；
>
> 注意，这不是归一，还没有对各项指标进行归一呢

1. 指标**正向化**：

  > 当然正向化的同时让数据落到[0,1]内更好

  在处理数据时，有些指标的数据**越大越好**，有些则是越小越好，有些又是中间某个值或者某段区间最好。我们可以对其进行“正向化处理”，使指标都可以像考试分数那样，**越大越好**。

  <img src="README.assets/image-20220725110934427.png" alt="image-20220725110934427" style="zoom:67%;" />

  > 对于区间型和中值型也要区分是离区间/中值近一点好还是远一点好；
  >
  > 有的时候也可以用$\frac 1X$去正向化

  > 区间型的那个$M=max\{a-min\{x_i\},max\{x_i\}-b\}$
  >
  > **<u>中值型最下面那个公式，分子上应该有一个绝对值</u>**

  > 常见的说法：
  >
  > - 效益型指标：极大型
  > - 成本型指标：极小型
  > - 区间型指标：区间型

2. 指标无量纲化（标准化）：

  为了消除不同的数据指标量纲的影响，我们还有必要对已经正向化的矩阵进行标准化。

  - 比较常用的是**每一项除以这一列的平方和开根号**

  - Z-score规约就是一种方法
  - $\frac X{\sqrt{2X^2}}$也可以

Python数据正向化：

```python
import numpy as np
# 数据正向化：极大极小型、区间型、中值型
# idx：第几个指标是这个类型的
def standard(data, max_idx, min_idx, range_idx, range_description, mid_idx, mid_description):
    data = np.array(data)
    
#     for i in max_idx:
#         data[:,i] = (data[:,i] - data[:,i].min()) / (data[:,i].max() - data[:,i].min())
        
    for i in min_idx:
#         data[:,i] = (data[:,i].max() - data[:,i]) / (data[:,i].max() - data[:,i].min())
        data[:,i] = data[:,i].max() - data[:,i]
        
    range_des_idx = 0
    for i in range_idx:
        a = range_description[range_des_idx][0]
        b = range_description[range_des_idx][1]
        M = np.max([a - data[:,i].min(), data[:,i].max() - b])
        data[:,i] = np.where(data[:,i]<a, 1 - (a-data[:,i])/M, data[:,i])
        data[:,i] = np.where(np.logical_and(a<=data[:,i],data[:,i]<=b), 1, data[:,i])
        data[:,i] = np.where(data[:,i]>b, 1 - (data[:,i]-b)/M, data[:,i])
        range_des_idx += 1
    
    mid_des_idx = 0
    for i in mid_idx:
        best = mid_description[mid_des_idx]
        M = np.abs(data[:,i] - best).max()
        data[:,i] = 1 - np.abs(data[:,i] - best)/M
        mid_des_idx += 1
    return data
```

#### 2.2.2 评分

最优解/最劣解其实就是每个指明都取所有方案中能达到的最优/最劣的

<img src="README.assets/image-20220725112110986.png" alt="image-20220725112110986" style="zoom:80%;" />

<img src="README.assets/image-20220725165040429.png" alt="image-20220725165040429" style="zoom:70%;" />

> 先**求距离**，再**概率归一化**

#### 2.2.3 总结

![image-20220725112101019](README.assets/image-20220725112101019.png)

![image-20220725163011957](README.assets/image-20220725163011957.png)

> 如果要**加权**的话，就把d换成下面的D
>
> ![image-20220725163523462](README.assets/image-20220725163523462.png)
>
> **熵权法**就可以用来获得一个较为合理的权重，后面还会讲一种方法

#### 2.2.4 Python代码实现

```python
import numpy as np

# 从numpy-熵权法那里抄过来的
def entropy_weight(data):
    # 假设data已经正向化过了
    data = np.array(data)
    # 概率矩阵
    p = data / data.sum(axis=0)
    # 信息熵
    E = - np.nansum(p * np.log(p), axis=0) / np.log(len(data[0]))
    # 熵权
    return (1 - E) / (1 - E).sum()

# 从numpy-数据预处理那里抄过来的
def standard(data, max_idx, min_idx, range_idx, range_description, mid_idx, mid_description):
    data = np.array(data)
        
    for i in min_idx:
        data[:,i] = data[:,i].max() - data[:,i]
        
    range_des_idx = 0
    for i in range_idx:
        a = range_description[range_des_idx][0]
        b = range_description[range_des_idx][1]
        M = np.max([a - data[:,i].min(), data[:,i].max() - b])
        data[:,i] = np.where(data[:,i]<a, 1 - (a-data[:,i])/M, data[:,i])
        data[:,i] = np.where(np.logical_and(a<=data[:,i],data[:,i]<=b), 1, data[:,i])
        data[:,i] = np.where(data[:,i]>b, 1 - (data[:,i]-b)/M, data[:,i])
        range_des_idx += 1
    
    mid_des_idx = 0
    for i in mid_idx:
        best = mid_description[mid_des_idx]
        M = np.abs(data[:,i] - best).max()
        data[:,i] = 1 - np.abs(data[:,i] - best)/M
        mid_des_idx += 1
    return data

# 假设数据已经预处理过了
def topsis(data, weight=None):
    data = np.array(data)
    # 标准化（可能不需要）
    data = data / np.sqrt((data**2).sum(axis=0))
    # 最优最劣
    z_max = data.max(axis=0)
    z_min = data.min(axis=0)
    # 权重
    w = entropy_weight(data) if weight is None else np.array(weight)
    # 距离
    d_max = np.sqrt((w*(data - z_max)**2).sum(axis=1))
    d_min = np.sqrt((w*(data - z_min)**2).sum(axis=1))
    # 得分
    s = d_min / (d_max + d_min)
    # 归一化
    s = s / s.sum()
    return s, w

data = [
    [4.69, 6.59, 51, 11.94],
    [2.03, 7.86, 19,  6.46],
    [9.11, 6.31, 46,  8.91],
    [8.61, 7.05, 46, 26.43],
    [7.13, 6.5,  50, 23.57],
    [2.39, 6.77, 38, 24.62],
    [7.69, 6.79, 38,  6.01],
    [9.3,  6.81, 27, 31.57],
    [5.45, 7.62, 5,  18.46],
    [6.19, 7.27, 17,  7.51],
    [7.93, 7.53, 9,   6.52],
    [4.4,  7.28, 17,  25.3],
    [7.46, 8.24, 23, 14.42],
    [2.01, 5.55, 47, 26.31],
    [2.04, 6.4,  23, 17.91],
    [7.73, 6.14, 52, 15.72],
    [6.35, 7.58, 25, 29.46],
    [8.29, 8.41, 39, 12.02],
    [3.54, 7.27, 54,  3.16],
    [7.44, 6.26, 8,  28.41],
]
max_idx = [0]
min_idx = [2]
range_idx = [3]
range_description = [[10, 20]]
mid_idx = [1]
mid_description = [7]

data = standard(data, max_idx, min_idx, range_idx, range_description, mid_idx, mid_description)
topsis(data, [1, 1, 1, 1]) #暂不考虑权重
```

#### 2.2.5 具体案例

那个是预期毕业率