---
title: 基于SSM架构的网络租车系统
date: 2018-06-13 09:23:06
categories: "开发"
tags:
	- 支付宝
	- 技术
	- 需求分析
	- 百度地图
	- 百度钱包

---

**项目来源：**

之前就做了一个简易的租车都不能说是项目的项目，就是将数据库中的信息在页面以表格形式展示，输入租车天数，租赁数量确定租车信息。所以毕业设计以此为思路做一个项目。

**项目代码地址**

https://github.com/liunaijie/car-project 。里面包含论文

**项目说明：**

项目定位是一个租车平台，即将线下租车公司的资源进行整合。让线下租车公司进驻平台，推广平台，获取用户。

架构： SSM(spring+springmvc+mybatis) 使用该框架主要是实习期间接触了这个框架（第一次使用框架），觉得这个框架整体较之前写的简单，例如在controller类文件中加注解等方式就可以配置控制层。

maven：使用maven方式构建项目，整体项目小，不在有lib文件夹，调整jar包只需修改pom文件。

**需求分析：**

1.用户分类： 平台管理员（超级管理员），商家管理员（普通管理员），用户

（1）超级管理员：作为平台的管理员，主要是对商家的信息进行增删改查、设置普通管理员。新建商家，修改商家信息，删除商家。平台管理员也会赋予上传车辆（需指定商家）和删除车辆的权限，主要是对违规车辆进行删除。对进驻的商家设置管理员。

（2）普通管理员：进驻商家的管理员，主要是对本商家进行车辆上传，修改，删除操作。

（3）用户：用户浏览平台，筛选车辆，租赁车辆

**对项目所加的一些小功能**

1.邮箱注册

用户注册，商家注册，用户租赁车辆时都会发送邮件。

（1）用户注册时发送激活邮件，只有激活后账号才能登录。

（2）用户租赁车辆后，会向用户发送邮件提醒用户刚才租赁过车辆，确保是本人操作，并同时向商家发送邮件，提醒商家准备车辆。

毕业项目演示时将项目放到了阿里服务器上，但阿里服务器的25端口关闭了。所以改写了发送邮件代码使用465端口

2.调用百度地图

查看车辆信息，商家信息时会展示商家位置，并通过浏览器定位到用户，实现驾车导航。

由于百度地图的定位不准确，所以用户的定位不是很准确。商家注册时需要添加商家经纬度，后来发现可以可以填写具有一定格式的商家位置，百度地图会自动计算经纬度。

**遗憾**

本来想做支付模块，但发现支付宝，微信以及百度钱包等方式都需要工商注册信息。所以现在支付只是做了一个弹出框。

![基于SSM架构的网络租车系统][SSM]


[SSM]: static/resources/crawler/B7NI-ZNMU-3QNZ.jpg
 *  **原文作者：** 程序员小新人学习
 *  **原文链接：** https://www.toutiao.com/item/6566373577786917390/
 *  **版权声明：** 本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 4.0][] 许可协议。转载请注明出处。
