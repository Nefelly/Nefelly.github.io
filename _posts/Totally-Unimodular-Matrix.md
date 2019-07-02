---
title: Totally Unimodular Matrix
toc: true
date: 2019-01-15 17:32:37
tags: [Graph Theory, Matrix Analysis]
categories: 
- Graph Theory
- Chapter 01  Graphs
mathjax: true
---

全幺模矩阵是矩阵分析中的重要概念，它在整数线性规划中亦起到了重要的作用。这一概念将整数规划与线性规划的可行解联系起来，同时对图论中一些经典问题的理解也有很大的帮助。本文简单引入这一概念，并简单介绍其在图论中的应用。

------

## 定义

> 一个矩阵是全幺模的，当且仅当它的每一个子方阵的行列式是0、1或-1。

## 性质

> 若矩阵 $A$ 是全幺模的，则
>
> 1.  $a_{ij} \in \{-1, 0, 1\}$
> 2. $A$ 的任意一行或一列乘以-1后得到的矩阵是全幺模的
> 3. 矩阵 $-A$，$A^\top$，$[A,I]$，$[A,-A]$ 也是全幺模的

------

当然，全幺模矩阵最重要的性质在于其在线性规划中的应用。当一个线性规划问题的约束矩阵是全幺模矩阵时，它的最优解一定是整数解。

## 定理 1

> 若 $A(A \in \mathbb{Z}^{m \times n})$ 是全幺模矩阵，那么 $A \boldsymbol{x} \ge \boldsymbol{b}$ 的所有基解都是整数解。

**证明：** 

线性规划的基解由线性方程组 $A' \boldsymbol{x} = \boldsymbol{b}$ 解得，其中  $A'$ 是约束矩阵 $A$ 的一个 $n$ 阶非奇异子矩阵。

因为 $A$ 是全幺模矩阵，所以 $det(A') = 1$ 或 $-1$ 。

由Cramer法则可知， $\boldsymbol{x}_i = \frac{det(A'_i)}{det(A')}$，故 $\boldsymbol{x}$ 是整数向量。

------

因此，当整数规划问题的约束矩阵是全幺模矩阵时，可以将问题看做线性规划来解决，因为线性规划的最优解必定是整数解，也就对应了原整数规划的最优解。

接下来，我们来说明图论中两类图的关联矩阵(incidence matrix)是全幺模矩阵。

------

## 定理 2

> 无向二分图的关联矩阵是全幺模矩阵。

**证明：** 记二分图的关联矩阵为 $A$，取 $A$ 的任意子方阵 $A'$ 。

对 $A'$ 的大小进行归纳。

当 $A' \in \mathbb{Z}^{1 \times 1}$ 时，因为无向图关联矩阵中的元素只有 $0$ 和 $1$，所以结论成立。

假设当 $A' \in \mathbb{Z}^{k \times k}$ 时， $det(A')=0,1,-1$，现证明当 $A' \in \mathbb{Z}^{(k+1) \times (k+1)}$ 时，结论也成立。

Case 1：若 $A'$ 的某一列为 $0$，则 $det(A') = 0$

Case 2：若 $A'$ 的某一列只有一个 $1$ ，则可将 $A'$ 写作
$$
A' = \left[
    \begin{matrix}
    1 & a^\top \\
    0 & A''
    \end{matrix}
\right]
$$
因此有 $det(A') =det(A'')$ 或 $det(A') = -det(A'')$ ，由归纳假设， $det(A') \in \{0,1,-1\}$

Case 3：若 $A'$ 的每一列都有两个 $1$ ，则可将 $A'$ 写作
$$
A' = \left[
    \begin{matrix}
    A_{up} \\
    A_{down}
    \end{matrix}
\right]
$$
因为 $A$ 是二分图的关联矩阵，所以可以令 $A_{up}$ 和 $A_{down}$ 的每一列都有且仅有一个 $1$

将 $A_{up}$ 的每一行乘以 $1$ 加上 $A_{down}$ 的每一行乘以 $-1$ 后求和，可得到 $0$ 向量。因此，$A'$ 的行向量是线性相关的，故 $det(A') = 0$，结论成立。



## 定理 3

> 有向图的关联矩阵是全幺模矩阵。

**证明：**证明过程同**定理2**，其中Case 3有细微差别。

Case 3：若 $A'$ 的每一列都有两个非零元素，则每列都恰好包含一个 $1$ 和一个 $-1$，故列和为 $0$ 。

因此， $det(A') = 0$，结论成立。

------

这两类图的全幺模矩阵在两个经典的问题中起到了重要作用，可结合线性规划与图的匹配、最大流问题进行分析。



## 参考资料

> - https://imada.sdu.dk/~marco/Teaching/Fall2009/DM204/Slides/TUM-lau.pdf
> - https://www.ise.ncsu.edu/fuzzy-neural/wp-content/uploads/sites/9/2016/02/or766_TUM.pdf
> - Bondy, John Adrian, and Uppaluri Siva Ramachandra Murty. *Graph theory with applications*. Vol. 290. London: Macmillan, 1976.
