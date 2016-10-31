---
layout: post
title: "文件下载"
date: 2016-10-31 22:04:46 +0800
categories: [iOS]
excerpt: 各种文件下载方式
tags:
  - 文件下载
  - NSURLConnection+下载
---

### 一、大文件下载

##### 1.方案：利用NSURLConnection和它的代理方法

1>发送一个请求

{% highlight ruby %}

// 1.URL
NSURL *url = [NSURL URLWithString:@"http://localhost:8080/MJServer/resources/videos.zip"];
// 2.请求
NSURLRequest *request = [NSURLRequest request requestWithURL:url];
// 3.下载（创建完conn对象后，会自动发起一个异步请求）
[NSURLConnection connectionWithRequest:request delegate:self];


{% endhighlight %}

2>在代理方法中处理服务器返回的数据

{% highlight ruby %}
/**
在接收到服务器的响应时：
1.创建一个空的文件
2.用一个句柄对象关联这个空的文件，目的是：方便后面用句柄对象往文件后面写数据
*/

-(void)connection:(NSURLconnection *)connnection didReceiveResponse:(NSURLResponse *)response
{
	 //文件路劲
	 NSString *caches = [NSSearchPathForDirectoriesInDomains(NSCachesDirectory,NSUserDomainMask,YES)lastObject];
	NSString *filepath = [caches stringByAppendingPathComponent:@"videos.zip"];
	
	//创建一个空的文件 到 沙盒中
	NSFileManage *mgr = [NSFileManager defaultManager];
	[mgr createFileAtPath :filepath contents:nil attributes:nil];
	
	//创建一个用来写数据的文件句柄
	self.writeHandle = [NSFileHandle fileHandleForWritingAtPath:filepath];
}

/**
 在接收到服务器返回的文件数据时，利用句柄对象往文件的最后面追加数据
 */
- (void)connection:(NSURLConnection *)connection didReceiveData:(NSData *)data
{
    // 移动到文件的最后面
    [self.writeHandle seekToEndOfFile];
    
    // 将数据写入沙盒
    [self.writeHandle writeData:data];
}

/**
 在所有数据接收完毕时，关闭句柄对象
 */
- (void)connectionDidFinishLoading:(NSURLConnection *)connection
{
    // 关闭文件
    [self.writeHandle closeFile];
    self.writeHandle = nil;
}


{% endhighlight %}


##### 2.注意点：千万不能用NSMutableData来拼接服务器返回的数据

### 二、NSURLConnection发送异步请求的方法
##### 1.block形式 - 除开大文件下载以外的操作，都可以用这种形式
[NSURLConnection sendAsynchronousRequest:<#(NSURLRequest *)#> queue:<#(NSOperationQueue *)#> completionHandler:^(NSURLResponse *response, NSData *data, NSError *connectionError) {
    
}];

##### 2.代理形式 - 一般用在大文件下载

{% highlight ruby %}
// 1.URL
NSURL *url = [NSURL URLWithString:@"http://localhost:8080/MJServer/login?username=123&pwd=123"];
// 2.请求
NSURLRequest *request = [NSURLRequest requestWithURL:url];
// 3.下载(创建完conn对象后，会自动发起一个异步请求)
[NSURLConnection connectionWithRequest:request delegate:self];

{% endhighlight %}


