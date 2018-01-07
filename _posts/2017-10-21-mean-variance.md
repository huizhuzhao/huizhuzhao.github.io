---
layout: post
title: stastics tips
date: 2017-10-21
---

frequentist statistics 或者 bayesian statstics 都认为事件（或者观测数据 $$X$$) 是以概率的形式发生的，这种概率的出发点导致后续几乎所有的概率解释，即对模型结果对概率解释（统计学解释），比如：

* 对于观测数据 $$D = \{x_1, x_2, .., x_n\}$$，通常认为 $$x_i, x_{i+1}, $$ 满足独立同分布，且服从概率 $$p(x)$$
* 对于观测数据 $$D = \{(x_1, y_1), (x_2, y_2), .., (x_n, y_n)\}$$，通常认为存在映射函数 $$f$$ 使得 $$y \sim f(x)$$；这里使用 $$\sim$$ 同样源于 $$y$$ 服从某种概率分布 $$p\(f(x)\)$$


假设观测数据集如下：
$$D = \{x_1, x_2, .., x_n\}$$

### 均值和方差
同时我们定义  

$$E(x) = \mu$$ 
$$var(x) = \sigma^2$$

那么变量 $$X = \sum_{i=1}^n x_i$$ 的均值和方差满足

$$
\begin{array}{ll}
E[X] &=  \sum_i E[x_i]\\
& = n \mu \\
var[X] &=  \sum_i var[x_i] \\
& = n\sigma^2
\end{array}
$$

### 无偏/有偏估计(biased/unbiased)

如果 $x～N(\mu, \sigma^2)$，根据最大似然估计

$$
\begin{array}{ll}
\mu_n & = \frac{1}{n} \sum_i x_i \\
\sigma^2_n & = \frac{1}{n} \sum_i (x_i - \mu_n)^2
\end{array}
$$

根据定义,估计值的偏差为
$$
\begin{array}{ll}
bias(\mu_n) & = E[\mu_n] - \mu \\
& = 0 \\
bias(\sigma^2_n) & = E[\sigma^2_n] - \sigma^2 \\
& = -\frac{1}{n} \sigma^2
\end{array}
$$

证明如下：

$$
\begin{array}{ll}
E[\mu_n] & = E\big[\frac{1}{n} \sum_i x_i \big] \\
& = \frac{1}{n} \sum_i E[x_i] \\
& = \mu
\end{array}
$$

$$
\begin{array}{ll}
E[\sigma^2_n] & = E\big[\frac{1}{n} \sum_i (x_i - \mu_n)^2 \big] \\
& = E\big[\frac{1}{n} \sum_i \big((x_i - \mu) - (\mu_n - \mu)\big)^2 \big]\\
& = E\big[ \frac{1}{n} \sum_i \big( (x_i - \mu)^2 - 2(x_i-\mu)(\mu_n - \mu) + (\mu_n-\mu)^2\big)\big]
\end{array}
$$

根据 $\mu_n  = \frac{1}{n} \sum_i x_i$ ，可得
$$
\begin{array}{ll}
\mu_n - \mu & = \frac{1}{n}\sum_i (x_i - \mu)
\end{array}
$$
因此替换上式中的第二项可得

$$
\begin{array}{ll}
E[\sigma^2_n] & = E\big[ \frac{1}{n} \sum_i (x_i - \mu)^2 \big] - E\big[(\mu_n - \mu)^2\big] \\
& = \frac{1}{n}\sum_i var\big[x_i\big] - var\big[\mu_n\big] \\
& = \frac{1}{n} \sum_i \sigma^2 - \sum_i var\big[\frac{1}{n} x_i\big] \\
& = \sigma^2 - \frac{1}{n} \sigma^2
\end{array}
$$


证明如下：
$$
\begin{array}{ll}
E[X] & = E\big[\sum_i x_i\big] \\
& = \sum_i E[x_i] \\
& = n \mu
\end{array}
$$

$$
\begin{array}{ll}
var\big[X\big] & = E\big[\big(X - E[X]\big)^2\big] \\
& = E\big[ \big(\sum_i x_i - n\mu\big)^2\big] \\
& = E\big[ \big(\sum_i (x_i - \mu)\big)^2\big] \\
& = E\big[ \sum_{i,j}(x_i - \mu) (x_j - \mu) \big] \\
& = \sum_{i,j} E\big[(x_i-\mu)(x_j-\mu)\big]
\end{array}
$$

如果 $x_i$, $x_j$ ($i != j$) 满足独立同分布 (i.i.d.)，则：

$$ E\big[ (x_i - \mu) (x_j - \mu)\big] = 0 $$
因此

$$
\begin{array}{ll}
var\big[X\big] & = \sum_{i} (x_i - \mu)^2 \\
& = \sum_i var[x_i]
\end{array}
$$

