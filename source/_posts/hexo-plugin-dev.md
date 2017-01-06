---
title: hexo-maintance插件开发
date: 2017-01-05 21:05:50
tags:
---

# 前言

2016年是比较忙碌的一年，在这过去一年里面并没有什么时间来写博客，所以2017年的一个小目标就是多写一些博客，把自己碰到的一些问题和想法记录下来。

由于我经常需要换电脑来工作，所以每次用hexo写博客都笔记麻烦，每次换电脑都需要重新配置，同步内容，主题什么的也都丢了之前写的一篇hexo的备份工具是基于已有的工具修改了，觉得源代码没有办法保存，因此去看了些hexo的API，开发了一个插件。

# 关于hexo-maintance

## 特性
> 1. 自动在发布之后备份博客源文件
> 2. 自动备份包括博客配置文件，主题
> 3. 命令行一键恢复博客，自动恢复已安装插件

## 使用

### 自动备份博客
```
//在博客目录下
npm install hexo-maintance --save

//在_config.yml中添加备份配置
backup:
  repo: repo_url
  branch: repo_branch

然后调用
hexo d
在发布成功之后就会自动将博客备份至指定仓库和制定分支
```

### 恢复博客

```
hexo init MyBlog
cd MyBlog
npm install hexo-maintance --save

//在_config.yml中添加备份配置
backup:
  repo: repo_url
  branch: repo_branch

hexo restore
```

**注：无论是备份或者恢复博客都需要github的仓库写入权限**  
[Github SSH验证配置](http://www.jianshu.com/p/ddd3122cb351)


# 实现原理

自动备份其实是利用hexo的[[Event API]](https://hexo.io/api/events.html)中的deployAfter来实现。在deployAfter之后自动在博客根目录下初始化git仓库，将博客推送到配置的git仓库中。

命令行一键恢复其实是利用hexo的[[Console Extension]](https://hexo.io/api/console.html)开增加了一个命令，调用命令后将配置的git仓库中的博客源文件拉取到本地替换掉之前的即可。

在完成之后并将插件打包发布到了[npm](https://www.npmjs.com/package/hexo-maintance)上，利用npm install hexo-maintance --save就可以安装了，使用还是蛮方便的.

# TODO
1. hexo一键升级工具
2. 博客同步
3. svn等其他仓库工具支持


插件并不完善，有很多的Bug,欢迎大家使用，发现问题[[点这里]](https://github.com/BoenYang/hexo-maintance/issue)！
插件地址：[hexo-maintance](https://github.com/BoenYang/hexo-maintance)
