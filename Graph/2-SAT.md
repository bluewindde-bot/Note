# 2-SAT

## 描述

通过给 $n$ 个变量赋值使得 $m$ 个形如「$x$ 为 `true/false` 且 $y$ 为 `true/false`」的条件得到满足，给出一种方案或说明无解。

## 解法

定义状态。对每个变量，有赋值 `true` 和 `false` 两种状态，总共有 $2n$ 个状态。

建图。**图上每条边 $(u, v)$ 的含义是「当状态 $u$ 被选中时状态 $v$ 必须被选中」**。

Tarjan SCC 对每个强连通分量内的状态染色。

如果存在一个变量，使得其两种状态颜色相同，则说明它处于「既要选又不能选」的矛盾情况，此时无解。否则，把几个互不矛盾的 SCC 拼起来就是一种方案。

## 例题

- [P4782 【模板】2-SAT](https://www.luogu.com.cn/problem/P4782)
- [P3825 [NOI2017] 游戏](https://www.luogu.com.cn/problem/P3825)
- [P6378 [PA2010] Riddle](https://www.luogu.com.cn/problem/P6378)