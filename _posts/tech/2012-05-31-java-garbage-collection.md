---
layout:     post
categories: "tech"
title:      "JAVA的内存分配策略和自动垃圾回收机制"
subtitle:   "Java Garbage Collection"
author:     "Charles"
---

JAVA和C++之间有一堵由内存分配和垃圾收集技术所围成的高墙，墙外的人想进来，墙内的人想出来。

对于从事C 和C++ 程序开发的开发人员来说，在内存管理领域，他们既是拥有最高权力的皇帝，又是从事最基础工作的劳动人民——既拥有每一个对象的所有权，又担负着每一个对象生命开始到终结的维护责任。

对于Java 程序员来说，在虚拟机的自动内存管理机制的帮助下，不再需要为每一个new 操作去写配对的delete/free 代码，而且不容易出现内存泄漏和内存溢出问题。看起来由虚拟机管理内存一切都很美好，不过，也正是因为Java 程序员把内存控制的权力交给了Java 虚拟机，一旦出现内存泄漏和溢出方面的问题，如果不了解虚拟机是怎样使用内存的，那排查错误将会成为一项异常艰难的工作。——周志明《深入理解Java虚拟机》

一、内存分配策略
一般内存粗糙的可以分为两块，堆heap空间和栈stack空间。但其实Java内存远比这个复杂，只是堆和栈是最重要的两块。
其中栈，也成为局部变量表，主要存储的是在非static的自动变量、函数参数、表达式的临时结果金额函数返回值。栈是线程私有的，生命周期与线程相同。
而堆heap是内存中最大的一块，为线程共享，JVM启动时创建。主要用于存放new出来的对象以及数组。而JAVA的垃圾回收机制管理的往往也就是这个堆内存，因此也称为GC（Garbage Collection Heap）堆。
此外还有方法区和常量池等内存区域。

二、自动垃圾回收机制
于堆的管理，不同的语言实现方式是不同的。其中C语言是通过库函数malloc()和free()来实现。而C++直接将对堆空间中对象的操作和分配释放到语言层次，使用new和delete语句。
而Java只需要开发人员在需要时候创建就可以了，何时释放都由JVM来控制。而在Java的Object类中有一个finalize()方法，在垃圾回收器真正回收之前调用。
Java的垃圾回收机制最为Java语言的一大特性，将Java堆空间内存的释放交给JVM自动处理，无须开发人员在程序中显示调用，从而避免了因为开发人员忘记释放内存而造成的内存溢出。
垃圾回收器通常是作为一个单独的低级别的线程运行，不可预知的情况下对内存堆中已经死亡的或者长时间没有使用的对象进行清楚和回收，程序员不能实时的调用垃圾回收器对某个对象或所有对象进行垃圾回收。
回收机制有分代复制垃圾回收和标记垃圾回收，增量垃圾回收。
