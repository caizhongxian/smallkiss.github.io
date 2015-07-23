---
layout : post
title : "Windows8/8.1上使用VHD安装Windows7的双系统启动方案"
category : 操作系统
duoshuo: true
date : 2014-11-17
tags : [操作系统 , VHD]
---

###导引:

		网上有很多针对在Windows7/8使用VHD建立Windows8.1的多重开机系统教程，但是现在的情况却正好相反，我搜了
	一下，在Windows8/8.1下使用VHD安装windows7无外乎两种，一种是挂羊头卖狗肉吸引目光的水贴，另一种就是大胆尝
	试，却以失败告终，寻找解决方案的提问贴！
		难道真的不行吗？表示不信，于是我查了一些资料，最终在——挨踢路人甲——上面找到了方案，以下是其转载，最后附
	上链接。

<!-- more -->

>本文简要说明如何在Windows8操作系统下利用VHD搭载Windows7，如图示效果：

![system_pic](/res/img/blog/2014/11/17/pic1.png)

**Windows8/8.1系统利用VHD安装Windows7系统需满足：**

- Windows 8/8.1必须支持VHD(Windows专业版以上均可)
- Windows Bios支持MBR引导格式的硬盘

>好了，具备了上述要求后，我们就开始吧。

##Windows 8/8.1系统安裝VHD的Windows 7操作(以C盘做介绍)

1. 快捷键「win」+「x」,以系统管理员权限进入cmd
2. 使用Diskpart取代原先的「Fdisk」处理磁碟管理，该功能强大，支持脚本运行，在命令行输入「diskpart」，回车，进入diskpart 

	![diskpart1](/res/img/blog/2014/11/17/pic2.png)
	
3. 在diskpart模式下，使用create命令在C盘建立一个20G固定大小VHD,create后的vdisk表示要建立的虚拟硬盘，file后虚拟磁盘的路径
而type可以是expandable（动态扩展）或者fixed（固定容量）。使用固定容量会依照设定直接划分一块区域分配给磁盘映像使用，优点是
存取效能最好，一般采用expandable(动态扩展)方式，此方式能够节省帮助你节省硬盘空间，最后参数maximum是指定容量大小，单位为MB，
例如下面此例：

	<pre class="brush: c; ">
	create vdisk file="c:\win7.vhd" maximun=20480 type=fixed
	<pre>

	![diskpart3](/res/img/blog/2014/11/17/pic3.png)
	
4. 使用select vdisk来选择运作的vhd，接着使用attach vdisk来挂载虚拟硬盘。

	<pre class="brush: c; ">
	select vdisk file="c:\win7.vhd"
	attach vdisk
	<pre>

	![diskpart4](/res/img/blog/2014/11/17/pic4.png)
	
5. 使用「Create Partition」对虚拟磁盘进行分割，使用「Format」指令进行格式化，其中FS指格式化的档案格式，LABEL是虚拟磁盘的名称，
quick是快速格式化的意思。

	<pre class="brush: c; ">
	Create Partition Primary
	Format  FS=ntfs LABEL="Win7 VHD" quick
	<pre>

	![diskpart5](/res/img/blog/2014/11/17/pic5.png)