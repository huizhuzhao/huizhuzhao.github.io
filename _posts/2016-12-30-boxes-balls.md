---
layout: post
title: others
date: 2016-12-30
comments: true
---

* 把 `m`个球放到`n`个箱子中，球不可分，箱子可分。每个箱子至少有一个球，共有

$$Y=C_{m-1}^{n-1}=\frac{(m-1)!}{(n-1)!(m-n)!} \qquad(Eq.1)$$

种分法。比如下图共有四个球(m=4), 三个箱子(n=3)，在保证每个箱子都有球的情况下共有 $$Y=C_3^2=3$$种放法。

![boxes](/images/boxes.png)

* 现在有`m`个球，`n`个箱子($$n\ge 2m-1$$)。现将每个球放进某个箱子中(一个箱子`至多`放一个球)，在保证球互不紧邻的情况下共有多少种放法`Y`。如下图所示 `m=2, n=4`时，有`Y=3`

  ![boxes](/images/boxes_2.png)

  * step 1：
 将`m`个球放进盒子中后，剩余`n-m`空箱，为了保证已放球的箱子互相不紧邻，我们需要将剩余的`n-m`个空箱插入`m`个球之间的间隙(共有`m-1`个)，并保证每个间隙插入``至少一个空箱``，如下图所示

  ![boxes](/images/boxes_input.png)
  * step2：
 `step 1`中的问题最终转化为将`n-m`个空箱划分为`m-1`个组(因此每个组中至少有一个空箱)，利用公式`Eq.1`，我们有$$C_{n-m-1}^{m-1-1}$$种划分方法。

  * step 3:
  除了`step 1`和`step 2`中讨论的情况下，我们还有另外两种情况需要考虑，即考虑两侧(或单侧)有空箱的情况，如下图所示
  ![boxes](/images/boxes_input_2.png)

  当两侧有空箱时,间隙个数为`m+1`；当单侧有空箱时，间隙个数为`m`

综上，$$ Y=C_{n-m-1}^{m-1-1}+2C_{n-m-1}^{m-1}+C_{n-m-1}^{m} $$，其中等式右侧第一，二，三项分别表示序列两侧没有空箱，单侧有空箱，两侧有空箱的情况。

---
# Random sampling

Consider the problem: after doing **n** times random sampling from **n** different balls with replacement, what is the probability of $$p_i$$ that
we get $$i$$ different balls in our result (**n** balls).

If $$i=1$$, we have the number of different solutions 
$$
s_1 = C_n^1*\alpha_1 = C_n^1
$$, 

where $$\alpha_1=1$$

if $$i=2$$, $$s_2 = C_n^2 * \alpha_2 = C_n^2(2^n-C_2^1\alpha_1)$$

if $$i=3$$, $$s_3 = C_n^3 * \alpha_3 = C_n^3(3^n-C_3^2\alpha_2-C_3^1\alpha_1)$$

...

if $$i=i$$, $$s_i = C_n^i * \alpha_i = C_n^i (i^n -\sum_{j=1}^{j=i-1}C_i^j\alpha_j)$$

In the following, we show the scatter plots of $$s_i$$ and $$p_i$$ in cases $$n=10$$ and $$n=15$$, the code of computing $$C_n^i$$ and $$\alpha_i$$ can be found in
 [github](https://github.com/huizhuzhao/Snow/blob/master/examples/random_sampling.py).

It worth noting that 

$$ \sum_{i=1}^n s_i = n^n$$

![](/images/boxes_balls/s_sample.png)

-----
## Distances distribution on circle/sphere
We compute the distribution of the distances of pairs of points on on a circle/sphere with radius $$r = 1$$, the data points are uniformly randomly sampled as the following code showing:

{% highlight python%}
def circle_points(n_samples):
    """
    inputs
    ------
    n_samples: int

    return
    ------
    u: 2D np.ndarray with shape=[n_samples, 2]
    """
    theta = np.random.uniform(low=0.0, high=2 * np.pi, size=(n_samples, 1))
    u = np.concatenate([np.cos(theta), np.sin(theta)], axis=1)
    return u
  

def sphere_points(n_samples):
    """
    inputs
    ------
    n_samples: int

    return
    ------
    u: 2D np.ndarray with shape=[n_samples, 3]
    """
    theta = np.random.uniform(low=0.0, high=2 * np.pi, size=(n_samples, 1))
    z = np.random.uniform(low=-1.0, high=1.0, size=(n_samples, 1))
    x = np.sqrt(1 - z**2) * np.cos(theta)
    y = np.sqrt(1 - z**2) * np.sin(theta)

    u = np.concatenate([x, y, z], axis=1)
    return u

def distance(x, y):
    """
    inputs
    ------
    x: 2D np.ndarray with shape=[n1, dim]
    y: 2D np.ndarray with shape=[n2, dim]

    return
    ------
    dist: 2D np.ndarray with shape=[n1, n2], 
        dist[i, j] = distance(x[i], y[j])
    """
    assert len(x.shape) == len(y.shape) == 2
    assert x.shape[1] == y.shape[1]
    x = x[:, np.newaxis, :]
    y = y[np.newaxis, :, :]
    z = np.square(x - y)
    dist = np.sqrt(np.sum(z, axis=-1))
    return dist

{% endhighlight %}
<div class="imgcap">
<img src="/images/others/distance_distribution.png">
<div class="thecap">Fig: distance distribution on circle (upper) / sphere (lower), 1000 data points are uniformly randomly sampled both on circle and sphere,
and the total segments are 499500.
</div>