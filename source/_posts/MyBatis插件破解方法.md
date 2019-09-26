---
title: MyBatis插件破解方法
date: 2017-05-20 17:33:51
categories: 
 - 工具使用
tags: 
 - idea
---

​	MyBatis插件的破解方法有很多，我个人还是比较喜欢这一种方式，简单明了，操作也不复杂，目前还未出现任何问题，如有问题请与我联系。

​	首先需要下载jar包，这里给出[链接](https://coding.net/u/rover12421/p/MyBatisPluginCrack/git)，需要自行clone，编译，打包，相信这对于你们不是问题；实在嫌麻烦的，我把jar包直接放到网上了  [点击即可下载](http://cdn.bayllech.cn/MyBatisPluginCrack-1.0.jar)

​	其次，在idea[64].exe.vmoptions里添加一行命令

​	`-javaagent:插件jar包位置/名字.jar`

即可使用。

​	idea中的位置如图：![vmoptions](http://oq8w1br9a.bkt.clouddn.com/QQ%E5%9B%BE%E7%89%8720170520175815.png)

