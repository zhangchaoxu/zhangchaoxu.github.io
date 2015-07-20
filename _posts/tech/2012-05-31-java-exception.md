---
layout:     post
categories: "tech"
title:      "Java的异常处理"
subtitle:   "Java Exception"
date:       2012-05-31 07:36
author:     "Charles"
---

<p>&#160;&#160;&#160; 下半年马上就要开始找工作毕业了。准备开始收拾一下以前的学习笔记，一些基础知识，来应付面试和笔试中可以遇见的各种问题。Ask &amp; Answer，就叫2A系列吧。</p>  <p>/************************************************/</p>  <p>&#160;&#160;&#160; 第一个是JAVA的异常处理。JAVA中的异常都是从Throwable父类中继承而来。Throwable父类有两个直接子类。分别是Error和Exception。</p>  <p>&#160;&#160;&#160; 其中Error应该是JVM在运行过程中发生的严重错误，因此也不应该由程序员去捕捉处理，可以忽视。</p>  <p>&#160;&#160;&#160; 另外一个就是Exception，就是我们常说的异常类。其子类定义了各种各样可能出现的问题，一般需要用户显示的声明与捕获。</p>  <p>&#160;&#160;&#160; 而Exception有许多子异常类，其中比较特别的是RuntimeException，指的是运行时错误。RuntimeException，可处理，也可不处理。不处理，发生错误时，直接抛出。这是一种JAVA类库内置的语义检查。例如数组下标越界,会引发IndexOutOfBoundsException;访问null的对象时会引发NullPointerException。</p>  <p>&#160;&#160;&#160; 而其他的就属于必须处理的异常，如数据转换异常DataFormatException、IO异常IOException等。</p>