---
title: Chrome插件开发-开发环境搭建
date: 2016-07-06 21:39:36
tags:
---

最近喜欢上了使用RSS订阅工具来订阅自己经常阅读的一些博客和网站，因此在Chrome插件商店找到了一款RSSFeed的插件，用起来还不错，但是免费版本不支持RSS订阅的云同步，而且需要注册RSSFeed的账号才可以进行云同步，索性学习一下Chrome插件开发玩玩，顺便练习一下一直不太熟练的JS。

## 环境搭建

Chrome插件的开发环境搭建非常的简单，可以说不需要什么开发环境，所以你只需要下面几样东西就可以开始开发Chrome插件了  
1. 一个支持代码高亮的文本编辑器，VSCode,Sublime等
2. Chrome浏览器，不多说。
3. 支持翻墙的网络，Chrome插件开发需要经常到Chrome develop网站上查询API

## Chrome开发概览
Chrome插件是用Html，CSS，和Javascript语言来开发的，并且可以使用类似于Bootstrap或者JQuery，AngluarJS等前端框架所以基本上写起插件来跟写前端程序比较类似。在Chrome插件发中最重要的就是manifest.json文件，这个文件中描述了Chrome插件的图标，所需要的权限，以及插件的各种配置。

## 第一步：编写mainifest.json文件
manifest.json是的一个json格式的文件，该文件有很多配置选项，在文件中配置chrome插件的权限，选项页等配置。

新建一个文件夹，在其中新建一个manifest.json文件然后将如下内容写入文件中
```
{
  "name": "Chrome Extension",                     //插件名称
  "version": "1.1",                               //版本信息
  "description": "My First Chrome Extension",     //描述
  "manifest_version": 2                           //配置文件版本
}
```
创建然后在chrome浏览器打开chrome://extensions扩展管理页面，点击*加载已解压的扩展程序*，
![](http://ww3.sinaimg.cn/large/b3ee9d59gw1f5kkcfef1hj20kq02rt8x.jpg)
选中刚刚创建的文件夹就可以将创建的chrome插件加载到chrome中进行测试了。  
成功加载后扩展管理页面会多出一个插件
![](http://ww1.sinaimg.cn/large/b3ee9d59gw1f5kkd2nuv5j20kn0523z3.jpg)
并且在chrome的右上角会多出一个插件的小图标，这就代表我们已经成功创建了一个Chrome插件
![](http://ww4.sinaimg.cn/large/b3ee9d59gw1f5kkd8oo34j202z01gglf.jpg)
仅仅使用几行代码就创建了一个chrome插件是不是很简单，但是这个小插件也没有任何的功能，在接下来的文章中，我会详细的描述一个简单的RSS订阅插件的开发过程，并解释开发过程使用到的各种API以及manifest文件的更多配置来帮助大家学习chrome插件的开发。