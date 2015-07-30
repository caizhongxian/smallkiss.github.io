---
layout : post
title : "Android NullPointerException解决方案"
category : Android
duoshuo: true
date : 2015-07-24
tags : [Android , NullPointerException ]
SyntaxHihglighter: true
shTheme: shThemeMidnight # shThemeDefault  shThemeDjango  shThemeEclipse  shThemeEmacs  shThemeFadeToGrey  shThemeMidnight  shThemeRDark
---

		不知道你们在Android开发中是否遇到Android空指针异常NullPointerException相关问题，引发此类异常的可能性
	较多，常规的错误如下：

<!-- more -->

1. 刚刚升级了Android SDK，没有对emulator做清理工作:在模拟器的命令行commandline下加入-wipe-data可以清空模拟器，通常还可以解决Android模拟器无法启动等问题

2. 升级了Android SDK，但ADT插件工作不正常
	1. 如果你升级了开发包，但使用Eclipse开发环境的网友应该更新你的Android ADT版本，参考 Android SDK 0.9版升级注意点
	2. 同时ADT Cache也需要清除，如果使用Windows系统可以定位到C:/Documents and Settings/系统用户名/Local configuration/Application Data/Android下，删除userdata.img和emulator.cfg这两个配置文件

3. 权限不足，拒绝执行: 使用Android m5-rc0.9 beta SDK的开发人员需要注意严格的权限请求，类似塞班中的能力，需要在androidmanifest.xml中加入user-permission，详细的权限中文解释参考 Android权限列表permission说明一文
4. 代码本身问题:使用Logcat跟踪调试下，同时网络延迟时也会产生很多异常。
