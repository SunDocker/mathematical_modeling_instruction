#### 4.3.3 SI模型

> S： Susceptible     I：Infectious      E：Exposed       R：Recovered

SI 模型是最简单的传染病传播模型，把人群分为**易感者（S类）和患病者（I类）**两类，通过 SI 模型可以预测传染病高潮的到来；提高卫生水平、强化防控手段，降低病人的日接触率，可以推迟传染病高潮的到来。

<img src="SI%E6%A8%A1%E5%9E%8B.assets/image-20220720152509976.png" alt="image-20220720152509976" style="zoom:67%;" />

**易感者**与**患病者**有效接触即被感染，变为**患病者**，无潜伏期、无治愈情况、无免疫力。

以一天作为模型的最小时间单元。**总人数为N**，不考虑人口的出生与死亡，迁入与迁出，此**总人数不变**。

**t 时刻两类人群占总人数的比率分别记为s(t)、i(t)**，**两类人群的数量为S(t)、I(t)**。

**初始**时刻 t=0 时，各类人数量所占**初始比率为s0、i0**。

每个患病者每天**有效接触的平均人数是 λ** ，即日**接触数**。

则可得以下微分方程
$$
\begin{cases}
N\frac{di}{dt}=\lambda s(t)Ni(t)\\
s(t)+i(t)=1
\end{cases}
$$

> 方程怎么来的？
>
> - 自变量取一段**极小的变化**，然后寻找因变量之间的关系，列等式
> - 这里找到的就是极小时间内**患病者增长的人数**
>
> 其实把dt乘过去更容易理解，dt和$\lambda$相乘代表dt时间内接触的人数

> 可以观察出，这其实属于Logisitc模型

```python
from scipy.integrate import odeint
from numpy import arange
import matplotlib.pyplot as plt

def di_dt(i, t, _lambda):
    return _lambda * (1 - i) * i
i0 = 1e-6
tarray = arange(0, 50, 1)
_lambda = 1
isol = odeint(di_dt, i0, tarray, args=(_lambda, ))

plt.plot(tarray, isol, ':.r', label='numerical')
plt.legend(loc='right')
plt.axis([0, 50, -0.1, 1.1])
plt.show()
```

<img src="SI%E6%A8%A1%E5%9E%8B.assets/image-20220720163820850.png" alt="image-20220720163820850" style="zoom:80%;" />