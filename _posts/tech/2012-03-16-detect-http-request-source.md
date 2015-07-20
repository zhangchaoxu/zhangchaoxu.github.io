---
layout:     post
categories: "tech"
title:      "服务器判断HTTP请求来源"
subtitle:   "detect-http-request-source"
date:       2012-03-16 08:24
author:     "Charles"
---

根据上一篇文章[HTTP请求模型]({{ site.url }}/tech/2012/03/16/http-request.html),我们知道在HTTP请求的消息头中包含了大量信息。
而在服务器端，我们可以通过这些信息，判断出客户端的许多信息，比如请求来自PC还是Mobile、客户端的操作系统、客户端的浏览器等。

## 1.判断HTTP请求来自PC还是Mobile

项目需求：交大wap主页，wap.bjtu.edu.cn需要同时支持PC和Mobile，当PC访问时，跳转到HTML页面；
当Mobile访问时，跳转到WAP1.2的WML或者WAP2.0的xHTML MP页面。

首先想到通过访问IP做判断，这个当手机等通过wap或者GPRS访问时没有问题，可当通过wifi访问时候，手机也可得到一个独立的IP，因此放弃。

其次利用HTTP消息头中的Accept来判断是否支持wml，支持则判定为Mobile，不支持则判定为PC。Java代码如下，但是问题又出现了，当前许多PC浏览器也支持WML，如Opera；
也有许多手机浏览器，如UC，也支持HTML。因此该方法也不可采用。

{% highlight java %}
String acceptHeader = request.getHeader("accept"); // 获取accept信息 
if (acceptHeader.indexOf("application/vnd.wap.xhtml+xml") != -1) // 支持WML 
    response.setContentType("application/vnd.wap.xhtml+xml"); 
else if (acceptHeader.indexOf("application/xhtml+xml") != -1) // 支持xHTML 
     response.setContentType("application/xhtml+xml"); 
else // 其他 
     response.setContentType("text/html");
{% endhighlight %}
 
最后采用判断HTTP消息头中的USER-AGENT来判断是否含有手机信息。
{% highlight java %}
String userAgent = request.getHeader("User-Agent");   // 获取User-Agent信息

if (userAgent.indexOf("Noki") > -1 || // Nokia phones and emulators 
    userAgent.indexOf("Eric") > -1 || // Ericsson WAP phones and emulators 
    userAgent.indexOf("WapI") > -1 || // Ericsson WapIDE 2.0 
    userAgent.indexOf("MC21") > -1 || // Ericsson MC218 
    userAgent.indexOf("AUR") > -1  || // Ericsson R320 
    userAgent.indexOf("R380") > -1 || // Ericsson R380 
    userAgent.indexOf("UP.B") > -1 || // UP.Browser 
    userAgent.indexOf("WinW") > -1 || // WinWAP browser 
    userAgent.indexOf("UPG1") > -1 || // UP.SDK 4.0 
    userAgent.indexOf("upsi") > -1 || //another kind of UP.Browser 
    userAgent.indexOf("QWAP") > -1 || // unknown QWAPPER browser 
    userAgent.indexOf("Jigs") > -1 || // unknown JigSaw browser 
    userAgent.indexOf("Java") > -1 || // unknown Java based browser 
    userAgent.indexOf("Alca") > -1 || // unknown Alcatel-BE3 browser (UP based) 
    userAgent.indexOf("MITS") > -1 || // unknown Mitsubishi browser 
    userAgent.indexOf("MOT-") > -1 || // unknown browser (UP based) 
    userAgent.indexOf("My S") > -1 ||//  unknown Ericsson devkit browser  
    userAgent.indexOf("WAPJ") > -1 ||//Virtual WAPJAG www.wapjag.de 
    userAgent.indexOf("fetc") > -1 ||//fetchpage.cgi Perl script from www.wapcab.de 
    userAgent.indexOf("ALAV") > -1 || //yet another unknown UP based browser 
    userAgent.indexOf("Wapa") > -1 || //another unknown browser (Web based "Wapalyzer") 
    userAgent.indexOf("Oper") > -1)
    
    System.out.println("Request is From Mobile"); // 请求来自Mobile
else
    System.out.println("Request is From PC"); //请求来自PC
{% endhighlight %}

虽然这样做存在的问题也很明显，一是无法穷举所有的手机品牌，二是[如何伪造User-Agent信息](http://www.path8.net/tn/archives/1760)。
但这也是当前最为可行的判断HTTP请求来自PC还是Moblie的一种方法了。

## 2.判断HTTP请求来源浏览器

在上方中可以看到USER-AGENT也包含了浏览器信息，如IE浏览器看到的是MSIE、Opera显示的是Opera、Chrome显示的是Chrome。应该可以通过和上面相同的办法来判断。
也可以通过[js、css、html判断浏览器的各种版本](http://www.jb51.net/web/42244.html)。