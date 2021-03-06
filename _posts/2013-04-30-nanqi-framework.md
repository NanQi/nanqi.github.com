---
layout: post
title: "闲话WinFrom与WPF(4)"
subtitle: "结合VS扩展,插件式开发框架"
description: "介绍正在使用的一套插件式开发框架，插件式开发概念很老，但结合了VS扩展功能显得别具一格。"
sourcecode: https://github.com/NanQi/demo/tree/master/NanQi.Project
category: demo
tags: [C#, WinForm]
---
{% include JB/setup %}

当我的[闲话WinFrom与WPF](http://www.cnblogs.com/nanqi/archive/2012/06/16/2551871.html)，还在进行的时候，突然出来介绍插件式开发框架，总觉得又会半途而废，最后偷懒，决定把这一篇定为闲话WinFrom与WPF的框架篇，倒也说的过去，反正还是使用WinForm，也没跑题。

先说说由来。  
也就在去年的5月，我离开了上一家公司来现在的公司继续当一个苦逼程序猿，没有使用过WPF，AIX，Oracle……好多的不会，看到公司的一套WPF系统，感觉很惊讶，之后随着接触项目，这份惊讶也越来越淡，感觉系统也很稀松平常。  
之后和领导一次闲谈时说起管理软件近几年的发展，如我这等只做了两年程序的人都开始大言不惭的谈软件【这几年】的发展，想起都有点可笑。  
当时领导拿公司这个WPF项目举例，说曾经公司一直想做一个自己的IDE工具，好简化开发人员，但是技术有限，而且也大多都是抄开源的SharpDevelop。现在这套框架，就直接使用VS扩展去做，这就是管理软件的一个发展。  

本篇文章不是谈论管理软件的发展，不论领导说的正确与否，以上都属闲话，所以还是到此为止。

##简介

---

插件式开发和VS扩展都不是新技术，扩展开发工具用在项目中我记得早在VC的年代就有很多项目这样做了，最简单的就是写一套模板去开发，而插件式开发几乎所有大型软件都有。  
技术不新，但是插件式开发，结合VS扩展，效果还是蛮不错的。  
我这里做了一个WinForm版的demo，来简单介绍一下。

首先安装项目Tools目录下NanQi.IDE.vsix扩展包，由于对VS扩展不熟，花了我不少时间去弄。  

![安装vsix](/image/framework/framework1.png)

安装好后，可以在工具-扩展管理器和帮助-关于中查看：  

![扩展管理器](/image/framework/framework2.png)

![关于](/image/framework/framework3.png)

打开解决方案，展开Form1和Form2项目，在文件夹上点击右键，会发现多出来一个编译交易的选项。

![编译交易](/image/framework/framework4.png)

每个页面可以说成一个交易，而编译交易就是把当前鼠标选择的文件夹下的页面编译成单独的DLL。  
可以打开NanQi.Project.Host\bin\Debug\Trades查看编译的DLL文件。  

主程序启动，加载菜单树，每个菜单对应一个类的FullName，当点击一个菜单时，程序会找到指定目录下【FullName】.DLL那个文件，然后反射加载、呈现。  

添加一个窗体基本需要以下几步：  

1. 新建一个窗体T\_Test，选择继承窗体，找到指定的Libs文件夹内的NanQi.Framework.Control.dll文件，继承NormalTradeWindow
2. 在项目的Trade.xml文件中增加一条，Key值与窗体类名相同：T\_Test
3. 在项目中增加一个文件夹，文件夹名称与窗体类名相同：T\_Test
4. 把新建的窗体拖到新建的文件夹中
5. 在主程序NanQi.Project.Host的Menu.xml中添加菜单，action必须是新建窗体的FullName
6. 在新建文件夹上点右键，编译交易
7. 运行主程序，点击相应菜单，打开新建的窗体

有人看到这里可能觉得这样做太麻烦了。  
是的，这是因为demo中的vs扩展还没有做新建交易，新建交易项目等一些功能，现在这些都需要手动完成，如果把新建交易的功能添加上，只需要在交易项目上点击右键，选择新建交易，填入交易名称和描述即可完成所有新建任务，然后点击右键编译交易即可完成。  

##优点与缺点

---

优点很明显，框架基本不需要修改，新增页面，也变得简单，如果框架再提供大量的控件，方法去简化开发人员，那么完全可以把写窗体的一些任务交给新人完成，分工很明确。  
页面都是在菜单点击后才加载相应的DLL，稍作改动，就是分模块加载的一个典型例子。  
而且修改页面不需要重启应用程序，程序可以一直启动着，编译好某个页面，重新打开即可看到改动后的效果，对于一些启动复杂的程序，能省下不少时间。  
VS扩展如果再进一步，完全可以让页面开发人员做到传说中的.NET程序猿（只会拖控件），真的只要拖拖控件就可以完成全部任务。（不要觉得不现实，这种东西早就有人实现了，页面开发人员不需要写过多的代码，都是一些简单的if、else判断、赋值与调用方法，根本不需要写循环、Sql语句等。）  

缺点主要一点是由于各个页面在独立的DLL中，无法相互调用、传递数据就比较困难，即使最简单的ShowDialog可能都变得十分麻烦。这时候，可能框架就需要提供一些方法去做这些事情。  
而由于将原本一个项目分为两个，就带来了使用的不方便，每次框架修改完，必须生成相应的DLL，然后放在项目层的Lib下。而调试框架就要使用附加到进程的方式去调试。

##关于demo

---

连带写博客算上，这个demo一共花了近2天时间，可算是付出太多。  
其中包括学习VS扩展和MEF，也算小有收获。  
框架是参考公司现用的结构，不是我的，所以这里只是以demo的形式与大家交流，估计后续也没有再多的时间去继续完善。  
关于WinForm与WPF的话题，我会继续，通过这个demo，也能看到WinForm还是有很大的限制，没有WPF下的路由事件、依赖属性，很多功能都无法实现，就算实现也太过麻烦。  

关于管理软件的发展，很希望有人一起探讨探讨。  
