---
title: Using MulVAL
date: 2017-06-07T08:42:53+08:00
---

# 使用MulVAL

MulVAL是基于逻辑推理的网络安全分析工具，能够实现网络攻击路径发现和策略违规发现。2005年提出，是X Ou的博士论文成果。在2005年时，2000个节点规模网络的分析时间不超过1分钟。

## 环境搭建

[项目主页](http://www.arguslab.org/mulval.html)，[v1.1软件包下载](http://www.arguslab.org/software/mulval_1_1.tar.gz)。

安装步骤如下（`doc/README`文件中有很多有用信息）：
```bash
# install XSB
wget "http://xsb.sourceforge.net/downloads/XSB.tar.gz"
tar xvf XSB.tar.gz
cd XSB/build
./configure
./makexsb
cd ..
export XSB_HOME=`pwd`
cd ..

# download
wget "http://www.arguslab.org/software/mulval_1_1.tar.gz"

# uncompress
tar xvf mulval_1_1.tar.gz

# make 
cd mulval
export MULVALROOT=`pwd`
make
```

## 案例测试

运行前要确保以下环境变量已设置：
```bash
export MULVALROOT=<>
export XSB_HOME=<>
export PATH=$MULVALROOT/bin:$MULVALROOT/utils:${XSB_HOME}/bin:$PATH
```

执行以下命令（`-v`选项表示生成`.csv`和`.pdf`格式的攻击图，`-p`表示对攻击图进行裁剪以优化视觉效果），执行成功后可以打开生成的`AttackGraph.pdf`文件查看攻击图：
```bash
cd $MULVALROOT/testcases/3host
graph_gen.sh input.P -v -p
```

