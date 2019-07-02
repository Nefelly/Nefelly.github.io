---
title: Two Essential Nonplanar Graphs
toc: true
date: 2018-12-28 20:22:35
tags: [Graph Theory]
categories: 
- Graph Theory
- Chapter 10  Planar Graphs
mathjax: true
---

$K_5$ 和 $K_{3,3}$ 是两个最基本的非平面图，它们也是平面图判定算法的基础。接下来，我们直接利用平面图的性质来说明这两个图不存在平面嵌入。

------

#### 定理 10.2    

> $K_5$ 是非平面图。

**证明：**反证法。记图中节点分别为 $v_1, v_2, v_3, v_4, v_5$，记 $v_1, v_2, v_3$ 围成的环为 $C$，不失一般性，设 $v_4 \in int(C)$。

![Figure10.3](\images\Figure10.3.png)

记环 $C_1 = v_2 v_3 v_4 v_2$， $C_2 = v_1v_3v_4v_1$，$C_3 =v_1v_2v_4v_1 $，易知 $v_i \notin int(C_i)\quad(i=1,2,3)$

因为 $v_5$ 与 $v_i$ 之间有连边，所以 $v_5 \notin int(C_i)$，否则边 $v_iv_5$ 会与环 $C_i$ 相交。而 $int(C_1) \cup int(C_2) \cup int(C_3) = int(C)$，所以 $v_5 \notin int(C)$。但是 $v_4 \in int(C)$，所以边 $v_4v_5$ 会与环 $C$ 相交，与 $K_5$ 是平面图矛盾。

因此，$K_5$ 是非平面图。

------

#### 练习 10.1.1b    

> $K_{3,3}$ 是非平面图。

**证明：** 反证法。记图中节点分别为 $v_1, v_2, v_3, v_4, v_5,v_6$，二分图的两侧分别为 $\{v_1,v_3,v_5\}$ 和 $\{v_2,v_4,v_6\}$ 。记 $v_1, v_2, v_3,v_4$ 围成的环为 $C$，不失一般性，设 $v_5 \in int(C)$。

![Ex10.1.1b](\images\Ex10.1.1b.png)

记环 $C_1 = v_2 v_3 v_4 v_5 v_2$， $C_3 =v_1v_2v_5v_4v_1 $，易知 $v_i \notin int(C_i)\quad(i=1,3)$

因为 $v_6$ 与 $v_i$ 之间有连边，所以 $v_6 \notin int(C_i)$，否则边 $v_iv_6$ 会与环 $C_i$ 相交。而 $int(C_1) \cup int(C_3) = int(C)$，所以 $v_6 \notin int(C)$。但是 $v_5 \in int(C)$，所以边 $v_6v_5$ 会与环 $C$ 相交，与 $K_{3,3}$ 是平面图矛盾。

因此，$K_{3,3}$ 是非平面图。

------



## 参考资料

> - Bondy, John Adrian, and Uppaluri Siva Ramachandra Murty. *Graph theory with applications*. Vol. 290. London: Macmillan, 1976.
