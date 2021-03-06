---
layout:     post
categories: "tech"
title:      "MySQL中自增字段初始值和偏移量"
subtitle:   "Mysql Auto Increment"
tags:       [db]
author:     "Charles"
---

MySQL有一个非常好好用的自增字段，将某一列(id号码)设置为主键，并且自增。
在使用过程中，只需要插入其他列的数据即可，无须对id做插入。
但是同样也会引起一些问题，比如说，原先有100条数据，我删除后，数据还是从101开始，而不是初始化到1开始。
这是由于这个表的状态中存储着一个Auto_increment的值。并且我们可以查看这个值网上称使用`select last_insert_id() as ID form tablename limit 1;`查看该值，但经本人测试该命令每次得出的都是0。
后来找到[Mark Eagleton](http://thebigreason.com/blog/2010/09/08/retrieve-the-auto-increment-value-of-a-mysql-table)提供的方法，如下

* `SHOW TABLE STATUS WHERE NAME='tablename';`

或者

* `SHOW TABLE STATUS LIKE 'tablename';`

其中有一个Auto_increment的字段，存储的就是下一次插入时候会产生的自增值。
但是当我们删除或清空表数据以后，希望增值字段重新从1或者某一个值开始自增。
就需要执行一下语句`ALTER TABLE 'tablename' Auto_increment=1;`最后的数值修改成为希望开始递增的值

而实际上整个数据库都维护着一个auto_increment_offset和一个auto_increment_increment的变量，用于存储全局默认的自增偏移量和自增初始值。
而且我们可以修改。查看和修改方法如下:

* 查看方法`SHOW VARIABLES LIKE 'auto_inc%';`

* 修改方法
`
SET auto_increment_offset=5;
SET auto_increment_increment=10;
`