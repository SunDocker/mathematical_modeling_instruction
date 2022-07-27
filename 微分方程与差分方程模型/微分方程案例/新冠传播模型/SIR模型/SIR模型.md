#### 4.3.4 SIR模型

>S： Susceptible     I：Infectious      E：Exposed       R：Recovered

在 SI 模型基础上考虑病愈免疫的康复者（R 类）就得到 SIR 模型：

- 考察地区的总人数N不变，即不考虑生死或迁移;
- 人群分为易感者(S类)、患病者(|类) 和康复者(R类)三类;
- 易感者(S类)与患病者(I类) 有效接触即被感染，变为患病者(I类)；患病者(I类) 可被治愈，治愈后变为康复者；康复者(R类)获得终身免疫不再易感；无潜伏期;
- 将第t天时S类、I类、R类人群的占比记为s(t)、i(t).、r(t)，数量为S(t)、I(t)、R(t)；初始日期t = 0时，S类、I类、R类人群占比的初值为s~0~、i~0~、r~0~
- 日接触数$\lambda$：每个患病者每天有效接触的平均人数;
- 日治愈率μ：**每天被治愈的患病者人数占患病者总数的比例**，即平均治愈天数为1/μ
- 传染期接触数σ= λ/μ（用来求$\mu$），即每个患病者在**整个传染期**内有效接触的易感者人数。

<img src="SIR%E6%A8%A1%E5%9E%8B.assets/image-20220720164436075.png" alt="image-20220720164436075" style="zoom:80%;" />
$$
\begin{cases}
N\frac{ds}{dt}=-Ni(t)\lambda s(t)\\
N\frac{di}{dt}=Ni(t)\lambda s(t)-Ni(t)\mu\\
s(t)+i(t)+r(t)=1
\end{cases}
$$

> 取一极小段时间变化，由于这里是s、i、r三者有和为1的关系，所以关于其中的两个再列一个额外的方程即可，这里选择的是s和i（因为初始时其实没有康复者。如果非要列r的方程，那和为1的方程就不用列了，因为可以直接推出来）：
>
> - s很简单，因为易感人群的变化只和感染者有关
> - 列i的时候可以这样思考：`增量=收入-支出`，易感人群相当于收入，康复者相当于支出

```python
from scipy.integrate import odeint
from numpy import arange
import matplotlib.pyplot as plt

# sirfun = [s, i]
# r不涉及其导数，所以不放在微分方程组中求解，最后通过r=1-s-i求解即可
def func(sirfun, t, _lambda, mu):
    ds_dt = -_lambda*sirfun[0]*sirfun[1]
    di_dt = _lambda*sirfun[0]*sirfun[1] - mu*sirfun[1]
    return [ds_dt, di_dt]
i0 = 1e-6
s0 = 1 - i0 # 初始时没有所谓的“康复者”
sirfun0array = [s0, i0]
tarray = arange(0.0, 200, 1)
_lambda = 0.2
sigma = 2.5 # 这个就是用来求mu的
mu = _lambda/sigma
sirsol = odeint(func, sirfun0array, tarray, args=(_lambda, mu))

plt.xlabel('t')
plt.axis([0, 200, -0.1, 1.1])
plt.axhline(y=0, ls='--', c='c')
plt.plot(tarray, sirsol[:,1], '-r', label='i(t)-SIR')
plt.plot(tarray, sirsol[:,0], '-b', label='s(t)-SIR')
# 这里体现了对r的求解
plt.plot(tarray, 1 - sirsol[ :,1] - sirsol[ :,0], '-m', label='r(t)-SIR')
plt.legend(loc='best') 
plt.show()
```

<img src="%E6%96%B0%E5%86%A0%E4%BC%A0%E6%92%AD%E6%A8%A1%E5%9E%8B.assets/image-20220720165351924.png" alt="image-20220720165351924" style="zoom:80%;" />