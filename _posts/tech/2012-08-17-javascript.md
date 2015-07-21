---
layout:     post
categories: "tech"
title:      "JavaScript学习笔记"
subtitle:   "JavaScript"
author:     "Charles"
---

>永远不要相信JavaScript，只有服务器端才是可靠的！

对于JavaScript并没有任何好感，对于上面那句话我一直觉得非常正确。以JavaScript最常见的表单验证功能为例，任何一个客户端JavaScript验证后的表单，势必在服务器端进行重新验证。否则只要在客户端浏览器关闭js，就瞎眼了。

可是随着WEB2.0的兴起，更多的服务器和浏览器交互，为了减轻服务器的负担，势必将一些工作交给浏览器来执行。而JavaScript在XML的配合下延伸出来的AJAX在交互上给用户带来了无与伦比的体验。而客户体验恰恰是WEB2.0最为重要的一个特征。使得浏览器WEB应用开发逐渐兴起，越来越像桌面WEB应用程序。

对应JavaScript，由网景开发，原先叫LiveScript这些狗屁历史不多做介绍。主要通过几个关键词理解JavaScript。

###  1、JavaScript  !=  Java + Script
JavaScript与Java没有毛线关系，有人用Carpet和Car来形容两者之间的关系。唯一沾上边的应该就是两者都有关于对象的概念，不过Java是真正面向对象的开发语言，而JavaScript顶多算是基于对象和事件驱动的脚本语言。

###  2、弱类型变量语言
JavaScript在变量声明中采用的是若变量的规则，变量在使用前并不知道类型。一律用var表示。甚至类与函数在定义的时候也都是var，无法区分，只有在使用的时候才知道。甚至变量不定义都可以直接使用(不推荐)。

###  3、闭包Closure

###  4、基于原型Prototyoe的面向对象
JavaScript并没有真正意义上的类的概念，类与函数都是通过function来定义的。

###  5、区分大小写 

###  6、函数的调用与引用
var one = excute();表示获取excute这个函数执行的结果（返回值）;

var two = execute;表示获取execute的地址给two，是对函数的一个引用。

###  7、同名覆盖规则
一般理解JavaScript是一种解释型的语言，因此函数可以在定义前使用。甚至当出现两个重名函数时候，调用的是后一个函数。
{% highlight javascript %}
function a(){ 
    alert("1"); 
} 
a(); 
function a(){ 
    alert("2"); 
}
{% endhighlight %}

上面那段代码，一般都会理解成应该显示2。不过结果测试，发现只有在IE中是显示的2。Opera、FireFox、Chrome都会显示1。可能是各个浏览器对这个同名覆盖的优化吧。

###  8、传参机制(重载的实现)
JavaScript中函数的参数个数不是在定义的时候确定的，而是在访问函数的时候根据传递参数的个数确定的。还是以上面那段函数为例子。
{% highlight javascript %}
function a(a){ 
    alert("1"); 
}

function a(a,b){ 
    alert("2"); 
}

a(1);
{% endhighlight %}

按照Java中Overlode重载的定义，应该去寻找参数类型和个数一样的函数，也就是显示1。不过实际显示的是2。也就是JavaScript忽略了参数的个数。

其实JavaScript的参数传递有点类似Java中的main函数，默认就只有一个参数，arguments数组。并且是隐式的传递，并不需要显示的声明。我们在函数中可以通过arguments[i]去调用传递的参数。

而根据这个传递参数的个数不同，我们也可以实现一定意义上的方法重载，只是都放在一个函数中。如下
{% highlight javascript %}
function a(){ 
    // 获取参数个数 
    var argNum = a.arguments.length; 
    if(0==argNum){ 
        // 无参函数定义 
        alert("0"); 
    }else if(1==argNum){ 
        // 1参数函数定义 
        alert("1"); 
    }else { 
        // 多参数函数定义 
        alert(">1"); 
    } 
} 
a(); 
a(1); 
a(1,2);
{% endhighlight %}
    