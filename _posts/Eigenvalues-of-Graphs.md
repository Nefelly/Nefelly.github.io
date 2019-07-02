---
title: Eigenvalues of Graphs
toc: true
date: 2019-01-14 17:54:05
tags: [Graph Theory, Spectral Graph Theory]
categories: 
- Graph Theory
- Chapter 01  Graphs
mathjax: true
---


图的特征值在图的研究中起到了非常重要的作用，谱图理论便是研究图的相关矩阵的特征值、特征向量与特征多项式之间的关系的学科。本文将简单介绍图的特征值的定义，给出几类特殊图的特征值，并给出特征值的实际应用。

------

#### 定义

> 图 $G$ 的特征值与特征向量定义为其邻接矩阵 $A_G$ 的特征值，即
>
> 若对于 $\lambda \in \mathbb{R}$，存在 $\boldsymbol{v} \in \mathbb{R}^N, \boldsymbol{v} \neq 0$ ，满足 $A_G \boldsymbol{v} = \lambda \boldsymbol{v}$，则称 $\lambda$ 为图 $G$ 的特征值， $\boldsymbol{v}$ 为 $\lambda$ 对应的特征向量。
>
> 特征值 $\lambda​$ 的特征向量构成 $R^N​$ 的一个子空间，该空间的维数即为特征值 $\lambda​$ 的重数，记作 $m(\lambda)​$ 。
>
> 为表示方便，将图 $G$ 的 $N$ 个特征值记作 $\lambda_1, \lambda_2, ...,\lambda_N$，且$\lambda_1 \ge \lambda_2 \ge ... \ge \lambda_N$ 。
>
> 图 $G$ 的谱 (spectrum)，记作 $Spec(G)$ ，定义为
> $$
> Spec(G) = Spec(A_G) = (\lambda_1)^{m(\lambda_1)}(\lambda_2)^{m(\lambda_2)}...(\lambda_N)^{m(\lambda_N)}
> $$
>

#### 性质 1

> 若 $\lambda$ 为图 $G$ 的一个特征值，$\boldsymbol{v}$ 为 $\lambda$ 对应的一个特征向量，其中 $\boldsymbol{v} = [\boldsymbol{v}_1, \boldsymbol{v}_2, ... ,\boldsymbol{v}_N]^T$，那么，
> $$
> \sum_{y \in N(x)} \boldsymbol{v}_y = \lambda \boldsymbol{v}_x
> $$
> 其中， $x$ 是图 $G$ 中任意一个节点， $N(x)$ 表示与 $x$ 相邻的节点组成的集合，即 $N(x) = \{y \in V(G):xy \in E(G)\}$。

#### 性质 2

> 因为无向图的邻接矩阵是实对称矩阵，所以显然有：
>
> - 无向图 $G$ 的特征值均为实数
> - 邻接矩阵 $A_G$ 是可对角化的
> - $A_G$ 特征向量可构成一组标准正交基

------

接下来，我们将给出两类特殊的图的特征值和相应的特征向量。

------

#### 定理 1  The Spectrum of $K_N$    

> $Spec(K_N) = (N-1)^1(-1)^{N-1}$

**证明：** 完全图 $K_N$ 的邻接矩阵可写作 $A=J - I$ ，显然，全 $1$ 向量 $\boldsymbol{j}$ 是 $A$ 的一个特征向量。因为 $A \boldsymbol{j} = J\boldsymbol{j} - I\boldsymbol{j} = (N-1) \boldsymbol{j}$ ，所以 $N-1$ 是图 $K_N$ 的一个特征值，但该特征值的重数未知。

因为不同特征值的特征向量相互正交，所以在寻找其它特征值时，只考虑所有与 $\boldsymbol{j}$ 正交的向量 $\boldsymbol{v}$ 。那么， $A\boldsymbol{v} = J\boldsymbol{v} - I\boldsymbol{v} = - \boldsymbol{v}$ 。因此，任意与 $\boldsymbol{j}$ 正交的向量都对应特征值 $-1$，所以特征值 $-1$ 的重数为 $N-1$，特征值 $N-1$ 的重数为 $1$ 。



