---
title: javaSE复习之——IO流的概念
categories: JavaSE 复习
copyright: true
date: 2019-04-10 15:08:28
tags:
- IO流的概念
---
# IO流的概念
> 1、IO流用来处理设备之间的数据
> 
> 2、java对数据的操作时通过流的方式
> 
> 3、java用于操作流的类都在IO包中
> 
> 4、流按照操作类型分为两种：
> - **字节流：**
> 字节流可以操作任何数据，因为在计算机中任何数据都是以字节形式储存的
> 
> - **字符流：**
> 字符流只能操作纯字符类型的数据，比较方便

<!--more-->

> 5、按照流向分类分为：输入流、输出流

### IO流的常用父类
- 字节流的抽象父类：
	> InputStream（输入流）
	> 
	> outputStream（输出流）
- 字符流的抽象父类：
	> Reader（输入流）
	> 
	> Writer（输出流）

### IO的使用
> 1、使用前，导入IO包
> 
> 2、使用时，进行IO异常处理
	> - ps：
	> 因为IO流时处理内存和硬盘之间的关系，如果硬盘没有某个文件，那么会出错


> 3、使用后释放资源
	> - ps：
	> 因为IO流相当于一个建立在内存和硬盘之间的管道，不用了就要把这个管道关闭。

### IO流的注意事项
> 流对象尽量晚开早关