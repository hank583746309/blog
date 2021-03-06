---
title: 教你不花一分钱搭建亚马逊云（EC2），可免费使用一年
date: 2018-06-30 12:37:28
categories: "开发"
tags:
	- Ubuntu
	- Google
	- 防火墙
	- Linux
	- 亚马逊公司

---

之前分享了谷歌云搭建教程，具体文章可以参见这篇：谷歌云搭建教程，可免费使用一年。谷歌云比较好，免费用户送 300 美金使用额。而亚马逊云，也可以免费使用一年，不过每个月在使用上也有一些限制，比如流量每个月只能免费使用 15 G的出口流量，超出就要额外收费，具体免费的限制可以看官网：https://amazonaws-china.com/cn/free/faqs/ 。

aws 注册前提条件

1.要有一个亚马逊账号

2.需要有一张双币信用卡，比如 Visa、MasterCard、用于注册验证。（网上有网友说可以使用财付通的美国运通卡，不过我没试过）

亚马逊云注册步骤

官网地址：https://amazonaws-china.com/cn

如果你没有亚马逊账号，那么先注册一个账号，访问官网后，点击右上角的注册选项开始注册：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2]

然后输入邮箱、密码等信息，如：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 1]

接着继续填写联系人信息，如下：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 2]

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 3]

然后点击创建账户并继续，如果上面填写的信息没问题，则进入到信用卡验证这一步。如下：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 4]

信息提交成功后，信用卡会扣款 1 美元。接着进入下一步，电话验证：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 5]

点击立即呼叫我，然后屏幕上就会显示 4 位 pin 码，紧接着你会收到来自亚马逊的验证电话：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 6]

接听电话后，你在电话正确输入屏幕上显示的 4 位 pin 码，即可验证成功：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 7]

然后接着点击继续进入下一步，选择支持计划：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 8]

我们选择基本方案免费选项，进入下一步，这一步会我们的账户处于激活中，如果成功激活后会收到一封激活邮件，这个过程大概几分钟的时间：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 9]

亚马逊云 EC2 搭建

点击右上角的我的账户，然后选择 AWS 控制台，输入账号、密码进行登录：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 10]

登录后，右上角的地区选择一个合适的地区，如：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 11]

接着，在左上角的服务，选择 EC2，如：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 12]

然后在新开的页面中，会有一个创建实例的选项：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 13]

点击启动实例，进入到选择一个 Amazon 系统映像选项，往下拉，找到 Ubuntu Server 14.04 LTS (HVM) 选项（注意，要记得选择符合条件的免费套餐）：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 14]

然后点击选择选项，进入到实例类型选项，仍旧选择符合条件的免费套餐，然后点击审核和启动：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 15]

接着是核查实例启动，这里不用操作什么，直接点击启动：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 16]

然后出现一个选择现有密钥对或创建新密钥对的弹窗，这里我们选择创建新密钥对，然后密钥对名称你可以随便取一个名字，不过该名字在登录时有用，这里我取 gufen，如下：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 17]

然后点击下载密钥对，下载一个后缀为 pem 的文件,因为我这里名称为gufen，所以下载的文件名称为 gufen.pem 。(注意该文件记得保存，后面会用到，用于服务器登录)。然后启动实例即可：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 18]

启动后，会提示启动状态：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 19]

如果你害怕不小心超出免费账单，那么可以选择创建账单警报。这里我忽略。

过一会而重新返回 EC2 首页，就会看到实例已经启动并在运行了：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 20]

点击正在运行的实例，可以查看外网 ip 、共有 dns 等信息：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 21]

使用 xshell 连接 EC2 服务器

这里连接工具我选择 xshell，你也可以选择其它连接工具。打开 xshell，然后在工具选项选择用户密钥管理者：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 22]

选择后，在弹出的对话框里面导入之前保存的 pem 文件，如下;

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 23]

导入后，新建连接，如：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 24]

然后在新建连接里面输入名称（随便填）、协议 ssh、主机（EC2 实例的连接ip)、端口号 22 ：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 25]

信息填完后，不要点击确定，点击连接下方的用户身份验证：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 26]

注意：方法选择 Public key，用户名填 ubuntu （根据你选择的 EC2 实例类型），用户密钥选择之前导入的 pem 文件。官方文档是说：

每个 Linux 实例类型均使用默认 Linux 系统用户账户启动。

对于 Amazon Linux，用户名称是 ec2-user。

对于 RHEL5，用户名称是 root 或 ec2-user。

