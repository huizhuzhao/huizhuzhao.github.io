---
layout: post
title: 分布函数
date: 2016-12-30
---
以下公式参考书籍 [Pattern recognition and machine learning (Bishop, Christopher)][PRML]
abc
### 特殊积分

* $$\int\limits_{-\infty}^{\infty}e^{-\alpha x^2}dx  =  \sqrt\frac{\pi}{\alpha} \qquad $$
$$\int\limits_{-\infty}^{\infty}x^{2n}e^{-\alpha x^2}dx = \frac{(2n-1)!!}{(2\alpha)^n}\sqrt\frac{\pi}{\alpha} $$

* $$\int\limits_{0}^{\infty}xe^{-\alpha x^2}dx  =\frac{1}{2\alpha} \qquad $$
$$\int\limits_{0}^{\infty}x^{2n+1}e^{-\alpha x^2}dx  =\frac{(2n)!!}{(2\alpha)^n}\frac{1}{2\alpha} $$

## 高斯分布
* 一元高斯

$$N(x|\mu, \sigma) = \sqrt{\frac{1}{2\pi \sigma^2}}exp\{-\frac{(x-\mu)^2}{2\sigma^2}\}$$

满足:

$$
E[x] = \mu \qquad var[x] = \sigma^2
$$

* 多元高斯（D维情形）

$$N(\vec x|\vec \mu, \vec \Sigma) = \frac{1}{(2\pi)^\frac{D}{2}}\frac{1}{|\vec \Sigma|^\frac{1}{2}} exp\{-\frac{1}{2}(\vec x-\vec\mu)^T\:\Sigma^{-1}\:(\vec x-\vec \mu)\}  
$$

## beta 分布
beta 分布取值区间为 $$[0, 1]$$, 这种分布函数有两个参数 $$a$$ 和 $$b$$， 下面是 $$a, b$$ 取不同值的情况下 beta 分布的示意图
![beta_distribution](/images/beta_distribution.jpg)

beta 函数定义如下：

$$beta(\mu|a, b) = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}\:\mu^{a-1}(1-\mu)^{b-1} \qquad \mu \in (0, 1)$$

$$E(\mu) = \frac{a}{a+b}  \qquad var(\mu)=\frac{ab}{(a+b)^2(a+b+1)}$$

上式中 $$\Gamma$$　表示 Gamma 函数

$$\Gamma(x) \equiv\int_0^\infty u^{x-1}e^{-u}du$$

且具有如下性质

$$\Gamma(x+1) = x\Gamma(x), \qquad \Gamma(n+1) = n!$$
![Gamma_function](/images/600px-Gamma_plot.svg.png)

## 伯努利分布
考虑随机变量 $$x\in [0, 1]$$， 并且参数 $$\mu$$ 表示 $$x=1$$ 的概率，则伯努利分布可表示为

 $$p(x=1|\mu) = \mu \qquad p(x=0|\mu)=1-\mu$$

 通过观测 $$n$$ 次试验（满足独立同分布条件）的结果，我们有数据集 $$\vec x=\{x_1, x_2, ..., x_N\}$$ ，则相应的似然函数如下：

 $$p(\vec x|\mu) = \prod_i p(x_i|\mu) = \prod_i \mu^{x_i}(1-\mu)^{1-x_i} \qquad (Eq.2.2)$$

* 在参数 $$\mu$$ 和观测总数 $$N$$ 条件下, 事件$$x=1$$ 发生总数$$m$$ 的二项分布：

$$Bin(m| \mu, N) =\frac{N!}{m!(N-m)!}\mu_m^{m} (1-\mu)^{N-m}$$

## 多项式分布
变量 $$\vec x =(0, 0, .., 1, .., 0)^T$$ 满足 $$1-of-K$$ 表示法 （$$\sum_{k=1}^{K}x_k = 1$$）
$$\vec x$$ 分布函数为：

$$p(\vec x|\vec \mu) = \prod_{k=1}^K\mu_k^{x_k} \qquad \vec \mu = (\mu_1, \mu_2, ..,\mu_K)T, \quad \mu_k\geq0, \quad\sum_k\mu_k = 1$$

对于数据集 $$D=\{\vec x_1, \vec x_2, ..., \vec x_N\}$$，对应的似然函数为：

$$
p(D|\vec \mu) = \prod_{n=1}^N\prod_{k=1}^K\mu_k^{x_{nk}}=\prod_{k=1}^K\mu_k^{(\sum_n x_{nk})} = \prod_{k=1}^K\mu_k^{m_k} \qquad m_k = \sum_n x_{nk}$$

最大化对数似然函数，以及限制性条件 $$\sum_k\mu_k = 1$$， 我们最终需要最大化

$$\sum_{k=1}^Km_klog\:\mu_k + \lambda (\sum_{k=1}^K\mu_k-1)$$

$$\Longrightarrow \mu_k = \frac{m_k}{N} \qquad \Longrightarrow \lambda = -N$$

* 在参数 $$\vec \mu$$ 和观测总数 $$N$$ 条件下 $$(m_1, m_2, ..., m_K)$$ 的联合分布：

$$Mult(m_1, m_2, ..., m_K|\vec \mu, N) =\frac{N!}{m_1!m_2!...m_K!}\prod_{k=1}^K\mu_k^{m_k}$$

满足如下的限制
$$\sum_{k=1}^K m_k = N$$

## 狄利克雷分布
此分布用来作为多项式分布的共轭先验，满足如下的形式

$$p(\vec \mu|\vec{\alpha}) \propto \prod_{k=1}^K\mu_k^{\alpha_k-1}$$

其中$$\vec \alpha = (\alpha_1, \alpha_2, ..., \alpha_K)^T$$ 是分布的超参数，满足下面的限制条件

$$
0\leq \mu_k \leq 1 \qquad \sum_k\mu_k = 1
$$

归一化后得：

$$
Dir(\vec \mu|\vec{\alpha}) =\frac{\Gamma(\alpha_0)}{\Gamma(\alpha_1)...\Gamma(\alpha_K)} \prod_{k=1}^K\mu_k^{\alpha_k-1}
$$

[PRML]: http://www.springer.com/us/book/9780387310732
