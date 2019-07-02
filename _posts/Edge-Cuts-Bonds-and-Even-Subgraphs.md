---
title: Edge Cuts, Bonds and Even Subgraphs
toc: true
date: 2019-01-21 10:32:09
tags: [Graph Theory]
categories: 
- Graph Theory
- Chapter 02  Subgraphs
mathjax: true
---

断集(edge cut)、割集(bond)是图论中的基本概念，由这两个概念引出了许多图论中的问题与算法。一个图是欧拉图当且仅当它是偶图(even graph)，偶图较好的性质引起了对其不少的探究。本文将简单介绍断集、割集的概念，及其与偶图的关联。

------

## 断集


### 定义

> 无向图 $G=(V,E)$ 中，$X,Y$ 是集合 $V$ 的两个子集(可以相交)。令 $E(X,Y)$ 表示图 $G$ 中一端在 $X$，另一端在 $Y$ 的边组成的集合，$e(X,Y)$ 表示其中边的数量。
> 当 $Y = X$ 时，可将 $E(X,X)$ 和 $e(X,X)$ 简记为 $E(X)$ 和 $e(X)$
> 当 $Y = V\backslash X$ 时，$E(X,Y)$ 称作图 $G$ 中关于点集 $X$ 的**断集**，记作 $\partial(X)$ 

由度数的等式，显然可以得到下面定理：

### 定理 2.9

> 对于任意图 $G$ 和顶点集 $V$ 的任意子集 $X$，有
> $$
> |\partial(X)| = \sum_{v \in X} d(v) - 2e(X)
> $$
>

该定理给出了断集与图中节点度数的基本关系，利用该等式可得到判断偶图的一个充要条件：

### 定理 2.10

> 图 $G$ 是偶图当且仅当对于顶点集 $V$ 的任意子集 $X$，$|\partial(X)|$ 都是偶数。

**证明：** 对于每个节点 $v$，$|\partial({v})| = d(v)$ 是偶数，故所有节点度数均为偶数，图 $G$ 是偶图。

由定理 2.9，必要性成立。


集合的对称差操作等价于异或运算，是构成割空间(bond spcae)与环空间(cycle space)的基础，以下命题是引入割空间这一概念的基础：

### 命题 2.11

> 若 $X,Y$ 是图 $G$ 顶点集的任意子集，那么
> $$
> \partial(X) \Delta \partial(Y) = \partial(X \Delta Y)
> $$
>

**证明：** 考虑点集 $V$ 的一个分割，
$$
(X \cap Y, X \backslash Y, Y\backslash X, \bar{X} \cap \bar{Y})
$$
如下图所示：

![Figure2.9](\images\Figure2.9.png)

在图中画出 $\partial(X), \partial(Y), \partial(X \Delta Y)$ 对应的边，即得下图：

![Figure2.10](\images\Figure2.10.png)

由此可知， $\partial(X)\Delta  \partial(Y) = \partial(X \Delta Y)$


由命题 2.11 可以得到下面的重要推论：

### 推论 2.12

> 两个断集的对称差仍是断集。


与命题 2.11 的证明类似，通过 Venn 图的表示，易知如下命题成立：

### 命题 2.13

> 若 $F_1$ 与 $F_2$ 是图 $G$ 的两个生成子图， $X$ 是 $V$ 的任意子集，则
> $$
> \partial_{F_1 \Delta F_2}(X) = \partial_{F_1}(X) \Delta \partial_{F_2}(X)
> $$
>

------

## 割集


### 定义

> 极小的非空断集称为**割集**，即割集的任意一个真子集都不是断集。


定理 2.14 给出了割集与断集之间的关系。


### 定理 2.14

> 边集 $X$ 是断集当且仅当它是若干个不相交的割集的并。

**证明：** 若 $X$ 不是割集，则存在一个 $X$ 的真子集是割集。从 $X$ 中去掉该真子集后得到的边集仍是断集，持续该过程直至 $X$ 是割集，即得到一个分割。


对于连通图，判断割集的方法十分简单，定理 2.15 给出了割集的充要条件。


### 定理 2.15

> 连通图 $G$ 中，非空断集 $\partial(X)$ 是割集当且仅当 $G[X]$ 与 $G[V \backslash X]$ 都是连通的。其中，$G[X]$，$G[V \backslash X]$ 分别表示 $G$ 关于点集 $X$ 与 $V \backslash X$ 的导出子图。

**证明：** 必要性。若 $\partial(X)$ 是割集，$Y$ 是 $X$ 的任意子集。因为图 $G$ 是连通的，所以 $\partial(X\backslash Y)$ 与 $\partial(Y)$ 非空。同时， $E[Y, X\backslash Y]$ 非空，若非不然，$\partial(Y)$ 是 $\partial(X)$ 的真子集，与 $\partial(X)$ 是割集矛盾。因此，$G[X]$ 连通。同理可证，$G[V\backslash X]$ 连通。

充分性。若 $\partial(X)$ 不是割集，则存在 $V$ 的真子集 $Y$，$X \cap Y \neq \empty$ 且 $\partial(Y) \subset \partial(X)$ 。这说明 $X \cap Y$ 与 $Y \backslash X$ 之间没有边， $\bar{X} \cap Y$ 与 $\bar{X} \backslash Y$ 之间也没有边。然而，因为 $G[X]$ 与 $G[V \backslash X]$ 都是连通的，所以 $X \cap Y$ 与 $\bar{X} \cap Y$ 都只能是空集，矛盾。

------

## 偶子图


### 定义

> 无向图的生成偶子图称为该图的偶子图。


由命题 2.13 可直接得到如下推论：

### 推论 2.16

> 两个偶子图的对称差仍是偶子图。


环是极小的偶图，因此Veblen定理可重述为如下定理：


### 定理 2.17

> 图 $G$ 是偶图当且仅当它的边集是若干个边不相交的环的并。


定理 2.14 与定理 2.17 的描述是构成了环空间与割空间的基础。关于这两个线性空间的概念，将在之后详述。

------

## 参考资料
> - Bondy, John Adrian, and Uppaluri Siva Ramachandra Murty. *Graph theory with applications*. Vol. 290. London: Macmillan, 1976.
