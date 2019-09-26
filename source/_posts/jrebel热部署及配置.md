---
title: jrebel热部署及配置
date: 2017-08-12 11:28:45
categories: 
 - 工具使用
tags:
 - idea
---

> jrebel作为热部署的优秀插件，很多人也受够了因为一些小的改动而重启容器，费时费力，但是，jrebel插件虽然安装上了，但好像并没有起作用，究其原因，可能需要以下步骤：

1. 下载安装jrebel插件，可选用编译器在线安装，也可以使用jar包本地安装，具体步骤，我相信你们都会，在此不再赘述。
2. 许多人可能都是忽略了这一步，比如我，因为网上大多数教程并没有这一步，此步骤是将需要热部署的项目添加到jrebel的配置中，其会生成一个/resources/rebel.xml文件，记得添加到.gitignore文件中哦。

![在view/Too Windows/Jrebel中添加该项目](https://pic.superbed.cn/item/5d8c8361451253d178deea18.png "添加项目至jrebel")


3. 如果是tomcat容器，还需配置on update 和 on frame deactivation 为Hot swap classes.