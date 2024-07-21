<link rel="stylesheet" type="text/css" href="../css/maindoc.css">

# Tree

这是树上操作的一些函数。

## 约定

- `dep`：数组。`dep[u]` 表示点 $u$ 的深度，默认根节点的深度为 $1$；
- `st`：数组。`st[u][i]` 表示点 $u$ 的 $2^i$ 级祖先，如果不存在则默认为 $0$。

## 祖先相关

<dt class="func-declaration">
<span class="func-type"> int </span>
<span class="func-title"> jump </span>
<span class="func-light"> ( </span>
<span class="func-type"> int </span>
<span class="func-light"> u, </span>
<span class="func-type"> int </span>
<span class="func-light"> dis </span>
<span class="func-light"> ) </span>
</dt>

跳至点 $u$ 的 $k$ 级祖先。

```cpp
static inline int jump(int u, int k) {
    for (int i = 19; i >= 0; --i)
        if (k & (1 << i))
            u = st[u][i];
    return u;
}
```

<dt class="func-declaration">
<span class="func-type"> int </span>
<span class="func-title"> LCA </span>
<span class="func-light"> ( </span>
<span class="func-type"> int </span>
<span class="func-light"> u, </span>
<span class="func-type"> int </span>
<span class="func-light"> v </span>
<span class="func-light"> ) </span>
</dt>

求点 $u$ 和点 $v$ 的最近公共祖先。

```cpp
static inline int LCA(int u, int v) {
    if (dep[u] < dep[v])
        swap(u, v);
    u = jump(u, dep[u] - dep[v]);
    if (u == v)
        return u;
    for (int i = 19; i >= 0; --i)
        if (st[u][i] != st[v][i]) {
            u = st[u][i];
            v = st[v][i];
        }
    return st[u][0];
}
```

<dt class="func-declaration">
<span class="func-type"> int </span>
<span class="func-title"> move_forwards </span>
<span class="func-light"> ( </span>
<span class="func-type"> int </span>
<span class="func-light"> u, </span>
<span class="func-type"> int </span>
<span class="func-light"> aim </span>
<span class="func-light"> ) </span>
</dt>

将点 $u$ 向 $aim$ 移动一条边。

```cpp
static inline int move_forwards(int u, int aim) {
    if (u == aim)
        return u;
    int lca = LCA(u, aim);
    if (lca == u || lca == aim)
        if (dep[u] < dep[aim])
            u = jump(aim, dep[aim] - dep[u] - 1);
        else
            u = st[u][0];
    else
        u = st[u][0];
    return u;
}
```

> 本文件的全部内容在 CC BY-SA 4.0 之下提供。  
> Copyright (C)  2024  Yile Wang and contributors  
> 查看项目级 [README.md](../README.md) 获取详细信息。