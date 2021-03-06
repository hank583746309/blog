---
title: 有个AI陪你一起写代码，是种怎样的体验？｜附ICLR论文
date: 2018-04-28 13:24:48
categories: "开发"
tags:
	- Java
	- 机器学习
	- GitHub
	- 编程语言
	- 人工智能

---

> 麻瓜栗 发自 凹非寺
> 
> 量子位 出品 | 公众号 QbitAI

从前，任何程序的任何功能，都需要一行一行敲出来。


后来，程序猿要写的代码越来越多，世界上便有了各种各样的API，来减少大家的工作量。有些功能，可以让API来帮我们实现。

不过，人类写下的话，API并不是每一句都能听懂。语言不通的话，愿望就无法实现。

![有个AI陪你一起写代码，是种怎样的体验？｜附ICLR论文][AI_ICLR]

现在，有会写代码的AI可以替你召唤API。以及，它能做的并不止这些。

# 吃得不多，写得不少 #

莱斯大学的一群极客，发布了一个基于深度学习的代码编写应用。神经网络从GitHub这样的线上源代码库里汲取养分，写自己的程序。

![有个AI陪你一起写代码，是种怎样的体验？｜附ICLR论文][AI_ICLR 1]

这个应用叫Bayou，是在美国国防高级研究计划局 (DARPA) 和谷歌研究院的资金支持下诞生的。

Bayou的爸爸们说，这个孩子和它的前辈不同。以前那些会写程序的AI，都需要事先投喂大量细节，才能开始生成代码。有空写好那些细节，不如自己写个程序了。

而要支配Bayou，开发者只要给它吃一点点信息，比如几个小小的**prompt**，它就会善解人意地猜测，人类想要怎样的程序，然后疾速补全代码。﻿

![有个AI陪你一起写代码，是种怎样的体验？｜附ICLR论文][AI_ICLR 2]

**△** input

举个简单的栗子，假设你想写个读取文件的Java方法。如果你知道某个API里面有个功能叫做**readline**，就可以写出上面这样的代码。


![有个AI陪你一起写代码，是种怎样的体验？｜附ICLR论文][AI_ICLR 3]

**△** output

然后，Bayou便知道它要召唤的技能叫做readline，随之为你输出以上代码，只要用这段代码来调用你需要的API就可以了。


不要忘了，专门给Bayou看的部分，要标上**///**，以示害羞。

![有个AI陪你一起写代码，是种怎样的体验？｜附ICLR论文][AI_ICLR 4]

除了调用一个或者几个API，我们还可以用**API数据类型**把自己的要求具体化。另外，Bayou有一个非常友好的特点，便是**多模态**，就算把各种不同的术语混进同一段代码，它也能看懂。

# 草图训练大法 #

毕竟，这只AI已经从大约1500个安卓应用里，学习了人类编写的上**亿**行Java代码。

用一种名为“**神经草图学习** (Neural Sketch Learning) ”的方法来训练神经网络，Bayou可以给自己想要读取的每个程序，创建一个树状结构的句法模型，称作“**草图** (sketch) ”。

![有个AI陪你一起写代码，是种怎样的体验？｜附ICLR论文][AI_ICLR 5]

当有人对Bayou提出要求的时候，系统会先做一个**判断**，感受一下自己要写的程序是怎样的。然后，就是为代码库里同类型的程序做草图。这里只识别**high-level**模式，而忽略所有low-level特征。

在那之后，Bayou还有一个用来理解**low-level**细节的模块，可以自动进行逻辑推理。它会根据第一步做出的判断，生成我们可能需要的代码。

哪怕问题没有解决，Bayou给出的代码示例或许也能帮我们提出更合适的问题。这时候再去Stack Overflow寻求答疑，疗效可能会好一些。

# 孩子你还小﻿ #

![有个AI陪你一起写代码，是种怎样的体验？｜附ICLR论文][AI_ICLR 6]

**△** 我有优秀的聚类能力

团队认为，Bayou非常适合为各种API**编写代码示例**。不过，现在的它并不十分成熟，还有一些局限性。


比如，它目前支持的**API非常有限**，只有java.lang，java.io和Java.util。再比如，它没办法处理通配符的多种类型。

作为一只年幼的AI，Bayou还有很长的路要走。抱着GitHub修炼的好处是，从那里识别出的模式会比较**通用**；缺点是GitHub上面的项目质量**参差不齐**。

![有个AI陪你一起写代码，是种怎样的体验？｜附ICLR论文][AI_ICLR 7]

目前，团队正在给Bayou增加一些**自然语言处理**技能，也想在用户体验里增加一些交互性。

调戏Bayou传送门：

http://askbayou.com/

论文传送门：

https://arxiv.org/pdf/1703.05698.pdf

这是发表在ICLR 2018的论文。不过，在5月1日的温哥华，团队可能又要端上新版本了。

— 完 —

诚挚招聘

量子位正在招募编辑/记者，工作地点在北京中关村。期待有才气、有热情的同学加入我们！相关细节，请在量子位公众号(QbitAI)对话界面，回复“招聘”两个字。

量子位 QbitAI · 头条号签约作者

վ'ᴗ' ի 追踪AI技术和产品新动态


[AI_ICLR]: static/resources/crawler/B2QI-ZVQI-BAFV.gif
[AI_ICLR 1]: static/resources/crawler/VFEB-AEA2-IEVA.gif
[AI_ICLR 2]: http://p3.pstatp.com/large/pgc-image/1524892583103e54b676090
[AI_ICLR 3]: static/resources/crawler/NBQB-NRIF-IBUF.jpg
[AI_ICLR 4]: static/resources/crawler/ZUNB-N3EV-ZYN3.gif
[AI_ICLR 5]: static/resources/crawler/JEM2-QUYA-AJNE.jpg
[AI_ICLR 6]: static/resources/crawler/RFRQ-226F-EMRQ.jpg
[AI_ICLR 7]: static/resources/crawler/7JFF-V3Z3-MEAR.gif
 *  **原文作者：** 量子位
 *  **原文链接：** https://www.toutiao.com/item/6549365946882982408/
 *  **版权声明：** 本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 4.0][] 许可协议。转载请注明出处。
