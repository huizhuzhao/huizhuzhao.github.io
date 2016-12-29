---
layout: post
title: "draft blog 1"
date: 2016-12-28
categories: jekyll update
---

SVM （支持向量机）模型对两类数据点进行分类。

{% highlight python %}
n_samples = 200
## 蓝色点集
x1 = np.random.randn(n_samples, 2) * 0.5 + np.asarray([[0, 1]])
y1 = np.asarray([[1, 0] for ii in range(len(x1))])

##　红色点集
x2 = np.random.randn(n_samples, 2) * 0.5 + np.asarray([[1, 0]])
y2 = np.asarray([[0, 1] for ii in range(len(x2))])
{% endhighlight %}

