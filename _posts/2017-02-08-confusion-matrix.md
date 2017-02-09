---
layout: post
title: Confusion matrix
date: 2017-02-08
categories: jekyll update
comments: true
---

## Confusion matrix

在机器学习领域，混淆矩阵用来衡量分类模型在测试数据上的表现。矩阵的列表示模型预测的类别实例，而行表示真实的类别实例。
[下图](https://en.wikipedia.org/wiki/Confusion_matrix)中是分类模型
对猫、狗、兔子三种动物进行分类的结果：

![](http://obmpvqs90.bkt.clouddn.com/cat_dog_rabbit.png)

图中第一行，模型将8只猫分对了5只，分错了3只（错分成狗）；第二行中，模型将6只狗分对了3只，分错了3只（其中2只错分成了猫，1只错分成了兔子）；
第三行中，模型将13只兔子分对了11只，分错了2只（错分成了狗）。可以看出该模型容易混淆猫和狗两种动物，而对兔子的识别较为准确。

因此，通过混淆矩阵不仅仅可以计算出模型在每一类别上的正确率，还可以得到错误分类的具体情况，这在数据类别严重不均衡的情况下尤为重要了。比如数据集中如果有95只猫，2只狗， 3只兔子，
那么当分类模型把所有输入都判断为猫的情况下，分类准确率仍达到95%；但是通过混淆矩阵我们除了可以得出综合准确率为95%以外，还可以得出模型判别猫的准确率为100%，判别狗和兔子的准确率却为0%。

我们以二分类问题为例来介绍一些更为专业的术语。

<!---
![](http://obmpvqs90.bkt.clouddn.com/tp_fn_fp_tn_part.png)
-->
![](/images/confusion_matrix/tp_tn_fp_fn_1.png)

[图中](http://www2.cs.uregina.ca/~dbd/cs831/notes/confusion_matrix/confusion_matrix.html)：

 condition positive -- **阳性**样本的真实数目 (c+d)
 
 condition negative -- **阴性**样本的真实数目 (a+b)
 
 predicted condition positive -- 模型预测结果中**阳性**样本的数目 (b+d)
 
 predicted condition negative -- 模型预测结果中**阴性**样本的数目 (a+c)

 true positive (TP) -- 实际为**阳性**样本且判断为**阳性**的数目 (d)
 
 true negative (TN) -- 实际为**阴性**样本且判断为**阴性**的数目 (a)

 false positive (FP) -- 实际为**阴性**样本但判断为**阳性**的数目 （b, Type I error: 错把未发生的事件判断为发生）

 false negative (FN) -- 实际为**阳性**样本但判断为**阴性**的数目 (c, Type II error: 把已发生的事件遗漏了)

 * accuracy (ACC):

   准确率：ACC = $$\frac{a+d}{a+b+c+d}$$

 * sensitivity, recall, hit rate, true positive rate (TPR):

   在真实**阳性**样本中，预测正确的样本所占的比例：
   TPR = $$\frac{d}{c+d}$$

 * precision, positive predictive value (PPV):
   
   预测结果为**阳性**的样本中，预测正确的样本所占比例：
   PPV = $$\frac{d}{b+d}$$

 * specificity, true negative rate (TNR):

   在真实**阴性**样本中，预测正确的样本所占的比例：
   TNR = $$\frac{a}{a+b}$$

 * negative predictive value (NPV):
 
   预测结果为**阴性**的样本中，预测正确的样本所占比例：
   NPV = $$\frac{a}{a+c}$$


## F1 score [(wiki)](https://en.wikipedia.org/wiki/F1_score)
 
 F1 score 是综合考虑了 precision 和 recall 的指标，用来衡量分类模型的准确率

 $$F1 = 2 \cdot \frac{1}{\frac{1}{recall}+\frac{1}{precision}} = \frac{2d}{2d+b+c}$$
 
 F1 的值在区间 [0, 1] 内，且越靠近 1 表明模型的准确率越高。

 另外一种称为 $$F_\beta$$ 形式如下:

 $$F_\beta = (1+\beta^2) \frac{1}{\frac{\beta^2}{recall}+\frac{1}{precision}}=\frac{(1+\beta^2)d}{(1+\beta^2)d+\beta^2c+b}$$

 可以看出 $$\beta^2$$ 的值越大，$$F_\beta$$ 赋予 recall 的权重就越大，也就是说 $$F_\beta$$ 的值更多的体现了 recall 的值。
 
## ROC (receiver operating characteristic) curve

ROC 曲线同 confusion matrix 一样用来衡量分类模型的优劣。如下图所示，x 轴表示 false positive rate (1-specificity)， y 轴表示 true positive rate (sensitivity)，因为 ROC 包含了 sensitivity 和 specificity， 因此 ROC 曲线上的每一点包含了该点对应的 confusion matrix 中的所有信息。


<!---
![](/images/confusion_matrix/ROC_space-2.png)
-->
![](http://obmpvqs90.bkt.clouddn.com/ROC_space-2.png?imageView2/1/w/500)


图中 A, B, C 和 C' 四个点对应的 confusion matrix 如下图所示

![](/images/confusion_matrix/ROC_space_1.png)

通常情况下，模型的 true positive rate (benefit) 值越大，false positive rate (cost) 的值也会越大，我们在选择模型时需要模型在这两个指标上达到最优（最理想的情况
是图中左上角的点(0, 1)）。



 ---