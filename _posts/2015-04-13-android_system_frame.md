---
layout : post
title : "Android系统架构"
category : Android
duoshuo: true
date : 2015-04-13
tags : [Android]
SyntaxHihglighter: true
shTheme: shThemeMidnight # shThemeDefault  shThemeDjango  shThemeEclipse  shThemeEmacs  shThemeFadeToGrey  shThemeMidnight  shThemeRDark
---

Android 手机操作系统是运行在 Linux Kernel 的分层操作系统，一共分为4层，从上到下依次为**应用层、应用框架层、系统运行库层、核心层**，具体分层结构如下图。

![android_system_frame](/res/img/blog/2015/04/13/android_system_frame.png) 

<!-- more -->

* **应用层**(略)

* **应用框架层**

	应用框架层提供API供开发者访问设备硬件、获取位置信息等，不需要关心底层具体的实现机制和硬件实现方式，简化了应用程序开发的框架设计。
	
	主要包括以下组件:
	
	+ **Views(视图)**
	
	+ **Resource(资源管理器)**
		
		提供非代码资源转换和访问，如本地字符串(XML 文件配置)、组件和布局文件
	
	+ **Notification Manager(通知管理器)**
	
		可以在状态栏中显示自定义的提示信息。
	
	+ **Activity Manager(Activity管理器)**
	
		管理Android应用程序界面的生命周期(onCreate--创建、onResume--显示、onpause--暂停、onStop--停止等)，一个手机屏幕界面可以对应一个Activity。
	
* **系统运行库层**
	
	+ **C/C++核心库**
	
		提供必须的C/C++核心库支持对应组件使用，例如(libc、SGL、OpenGL、SQLite、WebKit、SSL)
		
	+ **Dalvik虚拟机运行环境**
	
		运行库包含Android Runtime，核心为Dalvik虚拟机,每个android 应用程序都运行在Dalvik虚拟机上，且每一个应用程序都有独立运行的进程空间：**Dalvik虚拟机**只执行DEX可执行文件。
		
		DEX生成:**java应用程序 --> .class-->通过dx工具将class文件转换成DEX格式**
		
		总结Dalvik虚拟机特性:
		
		- **每个android应用运行在一个Dalvik虚拟机实例，每一个虚拟机实例都是一个独立的进程空间**
		
		- **虚拟机的线程机制、内存分配和管理、Mutex(进程同步)等的实现都依赖底层Linux系统**
		
		- **所有android 应用的线程都对应一个Linux线程，因而虚拟机可以更多的使用Linux系统的线程调度和管理机制**

* **核心层**

	提供核心系统服务，例如文件管理、内存管理、进程管理、网络堆栈、驱动模型，核心层内核同时也作为硬件与硬件之间的抽象层。
