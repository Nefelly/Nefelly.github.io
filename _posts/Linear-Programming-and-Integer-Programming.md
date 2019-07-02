---
title: Linear Programming and Integer Programming
toc: true
date: 2019-01-16 19:29:51
tags: [Graph Theory, Linear Programming]
categories: 
- Graph Theory
- Chapter 08  Complexity of Algorithms
mathjax: true
---

线性规划(Linear Programming)是在一定的线性约束条件下最优化目标函数的问题。而图论中的一些经典问题亦可转化为线性规划问题进行求解，本文将从线性规划的角度出发，重新理解图论中的几个经典问题。

------

## 线性规划的基本概念

**原问题**

> max $\boldsymbol{cx}$ 
> subject to $\boldsymbol{Ax} \le \boldsymbol{b}$
> and $\boldsymbol{x} \ge \boldsymbol{0}$

**对偶问题**

> min $\boldsymbol{yb}$
> subject to $\boldsymbol{yA} \ge \boldsymbol{c}$
> and $\boldsymbol{y} \ge \boldsymbol{0}​$

**弱对偶定理**

> 若 $\boldsymbol{x}$ 是原问题的可行解， $\boldsymbol{y}$ 是对偶问题的可行解，则 $\boldsymbol{cx} \le \boldsymbol{yb}$ 
> **推论：**
> 若 $\boldsymbol{cx} = \boldsymbol{yb}$，则 $\boldsymbol{x}$ 是原问题的最优解，$\boldsymbol{y}$ 是对偶问题的最优解。

**对偶定理**

> 若原问题存在最优解，则对偶问题也存在最优解，且两个目标函数的最优值相等。

------

借助弱对偶定理，一些图论上的经典定理得到了有趣的解释。接下来，我们将三个图论中的经典问题与线性规划联系起来。

------

## Max Stable Set and Min Edge Covering

记无向图 $G$ 的关联矩阵为 $\boldsymbol{M}$。对于图 $G$ 的任意一个独立集 $S$，记向量 $\boldsymbol{x} = (x_v : v \in V(G))$，其中当 $v \in S$ 时， $x_v = 1$；当 $v \notin S$ 时， $x_v = 0$ 。考虑如下线性规划问题：

> max $\boldsymbol{1x}$
> subject to $\boldsymbol{M^\top x} \le \boldsymbol{1}$
> and $\boldsymbol{x} \ge \boldsymbol{0}​$ 

其中每个约束条件表示对于边 $u,v \in E$， $x_u + x_v \le 1$ ，即一条边的两端点不同时出现在独立集 $S$ 中。那么，该问题的最优解就对应了图 $G$ 的最大独立集。

考虑该问题的对偶问题：

> min $\boldsymbol{y1}$
> subject to $\boldsymbol{y M^\top} \ge \boldsymbol{1}$
> and $\boldsymbol{y} \ge \boldsymbol{0}$

对偶问题的每一个可行解 $\boldsymbol{y}$ 对应了图 $G$ 的一个边覆盖。因为约束条件中限制了对于任意节点，至少有一条与它相邻的边属于边覆盖。因此，对偶问题的最优解就对应了图 $G$ 的最小边覆盖。

由弱对偶定理可知，

> $\alpha(G) \le \beta'(G)$，其中 $\alpha(G)$ 表示图 $G$ 的最大独立集， $\beta'(G)$ 表示图 $G$ 的最小边覆盖。

特别地，二分图的关联矩阵 $M$ 是全幺模矩阵，所以上述线性规划问题的最优解必为整数。因此有如下定理：

### 定理 8.30 The König-Rado Theorem

> 在任意无孤立点的二分图中，最大独立集与最小边覆盖的大小相等。

------

## Max Matching and Min Covering

记无向图 $G$ 的关联矩阵为 $\boldsymbol{M}$。对于图 $G$ 的任意一个匹配 $M$，记向量 $\boldsymbol{x} = (x_e : e \in E(G))$，其中当 $e \in M$ 时， $x_e = 1$；当 $e \notin M$ 时， $x_e = 0$ 。考虑如下线性规划问题：

> max $\boldsymbol{1x}$
> subject to $\boldsymbol{M x} \le \boldsymbol{1}$
> and $\boldsymbol{x} \ge \boldsymbol{0}$ 

