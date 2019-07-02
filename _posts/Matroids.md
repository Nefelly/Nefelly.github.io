---
title: Matroids
toc: true
date: 2019-01-18 09:51:54
tags: [Graph Theory, Linear Algebra]
categories:
- Graph Theory
- Chapter 04  Trees
mathjax: true
---

拟阵(matroid)最先由Whitney在1935年提出，这一概念抽象地概括了线性独立的本质。本文主要介绍拟阵的定义与性质，几个拟阵实例，以及与拟阵相关的贪心算法。

------

## 定义

> $X$ 是有限集， $\mathcal{I}$ 是非空的 $X$ 的子集族，若二元组 $(X, \mathcal{I})$ 满足：
> (M1)： 若 $Y \in \mathcal{I}$，$Z \subset Y$，则 $Z \in \mathcal{I}$
> (M2)：若 $Y,Z \in \mathcal{I}$ 且 $\|Y\| < \|Z\|$，则存在 $x \in Z\backslash Y$，使得 $Y \cup \{x\} \in \mathcal{I}$
> 则称二元组 $(X, \mathcal{I})$ 为拟阵。

一般而言，二元组 $(X, \mathcal{I})$ 成为**集合系统**(set system)，满足性质(M1)的集合系统称作**独立集合系统**(independence system)。在无关集合系统中，$\mathcal{I}$ 中的集合称为**相互独立**的。

**基(basis)：** 集合 $X$ 中的极大独立子集称为 $X$ 的一组基。
由性质(M2)，集合 $X$ 的基的基数相等。
**秩(rank)：** 集合 $X$ 的基的基数称为 $X$ 的秩。

------

## 例子

### 均匀拟阵(Uniform Matroids)

> $X$ 是有限集， 取任意整数 $k$，令
> $$
> \mathcal{I} = \{Y \subset X:\|Y\| \le k\},
> $$
> 则 $M = (X, \mathcal{I})$ 是拟阵，该拟阵称为均匀拟阵。

### 线性拟阵(Linear Matroids)

> 矩阵 $A \in \mathbb{R}^{m\times n }$，记 $A_i$ 为矩阵 $A$ 的第 $i$ 列。令 
> $$
> X = \{A_i:i=1,2,...,n\} \\
> \mathcal{I} = \{Y \subset X: Y 中向量是线性无关的\}
> $$
> 则 $M = (X, \mathcal{I})$ 是拟阵，该拟阵称为线性拟阵。

![LinearMatroid](\images\LinearMatroid.png)

由线性代数的知识可知，集合 $X$ 的基对应于矩阵 $A$ 的一个极大线性无关组，亦对应线性空间 $span(A)$ 的一组基。因为所有线性无关的向量组都可扩展为线性空间的一组基，所以性质(M2)成立。

### 图拟阵(Graphic Matroids)

> 图 $G=(V,E)$，令 $X = E$ 
> $$
> \mathcal{I} = \{F \subset E: F 中的边不形成环\}
> $$
> 则 $M = (X, \mathcal{I})$ 是拟阵，该拟阵称为图拟阵。

![GraphicMatroid](\images\GraphicMatroid.png)

图 $G$ 的每个连通块之间互不影响，所以可以假设 $G$ 是连通图。而连通图中最大的无环子图恰为原图的一棵生成树，故集合 $X$ 的一组基就对应一个生成森林。显然，对于原图一个无环子图可以通过不断加边的方式得到一棵生成树，故性质(M2)成立。

------

## 最大权独立集(Maximum Weight Independent Set)

> 给定一个拟阵 $M=(X,\mathcal{I})$ 与权重函数 $w:X \rightarrow \mathbb{R}$，找到一个独立集 $Y \in \mathcal{I}$，最大化函数 $w(Y) = \sum_{y \in Y} w(y)$ 

该问题可由贪心算法解决。假定独立集中前 $i-1$ 个元素 $e_1,e_2, ... ,e_{i-1}$ 已选定，在选择第 $i$ 个元素时，令剩余元素中权值最大的，能保证 $\{e_1,...,e_i\} \in \mathcal{I}$ 的元素作为 $e_i$。持续该过程，直至无法再加入元素(构成集合 $X$ 的一组基)。算法流程如下：

![GreedyAlgForMaxWeightIndependentSet](\images\GreedyAlgForMaxWeightIndependentSet.png)

算法正确性证明如下：

反证法。假设贪心算法返回的元素依次为 $e_1,e_2,...,e_k$，最优基为 $\{e_1,e_2,...,e_k\}$。若存在一组权值更大的基为 $\{f_1,f_2,...,f_k\}$，不妨规定 $w(f_1)\ge w(f_2) \ge ... \ge w(f_k)$ ，则有
$$
w(e_1)+w(e_2)+...+w(e_k) < w(f_1)+w(f_2)+...+w(f_k)，
$$
取最小的下标 $i$，使得如下不等式成立：
$$
w(e_1)+w(e_2)+...+w(e_i) < w(f_1)+w(f_2)+...+w(f_i)，
$$
因此，
$$
w(e_1)+w(e_2)+...+w(e_{i-1}) \ge w(f_1)+w(f_2)+...+w(f_{i-1})，
$$
且 
$$
w(f_1) \ge w(f_2) \ge ... \ge w(f_i) > w(e_i)
$$
因为 $\{f_1,f_2,...,f_i\}$ 是独立集，且基数大于 $\{e_1,e_2,...,e_{i-1}\}$，由性质(M2)，存在 $j$，$1\le j \le i$，集合 $\{e_1,e_2,...,e_{i-1},f_j\}$ 也是独立集。而 $w(f_j) > w(e_i)$，所以贪心算法会在第 $i$ 轮选择 $f_j$ 而不是 $e_i$，矛盾。

图论中求最小生成树的Kruskal算法便是该算法的一个经典应用。算法的时间复杂度瓶颈在于如何判断一个集合是否属于独立集，若独立集的大小为指数级别，那很可能没有好的判别方式。然而，对于常见的图拟阵、线性拟阵，都存在判断的多项式算法，所以该贪心算法的实用性是非常高的。

同时，关于最优基的唯一性，可知以下推论成立：

### 推论

> 若权值函数 $w$ 是单射，则权值最大的基唯一。

证明过程类似算法正确性的证明。

------

## 参考资料
> - Bondy, John Adrian, and Uppaluri Siva Ramachandra Murty. *Graph theory with applications*. Vol. 290. London: Macmillan, 1976.
> - https://www.inf.ethz.ch/personal/ladickyl/Matroids.pdf
> - http://www.maths.qmul.ac.uk/~pjc/comb/matroid.pdf
> - https://dcg.epfl.ch/wp-content/uploads/2018/10/7-Matroids.pdf