#### 定理 2  The Spectrum of $K_{MN}$    

> $Spec(K_{MN}) = (\sqrt{MN})^1(0)^{M+N-2}(-\sqrt{MN})^1$

**证明：** 不妨设 $K_{MN}​$ 的邻接矩阵为
$$
A = \left[
    \begin{matrix}
    0_{MM} & J_{MN} \\
    J_{NM} & 0_{NN}
    \end{matrix}
\right]
$$
因为
$$
A\left[
\begin{matrix}
\boldsymbol{v} \\
\boldsymbol{w}
\end{matrix}
\right]=\left[
    \begin{matrix}
    J_{MN}\boldsymbol{w} \\
    J_{NN}\boldsymbol{v}
    \end{matrix}
\right]=\lambda\left[
    \begin{matrix}
    \boldsymbol{v} \\
    \boldsymbol{w}
    \end{matrix}
\right]\tag{1}
$$
若 $\boldsymbol{v}$ 是与 $\boldsymbol{j}_M$ 正交的向量，$[\boldsymbol{v}, \boldsymbol{0}]^T$ 为特征值 $0$ 对应的特征向量。

同理，若 $\boldsymbol{w}$ 是与 $\boldsymbol{j}_N$ 正交的向量， $[\boldsymbol{0},\boldsymbol{w}]$ 为特征值 $0$ 对应的特征向量。

所以，特征值 $0$ 的重数为 $M+N-2$ ，而其余特征值对应的特征向量可写做 $a[\boldsymbol{j}_M, \boldsymbol{0}]^T + b [\boldsymbol{0},\boldsymbol{j}_N]^T$

代入 $(1)$ 式可得方程 $\lambda a = b N$ 与 $\lambda b = a M$，解得 $\lambda =\pm \sqrt{MN}$，由此亦可得到相应的特征向量。

------

特征值并不便于可视化，为了更好地理解，我们给出特征值的一些性质，以观察其与图的结构之间的联系。

------

#### 定理 3 Bounds of $\lambda_1$

> 图 $G$ 的最大特征值 $\lambda_1$ 满足不等式：
> $$
> \bar{d} \le \lambda_1 \le \Delta
> $$
> 其中， $\bar{d}$ 表示平均度数， $\Delta$ 表示最大度数。

**证明：** 不妨设 $\boldsymbol{v}$ 为 $\lambda_1$ 对应的特征向量，其中 $\boldsymbol{v}_x$ 为 $\boldsymbol{v}$ 中绝对值最大的一项。那么，

$$
\lambda_1 \boldsymbol{v}_x = \sum_{y \in N(x)} \boldsymbol{v}_y
$$

因此，
$$
|\lambda_1| |\boldsymbol{v}_x| \le \sum_{y \in N(x)} |\boldsymbol{v}_y| \le \sum_{y \in N(x)} |\boldsymbol{v}_x| \le \Delta |\boldsymbol{v}_x| 
$$
$\boldsymbol{v}$ 不是零向量，所以 $|\lambda_1| \le \Delta$。而因为 $\sum \lambda_i = Tr(A) = 0$，所以 $\lambda_1 > 0$ ，可得 $\lambda_1 \le \Delta$ 。

令 $\{\boldsymbol{v}_1,\boldsymbol{v}_2,\cdots,\boldsymbol{v}_N\}$ 为矩阵 $A$ 的 $N$ 个两两正交的特征向量，可将向量 $\boldsymbol{j}$ 写作 $\sum c_i \boldsymbol{v}_i$。那么，
$$
\boldsymbol{j}^T A \boldsymbol{j} = \sum c_i \boldsymbol{j}^T A \boldsymbol{v}_i = \sum c_i \boldsymbol{j} \lambda_i \boldsymbol{v}_i = \sum c_i^2 \lambda_i \le \lambda_1 \sum c_i^2 = N \lambda_1
$$
因为 $\boldsymbol{j}^T A \boldsymbol{j} = |2E(G)|$，所以 $\lambda_1 \ge \bar{d}$ 。

