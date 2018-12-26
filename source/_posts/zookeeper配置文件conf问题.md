---
title: zookeeper配置文件conf问题
date: 2017-08-07 21:07:22
categories: 
 - 服务器
tags:
 - zookeeper
---

zookeeper的配置文件zoo.cfg中的两个地址配置导致zookeeper启动报错，一闪而过的原因：

例如：

dataDir=F:/workspace/Servlet/zookeeper-3.4.6/data
dataLogDir=F:/workspace/Servlet/zookeeper-3.4.6/logs

必须使用斜杠(/)，而windows自带路径使用的是反斜杠(\\)，此问题只可意会不可言传，鬼知道我怎么会想到修改这个问题，还好最终能顺利启动，谢天谢地。