其中每个约束条件表示对于点 $v \in V(G)$， $\sum_{e \in E(G)} x_e \le 1$ ，即每个点至多与匹配中的一条边相邻。那么，该问题的最优解就对应了图 $G$ 的最大匹配。因此，匹配亦可称为最大边独立集。

考虑该问题的对偶问题：

> min $\boldsymbol{y1}$
> subject to $\boldsymbol{y M} \ge \boldsymbol{1}$
> and $\boldsymbol{y} \ge \boldsymbol{0}$

对偶问题的每一个可行解 $\boldsymbol{y}$ 对应了图 $G$ 的一个点覆盖。因为约束条件中限制了对于每条，至少有一个与它相邻的点属于点覆盖。因此，对偶问题的最优解就对应了图 $G$ 的最小点覆盖。

由弱对偶定理可知，

> $\alpha‘(G) \le \beta(G)$，其中 $\alpha’(G)$ 表示图 $G$ 的最大匹配， $\beta(G)$ 表示图 $G$ 的最小点覆盖。

特别地，二分图的关联矩阵 $M$ 是全幺模矩阵，所以上述线性规划问题的最优解必为整数。因此有如下定理：

### 定理 8.32 The König-Egerváry Theorem

> 在任意二分图中，最大匹配与最小点覆盖的大小相等。

------

## Max Flow and Min Cut

记无向图 $G$ 的关联矩阵为 $\boldsymbol{A}$，记 $\boldsymbol{A}$ 去掉 $s,t$ 所在行后得到的矩阵为 $\boldsymbol{A'}$。令权值向量为 $\boldsymbol{w} = (w_e : e \in E(G))$，当 $e$ 的终点为 $t$ 时， $w_e = 1$；否则， $w_e = 0$ 。考虑如下线性规划问题：

> max $\boldsymbol{w^\top x}$
> subject to $\boldsymbol{A' x} = \boldsymbol{0}$
> and $\boldsymbol{0} \le \boldsymbol{x} \le \boldsymbol{c}$ 

其中 $\boldsymbol{x}$ 表示每条边的流量，$\boldsymbol{c}$ 表示每条边的流量上限。约束条件分别表示中间节点的流量平衡条件与流量限制。因此，该线性规划问题的可行解 $\boldsymbol{x}$ 对应图 $G$ 的可行流，最优解对应图 $G$ 的最大流。

考虑该问题的对偶问题：

> min $\boldsymbol{c^\top y}$
> subject to $\boldsymbol{A'^\top z} + \boldsymbol{y} \ge \boldsymbol{w}$
> and $\boldsymbol{z} \in \mathbb{R}^{n-2}, \boldsymbol{y} \ge \boldsymbol{0}$

记原问题最优解为 $\boldsymbol{x^\star}$，对偶问题的最优解为 $(\boldsymbol{y}^\star,\boldsymbol{z}^\star)$ ，扩展向量 $\boldsymbol{z}^\star$ 至 $\mathbb{R}^n$ ，令 $z_s^\star = 0, z_t^\star = -1$ 。重新考察约束条件： $\boldsymbol{A^\top z^\star}+\boldsymbol{y^\star} = \boldsymbol{A'^\top z^\star} - \boldsymbol{w} + \boldsymbol{y} \ge 0$，因为 $\boldsymbol{y}$ 要尽可能地小，所以最优解中对于边 $e =(u,v)$， $y_e^\star = max\{z_u^\star-z_v^\star,0\}$

定义点集 $U = \{u \in V:z_u^\star \ge 0\}$，则 $s \in U,t \notin U$，$\partial(U)$ 是 $s-t$ 的割。而对于任意边 $e = (u,v) \in \partial(U)$，有 $y_e^\star \ge z_u^\star - z_v^\star \ge 1$ 。因此，$\boldsymbol{c^\top y^\star} \ge \sum_{e \in \partial(U)} c_e$ 。因为有向图的关联矩阵是全幺模矩阵，由弱对偶定理，$\boldsymbol{c^\top y^\star} = \boldsymbol{w^\top x^\star} \le \sum_{e \in \partial(U)} c_e$ 。因此，对偶问题的最优解对应了最小割。

------

## 参考资料
> - Bondy, John Adrian, and Uppaluri Siva Ramachandra Murty. *Graph theory with applications*. Vol. 290. London: Macmillan, 1976.
> - https://theory.stanford.edu/~jvondrak/MATH233B-2017/lec3.pdf
> - https://www.math.unipd.it/~luigi/courses/metmodoc/m07.assTum.en.pdf
