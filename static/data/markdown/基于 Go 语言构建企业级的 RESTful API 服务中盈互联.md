---
title: 基于 Go 语言构建企业级的 RESTful API 服务
date: 2018-06-29 12:08:28
categories: "开发"
tags:
	- Docker
	- 通信
	- Go语言
	- JSON
	- 红帽公司

---

> 文｜掘金小册
> 
> 源｜架构师小秘圈

现代软件架构已经逐渐从单体架构转向微服务架构，在微服务架构中服务间通信采用轻量级通信机制。对于轻量级通信的协议而言，通常基于 HTTP 和 RPC ，能让服务间的通信变的标准化并且无状态化。此外开发模式也越来越多的采用前后端分离的模式，在前后端分离的模式中，前后端通信一般是通过 HTTP 进行通信。

不管是微服务架构，还是前后端分离模式，都需要一个 HTTP API 服务器。而且在日后的开发生涯中可能需要构建很多个大大小小的 API 服务器，构建一个简单的 API 服务器很简单，网上有很多教程，但都是不成体系的，非常简单的 hello world 程序，这些教程通常只是讲解开发过程中的某个点，每个人的设计思路也都是不同，并没有一个成系统，成体系的 Go 服务器开发教程可供参考，实际上构建一个企业级的 API 服务还有很多工作要做。

在构建 API 时，有一种构建风格叫 REST，它虽然调用性能不及 RPC，但维护性和扩展性更好，也更通用。由于本小册不讨论微服务之间的高频调用场景， 而 REST 在实际开发中，能够满足绝大部分的需求场景，基于它的其他优势，本小册采用 REST 风格来构建 API 服务器。此外，在媒体类型上选择了 JSON，因为它的内容更加紧凑，数据展现形式直观易懂，开发测试都非常方便。REST + JSON，这也是 Go API 开发中很常用的组合。

![基于 Go 语言构建企业级的 RESTful API 服务][Go _ RESTful API]

笔者在近七年的服务器开发过程中，调研了很多 API 构建方式，这些构建方式各有优缺点，此外也构建了多个大型 API 服务器，通过这些调研、构建经验以及开发过程中遇到的坑，笔者沉淀了一套 API 服务器的构建方法，在实际工作中也得到了充分的验证。这里希望通过小册的形式给需要的朋友提供一些帮助和指引，尤其是刚接触 Go 服务器开发没多久，想早点进阶为高手的同学。希望通过阅读本小册，既能让你学会怎么更好地去构建 API 开发过程中的各个功能点，也能收获实用的构建方法和开发建议。

![基于 Go 语言构建企业级的 RESTful API 服务][Go _ RESTful API 1]

作者介绍

![基于 Go 语言构建企业级的 RESTful API 服务][Go _ RESTful API 2]

**雷克斯** 腾讯高级研发工程师，毕业后曾在 Red Hat、联想集团任职，主要做后台服务器的开发。在微服务、容器云和后台 API 服务器构建上有丰富的经验，构建过 10万+ Docker 容器的容器云项目、百万级 QPS 的 API 项目。

名人推荐

![基于 Go 语言构建企业级的 RESTful API 服务][Go _ RESTful API 3]

![基于 Go 语言构建企业级的 RESTful API 服务][Go _ RESTful API 4]

你会学到什么

本小册是一个实战类的小册，根据开发流程教读者怎样一步步构建一个企业级的 API 服务器。从开发准备到 API 设计，再到 API 实现、测试和部署，每一步都详细介绍了构建技术和笔者的开发经验和建议。通过 17 个 demo，最终构建出一个企业级的 API 服务器。通过本小册的学习，你将学到如下知识点：

![基于 Go 语言构建企业级的 RESTful API 服务][Go _ RESTful API 5]

知识点很多，跟着小册一节一节进行学习，你将从 Go 服务器开发的新手进阶为老鸟。

> 免责声明：本文转载仅作分享，版权归原作者所有。如侵权请联系我们，必予以整改或删除，谢谢您！


[Go _ RESTful API]: static/resources/crawler/7JVU-6N3A-ZUB2.jpg
[Go _ RESTful API 1]: static/resources/crawler/QQB7-NR6N-NUNJ.jpg
[Go _ RESTful API 2]: static/resources/crawler/2YMU-NJFZ-FB3I.jpg
[Go _ RESTful API 3]: static/resources/crawler/AMUJ-VV7F-BAEB.jpg
[Go _ RESTful API 4]: static/resources/crawler/IYAR-JMA6-ZUNQ.jpg
[Go _ RESTful API 5]: static/resources/crawler/3YE6-VBZR-RINB.jpg
 *  **原文作者：** 中盈互联
 *  **原文链接：** https://www.toutiao.com/item/6572353555968033293/
 *  **版权声明：** 本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 4.0][] 许可协议。转载请注明出处。
