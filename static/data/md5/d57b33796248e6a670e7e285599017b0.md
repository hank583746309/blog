---
title: 抓包｜获取移动app里的数据
date: 2017-11-16 22:18:21
categories: "开发"
tags:
	- 技术
	- Wi-Fi
	- 软件
	- 网络安全

---

什么是抓包?

抓包（packet capture）

> 就是将网络传输发送与接收的数据包进行

![抓包｜获取移动app里的数据][app]

 *  截获
 *  重发
 *  编辑
 *  转存

也用来`检查网络安全`

也经常`进行数据截取`等

--------------------

移动app抓包,获取图片,视频等数据

![抓包｜获取移动app里的数据][app 1]

> 很多app是没有网页版的　　

比如，游戏应用等

通过抓包分析http/https等数据

便可以获取其中的数据

如果应用本身没有加密措施

很容易获取到明文的密码,社交媒体,照片等信息

--------------------

搭建抓包环境，使用fiddler

> 什么是fiddler?

![抓包｜获取移动app里的数据][app 2]

Fiddler是一个http协议调试代理工具

它能够记录并检查所有你的电脑和互联网之间的http通讯

设置断点

> 下载fiddler

![抓包｜获取移动app里的数据][app 3]

> 设置截取https

![抓包｜获取移动app里的数据][app 4]

> 允许远程连接

![抓包｜获取移动app里的数据][app 5]

--------------------

下载安全证书

![抓包｜获取移动app里的数据][app 6]

> 解决Fiddler "creation of the root certificate was not successful”的问题

进入到fiddler安装的根目录

打开cmd命令窗口

    makecert.exe -r -ss my -n "CN=DO_NOT_TRUST_FiddlerRoot, O=DO_NOT_TRUST, OU=Created by http://www.fiddler2.com"-sky signature -eku 1.3.6.1.5.5.7.3.1 -h 1 -cy authority -a sha1 -m 120 -b 09/05/2012

如图 所示

![抓包｜获取移动app里的数据][app 7]

> 证书是需要在手机上进行安装的

![抓包｜获取移动app里的数据][app 8]

> 手机通过usb连接电脑

![抓包｜获取移动app里的数据][app 9]

将证书文件放置于手机TF卡或本机内存中

然后进入设置-更多设置-系统安全

从SD卡进行安装

![抓包｜获取移动app里的数据][app 10]

--------------------

网络设置

> cmd 中使用命令 ipconfig

查看电脑IP地址

找到无线局域网WLAN的`IPv4地址`

记下此地址。

![抓包｜获取移动app里的数据][app 11]

> 在手机wifi设置`手动代理`

![抓包｜获取移动app里的数据][app 12]

--------------------

开始抓包

> 你可用手机浏览器打开百度

也可以打开一个app

fiddler会自动截取网络数据

![抓包｜获取移动app里的数据][app 13]

> 附上图标的解释

![抓包｜获取移动app里的数据][app 14]

--------------------

不妨练一下手试试?

![抓包｜获取移动app里的数据][app 15]


[app]: static/resources/crawler/FIEI-BAMU-RUNI.jpg
[app 1]: static/resources/crawler/NNBV-ZEZU-MJQ3.jpg
[app 2]: static/resources/crawler/I6VU-MU26-R7NF.jpg
[app 3]: static/resources/crawler/3MAB-EJYQ-BFBZ.jpg
[app 4]: static/resources/crawler/VEAE-ZNUM-UUUI.jpg
[app 5]: static/resources/crawler/FAMB-VBNE-AEMN.jpg
[app 6]: static/resources/crawler/UUI2-MUMI-AFQI.jpg
[app 7]: static/resources/crawler/R3QN-3Y7B-NAEY.jpg
[app 8]: static/resources/crawler/3MBB-FVZ7-NIMY.jpg
[app 9]: static/resources/crawler/J77B-JUZV-M63Q.jpg
[app 10]: static/resources/crawler/7FFF-MERN-2AEZ.jpg
[app 11]: static/resources/crawler/JYQU-BFVV-EJNN.jpg
[app 12]: static/resources/crawler/U2I2-UA6R-MQBR.jpg
[app 13]: static/resources/crawler/NEUY-FJZY-EMNA.jpg
[app 14]: static/resources/crawler/VRNI-VV6Z-N67Z.jpg
[app 15]: static/resources/crawler/B3EE-VIRZ-MFBQ.jpg
 *  **原文作者：** 黑客与极客
 *  **原文链接：** https://www.toutiao.com/item/6489016553823011341/
 *  **版权声明：** 本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 4.0][] 许可协议。转载请注明出处。
