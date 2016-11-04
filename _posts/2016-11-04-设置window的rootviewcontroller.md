---
layout: post
title: "UI主框架相关"
date: 2016-11-04 19:40:10 +0800
categories: [iOS]
excerpt:
tags:
  - UI
  - 框架
---

##### 设置Window的rootViewController

* 由于没有了Storyboard，因此需要在IWAppDelegate中手动创建Window，rootViewController也需要手动指定

-(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
	1.创建窗口
	self.window = [UIWindow alloc]iniWithFrame:[UIScreen mainScreen].bounds];
	2.设置跟控制器
	self.window.rootViewController = [[IWTabBarController alloc]init];
	3.显示窗口
	[self.window makeKeyAndVisible];
	return YES;
}

##### 在PCH文件中添加常用的宏
1.日志开关
#ifdef DEBUG
#define JiaLog(...) NSLog(__VA_ARGS__)
#else
#define JiaLog(...)
#endif


2.判断是否为iOS7

#define iOS7 ([[[UIDevice currentDevice]systemVersion]floatValue]>=7.0)

3.获得颜色

#define JiaColor(r,g,b) [UIColor colorWithRed:(r)/255.0 grren:(g)/255.0 blue:(b)/255.0 alpha:1]

uitaberBar 和 navigationBar的用法，如何重写；

ui