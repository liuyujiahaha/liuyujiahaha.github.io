---
layout: post
title:  "iOS Study Notes"
date:   2018-04-25 21:50:30 +0800
categories: [iOS]
excerpt: 
tags:
  - iOS
---

# 学习笔记

###### &emsp;&emsp;最近这段时间我从3月份开始准备简历，然后再拉勾上面投简历，然后也去面试了几家公司。在这段反复的工作、学习和面试中，感觉自己知道了自己的不足，然后通过休息时间一直在提高自己，很多方面也确实有提高了，很开心。现在总结一下最近这一个月左右的工作与学习。
###### &emsp;&emsp;自己换了工作自己的学习热情也比较高涨，很多地方也有了比以前更加深入的理解。
###### 最近看了很多iOS业内的大牛的博客，然后也在简书和CSDN上看到了很多大V的文章，感觉受益匪浅，其中唐巧的博客给了我很深的印象。
###### &emsp;&emsp;然后下载了部分比较优秀的开源项目也在看，看看别人是怎么实现的感觉还是很有成就感。

###### &emsp;&emsp;每天在看了他们的文章之后要好好的分析还有研究记录下来。坚持一下每天都把当天学习到的东西记录一下，或者整理转发一下，然后加上自己的思想。
##### 常用的属性定义修饰符
- block用了copy
- nsstring用了copy
- 定义的宏全用大写；
- delegate用weak

- 枚举的格式
```
typedef enum : NSUInteger {
    YZTitleColorGradientStyleRGB , // RGB:默认RGB样式
    YZTitleColorGradientStyleFill, // 填充
} YZTitleColorGradientStyle;
```

- dispatch_block_t 简单的实现不带参数的回调函数
- 


```
代码结构：
#pragma mark - life cycle
#pragma mark - UITableViewDelegate
#pragma mark - CustomDelegate
#pragma mark - event response
#pragma mark - private methods
#pragma mark - getter and setter
```
