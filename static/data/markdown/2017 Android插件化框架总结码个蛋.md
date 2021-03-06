---
title: 2017 Android插件化框架总结
date: 2017-09-15 07:50:39
categories: "开发"
tags:
	- 脚本语言
	- 软件
	- 大众点评
	- 360手机助手
	- iOS

---

作者博客

http://www.jianshu.com/u/11f495898891

文章目录

 *  引言
 *  发展历史
 *  基础
 *  类库
 *  主流框架
    
      
    

0

引言

先简单介绍一下Android插件化。很早之前已经有公司在研究这项技术，淘宝做得比较早，但淘宝的这项技术一直是保密的。直到2015年才陆续出现很多框架，Android插件化分成很多技术流派，实现的方式都不太一样。

1

发展历史

首先，要记住2012年这个时间点。2012年的时候，就有人做插件化技术，是大众点评的屠毅敏，他推出了AndroidDynamicLoader框架，用Fragment来实现。大众点评是国内做App比较早的公司，他们积累了很多的经验，尤其是插件化技术 。通过动态加载不同的Fragement，把想换的页面都换掉。我们也是在这个项目中第一次看到了如何通过addAssetPath来读取插件中的资源。

2013年，出现了23Code。23Code提供了一个壳，在这个壳里可以动态下载插件，然后动态运行。可以在壳外编写各种各样的控件，放在这个框架下去运行。这就是Android插件化技术。这个项目的作者和开源地址，目前不是很清楚。

2014年初，大家也许看过一个视频，阿里一位员工做了一次技术分享，专门讲淘宝的Altas技术，以及这项技术的大方向。但是很多技术细节没有分享。

然后是任玉刚的里程碑式的项目。2014年底，玉刚发布了一个Android插件化项目，起名为dynamic-load-apk，这跟后续介绍的很多插件化项目都不太一样。它没有Hook太多的系统底层方法，而是从上层，即App应用层解决问题，创建一个继承自Activity的ProxyActivity类，然后让插件中的所有Activity都继承自ProxyActivity，并重写Activity所有的方法。之所以说这个项目是里程碑式的，是因为在2015年之前业界没有太多资料可以参考。

2015年4月，一个新框架推出来，叫OpenAltas，后来改名为ACDD。这个框架参考了淘宝App的很多经验，主要就是Hook的思想，同时，还首次提出来通过扩展AAPT来解决插件与宿主的资源id冲突的问题。

2015年8月，张勇发布DroidPlugin。这是Android插件化中第二个里程碑式的项目，这个项目太牛了，能把任意的App都加载到宿主里。可以基于这个框架写一个宿主App，然后就可以把别人写的App都当作插件来加载。这个框架的功能的确很强大，但强大的代价就是要改写很多Android系统的底层代码，更别提这哥们还比较懒，没有制订任何说明文档，导致技术人员掌握这个框架不太容易。

再之后就是百花齐放的时代了，GitHub上有很多插件化框架，但这些框架影响都不大，我们这里就略过了。

接下来登场的是热修复技术。2015年5月，iOS推出了JSPatch，JSPatch通过Runtime的机制，能迅速修复线上App任何一个类的任何一个方法。而当时的Android系统没有能迅速替换的方式。于是，在2015年9月，有人找到了实现迅速替换的途径，就是Andfix，后面会讲它的原理。

2015年10月，大众点评的贾吉鑫做了一个项目，起名为Nuwa（女娲），主要思路跟Andfix差不多，都是解决Android的修复问题，能修复线上的任何一个方法。可惜后来没有继续维护。

2015年底，仍然是Android插件化框架，福建的林广亮提出了一个新机制——Small框架，这个机制不太一样的地方就是，通过脚本的方式来解决资源冲突的问题。

2015 年 8 月，DroidPlugin 是 360 手机助手实现的一种插件化框架，它可以直接运行第三方的独立 APK 文件，完全不需要对 APK 进行修改或安装。一种新的插件机制，一种免安装的运行机制，是一个沙箱（但是不完全的沙箱。就是对于使用者来说，并不知道他会把 apk 怎么样）， 是模块化的基础。

