---
layout: post
title: RNN--addition
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
With **12+237** as an example, we hope the model can generate the result matrix representing string **359**.
```
3, [0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0]
5, [0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0]
9, [0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0]
```

## padding
In the example **(12+237, 359)**, the input and output matrices have shapes **(6, 11)** and **(3, 11)**, respectively.
However, in case **(999+999, 1998)**, the shapes will be **(7, 11)** and **(4, 11)**.

In order to train RNN successfully, we need to unify their shapes, in other words, all the input matrices will have the 
same shape, and the same is true for output matrices.

To do this, we transform the inputs/outputs to strings with length **7**/**4** by padding **#** at the end. 
Namely, **12+237** will be transformed to **12+237#**, and **359** to **359#**. Thus, the above two matrices will be:

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
**359#** with shape=**[4, 12]**
```
3, [0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0]
5, [0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0]
9, [0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0]
#, [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]
```

Noting that, symbol **#** was encoded as `#, [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]`, and the vector length of the 
other 11 symbols changed from **11** to **12**.

## RNN model
![](http://on1loo82k.bkt.clouddn.com/addition_3.svg)

In the above figure, the red rectangle indicates input vectors, and the blue one is output vector, and the middle
green ones are lstm layers which do the major computation in out model. The mechnism of lstm layer is shown below,
more details can be found in [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)


![](http://on1loo82k.bkt.clouddn.com/lstm.svg)

[understand-lstm-networks]: http://colah.github.io/posts/2015-08-Understanding-LSTMs/
