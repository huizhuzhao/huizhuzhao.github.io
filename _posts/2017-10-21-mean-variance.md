---
layout: post
title: Stastics 
date: 2017-10-21
---


假设观测数据集如下：
$$D = \{x_1, x_2, .., x_n\}$$

### 均值和方差
同时我们定义  

$$E(x) = \mu$$ 
$$var(x) = \sigma^2$$

那么变量 $X = \sum_{i=1}^n x_i$ 的均值和方差满足

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