2017年 6 月 ，VirtualAPK 是滴滴开源的一套插件化框架，支持几乎所有的 Android 特性，四大组件方面。

2017 年 7 月，RePlugin是一套完整的、稳定的、适合全面使用的，占坑类插件化方案，由360手机卫士的RePlugin Team研发，也是业内首个提出”全面插件化“（全面特性、全面兼容、全面使用）的方案。

2

基础

![2017 Android插件化框架总结][2017 Android]

介绍完Android插件化的历史，接下来讲一讲Android插件化需要的Android系统底层知识。在座的基本都是做Android开发出身，或许有一半到三分之一是资深的，还有的只做了一两年，希望对插件化有更深的认识。要想完全明白插件化技术，首先需要了解Android系统的底层实现。

首先，做Android系统原代码的人应该非常熟悉Binder，如果没有它真的寸步难行。Binder涉及两层技术。你可以认为它是一个中介者模式，在客户端和服务器端之间，Binder就起到中介的作用，这是我这段时间对Binder的思考。要实现四大组件的插件化，就需要在Binder上做修改。Binder服务端的内容没办法修改，只能改客户端的代码。四大组件每个组件的客户端都不太一样，这个需要大家自己去发现，时间关系，这里就不多说了。

学习Binder的最好方式就是AIDL。你可以读到很多关于AIDL的资料，通过制订一个aidl文件自动生成一个Java类，研究一下这个Java类的每个方法和变量，然后再反过来看四大组件，其实都是跟AIDL差不多的方式。

其次，是App打包的流程。代码写完了，执行一次打包操作，中途经历了资源打包、dex生成、签名等过程。其中最重要的就是资源的打包，即AAPT这一步，如果宿主和插件的资源id冲突，一种解决办法就是在这里做修改。

第三，App在手机上的安装流程也很重要。熟悉安装流程不仅对插件化有帮助，在遇到安装bug的时候也非常重要。手机安装App的时候，经常会有下载异常，提示资源包不能解析，这时需要知道安装App的这段代码在什么地方，这只是第一步。第二步需要知道，App下载到本地后，具体要做哪些事情。手机有些目录不能访问，App下载到本地之后，放到哪个目录下，然后会生成哪些文件。插件化有个增量更新的概念，如何下载一个增量包，从本地具体哪个位置取出一个包，这个包的具体命名规则是什么，等等。这些细节都必须要清楚明白。

第四，是App的启动流程。Activity启动有几种方式？一种是写一个startActivity，第二种是点击手机App，通过手机系统里的Launcher机制，启动App里默认的Activity。通常，App开发人员喜闻乐见的方式是第二种。那么第一种方式的启动原理是什么呢？另外，启动的时候，main函数在哪里？这个main函数的位置很重要，我们可以对它所在的类做修改，从而实现插件化。

第五点更重要，做Android插件化需要控制两个地方。首先是插件Dex的加载，如何把插件Dex中的类加载到内存？另外是资源加载的问题。插件可能是apk也可能是so格式，不管哪一种，都不会生成R.id，从而没办法使用。这个问题有好几种解决方案。一种是是重写Context的getAsset、getResource之类的方法，偷换概念，让插件读取插件里的资源，但缺点就是宿主和插件的资源id会冲突，需要重写AAPT。另一种是重写AMS中保存的插件列表，从而让宿主和插件分别去加载各自的资源而不会冲突。第三种方法，就是打包后，执行一个脚本，修改生成包中资源id。

第六点，在实施插件化后，如何解决不同插件的开发人员的工作区问题。比如，插件1和插件2，需要分别下载哪些代码，如何独立运行？就像机票和火车票，如何只运行自己的插件，而不运行别人的插件？这是协同工作的问题。火车票和机票，这两个Android团队的各自工作区是不一样的，这时候就要用到Gradle脚本了，每个项目分别有各自的仓库，有各自不同的打包脚本，只需要把自己的插件跟宿主项目一起打包运行起来，而不用引入其他插件，还有更厉害的是，也可以把自己的插件当作一个App来打包并运行。

