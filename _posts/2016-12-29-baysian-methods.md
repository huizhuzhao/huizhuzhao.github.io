---
layout: post
title: 理解贝叶斯公式和似然函数
date: 2016-12-29
---

假如现在有一枚硬币，我们通过观测连续地抛硬币后，硬币正反面出现的情况来估计硬币正面朝上的概率 $$\mu$$。这里假设连续抛出 $$N$$ 次，正反面出现的情况为 $$X=\{x_1, x_2, ..., x_N\}$$， 其中 $$x_i\in \{0, 1\} $$ ($$0$$代表正面，$$1$$代表反面)。根据数据 $$X$$ 对参数 $$\mu$$ 进行的估计的方法有如下两种：
1. **最大似然** 方法
2. **贝叶斯** 方法

### 理解似然函数(likelihood function)
根据上面提到的硬币问题，如果存在 $$\mu$$（？），那么该问题便可以看做为伯努利实验，即每次扔硬币正面朝上的概率为 $$\mu$$， 反面朝上的概率为 $$1-\mu$$，事件 $$X$$ 发生的概率为

 $$p(X|\mu) = \prod_i p(x_i|\mu) = \prod_i \mu^{x_i}(1-\mu)^{1-x_i}$$

 此概率函数便称作似然函数(likelihood function)。最大似然方法认为如果存在
 $$\mu = \mu_0$$ 能够使得似然函数取得最大值，那么 $$\mu_0$$ 便是我们要估计的参数值。因此我们将 $$\mu$$ 看做函数 $$p(X|\mu)$$ 的变量，最大化 $$p(X|\mu)$$ 等价于最大化其对数：

 $$ln p(X|\mu) = \sum_{n=1}^N \{x_n ln \mu + (1-x_n) ln (1 - \mu)\}$$

上式对 $$\mu$$ 求导，并使得导数值为0，便可得到 $$\mu_0 = \frac{1}{N}\sum_{n=1}^Nx_n$$。

 如果我们连续扔了三次硬币，并且硬币全都正面朝上，那么根据最大似然方法可以得到 $$\mu_0=1$$。根据此估计结果，那么第四次扔硬币正面朝上的概率也为 $$1$$。显然这样极端的结论并不成立，接下来介绍贝叶斯方法，该方法得出的结论将更加合理。

 ### 贝叶斯公式
 * $$ p(\vec w|D)= \frac{p(D|\vec w)p(\vec w)}{p(D)} $$
  $$\qquad D: dataset,\quad \vec w: parameters $$

![gaussin_distribution](/images/gaussin_distribution.png)

 假设有$$n$$个观测值$$\vec x = \{x_1, x_2, .., x_n\}$$，它们满足独立同分布条件(independent and identically distribution)，分布函数为高斯函数

 $$N(x|\mu, \sigma) = \sqrt{\frac{1}{2\pi \sigma^2}} exp\{\frac{(x-\mu)^2}{2\sigma^2}\} $$

 求解最大似然函数就是寻找合适的参数值 $$\mu, \sigma$$，使得上述$$n$$个观测值出现的概率最大，公式如下：

 $$maximize\quad p(\vec x|\mu, \sigma)=\prod_i N(x_i|\mu,\sigma) $$

  * step 1: 将 $$p(\vec x|\mu, \sigma)$$ 转化为 $$log\: p(\vec x|\mu, \sigma)$$
  进行求解

  * step 2: 令
  $$\frac{\partial log p(\vec x|\mu, \sigma)}{\partial \mu}=0$$
  以及　
  $$\frac{\partial log p(\vec x|\mu, \sigma)}{\partial \sigma^2}=0$$
  * 求解过程：

  $$log\: p(\vec x|\mu, \sigma) = -\frac{N}{2}log\:2\pi\sigma^2-\sum_i \frac{(x_i-\mu)^2}{2\sigma^2}$$

  $$\frac{\partial log\: p(\vec x|\mu, \sigma)}{\partial \mu} = \sum_i \frac{x_i - \mu}{\sigma^2}=0$$

  $$\frac{\partial log\: p(\vec x|\mu, \sigma)}{\partial \sigma^2}=\frac{N}{2\sigma^2}-\sum_i\frac{(x-\mu)^2}{2\sigma^4}=0$$

  $$\Longrightarrow \quad \mu_{ML}=\frac{1}{N}\sum_ix_i \qquad \sigma^2_{ML} = \frac{1}{N}\sum_i(x_i - \mu_{ML})^2 $$

*注 上面求解过程中$$\mu$$ 和 $$\sigma^2$$并没有发生耦合，这是由于高斯分布自身的特点造成的，因此使得求解过程更加简单。*

### 最大似然的局限性
根据上面的公式可以看出 $$\mu_{ML}$$ 和 $$\sigma^2$$ 都是与数据集 $$\vec x$$ 的函数，并且二者也可以看做随机变量，满足

$$E(\mu_{ML}) = \mu \qquad  E(\sigma^2_{ML}) = \frac{N-1}{N}\sigma^2$$

