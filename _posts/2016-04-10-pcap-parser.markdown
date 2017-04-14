---
layout: post
title: "Pcap文件Java解析器调优记"
date: 2016-04-10 22:02:45 +0800
comments: true
categories: 
---

# 主要性能优化点 #

1. 判断是否还有包的时候，调用了FileChannel的position和size函数；改为自行计算后，时间从800+ms降到了500+ms。经过本步骤优化后，性能主要瓶颈在IO上。
2. 使用BufferedInputStream代替FileChannel，时间从500+ms降低到100+ms，性能提升的原因是使用缓存可以降低IO次数。经过本步骤优化后，性能开销的大约1/3到1/2花在了解析上。
3. 原来以为反射会降低性能，但是改用侵入式接口直接读取数组后，性能提升大约5-10%。如果字段很多或者调用很多次的话是值得优化的。
4. 使用new代替反射调用Constructor，大约168ms→142ms，性能提升约10%。

性能参照：仅仅读取内容和必要的长度字段，不解析其它内容，大约是90 -100ms。

# 非性能优化点 #

1. 重用PacketHeader的16字节缓冲区，而不是每次都调用ByteBuffer.allocate分配；性能基本不变。