上面介绍了插件化的入门知识，一共六点，每一点都需要花大量时间去理解。否则，在面对插件化项目的时候，很多地方你会一头雾水。而只要理解了这六点核心，一切可迎刃而解。

3

类库

1.  DroidPlugin是360手机助手在Android系统上实现了一种新的插件机制
    
      
    
2.  Android-Plugin-Framework此项目是Android插件开发框架完整源码及示例。用来通过动态加载的方式在宿主程序中运行插件APK。
    
      
    
3.  Small世界那么大，组件那么小。Small，做最轻巧的跨平台插件化框架。里面有很详细的文档
    
      
    
4.  dynamic-load-apkAndroid 使用动态加载框架DL进行插件化开发
    
      
    
5.  AndroidDynamicLoaderAndroid 动态加载框架，他不是用代理 Activity 的方式实现而是用 Fragment 以及 Schema 的方式实现
    
      
    
6.  DynamicAPK实现Android App多apk插件化和动态加载，支持资源分包和热修复.携程App的插件化和动态加载框架.
    
      
    
7.  ACDD
    
    非代理Android动态部署框架
8.  android-pluginmgr
    
    不需要插件规范的apk动态加载框架。
9.  VirtualAPK
    
    VirtualAPK是滴滴出行自研的一款优秀的插件化框架。
10. android-pluginmgr
    
    不需要插件规范的apk动态加载框架。
11. RePluginRePlugin是一套完整的、稳定的、适合全面使用的，占坑类插件化方案，由360手机卫士的RePlugin Team研发，也是业内首个提出”全面插件化“（全面特性、全面兼容、全面使用）的方案。

![2017 Android插件化框架总结][2017 Android 1]

4

主流框架

在 Android 中实现插件化框架，需要解决的问题主要如下：

 *  资源和代码的加载
    
      
    
 *  Android 生命周期的管理和组件的注册
    
      
    
 *  宿主 APK 和插件 APK 资源引用的冲突解决

下面分析几个目前主流的开源框架，看看每个框架具体实现思路和优缺点。

**DL 动态加载框架 ( 2014 年底)**

https://github.com/singwhatiwanna/dynamic-load-apk

DL支持的功能

1、plugin无需安装即可由宿主调起。

2、支持用R访问plugin资源

3、plugin支持Activity和

FragmentActivity（未来还将支持其他组件）

4、基本无反射调用

5、插件安装后仍可独立运行从而便于调试

6、支持3种plugin对host的调用模式：

（1）无调用（但仍然可以用反射调用）。

（2）部分调用，host可公开部分接口供plugin调用。 这前两种模式适用于plugin开发者无法获得host代码的情况。

（3）完全调用，plugin可以完全调用host内容。这种模式适用于plugin开发者能获得host代码的情况。

7、只需引入DL的一个jar包即可高效开发插

件，DL的工作过程对开发者完全透明

8、支持android2.x版本

DL框架原理

动态加载主要有两个需要解决的复杂问题：资源的访问和activity生命周期的管理，除此之外，还有很多坑爹的小问题，而DL框架很好地解决了这些问题。需要说明的一点是，我们不可能调起任何一个未安装的apk，这在技术上是很难实现的，我们调起的apk必须受某种规范的约束，只有在这种约束下开发的apk，我们才能将其调起。

**DroidPlugin ( 2015 年 8 月)**

https://github.com/DroidPluginTeam/DroidPlugin

DroidPlugin 是 360 手机助手实现的一种插件化框架，它可以直接运行第三方的独立 APK 文件，完全不需要对 APK 进行修改或安装。一种新的插件机制，一种免安装的运行机制，是一个沙箱（但是不完全的沙箱。就是对于使用者来说，并不知道他会把 apk 怎么样）， 是模块化的基础。

