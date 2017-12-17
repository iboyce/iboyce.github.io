---
title: Neural Networks for Machine Learning
date: 2016-06-07 13:26:48
tags:
      - 神经网络
      - Geoffrey hinton
      - 公开课
categories: AI梦
mathjax: true
---



# 机器学习：不必为特定任务编写程序
## 场景落地
- Recognizing pattern     
  - Objects    
  - facial    
  - Spoken word
- Recognizing anomalies    
  - credit card transaction    
  - Sensor reality
- Prediction    
  - stock price,
  - exchange rate   
  - movie like

##几种简单模型
- Linear neurons
$ y=b+\sum x_iw_i $
- Binary threshold neurons
$$
z=\Sigma x_i w_i \quad
y=\begin{cases}
1&if\;z \gt 0\\
0&otherwise
\end{cases} \quad or \qquad
\theta=-b \quad
z=b+\Sigma x_i y_i \quad
y=\begin{cases}
1&if\;z \gt \theta\\
0&otherwise
\end{cases}
$$
- Rectified Linear Neurons 2
$$z=\Sigma x_i w_i, y=
\begin{cases}
z,	&if\;z \gt 0 \\
0,	&\mbox{otherwise}
\end{cases}$$
- sigmoid neurons
$$ z=b+\Sigma x_i w_i  \quad y=\frac {1} {1+e^{-z}} $$
- Stochastic binary neurons
$$z=b+\Sigma x_i w_i  \quad p(s=1)=\frac {1} {1+e^{-z}}$$

## 学习的类型
- supervised learning
  * Regression
  * model class: $y=f(x;w)$
  * 1/2这个系数在求导时被抵消
  * classification
- reinforced learning
the output is an action or sequence of actions and the only supervisory is an occasional scalar reward._This is difficult_, The rewads are typically delayed so its had to know where we went wrong( or right)
- unsupervised learning

## 神经网络的类型
- Feed-Forward neural network
  if there is more than one hidden layer, we call them "deep" neural networks.
- Recurrent network
  It is hard to train but natural way for modeling sequence, recent algorithm can be able to do this
  also can be used to predict stock price.
- Symmetrically connected networks

## 感知器
> how to learn biases using the same rule as we use for learning weights

  - if the output unit is correct, leave its weights alone, if the output unit incorrectly output
  - __错误的输出了零，则Z需要新增以致其逐渐大于零而产生y=1（往正面），反之则需要减__ ？？此偏移向量为负如何解释，或者必须保证 该向量是指向正确的分类超平面的（perpendicular，正交）。
  - $(w,b) \leftarrow (w,b)-(x,1)$
    $(w,b) \leftarrow (w,b)+(x,1)$
  - *just like penalty function*

> Why the learning works: _Informal sketch of proof of convergence_

  1. Each time the perceptron makes a mistake, the current weight vector moves to decrease its squared distance from every weight vector in the "generously feasible" region.
  2. <strong> The squared distance decreases by at least the squared length of the input vector. </strong>（。。向量的运算，几何解释）
  3. So after a finite number of mistakes, the weight vector must lie in the feasible region if the region exist.

## 感知器的缺陷
> **right feature**

  Once the hand-coded features have been determined, there are very strong limitations on what a perceptron can learn.
  _The main question is : This type of table look-up won't generalize, it need too many feature_
  _此篇习题未理解_

> Group Invariance Theorem---Minsky and Papert
can't learn to do this if the transformations from a group{欧氏变换之内}，so it needs to use multiple feature unit to recognize transformations of informative sub-patterns.

So,more  important was all about how you learn **feature detectors, that's hidden units**
After 20 years, We know:
we need multiple layer of adaptive, non-linear hidden units.
