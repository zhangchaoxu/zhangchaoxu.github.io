---
layout:     post
categories: "tech"
title:      "JAVA中的逻辑运算符"
subtitle:   "Java Logic Operate"
date:       2012-05-31 12:23
author:     "Charles"
---

在JAVA中的逻辑运算符主要有逻辑与(&)/逻辑或(|)/逻辑非(!)/逻辑异或(^)短路与(&&)/短路非(||)五种。

* &  逻辑与and   表达式两边都为true，才为true
* |  逻辑或or    表达式两边有一个为true，则为true
* !  逻辑非not   取反
* ^  逻辑异或xor 表达式两边相同则为false，不同则为true
* && 短路与      当第一个为false时候，不再判断第二个。例如，对于if(str != null && !str.equals(“”))表达式，当str为null时，后面的表达式不会执行，所以不会出现NullPointerException异常。If(x==33 & ++y>0) y自增执行；If(x==33 && ++y>0) y自增不执行。
* || 短路或      当第一个为true时，不再判断第二个是否正确。

同时逻辑&和逻辑或|还可以作为位运算符来使用，当表达式两边不是布尔boolean型数据时，则两边按位与或。

* 取一个整数的最低4位。我们可以用该int数，逻辑& 0x0f，由于高4bit是0，按位与都变成0。因此得到的为这个整数的低4位；
* 想要填充某个数字的某几位的话，可以将该数与对应位为1的数字做或运算。