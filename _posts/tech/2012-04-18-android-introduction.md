---
layout:     post
category:   "tech"
title:      "Android学习笔记-入门简介"
subtitle:   "Android Introduction"
date:       2012-04-18 03:03
author:     "Charles"
header-img: "img/post-bg-01.jpg"
---

<p>&#160;&#160;&#160; 2010年的时候跟着SJ一起做过一次Android的比赛，做一个小的英语单词学习软件，很抱歉让SJ失望了，不过那也是我第一次接触Android。然后就一直搁下了，想想也是后悔，那时候的Android已经能望见它以后的红火，当时如果坚持学习Android了下来，那么现在对Android应该已经非常精通了。有好的眼光，也需要有坚持不懈的精神。貌似自己还缺点耐心。如今马上就要面临毕业找工作了。开始重新拾起Android。</p>  <p>&#160;&#160;&#160; 当时的SDK1.6，已经发展到了SDK4.0.3。好吧，把笔记记载在博客上，也当是督促自己吧。</p>  <p>&#160;&#160;&#160; 要开发Android项目首先需要一个IDE，虽然记事本也能编写项目，可效率毕竟不高。Eclipse就是当前最好用的一款IDE工具。</p>  <p>&#160;&#160;&#160; 首先安装SDK，在Android官网<a href="http://developer.android.com/sdk/index.html">http://developer.android.com/sdk/index.html</a>下载对应操作系统的SDK，然后按步骤安装，其实安装的是一个SDK Manager。然后将SDK安装路径中的tools文件夹路径加到path环境变量中。注意SDK中下载platform时间比较慢，我只下了4.0.3就总共有700M+。如果有现成的话，直接复制过来更好。</p>  <p>&#160;&#160;&#160; 然后安装Eclipse中的Android开发插件ADT，安装步骤在这里<a href="http://developer.android.com/sdk/eclipse-adt.html">http://developer.android.com/sdk/eclipse-adt.html</a></p>  <p>&#160;&#160;&#160; 完成以上操作就可以试着新建一个Android项目试试手了。修建的项目中src目录用于存放java源代码；gen目录用于存放自动生成的配置文件以及资源管理文件，如R.java里面就有所有包括图片之类的资源的配置信息；bin目录为生成的可安装文件；assets和res都是资源包，后者中所有的内容都会在R.java中配置；AndroidManifest.xml是整个项目的配置文件，里面声明了诸如项目图标、名称、默认Activity、最低版本等信息。</p>  <p>&#160;&#160;&#160; Android中有四个最重要的部分组成，分别是</p>  <ul>   <li>Activity 用于显示界面</li>    <li>Intent 用于界面之间传输数据</li>    <li>Service 用于处理数据</li>    <li>Content Provider 用于提供数据</li> </ul>