DroidPlugin 插件机制 :它可以在无需安装、修改的情况下运行APK文件,此机制对改进大型APP的架构，实现多团队协作开发具有一定的好处。

**定义：**

HOST程序：插件的宿主。

插件：免安装运行的APK

**限制和缺陷:**

无法在插件中发送具有自定义资源的Notification，例如：

a. 带自定义RemoteLayout的Notification

b. 图标通过R.drawable.XXX指定的通知（插件系统会自动将其转化为Bitmap）

无法在插件中注册一些具有特殊Intent Filter的Service、Activity、BroadcastReceiver、ContentProvider等组件以供Android系统、已经安装的其他APP调用。

缺乏对Native层的Hook，对某些带native代码的apk支持不好，可能无法运行。比如一部分游戏无法当作插件运行。

**特点：**

1.  支持Androd 2.3以上系统
2.  插件APK完全不需做任何修改，可以独立安装运行、也可以做插件运行。要以插件模式运行某个APK，你无需重新编译、无需知道其源码。
3.  插件的四大组件完全不需要在Host程序中注册，支持Service、Activity、BroadcastReceiver、ContentProvider四大组件
4.  插件之间、Host程序与插件之间会互相认为对方已经"安装"在系统上了。
5.  API低侵入性：极少的API。HOST程序只是需要一行代码即可集成Droid Plugin
6.  超强隔离：插件之间、插件与Host之间完全的代码级别的隔离：不能互相调用对方的代码。通讯只能使用Android系统级别的通讯方法。
7.  支持所有系统API
8.  资源完全隔离：插件之间、与Host之间实现了资源完全隔离，不会出现资源窜用的情况。
9.  实现了进程管理，插件的空进程会被及时回收，占用内存低。
10. 插件的静态广播会被当作动态处理，如果插件没有运行（即没有插件进程运行），其静态广播也永远不会被触发。
    
      
    

**Small ( 2015 年底)**

https://github.com/wequick/Small

Small 是一种实现轻巧的跨平台插件化框架，基于“轻量、透明、极小化、跨平台”的理念

![2017 Android插件化框架总结][2017 Android 2]

**优点如下：**

所有插件支持内置宿主包中。

2.插件的编码和资源文件的使用与普通开发应用没有差别。

3.通过设定 URI ，宿主以及 Native 应用插件，Web 插件，在线网页等能够方便进行通信。

4.支持 Android 、 iOS 、和 Html5 ，三者可以通过同一套 Javascript 接口实现通信。

**缺点如下：**

暂不支持 Service 的动态注册，不过这个可以通过将 Service 预先注册在宿主的 AndroidManifest.xml 文件中进行规避，因为 Service 的更新频率通常非常低。

**VirtualAPK (2017年 6 月 )**

https://github.com/didi/VirtualAPK

VirtualAPK 是滴滴开源的一套插件化框架，支持几乎所有的 Android 特性，四大组件方面。

**原理：**

VirtualAPK 对插件没有额外的约束，原生的 apk 即可作为插件。插件工程编译生成 apk后，即可通过宿主 App 加载，每个插件 apk 被加载后，都会在宿主中创建一个单独的 LoadedPlugin 对象。如下图所示，通过这些 LoadedPlugin 对象，VirtualAPK 就可以管理插件并赋予插件新的意义，使其可以像手机中安装过的 App 一样运行。

 *  合并宿主和插件的ClassLoader 需要注意的是，插件中的类不可以和宿主重复
    
      
    
 *  合并插件和宿主的资源 重设插件资源的 packageId，将插件资源和宿主资源合并
    
      
    
 *  去除插件包对宿主的引用 构建时通过 Gradle 插件去除插件对宿主的代码以及资源的引用

**特性如下：**

四大组件均不需要在宿主manifest中预注册，每个组件都有完整的生命周期。

1.Activity：支持显示和隐式调用，支持Activity的theme和LaunchMode，支持透明主题；

