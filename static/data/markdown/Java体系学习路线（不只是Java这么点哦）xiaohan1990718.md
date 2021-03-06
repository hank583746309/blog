---
title: Java体系学习路线（不只是Java这么点哦）
date: 2012-11-07 23:10:26
categories: "开发"
tags:
	- Java

---

这篇是知通团队的（字面上看的哈），是我从百度荡下来的。具体的做了删减，是初级学习的路线。这段时间在重新复习java，所以就发到CSDN上来了，原出处没了，删改了部分。卞飞(这是原作者，我就留下此人名了)

# 学习线路图 #

## Java SE ##

### 学习内容 ###

（1）下载安装JDK，配置本机Java环境

（2）Java基础语法

（3）Java面向对象特性（抽象—继承—封装—多态）

（4）数组

（5）集合类【熟练掌握，特别是List、Set、Map类谱】

（6）常用类【熟练掌握，如：Object、String、Date、Math类等】

（7）异常处理【了解原理和规则，会使用】

（8）I/O编程【熟悉使用方法，了解基本原理】

（9）新特性（泛型、自动打包解包、枚举、for-in循环等）【会使用，看到代码能明白】

（10）多线程【了解原理和使用】

（11）Java日期处理和正则表达式【熟悉】

（12）网络编程（Socket）【了解】

（13）GUI程序设计【了解】

（14）反射机制【了解，可跳过】

（15）Applet程序设计【了解，可跳过】

### 学习资料 ###

**视频资料：**

（1）尚学堂（马士兵）JavaSE教程--（初入门可看）

（2）V512工作室JavaSE教程（这个我不了解--看张龙的吧-风中叶 北京圣思园 现在已关闭）

（3）传智播客（张孝祥）JavaSE教程（1、3、4 选一个得了，2我之前看的时候讲的有深入的东西，进阶看）

（4）孙鑫JavaSE教程（入门）

**书籍资料：**

（1）《Head First Java》 【团队图书馆藏】

（2）《Java 核心技术 (卷1)》【团队图书馆藏】

（3）其它JavaSE基础的书籍

**电子资料：**

（1）Java 2 SE 6 Documentation

（2）JAVA编程百例 （练习为主）

（3）30分钟学会正则表达式

（4）SUN Java培训教程－翻译稿

### 2.1.3学习时间 ###

30天

### 2.1.4学习工具 ###

（1）前期（20天）使用Editplus、UltraEdit或Notepd++等二进制文本编辑器

（2）后期（10天）使用Eclipse IDE【熟悉Eclipse的基本使用】

### 2.1.5实例项目  ###

（1）尚学堂（聊天系统）

（2）尚学堂（坦克大战）

### 2.1.6注意事项 ###

学习JavaSE会比较枯燥，有些内容不是很理解，不理解的可以先记下，在以后的实践中会慢慢理解，灵活运用。至于学习枯燥，可以到网上找些JavaSE的简单程序题目做做（可以打印图案类的），还可以调调applet或GUI（awt/swing）的程序。这部分需要熟练掌握的一定要做到，这里是Java大厦的地基。

**如果是自学的话，淡红色部分均不要关注，上面淡红色部分是我认为扯淡的东西，故而删除。但为保持原作者结构，保留而改色。**




## 数据库&JDBC（MySQL或Oracle）--个人认为MYSQL入门最好 ##

### 学习内容 ###

**数据库部分：**

（1）下载安装数据库

（2）数据库基础（发展历史，基本原理等）

（3）SQL数据查询语句（条件查询，排序，分组，模糊，多表查询，子查询等）【熟练掌握】

（4）SQL数据操作语句（插入、删除、更新表数据等）【熟练掌握】

（5）SQL数据定义语句（创建表，修改表结构，删除表等）【熟练掌握】

（6）SQL数据控制语句（授权等）【了解】

（7）数据库基本函数【熟悉】

（8）数据库对象（表、视图、索引、序列、约束等）【熟悉】

（9）数据库事务控制（断点，提交，回滚等）【熟悉】

（10）存储过程、触发器等【了解，可跳过】

（11）数据库设计三范式【熟练掌握】

（12）PowerDesigner工具使用（Physical Data Model设计）【熟练掌握】

**JDBC部分：**

（1）熟悉java.sql.\*;包的类结构【熟悉】

（2）熟悉JDBC连接数据库的原理和步骤【熟练掌握】

（3）使用JDBC连接数据库并封装到工具类【熟练掌握】

（4）使用JDBC完成对数据库的CRUD（create，read，update，delete）操作【熟练掌握】

（5）完成各种数据类型的数据读取（String，Integer，Date等），了解数据库类型和Java类型的对应关系【熟练掌握】

