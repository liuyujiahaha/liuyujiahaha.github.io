---
layout: post
title:  "NSOperation和NSOperationQueue"
date:   2016-10-29 21:16:10 +0800
categories: [iOS]
excerpt: 
tags:
  - iOS
  - NSOperation
  - NSOperationQueue
---



### 一、NSOperation和NSOperationQueue

#### 1.队列的类型

1> 主队列

* [NSOperationQueue mainQueue]
* 添加到"主队列"中的操作，都会放到主线程中执行

2> 非主队列

* [[NSOperationQueue alloc] init]
* 添加到"非主队列"中的操作，都会放到子线程中执行

2.队列添加任务

* -(void)addOperation:(NSOperation *)op;
* -(void)addOperationWithBlock:(void (^)(void))block;

3.常见用法

1> 设置最大并发数

-(NSInteger)maxConcurrentOperationCount;

-(void)setMaxConcurrentOperationCount:(NSInteger)cnt;

2> 队列的其他操作

* 取消所有的操作
-(void)cancelAllOperations;

* 暂停所有的操作
[queue setSuspended:YES];

* 恢复所有的操作
[queue setSuspended:NO];

4.操作之间的依赖（面试题）

* NSOperation之间可以设置依赖来保证执行顺序
* [operationB addDependency:operationA];



// 操作B依赖于操作A，等操作A执行完毕后，才会执行操作B

* 注意：不能相互依赖，比如A依赖B，B依赖A
* 可以在不同queue的NSOperation之间创建依赖关系

5.线程之间的通信

{% highlight ruby %}
	NSOperationQueue *queue = [[NSOperationQueue alloc] init];
	[queue addOperationWithBlock:^{
    // 1.执行一些比较耗时的操作
    
    // 2.回到主线程
    [[NSOperationQueue mainQueue] addOperationWithBlock:^{
        
    }];
	}];
{% endhighlight %}



### 二、从其他线程回到主线程的方式

####  1.perform...

{% highlight ruby %}
	[self performSelectorOnMainThread:<#(SEL)#> withObject:<#(id)#> waitUntilDone:<#(BOOL)#>];
{% endhighlight %}



####  2.GCD

{% highlight ruby %}
	dispatch_async(dispatch_get_main_queue(), ^{

	});
{% endhighlight %}


####  3.NSOperationQueue

{% highlight ruby %}
	[[NSOperationQueue mainQueue] addOperationWithBlock:^{
    
	}];
{% endhighlight %}



###  三、判断编译器的环境：ARC还是MRC？

{% highlight ruby %}
	#if __has_feature(objc_arc)
	// 当前的编译器环境是ARC

	#else
	// 当前的编译器环境是MRC

	#endif
{% endhighlight %}



### 四、类的初始化方法

#### 1.+(void)load

* 当某个类第一次装载到OC运行时系统（内存）时，就会调用
* 程序一启动就会调用
* 程序运行过程中，只会调用1次

#### 2.+(void)initialize

* 当某个类第一次被使用时（比如调用了类的某个方法），就会调用
* 并非程序一启动就会调用

#### 3.在程序运行过程中：
1个类中的某个操作，只想执行1次，那么这个操作放到+(void)load方法中最合适
