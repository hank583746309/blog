---
title: 开发要不要自己做测试？怎么做？
date: 2018-07-02 13:41:22
categories: "开发"
tags:
	- 脚本语言
	- Java
	- Google
	- 软件
	- Facebook

---

![开发要不要自己做测试？怎么做？][YQMZ-UF7V-RBEF.jpg]

作者｜茹炳晟

编辑｜小智

出处｜软件质量报道

现在包括 Google、Facebook 和 eBay 等一线互联网巨头公司都在逐渐推行“没有专职测试，测试工作由开发人员完成”的全新模式，原本专职的业务功能测试团队的规模逐渐缩小，有些甚至已经完全没有了，而原本的测试开发团队逐渐在向工程效能（Engineering Productivity）团队转型。这些互联网巨头之所以能够很好地落地这种全新的模式，是因为他们都较好地解决了这个模式的两个最大的难题：

开发人员如何能够胜任测试

工程效能团队如何赋能开发人员，帮助开发人员高效地完成高质量测试

本文会围绕这两个问题来展开讨论。首先让我们一起看一下开发人员自己做测试都会遇到哪些问题和阻碍。

1 开发人员自己做测试会遇到哪些问题

人性角度引发的问题

首先从人性的角度来看，开发人员通常是属于“创造性思维”，自己开发的代码就像是亲儿子一样，怎么看都觉得实现很棒；而测试人员则属于“破坏性思维”，测试人员的职责就是要尽可能多的找到潜在的缺陷，而且专职的测试人员通常已经在以往的测试实践中积累了大量典型的容易出错的模式，所以测试人员比起开发人员，往往更能客观且全面做好充分的测试。

思维惯性的问题

刚才是从人性角度上来讲的，如果从技术层面来看，由开发人员自己测试，会存在严重的“思维惯性”，通常开发人员在设计和开发过程中没有考虑到的分支和处理逻辑，在自己做测试的时候同样不会考虑到。比如对于一个函数，其中有一个 String 类型的输入参数，如果开发人员在做功能实现的时候压根没有考虑到 String 存在 值得可能性，那么代码的实现里面也不会对 值做处理，连带结果就是测试的时候就更不会设计 值得测试数据，这样的“一条龙”缺失就会给代码的质量留下了缺陷隐患。更糟糕的是，对于这种情况，即便启用了代码覆盖率指标去衡量测试完整程度，也不能有效暴露这类问题，因为处理 值得代码压根没有写，又何来代码覆盖率一说呐。

被测试环境和测试执行环境的复杂性问题

有专职测试的时候，测试工作是专职测试人员完成的，专职测试人员通常会负责搭建被测试环境以及管理测试执行环境。被测试环境好理解，就是 System Under Test（SUT）。而测试执行环境是指用于执行测试用例的机器，比如对于 Web 的 GUI 测试，最简单的测试执行环境就是你本地机器上的浏览器。但是对于大型互联网企业，测试执行环境远远要比你想象的更复杂。通常都是一些大型的测试执行集群，甚至是内部的测试执行私有云，比如用 Selenium Grid 搭建的 GUI 测试执行环境，往往这样的集群都会有成百上千台机器，再比如用 Appium+Selenium Grid 搭建的移动设备测试集群，也往往会有上千台设备。现在没有了专职的测试人员，那就需要开发人员自己去管理、维护和搭建这些测试基础架构，这样做其实是得不偿失的，工作量本身并没有减少，只是换了一批人来做同样的事情，而且开发的精力往往更应该花在构建新的业务功能上，而不是用在维护测试基础设施。

测试数据准备的问题

测试数据准备是测试过程中必不可少的关键步骤，有专职测试的时候，是由测试人员来准备测试数据的，一方面测试人员往往比开发人员在全局层面上更了解被测系统，所以对于测试数据的设计与生成也会更高效，另一方面测试人员在以往的测试过程中已经积累了很多测试数据生成的方法和小工具。现在这些都需要开发人员自己来完成了，无疑进一步加大了开发人员的工作量，而且开发人员往往对跨模块，跨系统的测试数据准备缺乏系统性的理解，往往为了生成一条非自己业务领域的数据而花费大量的学习成本。举个例子，假设现在“买家模块”的开发人员需要测试“商品买入”的操作，那么就需要事先准备好“可以被卖的商品”，这就意味着“买家模块”的开发人员需要明确知道“卖家模块”和“商品模块”的细节，才能生成“可以被卖的商品”。这类问题在目前主流的微服务架构面前会更严重，原因是为了产生一条测试数据，可能会需要依次调用很多个服务。

测试执行与 CI/CD 集成问题

