# 2 非线性规划模型

### 2.1 概述

相比于线性问题：

- 在线性规划的基础上，**目标函数**可以非线性，**限制条件**可以非线性，包括非线性的不等式和非线性的等式。

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220711222758413.png" alt="image-20220711222758413" style="zoom:80%;" />

### 2.2 二次规划问题

#### 2.2.1 二次规划的基本形式

目标函数形式如果是一个二次函数那就是一个二次规划：

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220711222949616.png" alt="image-20220711222949616" style="zoom:80%;" />

#### 2.2.2 数学知识补充

多元函数的微分：

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220711223507105.png" alt="image-20220711223507105" style="zoom:80%;" />

多元函数的极值求解：

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220711223528789.png" alt="image-20220711223528789" style="zoom:80%;" />

拉格朗日乘子法与KKT：

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220711223637049.png" alt="image-20220711223637049" style="zoom:80%;" />

- 用**KKT条件**处理不等式约束

  > 之前学过，引入**松弛变量**也可以处理不等式约束；
  >
  > 这里使用KKT条件，没有讲解原理，直接套用即可

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220711223754891.png" alt="image-20220711223754891" style="zoom:80%;" />

> $\mu g(X^*)=0$是为了不让不等式条件影响到极值

#### 2.2.3 二次规划的求解举例

数学描述举例：

![image-20220711224328428](%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220711224328428.png)

**KKT条件是求解线束优化问题的通用方法**

实际场景举例：

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220712101056401.png" alt="image-20220712101056401" style="zoom:80%;" />

- scipy求解：

  > 官方文档：
  >
  > https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.minimize.html

  ```python
  from scipy.optimize import minimize
  import numpy as np
  
  
  def func(x):
      return 10.5 + 0.3 * x[0] + 0.32 * x[1] + 0.32 * x[2] + 0.0007 * x[0] ** 2 + 0.0004 * x[1] ** 2 + 0.00045 * x[2] ** 2
  
  
  cons = ({'type': 'eq', 'fun': lambda x: x[0] + x[1] + x[2] - 700})
  b1, b2, b3 = (100, 200), (120, 250), (150, 300)
  x0 = np.array([100, 200, 400])  # 初始猜测解
  res = minimize(func, x0, bounds=(b1, b2, b3), constraints=cons)
  print(res)
  ```

  > 注：关于`method`参数
  >
  > - Method BFGS cannot handle constraints nor bounds.
  > - Method L-BFGS-B cannot handle constraints.
  > - ...
  >
  > 所以还是建议保持默认，这样会根据是否有条件约束和变量约束来选择合适的方法

  - res.fun：最优解
  - res.hess_inv：偏导数
  - res.jac：梯度
  - res.x：最优解

- 遗传算法求解：之后再次遇到遗传算法，再认真学一遍

  > 要先`pip install scikit-opt`

  ```python
  from sko.GA import GA
  
  
  def func(x):
      return 10.5 + 0.3 * x[0] + 0.32 * x[1] + 0.32 * x[2] + 0.0007 * x[0] ** 2 + 0.0004 * x[1] ** 2 + 0.00045 * x[2] ** 2
  
  
  def cons_eq(x):
      return x[0] + x[1] + x[2] - 700
  
  
  ga = GA(func=func, n_dim=3, size_pop=500, max_iter=1000, constraint_eq=(cons_eq,),
          lb=[100, 120, 150], ub=[200, 250, 300])
  print(ga.run())
  ```


### 2.3 非线性规划案例

#### 2.3.1 案例1

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220712110308522.png" alt="image-20220712110308522" style="zoom:80%;" />

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220712110733396.png" alt="image-20220712110733396" style="zoom:80%;" />

> 如果将不等号改成等号，模型的效果会变好吗？

#### 2.3.2 案例2

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220712110830497.png" alt="image-20220712110830497" style="zoom:67%;" />

- 刚性约束与柔性约束

<img src="%E9%9D%9E%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220712205854848.png" alt="image-20220712205854848" style="zoom:67%;" />

- 用**未满误差**和**过盈误差**来描述“不超过”和“**尽可能**”

  > 在本题中，“不超过”的两个约束都是**刚性约束**，“尽可能”的那个约束是**柔性约束**

  > :star:用在等式中的实际的数量，都是：$可计算数量+未满误差-过盈误差$，
  >
  > - 如果是刚性约束，就是只让未满的或过盈的达到极小值
  > - 如果是柔性约束，就是让$未满误差-过盈误差$达到极小值

- 引入了松弛变量，就可以大胆使用等式了

<img src="%E5%87%BD%E6%95%B0%E6%9E%81%E5%80%BC%E4%B8%8E%E8%A7%84%E5%88%92%E6%A8%A1%E5%9E%8B.assets/image-20220712210014570.png" alt="image-20220712210014570" style="zoom:67%;" />