------

最后，我们给出特征值一个简单应用。

------

#### 引理 4 Number of Closed Walk

> 图 $G$ 中长度为 $k$ 的闭路径数量等于 $\sum \lambda_i^k$。

**证明：** 由邻接矩阵的性质，节点 $i$ 到 $j$ 的长度为 $k$ 的路径数量为 $A_{ij}^k$，故所求即为 $\sum A_{ii}^k$ 。

将 $A$ 正交分解为 $A = S D S^{-1}$，其中 $D$ 为 $A$ 的特征值矩阵， $S$ 为相应的特征向量构成的正交矩阵。

$$
\sum A_{ii}^k = Tr(A^k) = Tr(SD^kS^{-1}) = Tr(D^k) = \sum \lambda_i^k
$$

证毕。



引理4给出了长度为 $k$ 的闭路径数量的一种近似方法：

> 令 $\boldsymbol{j} = \sum c_i \boldsymbol{v}_i$，则
> $$
> \lim_{k\rightarrow+\infty} \frac{\boldsymbol{j}^T A^k \boldsymbol{j}}{\lambda_1^k} = \lim_{k\rightarrow+\infty} \sum c_i^2 \frac{\lambda_i^k}{\lambda_1^k} = c_1^2
> $$
> 因此，当 $k$ 足够大时， $Tr(A^k) \approx c_1^2 \lambda_1^k $ 。




#### 定理 5 Bipartiteness

> 一个图是二分图当且仅当它的谱是对称的，即若 $\lambda$ 是图 $G$ 的特征值，则 $-\lambda$ 也是，且重数相等。

**证明：**  不妨设二分图 $G$ 的邻接矩阵为
$$
A = \left[
    \begin{matrix}
    0_{MM} & B \\
    B^T & 0_{NN}
    \end{matrix}
\right]
$$
若 $\lambda$ 是图 $G​$ 的特征值，
$$
A\left[
\begin{matrix}
\boldsymbol{v} \\
\boldsymbol{w}
\end{matrix}
\right]=\left[
    \begin{matrix}
    B \boldsymbol{w} \\
    B^T \boldsymbol{v}
    \end{matrix}
\right]=\lambda\left[
    \begin{matrix}
    \boldsymbol{v} \\
    \boldsymbol{w}
    \end{matrix}
\right]
$$

那么 $-\lambda$ 也是图 $G​$ 的特征值，
$$
A\left[
\begin{matrix}
\boldsymbol{v} \\
\boldsymbol{-w}
\end{matrix}
\right]=\left[
    \begin{matrix}
    -B \boldsymbol{w} \\
    B^T \boldsymbol{v}
    \end{matrix}
\right]=\lambda\left[
    \begin{matrix}
    \boldsymbol{v} \\
    \boldsymbol{-w}
    \end{matrix}
\right]
$$

显然，$\lambda$ 与 $-\lambda$ 的重数相同，所以二分图的谱是对称的。

若图 $G$ 的谱是对称的，那么对于任意奇数 $k$，
$$
\sum \lambda_i^k = 0
$$
因为 $\lambda$ 与 $-\lambda$ 在求和式中相消。这说明，图 $G$ 中不存在奇环，则图 $G$ 是二分图。

------



## 参考资料

> - https://dcg.epfl.ch/wp-content/uploads/2018/10/ADM-Eigenvalues-v3.pdf
> - Butler, Steven Kay. *Eigenvalues and structures of graphs*. Diss. UC San Diego, 2008.