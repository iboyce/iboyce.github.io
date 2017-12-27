---
title: draft
date: 2017-12-27 15:10:09
tags:
  - draft
mathjax: true
---

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
