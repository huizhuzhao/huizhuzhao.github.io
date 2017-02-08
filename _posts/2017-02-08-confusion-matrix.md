---
layout: post
title: Confusion matrix
date: 2017-02-08
categories: jekyll update
comments: true
---

## Confusion matrix

在机器学习领域，混淆矩阵通常用来衡量算法在测试数据上的表现。矩阵的列表示算法预测的类别实例，而行表示真实的类别实例。比如，有一个
分类模型对猫、狗和兔子三种动物进行分类，我们可以使用混淆矩阵对该模型的预测结果进行评价。假设有8只猫，6只狗，13只兔子，模型预测结果的混淆矩阵如下所示：

![](http://obmpvqs90.bkt.clouddn.com/cat_dog_rabbit.png)

图中第一行该模型将8只猫分对了5只，分错了3只（错分成狗），第二行中6只狗分对了3只，分错了3只（其中2只错分成了猫，1只错分成了兔子），
第三行中13只兔子分对了11只，分错了2只（错分成了狗）。由此可以看出，通过混淆矩阵不仅仅可以计算出模型在每一类别上的正确率，还可以得到
错误分类的具体情况。在数据类别严重不均衡的情况下，混淆矩阵所起作用就更重要了，比如数据集中有95只猫，5只狗，那么当分类模型把所有输入都
判断为猫的情况下，分类准确率仍达到95%，但是通过混淆矩阵我们可以看出虽然模型判别猫的准确率达到100%，但是判别狗的准确率却为0%。

我们以二分类问题为例来介绍一些更为专业的术语。

![](http://obmpvqs90.bkt.clouddn.com/tp_fn_fp_tn_part.png)

图中：

 condition positive -- **阳性**样本的真实数目
 
 condition negative -- **阴性**样本的真实数目
 
 predicted condition positive -- 模型预测结果中**阳性**样本的数目
 
 predicted condition negative -- 模型预测结果中**阴性**样本的数目

 true positive (TP) -- 实际为**阳性**样本且判断为**阳性**的数目
 
 true negative (TN) -- 实际为**阴性**样本且判断为**阴性**的数目

 false positive (FP) -- 实际为**阴性**样本但判断为**阳性**的数目 （Type I error: 错把未发生的事件判断为发生）

 false negative (FN) -- 实际为**阳性**样本但判断为**阴性**的数目 (Type II error: 把已发生的事件遗漏了)

 sensitivity, recall, hit rate, true positive rate (TPR): 
 $$TPR=\frac{TP}{P}=\frac{TP}{TP+FN}$$

 precision, positive predictive value (PPV):
 $$PPV=\frac{TP}{TP+FP}$$

 specificity, true negative rate (TNR):
 $$TNR=\frac{TN}{N}=\frac{TN}{FP+TN}$$
 
 negative predictive value (NPV):
 $$NPV=\frac{TN}{TN+FN}$$

 accuracy (ACC):
 $$ACC=\frac{TP+TN}{P+N}$$

 F1 score
 $$F_1=\frac{2TP}{2TP+FP+FN}$$

 ---