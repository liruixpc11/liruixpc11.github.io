---
layout: single
title: "Using Octopress"
date: 2017-04-14T11:16:01+08:00
---

# Using Octopress

## 基本用法

1. 创建新博客：`octopress new post 'TITLE'`；
2. 构建博客：`jekyll build`；
3. 本地预览：`jekyll serve`；
4. 部署到github.io：`octopress deploy push`；
5. 同步源代码：`git add -A && git commit -m 'MSG' && git push`。

## Windows环境搭建

1. 安装RubyInstaller；
2. 安装DevKit，在解压后的目录里面执行`ruby dk.rb init`和`ruby dk.rb install`；
3. 切换源：`gem sources --add http://gems.ruby-china.org/ --remove https://rubygems.org/`；
4. 安装包管理工具，`gem install bundler`；
5. 在克隆出来的目录中执行`bundle install`以安装依赖的包；
6. 安装证书：`curl -o C:/windows/ca.perm https://curl.haxx.se/ca/cacert.pem`，在执行`jekyll`命令之前运行命令`export SSL_CERT_FILE=c:/windows/cacert.pem`；
7. 执行`jekyll serve`默认监听的端口是4000，和foxit服务（安装了福昕阅读器的计算机都可能有这个服务）冲突，需要关闭该服务或通过修改`_config.yml`的`port: <NEW_PORT>`来避开端口冲突。
