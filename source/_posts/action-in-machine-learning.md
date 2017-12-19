---
title: action in machine learning
date: 2017-08-29 18:21:54
tags:
      - 机器学习
      - 经典著作
categories: AI梦
mathjax: true
---

### 树回归
* 连续型数值的混乱度：总平方误差来表示，即方差*m
* 离散型的标称的混乱度可以用香农熵表示
* 若叶节使用的模型是分段常数则称为回归树，若叶节点使用的模型是线性回归方程则称为模型树
* 使用CART构建出的树倾向于过拟合，分别使用预剪枝和后剪枝解决这个问题。预剪枝设置停止条件来调整拟合问题，这需要不断调整，见P168。而后剪枝首先构造足够复杂的树，然后使用测试集来判断叶节点合并能否降低误差
* 决策树通过迭代实现分类，离散情况下，叶节点的类别即预测的类别，连续情况下，若是回归树则是该子树叶子节点的平均值，若是模型树，则是该（线性）模型的值

### Random Forest/GBDT
[参考介绍一：二分类](http://blog.csdn.net/google19890102/article/details/51746402)
[参考介绍一:多分类](http://www.cnblogs.com/LeftNotEasy/archive/2011/03/07/random-forest-and-gbdt.html)
*  随机建立树的方式，随机采样包括行采样（样本），列采样（特征）
* 即本质是每颗树是窄领域内的专家，众专家一起投票

###预测数值型数据:回归
#### 线性回归
  使用最小二乘法，得$若X非奇异，则有w=(X^tX)^{-1}X^ty$
#### 局部加权线性回归（Local Weighted Leaner Regression）
  线性回归的问题是容易欠拟合，因此引入局部加权
  $$\hat{w}=(X^twX)^{-1}X^twy$$
  通常使用高斯核用来赋于权重$w(i,i)=e^{\frac {x^{(i)}-x}{-2k^2}}$，即有离预测点越近的点权重越大，同时参数K控制了参与运算的数据，这样就有如下图:
![aiml-localweightedLR](http://p15i7i801.bkt.clouddn.com/d1676ee6aefd1a476cc7f40036c87f5c.png)

  此方法缺点在于**计算量增加，每次预测必须在全集上运行**，好处在于可以控制拟合程度
![aiml-LR](http://p15i7i801.bkt.clouddn.com/e9cc4d793fd511a4e7749fa6660005c5.png)

#### 缩减系数——用于更好的理解数据并处理特征比样本多的问题
  对于$X^TX$为奇异矩阵，在$X^TX$基础加上 $\lambda I$使得矩阵非奇异，这种方法称为*岭回归*。此方法有三个用途：
  * 用于处理特征比样本多的情况
  * 用于在估计中加入偏差，从而得到更好的估计
  * 通过引入   $\lambda$ 来限制 $w$ 之和，通过引入惩罚，能够减少不重要的参数，这类技术在统计学称为衰减。（迹不变）
  * 此公式$$等价于最小二乘加入约束

### 附加篇：各类方法的一个归纳
* 树模型：DT, GBDT, RF
* 概率模型：Bayes
* 最优化：LR, SVM
    * LR：简单实用，互联网CTR预估被广泛使用
    * SVM：简单、多分类问题比SVM好，不好解释；
* 距离划分，判别模型
    * KNN：简单、多分类问题比SVM好，不好解释；
* 集成方法：Adaboost
* 方法比较
    * NB与LR
      * 相同点：都是特征的线性表述，解释性对较好；
      * 不同点：NB要求严格独立，NB有利于并行化，但随着数据量和维度增多，LR更合适
* 可持久化的模型：决策树

### 决策树|随机森林|adaboost|GBDT
* [决策树模型组合之（在线）随机森林与GBDT](http://www.cnblogs.com/wentingtu/archive/2011/12/13/2286212.html)
* [Bagging（Bootstrap aggregating）、随机森林（random forests）、AdaBoost](http://blog.csdn.net/xlinsist/article/details/51475345 )
* [决策树ID3、C4.5、C5.0以及CART算法之间的比较-并用scikit-learn决策树拟合Iris数据集](http://blog.csdn.net/xlinsist/article/details/51468741)
* ID3缺点:
    *  对于多值的属性非常之敏感
    *  无法处理连续值
    *  容易产生过拟合，即训练数据训练太彻底，但大一点数据集错误率上升，关注了些局部信息
* C4.5---C5.0
  * 解决上述1、2的问题，核心思想是加入了增益率
* CART
  * 能预测出值（回归），同时能全用训练和交叉验证不断评估，修剪决策树

### K-nearest
* 思路：基于现有已知标签的样本数据集，寻找被预测样本的最近的K个样本，返回K个里频率最多的那个标签。
* 优点：最简单有效的分类、对异常值不敏感
* 缺点：解释性差、类别评分无规格化，不平衡问题
* 适应：[brute force\kd_tree\balltree的选择](http://scikit-learn.org/stable/modules/neighbors.html#unsupervised-nearest-neighbors )

### PCA与SVD
http://blog.csdn.net/jacke121/article/details/59057192
pca是单方向上的降维，SVD是两个方向上的降维。
SVD表示是$A=U\Sigma V^T$，其中U,V是正交的。
若要降维：使用这个公式，其具体数学推导，暂不明。现实含义可以这样理解：
在SVD的三个矩阵（假设叫1，2，3）中，1-2表示用户降维转换，2-3表示物品降维转换，在用户推荐那个场景，由于是使用基于物品的推荐，要计算两物品的相似度，则可理解为只需要用户角度降维，即1-2的转换。即有
$$U_k \Sigma V=> A^T U_k \Sigma$$
推导点：**如如此在用户上降维，那是否可以直接通过PCA在用户角度降维？**

### 关联分析
支持度，可信度
* Apriori

### 附加篇一
> 张同学的问题：SVM中，如下代码中权重 $w$ 为何不能做特征的权重值。

```python
def calcWs(alphas, dataArr, classLabels):
    """
    输入：alphas, 数据集, 类别标签
    输出：目标w
    """
    X = mat(dataArr)
    labelMat = mat(classLabels).transpose()
    m, n = shape(X)
    w = zeros((n, 1))
    for i in range(m):
        w += multiply(alphas[i] * labelMat[i], X[i, :].T)
    return w
```
对比线性情况而言,有 $w= \Sigma \alpha y_i x_i$ ，书中有下代码
```python
w += multiply(alphas[i] * labelMat[i], X[i, :].T)
```
目标函数为：$y=(\Sigma \alpha y_i x_i) x + b$ 而对于映射核空间的情况，书中有描述
![aiml-weightbook](http://p15i7i801.bkt.clouddn.com/c9fb298cf712884a5ad1c6d2407c4b95.png)
此时目标函数则为 $y=\Sigma \alpha y_i k(\phi(x_i),\phi(x_j))+b$。显然，特征向量 $w$ 是无法拆出来的。

> 对weights = weights + alpha * dataMatrix.transpose() * error 这一行的理解

* 角度一：http://blog.csdn.net/lu597203933/article/details/38468303  AndrewNg
![aiml-weight](http://p15i7i801.bkt.clouddn.com/79f4eb72472afa25f82690b0823b603d.png)
* 角度二：矩阵微分的角度理解 http://blog.csdn.net/aichipmunk/article/details/9382503

### 附加篇二：机器学习算法路径图
![aiml-algorithm chea-sheet](http://p15i7i801.bkt.clouddn.com/e161673fc2063c42f4d407fd7057fc1f.png)
![aiml-td](http://p15i7i801.bkt.clouddn.com/daa070eafedebe29f976a12a0b65b08c.png)
