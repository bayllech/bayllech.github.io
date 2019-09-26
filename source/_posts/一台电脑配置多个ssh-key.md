---
title: 一台电脑配置多个ssh-key
date: 2017-08-10 22:50:07
categories: 
- 技术研究
tags:
- git
---

> 在公司使用电脑时，公司代码提交到gitlab，个人代码提交到github,如何生成多个ssh-key，同时连接gitlab和gitgub呢？

1. 生成多个ssh-key，分别命名为不同的id_rsa,如：id_rsa_gitlab、id_rsa_githab。并将对应的*_pub添加到远程git的ssh-key设置中。

   ```java
   $ ssh-keygen -t rsa -C "youremail@yourcompany.com” -f ~/.ssh/id-rsa_gitlab

   $ ssh-keygen -t rsa -C "youremail@yourcompany.com” -f ~/.ssh/id-rsa_github
   ```
   <!-- more -->

2. 添加私钥

   ```java
   $ ssh-add ~/.ssh/id_rsa_gitlab

   $ ssh-add ~/.ssh/id_rsa_github
   ```

   如果执行ssh-add时提示"Could not open a connection to your authentication agent"，可以现执行命令：

   ```java
   $ ssh-agent bash
   ```

   然后再执行上面的ssh-add命令。

   ```
   # 可以通过 ssh-add -l 来确私钥列表
   $ ssh-add -l
   # 可以通过 ssh-add -D 来清空私钥列表
   $ ssh-add -D
   ```

3. 在~/.ssh目录下新建一个名为config的文件

   添加内容：

   ```
   # gitlab
   Host gitlab.com //或你公司私服ip地址
       HostName gitlab.com
       PreferredAuthentications publickey
       IdentityFile ~/.ssh/id_rsa_gitlab
   # github
   Host github.com
       HostName github.com
       PreferredAuthentications publickey
       IdentityFile ~/.ssh/id_rsa_github
   ```

4. 可能需要重新配置全局账号，以后每个项目如果使用的不是全局账号，在其项目里配置单独账号。

5. 可以通过以下命令测试是否连通

   ```
   $ ssh -T git@github.com
   $ ssh -T git@gitlab.com  //或公司私服ip
   ```