对于 Ubuntu，用户名称是 ubuntu。

对于 Fedora，用户名称是 fedora或 ec2-user。

对于 SUSE Linux，用户名称是 root 或 ec2-user。

你可以根据你自己选择的系统类型选择填写对应的用户名。

只要信息没填写错误，点击确定后就可以连接成功：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 27]

然后就可以开始搭建各种服务了，诸如酸酸等各种服务。:) 。如果在搭建过程中需要使用 root 用户，使用 sudo -i 命令切换到 root 用户即可。上面关于亚马逊云aws搭建基本就完成了，不过还要记得配置防火墙。

修改 EC2 防火墙配置

在搭建完相应的服务后，比如酸酸，发现始终连接不上。亚马逊云 EC2 防火墙入站配置默认只开启了 22 端口的流量，你可以修改该配置，把协议和端口范围都改成全部，或者新建一条防火墙规则，开启某个特定端口。

在实例列表中，往右边拖动，有一个安全组标签，选择该标签进入防火墙配置：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 28]

然后编辑入站规则：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 29]

改成所有流量通行，或者你可以添加其它端口规则：

![教你不花一分钱搭建亚马逊云（EC2），可免费使用一年][EC2 30]

修改完后，基本上就立即生效了，这时候就可以愉快的使用各种服务了。上面的图文比较详细，基本把所有的步骤都截图贴上了，有需要的小伙伴可以添加收藏。


[EC2]: static/resources/crawler/UFBY-BBZI-BMRM.jpg
[EC2 1]: static/resources/crawler/VYAF-EEZZ-FZMM.jpg
[EC2 2]: static/resources/crawler/2YJB-NMNU-2EZU.jpg
[EC2 3]: static/resources/crawler/VE2Q-2UF6-VARN.jpg
[EC2 4]: static/resources/crawler/MF3A-2UAN-MJJU.jpg
[EC2 5]: static/resources/crawler/MIQ7-B37Z-QMQY.jpg
[EC2 6]: static/resources/crawler/7FIZ-BJB2-ENQE.jpg
[EC2 7]: static/resources/crawler/67NV-3IRU-J6FU.jpg
[EC2 8]: static/resources/crawler/VYRM-NEYZ-7RAV.jpg
[EC2 9]: static/resources/crawler/BVRN-AVFQ-VEJJ.jpg
[EC2 10]: static/resources/crawler/FF2I-MYJQ-FEVQ.jpg
[EC2 11]: static/resources/crawler/B2Q6-BVMZ-AUYQ.jpg
[EC2 12]: static/resources/crawler/RFER-EIIB-YEER.jpg
[EC2 13]: static/resources/crawler/NUVM-NJJU-2AVI.jpg
[EC2 14]: static/resources/crawler/FYYM-N3Y2-YZJJ.jpg
[EC2 15]: static/resources/crawler/IIEM-BMUQ-EF73.jpg
[EC2 16]: static/resources/crawler/IVEM-BVUA-IJIB.jpg
[EC2 17]: static/resources/crawler/YQFN-YQEZ-MRYN.jpg
[EC2 18]: static/resources/crawler/ZIEN-VIR2-6B6V.jpg
[EC2 19]: static/resources/crawler/BYU6-BEFJ-FEAQ.jpg
[EC2 20]: static/resources/crawler/RV2E-AAYF-AFJY.jpg
[EC2 21]: static/resources/crawler/MYEE-JY6Z-ZB2E.jpg
[EC2 22]: static/resources/crawler/FUBF-YF7F-2EUJ.jpg
[EC2 23]: static/resources/crawler/UMBY-MYUN-RBFU.jpg
[EC2 24]: static/resources/crawler/MJUZ-ENBV-VMIR.jpg
[EC2 25]: static/resources/crawler/EFVA-YQE6-RRRM.jpg
[EC2 26]: static/resources/crawler/MQUV-ANUR-7JMR.jpg
[EC2 27]: static/resources/crawler/UZJ3-AEII-FJFN.jpg
[EC2 28]: static/resources/crawler/F6JA-NF7V-Y3AA.jpg
[EC2 29]: static/resources/crawler/ZIJM-ZMYF-Z6NJ.jpg
[EC2 30]: static/resources/crawler/3UNU-NUYV-UJUE.jpg
 *  **原文作者：** 蜻蜓微微点水
 *  **原文链接：** https://www.toutiao.com/item/6572732112049275405/
 *  **版权声明：** 本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 4.0][] 许可协议。转载请注明出处。
