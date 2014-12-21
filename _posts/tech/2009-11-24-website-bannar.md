---
layout:     post
categories: "tech"
tags:       [web]
title:      "网站banner制作与显示"
subtitle:   "website-bannar"
author:     "Charles"
---

Banner不是banana
原本指的是网站上方的横幅广告
但是我更愿意理解为网站上方的Logo图片
刚才给实验室制作了几个banner
Photoshop只会最简单的去痘痘之类操作
Flash也只是会点皮毛
而学校以及科研单位的网站最大的特点就是要简洁
因此蓝白就成了最大的主题
利用的是阿里妈妈的BannerMaker(没有任何广告成分，此类网站很多，大家尽可以用别的)
这个网站可以生成Flash、jpg和png三种格式的文件
而其中flash的文件必须联网才能显示
因此不需要动态显示的，一般下载为jpg或png格式即可
如果需要动态显示的话，建议用前面动态图片，图片后面用Flash显示的效果
这样的话，即使动态Flash显示出了问题，至少前面的图片还能显示，不至于过于寒酸
而一般建议做一套
然后网站中随机显示其中的一个
代码如下：

` <script language=JavaScript>
           //four banners named bx.jpg display on random
           var pic=Math.floor(Math.random()*4+1);
           document.write("<Img src='images/banner",pic,".jpg' width='760' height='130'>");
     </script>`

* `SHOW TABLE STATUS WHERE NAME='tablename';`

代码很清楚，也很简单，随机产生一个1—4之间的数pic，然后在images文件夹选取长760px，高130px的图片banner+pic.jpg显示，注意根据自己图片的大小、文件名、格式进行修改

![website-bannar-1]({{site.imageurl}}/website-bannar-1.jpg)
![website-bannar-2]({{site.imageurl}}/website-bannar-2.jpg)
![website-bannar-3]({{site.imageurl}}/website-bannar-3.jpg)
![website-bannar-4]({{site.imageurl}}/website-bannar-4.jpg)

