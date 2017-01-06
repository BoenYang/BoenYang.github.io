---
title: Unity九宫格切图图片制作进度条
date: 2017-01-06 14:01:51
tags:
---

在Unity游戏UI开发的过程中，我们经常会用到使用到九宫格切图的图片来制作UI，对于简单的图片使用九宫格切图可以有效减少图片大小，避免UI拉伸变形，提高UI的精细度。
但是在很多种情况下九宫格切的图片就派不上用场了，比如进度条。


如果美术给了这样一张大小30x20的进度条前景图要你制作一个300*20的进度条  
![](http://ww4.sinaimg.cn/large/b3ee9d59gw1fbgvpp0ot7j206403jwed.jpg)  
按照正常的逻辑，直接拉伸肯定是不行的，于是对该图片进行九宫格切图处理，然后再制作UI的时候将图片的Image Type改为Sliced，然后宽度设置为300就可以了.如果这样的话,尴尬的事情就发生了。  

在设置Image Type类型类Sliced后，**Image Type没办法设置成Filled**，也就没办法改变fillamount来做进度条了。

下面就推荐一个简单的方案给大家，不需要代码什么的，也不需要扩展新组件就可以达到使用sliced类型的图片来做进度条了。

这个方法就是利用**Mask组件**：
1. 创建一个Image命名为ProgressbarFg，将Image Type设置为sliced，然后宽度设置为300，图片为进度条前景图
2. 然后再创建一个Image命名为Mask，将长度和宽度设置和前景图一致，图片设置为一张没有透明像素的小图片（就是整张图片都有颜色）
3. 给Mask加上一个Mask组件，去掉Show Mask Graphic 勾选
4. 将Mask中的Image组件的Image Type设置为Filled
5. 强ProgressbarFg拖到Mask下
6. 完成，改变Mask中的fillamount就是一个进度条了

创建完成之后的结构如下  
![](http://ww2.sinaimg.cn/large/b3ee9d59gw1fbgwbhd584j205k023q2q.jpg)  

Mask设置如下：  
![](http://ww4.sinaimg.cn/large/b3ee9d59gw1fbgwc5703wj20cn0emjsp.jpg)  

效果图：
![](http://ww1.sinaimg.cn/large/b3ee9d59gw1fbgwcsybukj20ob073wey.jpg)  

这个简单方法的实现原理其实很简单，就是利用Mask来遮罩，但是Mask的图片fillamount是可以修改了，也算是曲线救国吧。

