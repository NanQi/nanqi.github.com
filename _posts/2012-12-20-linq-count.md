---
layout: post
title: "从LINQ的Count方法说起"
description: "从LINQ的Count方法说起"
category: demo
tags: [C#, LINQ]
---
{% include JB/setup %}

##几句闲扯

---

在我学习LINQ时，确实感觉很爽。  
但是时间久了，慢慢也就不那么在意了。但是周围朋友总是记得`我会使用LINQ`编程。  
记得初中时候学几何，有一个已知三角形边长求面积的题，而我正巧知道[海伦公式](http://baike.baidu.com/view/1279.htm)，之后凡是碰到可以使用此公式的题，同学都想起我会做，仿佛那公式应该以我的名字命名一样……  
某人问我有没有学习LINQ的资料，我实在说不出，因为我从来都没有系统的去学过LINQ。我基本只是使用几个IEnumerable<T>的扩展方法，要说学习也只是从某些第X版书中读过几句，平时也就在一个集合点一下然后看看各自说明。  
当然，LINQ不止于此，我也说不出到底LINQ都包含什么，什么是LINQ。  

> 给一个东西，一门技术下定义，从来都不是一件简单的事。  

##事出有因

---

事情是这样的，今天有人问我一个小问题，关于LINQ，然后我不经意间看到一行代码：  

    int count = lst.Where(ch => char.IsNumber(ch)).Count();

代码读起来很简单，就是从一个char集合里找出为数字的个数。  
代码没问题，但是还有个更好的写法：  

    int count = lst.Count(char.IsNumber);

即便他不知道Count方法可以传参，那么他为什么不写成：  

    int count = lst.Where(char.IsNumber).Count();

我相信他根本就不知道这里为什么要写ch => char.IsNumber(ch)，根本就不知道这里需要的是一个方法。  
这让我想起一个男同事说一个女同事（所谓同事，都是程序猿），女的刚毕业，不怎么会，然后男的说女的写代码ToString不带括号。  
这姑且说是这个女同事不知道调用方法即使没有参数也需要带括号，或者说她根本就不知道ToString是一个方法，但是同样也说明这个男同事以为方法只能去调用（call）。  
或许简单下面的代码他会觉得很惊讶：  

    string[] arr = lst.Where(char.IsNumber).Select(char.ToString);

又或者在事件上：  

    delegate string GetNumberDelegate(char ch);
    event GetNumberDelegate GetNumberEvent;
    ...
    this.GetNumberEvent += char.ToString;

##几点思考

---

我想大多数人习惯于使用ch => char.IsNumber(ch)是因为这样感觉很好理解，程序可以`读出来`。是的，写LINQ最爽的一点就是这里了。  
比如说使用Where方法，知道集合是一个char集合，那么ch很自然的可以当做char集合中每个元素，=>之后写下对每个元素的判断，很好理解，用起来很舒服。  
但是切莫执迷于表像而偏离本质。  
说起函数当做参数传递，记起曾经在封装一个日历控件的时候遇到一个问题：需要在已提交报表、未提交报表和还没到的日子分颜色：  

![日历控件](/image/ucCalendar.gif)

但是关于颜色问题，修改了好多次，最后干脆我给封装的控件增加一个Func<string, Color>，根据给定的类型（提交或未提交）去给定颜色。  
最后我要说的是我本来初衷不是写好多人不知道`函数也是一个对象`，不知道函数也可以去传递，但是写一下给写跑题了，干脆就继续写下去。而原本我是想说说几个LINQ扩展方法的先后问题，留在下一篇博客中说吧。  

