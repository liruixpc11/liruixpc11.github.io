---
layout: single
title: "Compile ns2 in Linux Mint 18"
date: 2017-01-26 08:33:17 +0800
comments: true
categories: MISC
---

编译NS2的时候，`${NS_DIR}/ns-2.35/linkstate/ls.h`报错：`erase not in this scope`（大概是这样，记不清了）。修改该文件的第137行如下：

```c++
void eraseAll() { erase(baseMap::begin(), baseMap::end()); }
```

```c++
void eraseAll() { baseMap::erase(baseMap::begin(), baseMap::end()); }
```