（6）可滚动结果集与分页技术（掌握MySQL或Oracle的分页技术）【熟练掌握】

（7）数据库事务处理和批处理【了解】

（8）数据库连接池的原理和实现【了解】

（9）数据库的元数据信息（关于数据的数据）【了解，可跳过】

（10）DAO设计模式与搭建【了解，可跳过】

（11）Java反射在JDBC中的应用【了解，可跳过】

（12）数据库连接池的原理和实现【了解】

### 2.2.2学习资料 ###

**视频资料：**

（1）尚学堂MySQL教程

（2）V512工作室Oracle教程

（3）IT电子教育门户Oracle教程

（4）传智播客JDBC教程 张龙的也还行。

**书籍资料：**

（1）《Oracle宝典》  W3CSHOl.com.cn就很不错的了

**电子资料：**

（1）MySQL 5.1查考手册

（2）深圳-华为Oracle数据库基础知识

（3）Oracle 10G SQLReference

### 2.2.3学习时间 ###

数据库(10天) + JDBC(15天) = 25天 【建议两部分内容交叉学习】

### 2.2.4学习工具 ###

（1）Eclipse IDE

（2）DOC（连接数据库，操作数据库）

（3）PowerDesigner 自学的话 现在接触就不适当（凭个人学习经验来说）

### 2.2.5实例项目 ###

完成“知通团队技术论坛”的数据库设计，分析查考：www.javaeye.com论坛。要求符合数据库设计三范式，具有可操作性，下面学习部分的实例项目要使用到这里设计的数据库。

### 2.2.6注意事项 ###

这里之所以把数据库和JDBC的学放到一起，是因为他们的耦合性太强了，需要交叉起来学习。另外，这里所有的数据库操作都是显示在控制台，JavaSE部分的GUI或Applet有兴趣的成员可以实现读取数据库通过它们显示。

## 2.3HTML&CSS&JavaScript ##

### 2.3.1学习内容 ###

（1）复习刚进团队学习的Html

（2）CSS基本语法【熟练掌握】

（3）了解CSS中的盒子模型【了解】

（4）结合Html模仿一个简单博客页面的CSS+div布局

（5）JavaScript基本语句【熟练掌握】

（6）熟悉JavaScript常用函数【熟悉】

（7）实现简单的Form表单验证

（8）熟悉DOM编程【熟悉】

（9）了解JavaScript中运用正则表达式【了解】

（10）Javascript方法的创建和使用【熟练掌握】

（11）了解Ajax的定义和基本原理【了解，可跳过】

（12）DreamWeaver使用初步（建立HTML、Table、Form、CSS等）

### 2.3.2学习资料 ###

**视频资料：**

（1）《CSS彻底设计研究》视频教程

（2）张孝祥JavaScript教程 www.w3school.com.cn很好！

**书籍资料：**

（1）《CSS彻底设计研究》

（2）《JavaScript经典入门教材》 Javascript高级程序设计

**电子资料：**www.w3school.com.cn帮助文档下载学习基本知识就囊括完了

（1）Html入门

（2）CSS2.0.chm

（3）JScript手册.chm

（4）CSS速成手册.chm

### 2.3.3学习时间 ###

Html（1天）+CSS（3天）+JavaScript（6天）= 10天

### 2.3.4学习工具 ###

（1）Editplus、UltraEdit或Notepd++等二进制文本编辑器

（2）Dreamweaver

（3）Firefox +Firebug 【用于Javascript调试】

### 2.3.5实例项目 ###

（1）结合Html模仿一个简单博客（网易等）页面的CSS+div布局

（2）使用JavaScript完成一个简单注册模块的Form表单验证

（3）参考www.javaeye.com论坛的格式，设计论坛实例项目各级页面的静态页面

### 2.3.6注意事项 ###

此部分学习的内容应多结合浏览器进行代码练习，还有很多不太常用的标签或属性可以不用死机硬背，到用时在去文档查找，但是常用标签一定要记得很牢。另外，不能太依靠Dreamweaver，也应该在开始的时候多练习用记事本手写代码。

## 2.4Servlet&JSP ##

### 2.4.1学习内容 ###

（1） 熟悉HTTP协议基本原理【熟悉】

（2） 下载安装Tomcat服务器，了解各个目录及配置文件作用【熟悉】

（3） 熟悉一个Java Web项目的结构和web.xml作用和简单配置，并自己搭建一个Java Web项目【熟练掌握】

（4） 熟悉Servlet的历史，原理，写一个简单的打印HelloWorld 的Servlet【熟悉】

（5） Servlet生命周期【熟练掌握】

