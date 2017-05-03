---
layout: post
title: 变分贝叶斯
date: 2017-05-03
categories: jekyll update
comments: true
---

* 变分推断(variational inference)

后验分布是关于 **非观测变量 Z** 的分布，此分布是基于观测数据 X 给出的，即 $$P(Z\mid X)$$，

在复杂的统计模型中无法得到 $$P(Z\mid X)$$ 的解析表达式，变分推断则是一种寻找

$$Q(Z)$$ 使得 $$P(Z\mid X) \approx Q(Z)$$ 的一种方法。

通常情况下使用 KL 散度来衡量 $$P(Z\mid X)$$ 和 $$Q(Z)$$之间的”距离“， KL divergence 定义为

$$D_{KL}(Q\mid P) = \sum_{Z}Q(Z) log\frac{Q(Z)}{P(Z\mid X)}$$

$$\longrightarrow$$

$$D_{KL}(Q\mid P) = \sum_{Z}Q(Z) log\frac{Q(Z)}{P(Z, X)} + logP(X)$$

显然，通过最小化$$D_{KL}(Q||P) $$ 可以使得 $$P(Z\mid X) \prompt Q(Z)$$成立

* 因式分解

操作中，通常假设$$Q(Z)$$可进行如下因式分解


$$Q(Z)=\prod_{i=1}^M q_i(Z_i|X)$$

此时，根据上面的式子以及[变分学](https://en.wikipedia.org/wiki/Calculus_of_variations)可以得出 $$q_j$$ 的最优解为

$$q_j^*(Z_j\mid X) = \frac{e^{E_{i\neq j}[lnp(Z, X)]}}{\int e^{E_{i\neq j}[lnp(Z, X)]} dZ_j}$$



