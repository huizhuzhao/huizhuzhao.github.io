---
layout: post
title: 将球放到盒子里
date: 2016-12-30
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

In the following, we show the scatter plots of $$s_i$$ in cases $$n=10$$ and $$n=15$$, as well as the code of computing $$C_n^i$$ and $$\alpha_i$$.

![](/images/boxes_balls/s_sample.png)



{%highlight python%}
def memo(func):
    """
    memoization for recursive func
    """
    cache = {}
    ii = []
    @wraps(func)
    def wrap(*args):
        if args not in cache:
            cache[args] = func(*args)
        ii.append(1)
        return cache[args]
    return wrap

@memo
def combination(n, i):
    """
    compute C(n, i) = n! / (i! * (n-i)!)
    """
    n, i = int(n), int(i)
    x = np.math.factorial(n)
    y1 = np.math.factorial(i)
    y2 = np.math.factorial(n-i)

    return x / (y1 * y2)

@memo
def alpha_i(n, i):
    """
    compute \alpha_i
    """
    if i == 1:
        alp = 1
    elif i>1:
        s = np.power(i, n)
        m = 0
        for k in range(1, i):
            m += combination(i, k) * alpha_i(n, k)
        alp = s - m
    else:
        raise ValueError('Invalid value {0} received.'.format(i))
    return alp
{% endhighlight%}