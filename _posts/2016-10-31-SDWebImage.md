---
layout: post
title: "SDWebImage"
date: 2016-10-31 20:50:20 +0800
categories: [iOS]
excerpt: sdwebimage的原理
tags:
  - SDWebImage
  - 第三方库
---
 
  
### 第三方框架的使用建议

1. 用第三方框架的目的

1> 开发效率： 快速开发，人家封装好的一行代码顶自己写的N行

2> 为了使用这个功能最牛逼的实现

2. 第三方框架过多，很多坏处(忽略不计)

1> 管理、升级、更新

2> 第三方框架有BUG，等待作者解决

3> 第三方框架的作者停止更新（潜在的BUG无人解决）

3. 比如 

流媒体：播放在线视频、音频（边下载边播放）

非常了解音频、视频文件的格式

每一种视频都有自己的解码方式（C\C++）

4. 总结

1> 站在巨人的肩膀上编程

2> 没有关系，使劲用那么比较稳定的第三方框架


### cell的图片下载


1> 如何防止一个url对应的图片重复下载

* “cell下载图片思路 – 有沙盒缓存”

2> SDWebImage的默认缓存时长是多少？

* 1个星期

3> SDWebImage底层是怎么实现的？

* 上课PPT的“cell下载图片思路 – 有沙盒缓存”

  
###  SDWebImage


*  iOS中最牛逼的网络图片处理框架：图片下载、图片缓存、下载进度进度、GIF处理等等，imageIO专门用于处理GIF；
 
 
1> 常用方法

{% highlight ruby %}
- (void)sd_setImageWithURL:(NSURL *)url placeholderImage:(UIImage *)placeholder;
- (void)sd_setImageWithURL:(NSURL *)url placeholderImage:(UIImage *)placeholder options:(SDWebImageOptions)options;
- (void)sd_setImageWithURL:(NSURL *)url placeholderImage:(UIImage *)placeholder completed:(SDWebImageCompletionBlock)completedBlock;
- (void)sd_setImageWithURL:(NSURL *)url placeholderImage:(UIImage *)placeholder options:(SDWebImageOptions)options progress:(SDWebImageDownloaderProgressBlock)progressBlock completed:(SDWebImageCompletionBlock)completedBlock;

{% endhighlight %}



2> 内存处理：当app接收到内存警告时


{% highlight ruby %}
/**
 *  当app接收到内存警告
 */
- (void)applicationDidReceiveMemoryWarning:(UIApplication *)application
{
    SDWebImageManager *mgr = [SDWebImageManager sharedManager];
    
    // 1.取消正在下载的操作
    [mgr cancelAll];
    
    // 2.清除内存缓存
    [mgr.imageCache clearMemory];
}

{% endhighlight %}




3> SDWebImageOptions

* SDWebImageRetryFailed : 下载失败后，会自动重新下载
* SDWebImageLowPriority : 当正在进行UI交互时，自动暂停内部的一些下载操作
* SDWebImageRetryFailed / SDWebImageLowPriority : 拥有上面2个功能