---
title: draft
date: 0000-01-30 21:35:09
tags:
  - draft
mathjax: true
---

# LSTM
* 此篇文章对[LSTM单元](http://blog.csdn.net/songhk0209/article/details/71134698)讲的比较 细，主要是两张图，几个公式
![LSTM_originpic](http://p15i7i801.bkt.clouddn.com/34b4636de5dbb1676a6d547beb412cbc.png)
![LSTM_changpic](http://p15i7i801.bkt.clouddn.com/f579fb8e69d5b8920f84bf8936fd629c.png)

* 常见变种一：Gers & Schmidhuber在2000年提出。这种方法增加了“peephole connections”，即每个门都可以“窥探”到单元状态。这里，遗忘门和输入门是与上一单元状态建立连接，而输出门是与当前单元状态建立连接。
![LSTM_peephole](http://p15i7i801.bkt.clouddn.com/2488e6f9c12e514cea6088e878046b90.png)

* 常见变种二:将新信息加入的多少与旧状态保留的多少设为互补的两个值（和为1），即：只有当需要加入新信息时，我们才会去遗忘；只有当需要遗忘时，我们才会加入新信息。
![LSTM_MINUSONE](http://p15i7i801.bkt.clouddn.com/78d2296bdfe71e20e12cb13961a2c80a.png)

* 常见变种三：Gated Recurrent Unit（GRU），最早由Cho, et al.在2014年提出。这种方法将遗忘门和输入门连入了一个“更新门”（update gate），同时也合并了隐藏状态ht和单元状态Ct，最终的结果比标准LSTM简单一些。
* LSTM变种很多，结果显示这些变种表现差不多，具体参见Greff, et al. (2015)及Jozefowicz, et al. (2015)
* [来自MIT的Edwin Chen的一篇很有意思的解释](https://zhuanlan.zhihu.com/p/27345523)

# 增强学习
* 四个要素 $(A,S,R,P)$

* 策略 $\pi$ 决定选择哪个行动 $a$, 即：
  $$
  \begin{cases}
  \pi(s) \implies a \\
  \pi(a|s)
  \end{cases}
  $$
* 根据要素抽象行为成序列，通常要满足[马尔可夫条件](http://www.cnblogs.com/jinxulin/p/3517377.html),这些序列构成训练模型样本
  $$ \{s_1,a_1,r_1,s_2,a_2,r_2,...,s_t,a_t,r_t\} $$
* 定义目标 $G_t$，作为长期回报，其值用收益折现来表达，有 $G_t=\sum_{k=0}^N\gamma^kr_{k+t}$, 因此可推导目标期望：
$$
V_\pi(s)=E_\pi(G_t|S_t=s)  \\
Q_\pi(s,a)=E_\pi(G_t|S_t=s,A_t=a)
$$
* [Bellman等式](https://en.wikipedia.org/wiki/Bellman_equation)，也称动态规划等式，在RL里非常重要，其在此场景下用来表示长期回报——值函数：
$$
\mbox{ 在某策略下：}V_\pi(s)=\sum\pi(a|s)E[R_{t+1}+\gamma V(s_{t+1})|S_t=s]  \\
 V_*(s)=E[R_{t+1}+\gamma max_\pi V(s_{t+1})|S_t=s]  \\
 Q_*(s,a)=E[R_{t+1}+\gamma max_{a^\prime} Q(s_{t+1},a^\prime)|S_t=s,A_t=a]
$$
* 有了值函数 $V_\pi$的概念后,则问题抽象为在马尔可夫决策过程中，任意初始条件 $s$下，求能够最大化值函数的策略 $\pi$，其可表达为 $\pi^*=arg_\pi \{maxV_\pi(s)\}$，具体求解过程可参看[计算实例](http://www.cnblogs.com/jinxulin/p/3517377.html)
