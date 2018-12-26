---
title: Hexo博客迁移电脑
date: 2018-12-26 18:03:07
modified: 2018-12-26 21:25:02
categories:
- 技术研究
tags:
- 博客
---

> 背景：新换了一台电脑，迁移文件资料，配置等搞了大半天，最后想了想，能不能把常用配置和高频使用的文件都进行云备份，以后再有这种情况，可以快速搭建环境？目前正在逐步寻找云备份，等整理完了，再总结一下，现在先把博客迁移实现

通常情况下，我们写完文章，执行：

`$ hexo d`

就是把public文件夹下的文件同步到github，然后就能通过https://username.github.io/ 访问博客了。所以，我们的思路其实就是把静态文件和Hexo环境，分别存在username.github.io的master和hexo分支上，示意图如下：

![分支图](https://api.superbed.cn/pic/5c231fbbc4ff9e2b4d699716)

### 原电脑上传配置

原理已经清楚，本打算按此分开操作，后来发现最新的 [*hexo-deployer-git*](https://github.com/hexojs/hexo-deployer-git) 插件，可以同步进行，安装：

`$ npm install hexo-deployer-git --save`

在项目根目录下的 _config.yml 里面就可以这样配置
```yaml
# _config.yaml
deploy:
  - type: git
    repo: git@github.com:<username>/<username>.github.io.git
    branch: master
  - type: git
    repo: git@github.com:<username>/<username>.github.io.git
    branch: hexo
    extend_dirs: /
    ignore_hidden: false
    ignore_pattern:
        public: .
```

最好，在github项目中，将hexo设为默认分支

然后重新部署即可

### 新电脑获取资源

直接clone远程hexo分支源文件

`git clone ...`

默认即在hexo分支(如果有设置的话，否则手动切换到hexo分支)，安装好插件
`npm install`
之后直接重新`hexo d`发布

:o: **踩坑记录**

repo可以使用ssh的git@地址，也可以使用https协议地址

1. ssh需要密钥，并且测试一下：ssh -T git@github.com
2. https如果提示: can not read a block mapping entry, 上面的yaml格式，需要有空格
3. 如果提示：Error: EPERM: operation not permitted，删除文件夹里的.deploy_git文件夹，重新部署

------

### 更新
:alarm_clock: 2018年12月26日 21点25分 修改
上述方式正常操作没什么问题，主要就在删除.deploy_git文件夹后，重新部署，可能会导致之前的commit历史丢失，只剩下最近一次的commit，如果对历史记录没什么要求的，完全不用理会，但作为稍微强迫症的我，还是略有不爽，所以，最终还是分离源文件与静态资源上传

```yaml
# _config.yaml
deploy:
  - type: git
    repo: git@github.com:<username>/<username>.github.io.git
    branch: master
```
静态资源正常部署，源文件手动add, commit到hexo分支。