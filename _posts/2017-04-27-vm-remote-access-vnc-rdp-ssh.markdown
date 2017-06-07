---
title: VM Remote Access(VNC/RDP/SSH)
date: 2017-04-27T09:20:50+08:00
---

# VM Remote Access (VNC/RDP/SSH)

## VNC

解决方案：noVNC（前端） + websockify（WebSocket → VNC/TCP）。

当前的问题：现在使用的基于Python的websockify服务在性能方面存在一些问题，在连接一段时间之后有很大概率会断开。在高性能约束条件下，需要重新选取一个更高性能的工具。

## RDP

有几种备选方案：

- RDPWebClient, from VirtualBox project，flash-based.
- [FreeRDP-WebConnect](https://github.com/FreeRDP/FreeRDP-WebConnect), HTML5-based.

### RDPWebClient

包含在VirtualBox的SDK里面。

现在还没有测试成功直接连接Windows的RDP服务，报`E: TCP: SECURITY_ERROR Error #2048`错。

### FreeRDP


## SSH