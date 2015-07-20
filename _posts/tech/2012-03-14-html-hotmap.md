---
layout:     post
category:   "tech"
title:      "HTML页面图片指定位置链接--MAP热点地图标签的使用"
subtitle:   "Html Hotmap"
date:       2012-03-14 01:28
author:     "Charles"
---

在页面中我们经常能看见点击一张图片的不同位置，可以指向不同的链接。
如在一张中国地图中，点击不同的省市位置，链接向不同的页面

这种情况，最简单的便捷的解决方法就是利用HTML语言中的MAP标签。W3School中关于[MAP](http://www.w3school.com.cn/tags/tag_map.asp)标签介绍，MAP标签的热点形状有rect矩形、circle圆形、poly多边形三种。
我们使用Macromedia打开一个含有图片的页面。
然后在设计界面中选中图片，就可以在属性中选择MAP的形状了。
如下图所示，新疆、西藏、青海分别使用了矩形、圆形和多边形。

![htmlhotmap](/img/htmlhotmap.png)

然后切换到代码视图，我们就可以看到上方操作对应的代码。

{% highlight html %}
<img src="http://www.china-holiday.com/english/chinamap/chinamap.jpg" alt="中国地图" border="0" usemap="#Map" />
 <map name="Map" id="Map">
 <area shape="rect" coords="88,121,158,174" href="#" />
 <area shape="circle" coords="105,265,31" href="#" />
 <area shape="poly" coords="149,189,161,185,170,184,179,185,188,187,196,192,200,196,206,194,205,188,209,189,213,192,222,193,228,199,234,199,241,208,247,214,252,224,251,238,244,250,239,263,233,274,225,269,215,264,207,264,206,273,199,276,195,278,185,278,178,271,169,265,156,261,147,252,140,248,135,240,136,225,147,218,150,214,153,203,153,198" href="#" /></map>
{% endhighlight %}

可以看到，首先需要对图片指定usemap对应的MAP名称。
然后在MAP标签中指定三个形状,以及三个热点对应的区域。
区域是通过coords坐标来对应的。

每一张图片都是由像素构成的，图片的左上角对应的坐标是（0，0）。
一个像素对应的是一个坐标刻度。

其中rect矩形的coords对应格式是`coords="x1,y1,x2,y2"`，（x1，y1）对应的是矩形左上角坐标，（x2，y2）对应的是矩形右下角坐标。
circle圆形的coords对应格式是`coords="x,y,r"`，（x，y）对应圆心坐标，r表示圆形的半径。
poly多边形的coords对应格式是`coords="x1,y1,x2,y2,x3,y3……"`。
多边形是由众多点组成的，其中的（xi，yi）表示的就是第i个点的坐标位置，多边形至少需要三个点构成。