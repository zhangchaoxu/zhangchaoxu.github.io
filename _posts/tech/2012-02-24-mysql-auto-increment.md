---
layout:     post
title:      "MySQL中自增字段初始值和偏移量"
subtitle:   "Mysql Auto Increment"
date:       2012-02-24 03:15
author:     "Charles"
header-img: "img/post-bg-01.jpg"
---

MySQL有一个非常好好用的自增字段，将某一列(id号码)设置为主键，并且自增。在使用过程中，只需要插入其他列的数据即可，无须对id做插入。</p>  <p>&#160;&#160;&#160;&#160;&#160; 但是同样也会引起一些问题，比如说，原先有100条数据，我删除后，数据还是从101开始，而不是初始化到1开始。这是由于这个表的状态中存储着一个Auto_increment的值。并且我们可以查看这个值网上称使用select last_insert_id() as ID form tablename limit 1;查看该值，但经本人测试该命令每次得出的都是0。后来找到<a href="http://thebigreason.com/blog/2010/09/08/retrieve-the-auto-increment-value-of-a-mysql-table" target="_blank">Mark Eagleton</a>提供的方法，如下</p>  <blockquote>   <p>SHOW&#160; TABLE STATUS WHERE NAME='tablename';</p>    <p>#或者</p>    <p># SHOW TABLE STATUS LIKE 'tablename';</p> </blockquote>  <p>&#160;&#160;&#160;&#160;&#160; 其中有一个Auto_increment的字段，存储的就是下一次插入时候会产生的自增值。</p>  <p>&#160;&#160;&#160;&#160;&#160; 但是当我们删除或清空表数据以后，希望增值字段重新从1或者某一个值开始自增。就需要执行一下语句</p>  <blockquote>   <p>#最后的数值修改成为希望开始递增的值</p>    <p>ALTER TABLE 'tablename' Auto_increment=1;</p> </blockquote>  <p>&#160;&#160;&#160;&#160;&#160;&#160; 而实际上整个数据库都维护着一个auto_increment_offset和一个auto_increment_increment的变量，用于存储全局默认的自增偏移量和自增初始值。而且我们可以修改。查看和修改方法如下:</p>  <blockquote>   <p>#查看方法</p>    <p>SHOW VARIABLES LIKE 'auto_inc%';</p>    <p>#修改方法</p>    <p>SET auto_increment_offset=5;</p>    <p>SET auto_increment_increment=10;</p></blockquote>