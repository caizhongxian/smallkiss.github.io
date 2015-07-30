---
layout : post
title : "操作系统提示“必须重新启动才能执行应用更新解决方案”"
category : 操作系统
duoshuo: true
date : 2014-09-22
tags : [操作系统]
---

操作系统提示“必须重新启动才能执行应用更新解决方案”

运行----输入gpedit.msc---打开组策略，计算机配置--管理模板--Windows组件---Windows Update中找"对于已登录的用户，计划的自动更新安装不执行重新启动",双击,设置选"已启用",确定。

<!-- more -->

**解决方案**
	![pygments-autumn](/res/img/blog/2014/9/22/system_restart.png)  