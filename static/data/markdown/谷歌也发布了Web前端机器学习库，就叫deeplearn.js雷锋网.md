---
title: 谷歌也发布了Web前端机器学习库，就叫deeplearn.js
date: 2017-08-08 18:17:32
categories: "开发"
tags:
	- Google
	- 机器学习
	- JavaScript
	- 编程语言
	- 人工智能

---

雷锋网 AI 科技评论按：在人工智能时代，不管是音箱、手机、汽车、app，自家产品没有用上深度学习都不好意思跟别人打招呼；另外，谷歌和 Facebook 都分别在 TensorFlow 和 Caffe 2 里提出了在移动设备上运行机器学习算法的目标和相关支持，更优秀的框架和更低的计算力要求确实是移动应用开发者的福音。不过这还没完，在浏览器上以 WebApp 的形式做模型推理甚至模型训练也有重要的开发和应用需求。

以往大家对前端机器学习库的关注度较低，不外乎人们认为 JavaScript 运行速度低、应用范围窄、支持前端的库少等几个原因。不过许多JS图形库已经有力地证明了 JavaScript 不是低速的代名词，带有构建好的机器学习算法的库也确实有一些，比如 brain.js、Synaptic、Natural、ConvNetJS、mljs等等，分别是几个神经网络、自然语言处理等的库，其中最出名、最先进的是卷积神经网络库 ConvNetJS，不过据雷锋网 AI 科技评论了解，它已经不再积极地维护了。

![谷歌也发布了Web前端机器学习库，就叫deeplearn.js][Web_deeplearn.js]

现在谷歌也决定在机器学习前端开发领域添一把柴，昨天发布了开源了自己的前端机器学习库 deeplear.js（https://pair-code.github.io/deeplearnjs/）。

谷歌的 PAIR（People + AI Research）研究小组是一个以人为中心的 AI 系统研究小组，他们的研究兴趣是各种人类和人工智能之间的互动可能，包括为工程师提供更便捷的开发方式，一直到用人工智能理解生活中各种各样的事情。deeplearn.js 就是 PAIR 出力、借助了谷歌大脑团队的一点帮助开发出来的，它除了支持构建可微的数据流图、带有可以直接使用的数学函数外，还使用 WebGL 来加速训练和推理过程，从而提供了高性能的机器学习模型开发平台，可以在浏览器环境下训练模型或者用训练好的模型做推理。PAIR 希望对机器学习感兴趣的人可以把它用在教育、理解模型、艺术工作等各个领域。

deeplear.js 提供了两套 API，一套是类似 NumPy 的即时执行模型，另一套是对 TensorFlow API 的重现，不过会略有延迟。它当然也提供了详细的开发文档和新手教程。为了方便刚接触的人快速了解核心概念，新手教程里有专门面向初次接触机器学习者的部分，讲解了基本的计算原理；自带的 demo 也非常简单直观便于操作，比如下图就是用 deeplear.js 实现的经典卷积网络 MNIST 识别模型，界面美观、清晰易懂。只有加载时候花一点时间，修改模型的时候非常方便快捷。

![谷歌也发布了Web前端机器学习库，就叫deeplearn.js][Web_deeplearn.js 1]

在 deeplear.js 的官网上也一并介绍了这个项目的路线图，除了下一步要支持到 WebGL 2.0以外，SGD之外的优化器、2D逻辑采样（目前需要在3D逻辑空间实际2D空间之间转换）、增大batch大小、提高与 TensorFlow 之间协作的易用性、增加循环网络类型等等修补、增添也会加入到 deeplear.js 中来。可预见的是，deeplear.js 在不久的将来会成为真正完善好用的前端机器学习库，成为轻量的初学者和严肃的web开发者的一个好选择。

雷锋网 AI 科技评论报道。


[Web_deeplearn.js]: static/resources/crawler/BYNZ-VBYF-ANIN.jpg
[Web_deeplearn.js 1]: static/resources/crawler/QMJY-R2Q7-FIQ3.jpg
 *  **原文作者：** 雷锋网
 *  **原文链接：** https://www.toutiao.com/item/6451845989606097422/
 *  **版权声明：** 本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 4.0][] 许可协议。转载请注明出处。
