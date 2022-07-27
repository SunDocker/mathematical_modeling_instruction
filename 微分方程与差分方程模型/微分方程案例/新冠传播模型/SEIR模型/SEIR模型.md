#### 4.3.4 SEIR模型

SEIR 模型考虑存在易感者（Susceptible）、暴露者（Exposed）、患病者（Infectious）和康复者（Recovered）四类人群，适用于具**有潜伏期**、**治愈后获得终身免疫的传染病**。**易感者（S 类）被感染后成为潜伏者（E类）**，随后发病成为患病者（I 类），治愈后成为康复者（R类）。这种情况更为复杂，也更为接近实际情况。

**易感者（S 类）与患病者（I 类）有效接触即变为暴露者（E 类）**，暴露者（E 类）经过平均潜伏期后成为患病者（I 类）；患病者（I 类）可被治愈，治愈后变为康复者（R 类）；康复者（R 类）获得终身免疫不再易感

<img src="SEIR%E6%A8%A1%E5%9E%8B.assets/image-20220720191741562.png" alt="image-20220720191741562" style="zoom:67%;" />

增加常量**日发病率**$\delta$：**每天发病成为患者的潜伏者占潜伏者总数的比例**

微分方程：
$$
\begin{cases}
N\frac{ds}{dt}=-Ni(t)\lambda s(t)\\
N\frac{de}{dt}=Ni(t)\lambda s(t)-Ne(t)\delta\\
N\frac{di}{dt}=Ne(t)\delta-Ni(t)\mu\\
s(t)+e(t)+i(t)+r(t)=1
\end{cases}
$$

> 这里是对s、e、i列方程：
>
> - s减少量的等式：虽然引入了疑似病例，但引起易感人群数量变化的**因素**还是感染者，**本质没有变**，所以方程也没变
> - e和i的增量等式：都有两个影响因素，依然是“收入”和“支出”的思考方式
>
> r的话根据seir和为1去求即可
>
> > 这里可以进一步思考，这其实是一种**单影响因素**和**多影响因素**变量的列方程套路

```python
from scipy.integrate import odeint
from numpy import arange
import matplotlib.pyplot as plt

# seirfun = [s, e, i]
def func(seirfun, t, _lambda, mu, delta):
    ds_dt = -_lambda*seirfun[0]*seirfun[2]
    de_dt = _lambda*seirfun[0]*seirfun[2] - seirfun[1]*delta
    di_dt = seirfun[1]*delta - mu*seirfun[2]
    return [ds_dt, de_dt, di_dt]
i0 = 1e-6
e0 = 1e-3
s0 = 1 - i0 - e0
seirfun0array = [s0, e0, i0]
tarray = arange(0.0, 300, 1)
_lambda = 0.3
mu = 0.06
delta = 0.03
seirsol = odeint(func, seirfun0array, tarray, args=(_lambda, mu, delta))

plt.xlabel('t')
plt.axis([0, 300, -0.1, 1.1])
plt.axhline(y=0, ls='--', c='c')
plt.plot(tarray, seirsol[:,0], '-r', label='s(t)-SIR')
plt.plot(tarray, seirsol[:,1], '-g', label='e(t)-SIR')
plt.plot(tarray, seirsol[:,2], '-b', label='i(t)-SIR')
plt.plot(tarray, 1 - seirsol[ :,0] - seirsol[ :,1] - seirsol[ :,2], '-k', label='r(t)-SIR')
plt.legend(loc='right') 
plt.show()
```

<img src="SEIR%E6%A8%A1%E5%9E%8B.assets/image-20220720200047817.png" alt="image-20220720200047817" style="zoom:80%;" />

> 关于SEIR模型的进一步思考：
>
> <img src="SEIR%E6%A8%A1%E5%9E%8B.assets/image-20220720200251851.png" alt="image-20220720200251851" style="zoom:67%;" />
>
> - 由于病毒的变异，康复者可能再次成为易感者
> - 关于死亡病例的影响
> - 易感者接种疫苗后也相当于康复者