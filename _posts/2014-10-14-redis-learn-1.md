---
layout: post
title: redis学习笔记（一）
category: 数据库
tags: redis
description: 
---

## 安装

### mac系统
因为我用的[HomeBrew](http://brew.sh/index_zh-cn.html)，简单有效地执行下面代码就安装完成：
    
    sudo brew install redis    

### ubuntu

部署服务器时可能会用到，[Redis官方安装](http://www.redis.cn/download.html)介绍的比较详细。    

## 配置及启动

下面说的都是日常我在mac下的操作，Linux大同小异。

在开发环境下，redis可以使用内置的配置，也可以通过命令行传参，下面就是在8000端口启动了redis

    redis-server --port 8000

正式环境下，还是应该通过配置文件启动，redis的配置文件一般为redis.conf，假设当前目录下有 redis.conf文件:

    redis-server redis.conf

关于详细配置可以参见这篇博客[redis的安装](http://blog.csdn.net/zhu_xun/article/details/16804487)    


