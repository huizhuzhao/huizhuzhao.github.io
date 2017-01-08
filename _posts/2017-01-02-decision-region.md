---
layout: post
title: 联合分布
date: 2016-12-28
categories: jekyll update
---

### 联合分布 $$p(x, y)$$
* $$x, y$$ 分别为`连续`和`离散`的情况

  如下图所示黄色线和绿色线分别表示联合概率函数$$p(x, y_1)$$ 和 $$p(x, y_2)$$

  其中$$x\in (-\infty_, \infty_)$$为连续变量， $$y \in (y_1, y_2)$$为离散变量
  ![two_gaussian_plots](/images/two_gaussian_plots.png)

  在已知$$p(x, y_1)$$ 和 $$p(x, y_2)$$ 的前提下，我们来计算边缘概率(marginal probability) $$p(x)$$ 和 $$p(y)$$。

   * 边缘概率$$p(x)$$可以通过

	 $$p(x) = p(x, y_1)+p(x, y_2)$$

     计算出来，即两条联合分布曲线的叠加，如下图中的蓝色线所示，且满足 $$\int_x p(x) dx = 1$$。
 ![three_gaussian_plots](/images/three_gaussian_plots.png)


   * 因为$$y$$是离散变量，因此我们可以方便的计算出

     $$p(y=y_1)=\int_x p(x, y_1)dx$$

     $$p(y=y_2)=\int_x p(x, y_2)dx$$

     也就是说红色线与$$x$$ 轴之间的面积表示概率$$p(y=y_1)$$，蓝色线与$$x$$ 之间的面积表示概率 $$p(y=y_2)$$，并且有 $$\sum_{k=1}^2p(y=y_k)=1$$



  假如$$x$$是模型的输入, $$y$$ 是模型的输出，那么模型将如何对$$x$$轴进行区间划分以使得分类的准确率达到最高，也就是最大化下面的函数 [[PRML]][PRML]

  $$maximize \quad p(correct) = \sum_{k=1}^K p(x\in R_k, y_k) \qquad (Eq.1)$$

  其中 $$R_k$$表示$$x$$轴上的第$$k$$分类区间，$$p(x\in R_k, y_k)$$表示数据集$$(x\in R_k, y_k)$$的联合分布。我们该如何理解上式所代表的意义呢？想象我们在高维空间划分出来很多小的子区域$$r_k^i$$，这些子区域都是由多个超平面包围起来构成的，并且每个子区域都有自己所属的类别（属于类别$$k$$的子区域可能有多个，并且互相不链接，因此我们写作$$r_k^i$$表示类别$$k$$的第$$i$$子区域，并且$$\sum_i r_k^i = R_k$$），这时当有新的数据点$$\vec x$$恰好落在子区域$$R_k$$，那么我们希望数据点$$\vec{x}$$属于类别$$k$$的概率大于其他类别的概率，即

  $$p(x\in R_k, y_k) > p(x \in R_k, y_j) \qquad j = [1, 2, .. k-1, k+1, .., K]$$

  这也就是上面最大化$$(Eq.1)$$的意义。

  在下图中我们标记出来三个点(黄色曲线和绿色曲线的交叉点)，这三个点便是我们寻找的划分点。由它们划分出的四个区间$$a=(-\infty, 1.72),\quad b=[1.72, 2.282), \quad c=[2.282, 2.595), \quad d=(2.595, -\infty)$$，

  ![decision_points](/images/decision_points.png)

  这里我们直接得出当

  $$R_1=b + d, \quad R_2 = a + c \qquad (Eq.2)$$

  时，方程$$(Eq.1)$$得以最大化(参考上一段的解释)。
  因此，如果我们构建的学习模型能够划分出等式$$(Eq.2)$$进行分类，那么该模型便具有最高的分类正确率。然而实际问题中我们通常得不到变量的联合分布函数（$$p(x, y)$$），如图中的黄色和绿色曲线。我们将证明通过乘法公式

  $$p(x, y) = p(y|x)\:p(x)$$

  最大化公式$$(Eq.1)$$ 等价于


  $$maximize \quad p(correct) = \sum_{k=1}^K p(y_k|x\in R_k) \qquad (Eq.3)$$

  其中
  $$p(y_k |x \in R_k)$$
  表示在已知 $$x\in R_k$$ 的信息条件下，$$y== y_k$$ 的条件概率，此条件概率便是各种学习模型的输出结果，因此是可以得到的。

[PRML]: http://www.springer.com/us/book/9780387310732
[PRML-pdf]: http://users.isr.ist.utl.pt/~wurmd/Livros/school/Bishop%20-%20Pattern%20Recognition%20And%20Machine%20Learning%20-%20Springer%20%202006.pdf