对于不同的业务开发团队，各个阶段采用的自动化测试框架可能都不同，比如有些会使用基于 Java 的 Selenium，也有些会使用基于 JavaScript 的 Nightwatch 等，有专职测试的时候，各种不同的测试框架与 CI/CD 的集成，都是由各个业务团队的测试人员和 CI/CD 的人员一起完成的，现在没有了专职测试，这部分工作就需要开发人员自己和 CI/CD 人员一起完成，这就要求开发人员不仅需要非常熟悉自动化测试框架的细节（很多时候为了更好地和 CI/CD 集成，会对开源测试框架或者是自研测试框架做二次开发，比如改进 retry 机制，增加覆盖率统计等等），还必须了解 CI/CD 的流水线设计以及脚本设计，然后再将需要支持的自动化测试框架的运行命令行和需要暴露的参数（测试用例 Git 路径、测试执行环境、测试报告路径等等）写进 CI/CD 的脚本。这些工作在很大程度上分散了开发的精力，对于提高开发自身效率是非常不利的。

失败测试用例归属问题

有专职测试的时候，开发人员往往只关注自己修改部分相关的测试用例，模块或者服务的全回归测试中如果有失败的测试用例，通常是由测试人员跟进去分析具体原因，并协调解决然后才能发布上线。但是现在开发人员负责所有测试，他就必须关注全局的测试。举个实际的例子来看，比如“用户登录”服务的开发工程师修复了一个缺陷，然后本地自测通过后递交了代码，然后很不幸，在 CI/CD 的流水线上全回归测试却发现有部分用例失败了，虽然这些失败的用例和这次的代码修改没有任何关系，但是为了保证自己的修改能够顺利上线（CI/CD 的流水线要求只有全回归测试 100% 通过才可以上线），他必须挨个去分析失败的测试用例然后自己去找到对应的人去协调解决，这显然是非常不合理和不敏捷的做法。

归根结底，这些问题的本质都会直接影响开发人员本质工作的进度和效率，那么我们应该如何解决或者在一定程度上缓解这些问题呢？这就是接下来要讨论的问题，工程效能团队如何赋能开发人员，帮助开发人员高效地完成高质量的测试。

2 工程效能团队赋能开发人员进行高效率高质量的测试

赋能的基本思路是能够让开发人员更专注于测试本身，而从那些辅助测试的工作（比如搭建测试执行环境、CI/CD 集成等）上解放出来，这些辅助测试的工作由“工程效能”服务或者相关支持工具链来统一解决。这个思想和和目前非常流行的 Service Mesh 的设计思想不谋而合，Service Mesh 也是可以让服务的开发人员可以把所有的精力集中在业务功能的实现上，而不需要去关心服务间通信的基础设施，像类似于服务的注册与发现，熔断机制等都会统一由 Service Mesh 以对业务应用透明的方式来实现。这些“工程效能”服务或者相关支持工具链通常都会由原本从测试开发转型过来的工程效能团队来设计和开发。那么我们接下来看一下可以提供哪些“工程效能”服务或者相关支持工具链，并且能以什么样的方式来解决或缓解上面提到的开发自己测试带来的问题。

测试执行服务（Test Execution Service）

CI/CD 各个阶段所有的测试执行发起都通过测试执行服务（TES，Test Execution Service），TES 通过统一的 Web Service 接口与 CI/CD 以解耦的方式进行集成。无论是 CI/CD 流水线，还是开发人员执行测试，都通过 TES 来发起，唯一的区别是开发人员一般使用 TES 的 UI 界面发起测试，而 CI/CD 是直接在流水线脚本里面调用 TES 的 Restful API 发起测试。测试执行服务的输入参数也很简单直观，通常只包括测试框架名字、测试用例集版本号、测试用例路径、 测试报告获取方式、同步 / 异步执行开关等。一旦调用 TES 发起测试，后续如何调用 Jenkins job、如何打包下载 test jar、如何找到适合的测试执行环境、如何发起测试以及如何收集测试报告等都对使用者完全透明。可以想象，现在，开发人员在和 CI/CD 集成以及执行测试的时候，已经可以完全不需要去关心执行测试的命令行、发起测试的 Jenkins job 以及配置、测试的具体执行环境、测试报告获取等信息。这将大大提高开发人员自己执行测试的效率和便利程度。

测试数据服务（Test Data Service）

