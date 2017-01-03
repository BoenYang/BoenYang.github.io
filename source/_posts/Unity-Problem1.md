title: 那些Unity中的坑（一）
date: 2016-11-20 23:00:46
tags:
---

对于Unity引擎的用户来说，大家对于Unity真的是又爱又恨，喜欢Unity的资源丰富，构建速度快，恨于Unity中的无数大坑之存在，下面就来说说Unity中的坑吧。

在Unity中，动画系统是很常用的功能，但是在这个动画系统中就有很多的坑点存在。  

最近在项目中使用到了Humanoid动画，这是一个专门用于人形骨骼，对应于3DMAX中的BipedBone。在使用的过程中发现，如果在动画软件中创建了非人形骨骼主体之外的骨骼（比如：披风，头发，枪支等额外骨骼），那么在Unity的Humanoid模式下面这些骨骼将不会运动。

经过各种摸索发现，在Unity中的Humanoid模式下，这些骨骼其实是可以运动的，但是Unity默认是把人形骨骼之外的骨骼给Mask掉的，所以造成了人形骨骼之外的骨骼不运动的情况。

![图一](http://ww2.sinaimg.cn/large/b3ee9d59gw1ew70im33z9j20bk054jrg.jpg)

上面就是普通的人形骨骼部分

![图二](http://ww1.sinaimg.cn/large/b3ee9d59gw1ew70jznfxgj20ar06aglp.jpg)

上面是除了人形骨骼额外的部分，在导入动画之后默认可能是没有勾上的，勾上之后就可以愉快的使用各种完美的人形动画了。

对于上面这种情况如果动画文件很多的话每个都勾一下挺麻烦的，可以考虑新建一个Avatar Mask，把模型的Avater拖到下面的位置Import就可以了，然后给将Mask赋予每个动画就行了。

![](http://ww4.sinaimg.cn/large/b3ee9d59gw1ew70o08t7oj20bv01dq2s.jpg)

总算是Humanoid动画可以用了。
