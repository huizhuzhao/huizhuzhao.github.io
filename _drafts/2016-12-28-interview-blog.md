---
layout: post
title: "first blog"
date: 2016-12-28
categories: jekyll update
---
### 最小二乘法
![sin_fitting](/assets/images/sin.jpg)

上图是数据点 $$\vec x, \vec y$$ 大致满足线性关系 `y = a x + b`，在生成过程中加入了随机噪声，具体生成代码如下。请使用最小二乘法拟合出参数　`a, b`　的值来。
{% highlight python linenos%}
a = 0.5; b = 2
n_samples = 50
x = np.linspace(0, 10, n_samples)
y = a * x + b + np.random.randn(n_samples) * 0.5
{% endhighlight %}
a paper about [layer normalization](/assets/Layer_Normalization.pdf).
The following is a math block:
$$ 5 + 5 $$
But next comes a paragraph with an inline math statement:
$$ 5 + 5 $$
\begin{equation}
a + b = c
\end{equation}

* abc 
$$ \frac{a}{b} $$


