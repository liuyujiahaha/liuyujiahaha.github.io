---
layout: post
title:  "MJRefresh使用笔记"
date:   2018-04-30 17:46:30 +0800
categories: [iOS]
excerpt: 
tags:
  - iOS
---

> 1.在GitHub中下载MJRefresh的项目，里面就有相应的demo；
> 下载地址：https://github.com/CoderMJLee/MJRefresh

> 2.我发现其实如果直接用pod导入了这个MJRefresh库，还有直接从GitHub下载下来内容是不一致的，因为如果导入库的话，会尽量的精简，而如果你是从GitHub克隆下载的话，则会有demo文件给你学习用；

###### MJDIYHeader自定义的header，然后重写prepare方法，里面可以重写很多东西，自己添加控件什么的；

###### 自定义文字的话，只要prepare中在setstate就可以了；

![image](https://liuyujiahaha.github.io/blogPic/MJRefresh类的关系.jpg)




#### 参考资料
*1.MJRefresh原理分析https://www.jianshu.com/p/8d44e1ee5693*

*2.解读 MJRefresh 框架 https://www.jianshu.com/p/437095c88717*