2.Service：支持显示和隐式调用，支持Service的start、stop、bind和unbind，并支持跨进程bind插件中的Service；

3.Receiver：支持静态注册和动态注册的Receiver；

4.ContentProvider：支持provider的所有操作，包括CRUD和call方法等，支持跨进程访问插件中的Provider。

5.自定义View：支持自定义 View，支持自定义属性和style，支持动画；

6.PendingIntent：支持PendingIntent以及和其相关的Alarm、Notification和AppWidget；

7.支持插件Application以及插件manifest中的meta-data；

8.支持插件中的so。

**优秀的兼容性**

 *  兼容市面上几乎所有的Android手机，这一点已经在滴滴出行客户端中得到验证。
    
      
    
 *  资源方面适配小米、Vivo、Nubia 等，对未知机型采用自适应适配方案。
    
      
    
 *  极少的 Binder Hook，目前仅仅 hook了两个Binder：AMS和IContentProvider，hook 过程做了充分的兼容性适配。
    
      
    
 *  插件运行逻辑和宿主隔离，确保框架的任何问题都不会影响宿主的正常运行。

**RePlugin (2017 年 7 月)**

https://github.com/Qihoo360/RePlugin

RePlugin是一套完整的、稳定的、适合全面使用的，占坑类插件化方案，由360手机卫士的RePlugin Team研发，也是业内首个提出”全面插件化“（全面特性、全面兼容、全面使用）的方案。

**其主要优势有：**

 *  极其灵活：主程序无需升级（无需在Manifest中预埋组件），即可支持新增的四大组件，甚至全新的插件
    
      
    
 *  非常稳定：Hook点仅有一处（ClassLoader），无任何Binder Hook！如此可做到其崩溃率仅为“万分之一”，并完美兼容市面上近乎所有的Android ROM
    
      
    
 *  特性丰富：支持近乎所有在“单品”开发时的特性。包括静态Receiver、Task-Affinity坑位、自定义Theme、进程坑位、AppCompat、DataBinding等
    
      
    
 *  易于集成：无论插件还是主程序，只需“数行”就能完成接入
    
      
    
 *  管理成熟：拥有成熟稳定的“插件管理方案”，支持插件安装、升级、卸载、版本管理，甚至包括进程通讯、协议版本、安全校验等
    
      
    
 *  数亿支撑：有360手机卫士庞大的数亿用户做支撑，三年多的残酷验证，确保App用到的方案是最稳定、最适合使用的

截止2017年6月底，RePlugin的：

![2017 Android插件化框架总结][2017 Android 3]

目前360公司几乎所有的亿级用户量的APP，以及多款主流第三方APP，都采用了RePlugin方案。

**特性**

![2017 Android插件化框架总结][2017 Android 4]

**参考文章**

APK动态加载框架（DL）解析

Android插件化从入门到放弃-最强合集

包建强的无线技术空间，写给Android App 开发人员看的 Android 底层知识 置顶8篇

有关Android插件化思考

Android插件化原理解析

Android插件化：从入门到放弃

Android博客周刊专题之-插件化开发

干货推荐

![2017 Android插件化框架总结][2017 Android 5]

点赞与转发就是对我最大的支持！


[2017 Android]: static/resources/crawler/FIAI-F2NR-YBNE.jpg
[2017 Android 1]: static/resources/crawler/2UQV-IVUB-UVAR.jpg
[2017 Android 2]: static/resources/crawler/A73Y-63QB-EEQN.jpg
[2017 Android 3]: static/resources/crawler/UFAN-J3YQ-FM6R.jpg
[2017 Android 4]: static/resources/crawler/VJJU-QVUF-MNIF.jpg
[2017 Android 5]: static/resources/crawler/RVQJ-IZIE-FRAR.jpg
 *  **原文作者：** 码个蛋
 *  **原文链接：** https://www.toutiao.com/item/6465785679203795470/
 *  **版权声明：** 本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 4.0][] 许可协议。转载请注明出处。
