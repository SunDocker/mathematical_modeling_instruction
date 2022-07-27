# 微分方程与差分方程模型

## 1 微分方程的理论基础

### 1.1 微分

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713181409775.png" alt="image-20220713181409775" style="zoom:67%;" />

### 1.2 导数

一阶导数：

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713181431593.png" alt="image-20220713181431593" style="zoom:67%;" />

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713181445158.png" alt="image-20220713181445158" style="zoom:67%;" />

> 右边的图是$y=\frac1{1+e^x}$，其导数为$y'=y(1-y)$

高阶导数：

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713181512055.png" alt="image-20220713181512055" style="zoom:67%;" />

### 1.3 泰勒公式

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713181849716.png" alt="image-20220713181849716" style="zoom:67%;" />

### 1.4 常微分方程

一元常微分方程：

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713182229002.png" alt="image-20220713182229002" style="zoom:67%;" />

一阶常微分方程：

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713182251032.png" alt="image-20220713182251032" style="zoom:67%;" />

- 一阶常微分方程的通解形式：

  <img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713182532377.png" alt="image-20220713182532377" style="zoom:67%;" />

二阶常微分方程：

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713182707165.png" alt="image-20220713182707165" style="zoom:67%;" />

- 二阶常微分方程的通解形式：

  <img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713182907769.png" alt="image-20220713182907769" style="zoom:67%;" />

  > 差分方程举例：
  >
  > <img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713183004232.png" alt="image-20220713183004232" style="zoom:67%;" />

  <img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713183042333.png" alt="image-20220713183042333" style="zoom:80%;" />

  正确性证明：

  <img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713183218672.png" alt="image-20220713183218672" style="zoom:67%;" />

- 二阶常微分方程的特解：

  <img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713183352220.png" alt="image-20220713183352220" style="zoom:80%;" />

  <img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220713183415309.png" alt="image-20220713183415309" style="zoom:67%;" />

## 2 常微分方程的python求解

[常微分方程的python求解](常微分方程的python求解/README.md)

## 3 常/偏微分方程(组)及python求解

### 3.1 相关数学知识

多元函数：有序对集到数集的映射

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220720105928598.png" alt="image-20220720105928598" style="zoom:80%;" />

多元函数的偏微分：**主元**法

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220720110757394.png" alt="image-20220720110757394" style="zoom:80%;" />

多元函数的偏微分方程：$u(X),X=[x_1,x_2,...,x_n]$

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220720111226462.png" alt="image-20220720111226462" style="zoom:80%;" />

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220720111911415.png" alt="image-20220720111911415" style="zoom:80%;" />

多元函数的常/偏微分方程组：

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220720112133592.png" alt="image-20220720112133592" style="zoom:80%;" />

### 3.2 python求解

在Python环境下搭建，一是采用基于基本原理自己写相关 函数，这样操作比较繁琐，但是对于整个的求解过程会比 较清晰明了。

第二就是利用python下面的ode（ordinary differential equation）求解包，熟悉相关的输入输出，就可以完成数值求解。基于这个demo，在不同方向领域可以套用不同的微分方程组模型，进行仿真求解。无论是常微分方程组还是偏微分方程组，使用的都是同一套思路， 就是用**差分代替微分**。

> 具体api调用方式见`scipy.ipynb`

<u>**python求解常微分方程组**</u>：

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220720142605086.png" alt="image-20220720142605086" style="zoom:80%;" />

```python
from scipy.integrate import solve_ivp
from numpy import arange
def func(t, w):
    x = w[0]
    y = w[1]
    z = w[2]
    return [2*x - 3*y + 3*z, 4*x - 5*y +3*z, 4*x - 4*y + 2*z]
t_span = (0, 10)
w0array = [1, 2, 1]
teval = arange(1, 10, 1)
solve_ivp(func, t_span, w0array, t_eval=teval)
# solve_ivp(func, t_span, w0array)
```

> 图的话，学了matplotlib之后再画吧

<img src="%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%B8%8E%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%A8%A1%E5%9E%8B.assets/image-20220720143354523.png" alt="image-20220720143354523" style="zoom:80%;" />

```python
from scipy.integrate import solve_ivp
from numpy import arange
import matplotlib.pyplot as plt
from jupyterthemes import jtplot
jtplot.style()
def func(t, w):
    x = w[0]
    y = w[1]
    return [-x**3 - y, -y**3 + x]
tspan = (0, 100)
w0vector = [1, 0.5]
teval = arange(0, 100, 1)
yy = solve_ivp(func, tspan, w0vector, t_eval=teval)
t = yy.t
data = yy.y
plt.rcParams['font.sans-serif'] = ['Microsoft YaHei']
plt.plot(t, data[0, :])
plt.plot(t, data[1, :])
plt.xlabel("时间s")
plt.show()
```

<u>python求解偏微分方程(组)</u>：没讲？？？

## 4 微分方程案例

[微分方程案例](微分方程案例/README.md)

## 5 差分方程与数值方法

[差分方程与数值方法](差分方程与数值方法/README.md)

## 6 数学建模的程序编写

### 6.1 数学建模程序的种类

- 数值计算
- 绘图

### 6.2 数值计算

- 文件读写
- 基本程序流程设计
- 使用面向对象的编程思想：封装
- 尝试复现经典算法（再说吧）
- 尽可能调用现成的工具包和代码
  - 自己之前写过的可以积累起来，改改就用
  - 网上找的代码资源（CSDN、知乎、博客园、简书、githubgitee）
- 尽可能节约时间和空间，并行化计算会比循环更快
  - 使用`numpy pandas`等
  - 利用数据结构加快速度，如`dict`读取的速度较快