前面提到过，跨模块，跨系统的测试数据准备对于开发自己做测试是个挑战，尤其是现在大量采用微服务架构，这个问题就会更突出。测试数据服务（TDS，Test Data Service）将会以 Web Service 接口的形式为所有类型的测试提供一致的测试数据准备入口。无论开发是要做 API 测试，还是 GUI 测试，或者是性能测试，都可以通过调用 TDS 的 Web Service 或者 UI 来准备各种组合类型和量级的测试数据。TDS 本身还是个开发平台，任何开发人员都可以通过脚手架代码来贡献新的数据类型支持，并且 TDS 平台本身借助自己的 Core Service 和内建数据库具有元数据管理能力，能够提供诸如测试数据数量以及质量的管理。下图展示了典型的 TDS 架构设计简图供参考。

![开发要不要自己做测试？怎么做？][QANY-NA3Q-EBQB.jpg]

测试执行环境服务（Test Bed Service）

正如前面提到的，测试执行环境对于大型企业来说是很庞大复杂的，为了方便开发人员使用测试执行环境，或者说为了使测试执行环境对于开发人员透明，就需要引入测试执行环境服务（TBS，Test Bed Service）。TBS 的主要职责是负责管理、创建，扩容 / 收缩测试执行集群。一个常见的测试执行环境架构如下图所示，TBS 会根据等待执行的测试用例的排队情况，动态决策测试执行集群的节点数量和类型，通常会使用 Docker 和 Kubernetes 来实现 TBS 的 Gird 管理。

![开发要不要自己做测试？怎么做？][FJIB-AFUE-NANZ.jpg]

构建工程效率工具链仓库（Engineering Productivity Tools Store）

类似于 App Store 的概念，可以把各种测试小工具以及提高效率的工具集统一在 Engineering Productivity Tools Store 里面集中版本化管理。比如文章开头我们提到过开发自己做测试的时候存在思维盲区，对于像 String 这样的参数可能遗漏 值得用例，我们就可以开发一个小工具对被测函数的输入参数类型基于边界值自动生成边界测试用例，比如 String 类型的参数一定会生成 ，SQL 注入攻击字符串，非英文字符，超长的字符串等，这样就可以系统性地避免开发的盲区。诸如此类的工具还有很多，以后有机会再和大家一一分享。

3 测试即服务（TaaS，Test as a Service）的全局架构

除了以上的内容，其实还有诸如测试报告服务（TRS，Test Report Service）、全局测试配置服务（GRS，Global Registry Service）和用于 API 测试解耦的 Mock 服务（Unified Mock Service），由于篇幅无法一一展开。需要强调是的是，这里谈到的很多服务已经在某些企业内部有了落地实践，并取得了很好地效果。最后，以 Test as a Service 的全局架构图来结束本文。

![开发要不要自己做测试？怎么做？][JQIE-JR6F-AQAJ.jpg]

##### 作者介绍 #####

茹炳晟，eBay 中国研发中心测试基础架构技术主管，先后任职于 HP 软件中国研发中心、阿尔卡特朗讯、Cisco 中国研发中心等公司。

##### 今日荐文 #####

点击下方图片即可阅读

![开发要不要自己做测试？怎么做？][FVBI-2MUF-FN7B.jpg]

那些年，云厂商宕机教会我们的事

茹炳晟老师在极客时间开设了《软件测试 52 讲》专栏，给你系统分享测试工程师的成长心法。他会用通俗易懂的语言，以知其然知其所以然的思路，为你系统梳理软件测试的知识体系，深入讲解自动化测试、性能测试和测试架构设计的核心原理，助你从软件测试的“小工”进阶为“专家”。

订阅福利

福利一：限时优惠¥68 元，原价¥99（ 7 月 7 日恢复原价）

福利二：每邀请一位好友购买，你可获得 24 元现金返现，多邀多得，上不封顶，可立即提现（提现流程：极客时间公众号 - 我的 - 现金奖励提现）

如何订阅？

安卓用户点击下图，微信支付，即可订阅

苹果用户扫描图中二维码或点击**【阅读原文】**，试读或订阅此专栏


[YQMZ-UF7V-RBEF.jpg]: static/resources/crawler/YQMZ-UF7V-RBEF.jpg
[QANY-NA3Q-EBQB.jpg]: static/resources/crawler/QANY-NA3Q-EBQB.jpg
[FJIB-AFUE-NANZ.jpg]: static/resources/crawler/FJIB-AFUE-NANZ.jpg
[JQIE-JR6F-AQAJ.jpg]: static/resources/crawler/JQIE-JR6F-AQAJ.jpg
[FVBI-2MUF-FN7B.jpg]: static/resources/crawler/FVBI-2MUF-FN7B.jpg
 *  **原文作者：** InfoQ
 *  **原文链接：** https://www.toutiao.com/item/6573490751190073860/
 *  **版权声明：** 本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 4.0][] 许可协议。转载请注明出处。
