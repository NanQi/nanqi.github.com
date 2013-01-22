---
layout: page
title: "问题"
group: navigation
---
{% include JB/setup %}

这里列出我现在存在的一些问题，尚未解决的，希望某位好心人在看到了可以帮忙解决一下。  

##更新历史：
---

* *2012-11-27* 创建文章，[cygwin中文乱码][1]，[jekyll导航栏排序][2]

##问题列表
---
* [cygwin中文乱码][1]
* [jekyll导航栏排序][2]

[1]: #CygwinCN
[2]: #JekyllNavOrder

<section id="CygwinCN"/>
###cygwin中文乱码
---

话说我的cygwin中文显示有问题，在首次登录系统或注销后登录正常显示，如果过一段时间（具体多长时间也没测试过），运行就是中文乱码。  
所以我一贯的做法都是注销一次，然后登录两个cygwin（登录两个是因为一个需要运行jekyll --server，运行在一个里面是可以，但是一有请求，他就会在当前命令行中生成一大堆东西。我使用eamcs不影响，但是我要是在emacs中运行shell就会有问题，还有，不知道为什么eshell不能运行windows环境的jekyll）。  
似乎说一个问题牵扯到很多问题，但是学习不就是这样，由一个问题引入另一个问题，如此逐步深入。  
反正不是工作，不是任务，喜欢深究也好，浅尝辄止也罢。

<section id="JekyllNavOrder"/>
###jekyll导航栏排序
---

刚开始没有注意这个问题，因为在本地显示是正确的。  
我不知道Jekyll Bootstrap他的导航栏是怎么排序的，但是我感觉和header属性有关。因为我删除了header属性顺序再就不发生变化了。  
比如下面：

    header : Post Archive
    header: Posts By Category
    header: Pages
    header: Posts By Tag

或许这些使用什么规则可以排序吧，但是我不知道怎么用，尝试了在所有地方都`Posts By XXX`但是还是不对。  
并且我在此看不出有什么规律。  

{% include JB/comments %}