为了纠正上式 $$E(\sigma^2_{ML})$$ 中的偏差， 我们对方差的估计改写为如下形式：

$$\sigma^2_{ML} = \frac{1}{N-1}\sum_i(x_i - \mu_{ML})^2$$

### 扔硬币问题
想象扔一个硬币，其正反两面出现的概率分别为$$p_1$$ 和 $$p_0$$。为了模拟这个问题我们设计一个满足连续高斯分布的随机数生成器，该生成器每次以概率 $$N(x|\mu, \sigma)$$ 产生数值 $$x$$，而 $$y= sgn(x)$$ 的结果$$1$$, $$0$$表示硬币的正反面。
* 理想情况下，如果硬币的正反面没有任何差别（除了可以分辨出正反面的差别外），则 $$p_0=p_1=1/2$$，  $$\mu=0$$
* 但是，当我们连续扔了两次后，均出现正面，那么 $$\mu=0$$ 是否成立
* 求解过程 (这里我们半定量的进行求解）
![gaussin_bayse](/images/gauss2_pRMkeev.png)
* 根据最大似然（maximium likelihood function）方法，我们的目标是寻找 $$\mu, \sigma^2$$， 从而最大化概率

  $$p(\vec x|\mu, \sigma)$$

  由于连续扔了两次硬币均出现正面，则 $$\vec x = \{x_1, x_2\}$$ 分布在坐标轴零点右侧，根据
 $$
 \mu_{ML}=\frac{1}{N}\sum_ix_i \qquad \Longrightarrow \quad \mu_{ML} > 0
 $$
* 从贝叶斯的观点出发，我们的目标是根据当前的观测值 $$\vec x = \{x_1, x_2\}$$， 寻找参数 $$\mu_{Bayes}, \sigma^2_{Bayes}$$ 使得贝叶斯公式(后验概率)的值最大

$$p(\mu, \sigma^2|\vec x)= \frac{p(\vec x|\mu, \sigma^2)p(\mu, \sigma^2)}{p(\vec x)}\propto p(\vec x|\mu, \sigma^2)p(\mu, \sigma^2)$$

我们已知在 $$\mu = \mu_{ML}$$ 时 $$p(\vec x|\mu, \sigma^2)$$ 取最大值，但是

$$p(\mu=\mu_{ML}, \sigma^2)< p(\mu=0, \sigma^2)$$

  （这里我们假设 $$\mu, \sigma^2$$ 都满足标准正态分布），因此
  $$p(\mu, \sigma^2|\vec x)$$
  最大值的位置将会出现在$$0<\mu_{Bayes}\le\mu_{ML}$$
  *注 可以看出加入先验概率后，使得贝叶斯公式的结果介于另外两条曲线之间 (??)*

### 曲线拟合问题
![](/images/fit.png)
我们现在有观测数据集
$$(\vec x, \vec t) = \{(x_1, t_1), (x_2, t_2), .., (x_n, t_n)\}$$， 我们期望寻找参数 $$\vec w$$ 对该数据集进行多项式拟合，我们假定目标值 $$t$$ 满足高斯分布：
$$p(t|x, \vec w, \beta) = N(t|y(x, \vec w), \beta^{-1})$$
其中 $$y(x, \vec w)$$ 和 $$\beta^{-1}$$ 对应高斯分布的均值和方差。
 * 根据最大似然方法，我们的目标是最大似然函数

$$p(\vec t|\vec x, \vec w, \beta) = \prod_i N(t_i|y(x_i, \vec w), \beta^{-1})$$

根据
$$log\:p(\vec t|\vec x, \vec w, \beta) = -\frac{\beta}{2}\sum_i \{y(x_i, \vec w) - t_i\}^2 + \frac{N}{2}log\:\beta - \frac{N}{2}log\:(2\pi)$$

则最大化
$$log\:p(\vec t|\vec x, \vec w, \beta)$$
等价于最小化

$$\sum_i \{y(x_i, \vec w) - t_i\}^2$$

* 根据贝叶斯方法，加入先验概率后有如下形式的后验概率

$$p(\vec w|\vec x, \vec t, \alpha, \beta) \propto p(\vec t|\vec x, \vec w, \beta) p(\vec w|\alpha)
$$

其中 $$p(\vec w|\alpha)$$
是参数 $$\vec w$$ 的分布函数, $$\alpha$$ 称为模型的超参数(拟合模型)

$$p(\vec w|\alpha) = N(\vec w|\vec 0, \alpha^{-1}I) = (\frac{\alpha}{2\pi})^{\frac{M+1}{2}}exp\{-\frac{\alpha}{2}\vec w^T\vec w\}$$

我们的目标是最大化下面的函数

$$log\:p(\vec w|\vec x, \vec t, \alpha, \beta) = log\:p(\vec t|\vec x, \vec w, \beta) + log\:p(\vec w|\alpha)$$

进而最小化

$$
\sum_i \{y(x_i, \vec w) - t_i\}^2+\frac{\alpha}{2}\vec w^T\vec w$$