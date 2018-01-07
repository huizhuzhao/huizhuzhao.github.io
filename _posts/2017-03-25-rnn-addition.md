---
layout: post
title: rnn--addition
date: 2017-03-25
---

Now we want to build an RNN model for addition, let's firstly to illustrate our problem clearly:

## the inputs

Let's restrict our model to up to 3 digits number addition, thus  the inputs includes two integer numbers (0-999) and 
one plus sign, like **12+237**. However, we need to do some tricks about the string **12+237** in order to let 
RNN model to understand it's meaning. The tricks consist of two parts:

* encoding

All the symbols need to be encoded to vectors before feeding into our model. In our problem, the symbols are integers 
*0*, *1*, *2*, *3*, *4*, *5*, *6*, *7*, *8*, *9* and plus sign *+*, and the one-hot type vectors with length 11 will be 
used, namely
```
0, [1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
1, [0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0]
2, [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0]
3, [0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0]
4, [0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0]
5, [0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0]
6, [0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0]
7, [0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0]
8, [0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0]
9, [0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0]
+, [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]
....
```

* feeding stream

After the encoding, we will now feed the encoded vectors, i.e. a matrix, sequentially into RNN model. Taking **12+237** as
an example, the encoded matrix is:
```
1, [0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0]
2, [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0]
+, [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]
2, [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0]
3, [0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0]
7, [0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0]
```

## the outputs
With **12+237** as an example, we hope the model can generate the result matrix representing string **249**.
```
2, [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0]
4, [0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0]
9, [0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0]
```

## padding
In the example **(12+237, 249)**, the input and output matrices have shapes **(6, 11)** and **(3, 11)**, respectively.
However, in case **(999+999, 1998)**, the shapes will be **(7, 11)** and **(4, 11)**.

In order to train RNN successfully, we need to unify their shapes, in other words, all the input matrices will have the 
same shape, and the same is true for output matrices.

To do this, we transform the inputs/outputs to strings with length **7**/**4** by padding **#** at the end. 
Namely, **12+237** will be transformed to **12+237#**, and **249** to **249#**. Thus, the above two matrices will be:

**12+237#** with shape=**[7, 12]**
```
1, [0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
2, [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0]
+, [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0]
2, [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0]
3, [0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0]
7, [0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0]
#, [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]
```
**249#** with shape=**[4, 12]**
```
2, [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0]
4, [0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0]
9, [0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0]
#, [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]
```
noting that the feature dimension changed from 11 to 12 above, with **#** as 

`#, [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]`.

and during training the model, **#** will be masked out.

## RNN model

![](http://on1loo82k.bkt.clouddn.com/addition_8.svg)

The first part of our RNN model is shown as the above figure in which the red rectangle indicates input vectors,
 and the blue one is output vector, and the middle green ones represent one lstm layer that has trainable parameters
 (weights and biases). It is this lstm layer that do the major computation in the model. The mechnism of lstm layer is shown below,
more details can be found in [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/).

![](http://on1loo82k.bkt.clouddn.com/lstm.svg)

As we can see in the above, the model read input vectors sequentially. Firstly, 

`1, [0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]`

was fed into the lstm layer, and we get it's output **h_1** . Secondly, 

`2, [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0]`  as well as **h_1** were fed into the lstm layer again, and we get the 
output **h_2**. Thirdly, 

`+, [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0]` and **h_2** were fed into the lstm layer, and the output is **h_3**, and so on.

Finally, we get the output **h_7** which contains all the infomation in string **12+237#**, and we hope the following
part the model have the potential to generate **249#** by taking **h_7** as input.

As the output string has length 4, we use four copies of vector **h_7** as the inputs of the second part of the 
RNN model as illustrated below (again, the four green rectangles represent one lstm layer). 
Thus we get four output vectors **o_1, o_2, o_3, o_4**

![](http://on1loo82k.bkt.clouddn.com/addition_5.svg)

Now, we can figure out the whole RNN model as the following. And we should train the parameters in the 
two lstm layers so that the four output vectors **o_1, o_2, o_3, o_4** always give the correct results.

![](http://on1loo82k.bkt.clouddn.com/addition_7.svg)


## code
As we restrict our model to 3 digits number addition, thus the dataset will be of size 1000 * 1000, i.e each sample has 
**input=a+b**, and **output=c** 
where $$a, b\in [0, 999]$$, $$c\in [0, 1998]$$


![](http://ok8deh2w3.bkt.clouddn.com/addition_matrix_4.png)

The training results is shown below:

![](http://ok8deh2w3.bkt.clouddn.com/addition_res.png?imageView2/0/w/2700)
<!---
![](/images/rnn_addition/embedding_2.svg)
-->