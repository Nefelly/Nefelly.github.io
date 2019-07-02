---
title: Menger's Theorem (Undirected Vertex Version)
toc: true
date: 2018-12-26 19:50:43
tags: [Graph Theory]
categories: 
- Graph Theory
- Chapter 09  Connectivity
mathjax: true
---

------

#### 定理 9.1   MENGER 定理 (无向图顶点版本)

> 在图$G$中，令$x$和$y$为不相邻的两顶点，则$x$和$y$之间点不相交的最大路径数量等于$x$和$y$之间点割的大小，即  $ p(x, y) = c(x, y) $  
>

**证明：** 方便起见，记  $k = c(x, y)$

显然， $p(x,y) \le k$ ，因为如果路径数量多于 $k$，则删 $k$ 个点图 $x$ 和 $y$ 仍连通。

以下只证明 $p(x,y) \ge k​$ 

对图 $G$ 边数 $e(G)$ 做归纳，

![Figure9.3](/images/Figure9.3.png)

整个证明的思路是去掉一条边 $e$，利用归纳假设，通过 $G \setminus e$ 中的不相交路径构造 $G$ 中的不相交路径。

找到一条边 $e=uv$ ，边的两端点不同于 $x$ 和 $y$ 。当$G$中不存在这样的边时， $x$ 到 $y$ 的所有路径都是长度为2的，只需割掉中间节点，就能使 $x$ 和 $y$ 不连通。

记图 $G \setminus e$ 中点割为 $S$ ，则 $ c_{G \setminus e}(x,y) = |S|$ ，因为 $G$ 和  只差了$G \setminus e$一条边，那么 $S \cup \{u\}$ 必定是图 $G$ 的一个点割，所以 $c_{G \setminus e}(x,y) = k$ 或者 $c_{G \setminus e}(x,y) = k-1$ 。

如果 $c_{G \setminus e}(x,y)=k$ ，那么根据归纳假设， $G/ e$ 中必存在 $x$ 到 $y$ 的 $k$ 条不相交路径，那么这 $k$ 条路径必然在 $G$ 中，故 $p_G(x,y) \ge k$ 。

如果 $c_{G \setminus e}(x,y)=k-1$ ，那么根据归纳假设， $G/ e$ 中必存在 $x$ 到 $y$ 的 $k-1$ 条不相交路径，则 $G$ 中第 $k$ 条路径必然包含 $e$ 。

记 $Y$ 为图 $G \setminus e-S$ 中 $y$ 所在的连通分支，在图 $G$ 中将 $Y$ 缩点，得到的图记为 $G/Y$ 。因为 $G$ 中 $x$ 到 $y$ 的路径可转化为 $G/Y$ 中 $x$ 到 $y$ 的路径，所以 $c_{G/Y}(x,y) \ge k$ ；又因为 $S \cup \{u\}$ 仍是 $G/Y$ 的点割，所以 $c_{G/Y}(x,y) \le k$ ；故 $c_{G/Y}(x,y) = k$ 。而 $v \ne y$ ，因此 $|Y| \ge 2$ ，那么 $e(G/Y) < e(G)$ ，满足归纳假设，可在 $G/Y$ 中找到 $k$ 条 $x$ 到 $y$ 的不相交路径。同理，也可以在 $G/X$ 中找到 $k$ 条 $x$ 到 $y$ 的路径。两种路径拼接后，即得到 $G$ 中 $x$ 到 $y$ 的 $k$ 条不相交路径。因此， $p_G(x,y) \ge k$ 。

**总结**：这个证明是比较繁琐的，主要是要想办法利用归纳假设。最核心的思路是删边、缩点、找路径，其中讨论了一些不方便归纳的特殊情况。

------

直觉上，图中不相邻的顶点之间的不相交路径数量应不多于相邻顶点间的数量。下面的定理给出了证明。

------

#### 定理 9.2   

> 若 $G$ 中存在至少一对不相邻的节点 $x$ 和 $y$ ，那么
> $$
> \kappa(G) = \min\{p(u,v):\quad u, v \in V, u \ne v, uv \notin V\}
> $$
> 其中, $\kappa(G)$表示 $G$ 的点连通度，即任意两点间最少有多少条不相交的路径。

**证明：** 只需证明 $p(u,v)$ 的最小值可在 $u$ 和 $v$ 不相邻时取得。

若 $p(u,v)$ 在相邻节点 $x$ 和 $y$ 处取得最小值，尝试找到与 $x$ 不相邻的节点 $z$，使得 $p(x,y) = p(x,z)$。

从图 $G$ 中删去边 $xy$，则图 $G\setminus xy$ 中 $x$ 到 $y$ 的路径减少一，即 $p_G(x,y) = p_{G \setminus xy} (x,y) +1$。而由Menger's Theorem可知，图 $G\setminus xy$ 中存在点割 $S (|S| = p_{G \setminus xy}(x,y))$，使得图 $G \setminus xy - S$ 中节点 $x$ 和 $y$ 不连通。

若图 $G \setminus xy -S $ 中只有节点 $x$ 和 $y$ ，则 
$$
\kappa(G) = p_G(x,y) = p_{G\setminus xy}(x,y) + 1 = c_{G\setminus xy}(x,y) + 1 = (n-2)+1 = n-1
$$
因此，图 $G$ 是完全图，与题设矛盾。

若图 $G\setminus xy -S$ 中存在节点 $z (z\ne x, y)$，不失一般性，可设 $z$ 与 $x$ 不在同一连通块中。那么， $S\cup \{y\}$ 是图 $G$ 中的一个点割，分离节点 $x$ 和 $z$。

**总结**：由以上结论可知，图的最小点割可在不相邻节点对处取得。

------



## 参考资料

> - Bondy, John Adrian, and Uppaluri Siva Ramachandra Murty. *Graph theory with applications*. Vol. 290. London: Macmillan, 1976.
> - Menger, Karl. "Zur allgemeinen kurventheorie." *Fundamenta Mathematicae* 10.1 (1927): 96-115.
> - Göring, Frank. "Short proof of Menger's Theorem." *Discrete Mathematics* 219.1-3 (2000): 295-296.