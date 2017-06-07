---
title: Spark Environment
date: 2017-05-18T22:01:55+08:00
---

# 搭建Spark环境

## 基本情况

目标：搭建Spark开发环境，使用Python语言，默认使用`ipython`，并支持使用`jupyter notebook`进行交互式数据分析。

运行环境：Ubuntu 16.04 x64 server + ipython 5.3.0 (with NumPy/SciPy/Matplotlib/Pandas) + jupyter 4.3.0 + Spark 2.1.1 with hadoop2.7

## 搭建步骤

1. 从官网下载二进制安装包；
2. 解压并设置相关环境变量，`export SPARK_HOME=${HOME}/spark; export PATH=$PATH:$SPARK_HOME/bin`；
3. 配置默认使用ipython，添加环境变量`export PYSPARK_DRIVER_PYTHON=/usr/local/bin/ipython; export PYSPARK_DRIVER_PYTHON_OPTS="notebook --no-browser --ip=0.0.0.0"`；
4. 现在，可以运行`pyspark`了。