（6） 使用Servlet处理上一个单元建立的注册表单，结合数据库，设计用户表，完成注册模块，要求解决中文用户名或用户描述问题

（7） 了解JSP相对于Servlet的优缺点，熟练掌握JSP基本语法【熟练掌握】

（8） 了解JSP内置的对象，熟练掌握常用内置对象的属性，作用和使用场合（request，response，out，session等）【熟练掌握】

（9） 了解Cookie使用方法和场合【了解】

（10） 熟悉J2EE\_API\_5.0\_DOC.CHM文档的javax.servlet.\*;javax.servlet.http.\*, javax.servlet.jsp.\*包中的常用的类，他们继承结构，常用方法，使用的场合。

（11） 下载和安装MyEclipse，学习MyEclipse的使用，下面的项目实践使用此工具

（12） 使用JSP结合JDBC完成注册模块，并同Servlet对比【熟悉】

（13） 使用JSP读取并显示注册模块注册的用户，使用分页技术，并实现用户信息的CRUD（增，删，改，查）和模糊查询用户的功能

（14） 了解EL表达式，JSTL【了解，可跳过】

（15） 了解Servlet监听器和过滤器的使用【了解】

（16） 了解文件上传与邮件发送【了解，可跳过】

### 2.4.2学习资料 ###

**视频资料：**

（1） V512工作室JavaWeb开发视频教程

（2） 尚学堂Servlet&JSP教程

**书籍资料：**

（1）《JSP宝典》【团队图书馆藏】

（2）《Head First JSP&Servlet》

**电子资料：**

（1）J2EE\_API\_5.0\_DOC.CHM

（2）servlet-2\_4-fr-spec.pdf

（3）jsp-2\_0-fr-spec.pdf

（4）jstl-1\_1-mr2-spec.pdf

### 2.4.3学习时间 ###

25天

### 2.4.4学习工具 ###

（1）前期（15天）使用Editplus、UltraEdit或Notepd++等二进制文本编辑器以及前台页面设计的Dreamweaver

（2）后期（10天）使用MyEclipse IDE【熟悉MyEclipse的基本使用】---该工具收费的，所以还是Eclipse好。

### 2.4.5实例项目 ###

（1）使用JSP结合JDBC完成注册模块【解决中文乱码问题】

（2）使用JSP读取并显示注册模块注册的用户，使用分页技术，并实现用户信息的CRUD（增，删，改，查）和模糊查询用户的功能

（3）结合上面单元的已经建好的数据库，设计好的静态页面，登陆注册模块，参考www.javaeye.com的论坛功能，完成整个BBS的编码。【要求完成：显示论坛子版块，论坛主题，发布主题，回复主题】

### 2.4.6注意事项 ###

此部分学习的时候应该先熟悉HTTP协议，Servlet的生命周期，JSP内置对象的使用，如何使用内置对象&集合类实现页面间数据传递，Servlet和JSP优缺点对比，如何解决乱码问题（硬编码和软编码对比、使用场合），如何搭建一个Java web项目的开发环境，怎样配合JDBC完成数据库的操作等。

Java 知识体系图

![R6ZV-RRBY-VRUE.jpg][]


\-------------------------------------------------------------------------------由于个人也要复习上述内容，根据个人学习习惯和经验，将上述路线调整了些。

送给我自己的话：基础是王道，思想最重要！ 以上部分的基础必须要深刻理解的。这样在今后的学习中就相对轻松多。

上诉内容基本囊括Java体系，当然他没有讲述SSH框架之类的东西，我个人认为这东西早学了没什么益处。

以上观点仅个人偏见，如有不同意见，请勿看。

现在个人复习的路子：Javascript基础、Java基础、SQL基础、Java提高。其中顺带有书籍阅读、代码练习。

Javascript书籍目前只研读一本：《Javascript高级程序设计》

Java方面近阶段只研究《Java核心技术核心卷I和卷II》

SQL方面《SQL基础教程》（我SQL底子薄，继续抓基础）

视频方面：抓薄弱的一些知识点学习，其中大部分应该要看书的。

知识总结：CSDN会频繁更新，内容均为学习内容和知识点总结之类的

复习周期：12月底截止。

目前情况：Javascript复习基本截止，少许细节东西还需多接触锻炼和记忆。Java复习和SQL方面的复习是交织的，刚开始。

//纯手敲，错误难免![微笑][QJVY-NZEN-YNZ2.gif]，希望坚持下去，并有良好的结果。


[R6ZV-RRBY-VRUE.jpg]: static/resources/crawler/R6ZV-RRBY-VRUE.jpg
[QJVY-NZEN-YNZ2.gif]: static/resources/crawler/QJVY-NZEN-YNZ2.gif
