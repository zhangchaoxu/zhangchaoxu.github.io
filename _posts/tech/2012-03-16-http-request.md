---
layout:     post
categories: "tech"
title:      "HTTP请求模型"
subtitle:   "http-request"
author:     "Charles"
---

##　一、HTTP协议
HTTP协议作为TCP/IP协议集中最为重要的一个应用层协议，定义了WEB客户端（浏览器）和WEB服务器之间数据交换的过程以及数据的本身格式。
在HTTP1.0中浏览器每一次网页的访问请求就是一个单独的HTTP请求，处理完请求后自动释放连接。
假如我们访问一个包含多张图片、音乐等多媒体资源的网页，首先返回网页，然后网页中的每一个资源都单独地重新向服务器发起一个资源访问的请求，因此对服务器的资源是一个极大的浪费。
于是在HTTP1.1中增加了一个TCP连接中可以传送多个HTTP请求和响应，并且多个请求和响应可以重叠进行。而且进一步增加了一些例如host等的请求头和响应头。<

## 二、HTTP请求
一个HTTP请求由请求行、请求消息头、空行、请求实体四部分组成。

### 2.1 请求行
存在以下8种可能
>GET                 检索URI中标识资源的一个简单请求 
 HEAD               与GET方法相同，服务器只返回状态行和头标，并不返回请求文档 
 POST                服务器接受被写入客户端输出流中的数据的请求 
 PUT                 服务器保存请求数据作为指定URI新内容的请求 
 DELETE            服务器删除URI中命名的资源的请求 
 OPTIONS          关于服务器支持的请求方法信息的请求 
 TRACE             Web服务器反馈Http请求和其头标的请求 
 CONNECT        已文档化但当前未实现的一个方法，预留做隧道处理

get请求行不能包含请求实体，而POST、PUT、DELETE可以包含消息实体，比如form表单的提交。就可以通过POST消息头提交。

### 2.2 请求头标
由关键字/值对组成，每行一对，关键字和值用冒号（:）分隔。 请求头标通知服务器有关于客户端的功能和标识，典型的请求头标有
>User-Agent        客户端厂家和版本 
 Accept            客户端可识别的内容类型列表 
 Content-Length    附加到请求的数据字节数
 
### 2.3 空行
最后一个请求头标之后是一个空行，发送回车符和退行，通知服务器以下不再有头标。

### 2.4 请求实体
使用POST传送数据，最常使用的是Content-Type和Content-Length头标。

## 三、HTTP响应
### 3.1 响应状态行
响应状态行由三个标记组成：HTTP版本、响应代码和响应描述。 

HTTP版本：向客户端指明其可理解的最高版本。 

响应代码：3位的数字代码，指出请求的成功或失败，如果失败则指出原因。 

响应描述：为响应代码的可读性解释。 例如：HTTP/1.1 200 OK 

HTTP响应码：
>1xx：信息，请求收到，继续处理 
 2xx：成功，行为被成功地接受、理解和采纳 
 3xx：重定向，为了完成请求，必须进一步执行的动作 
 4xx：客户端错误： 
 5xx：服务器错误，服务器不能实现一种明显无效的请求 
 
### 3.2 响应消息头
像请求头标一样，它们指出服务器的功能，标识出响应数据的细节。

### 3.3 空行
最后一个响应头标之后是一个空行，发送回车符和退行，表明服务器以下不再有头标。

### 3.4 响应数据
HTML文档和图像等，也就是HTML本身。

## 附录：
### 一、HTTP码应码
响应码由三位十进制数字组成，它们出现在由HTTP服务器发送的响应的第一行。 
响应码分五种类型，由它们的第一位数字表示： 
>1.1xx：信息，请求收到，继续处理 
 2.2xx：成功，行为被成功地接受、理解和采纳 
 3.3xx：重定向，为了完成请求，必须进一步执行的动作 
 4.4xx：客户端错误，请求包含语法错误或者请求无法实现 
 5.5xx：服务器错误，服务器不能实现一种明显无效的请求 
 下表显示每个响应码及其含义： 
 100            继续 
 101            分组交换协 
 200            OK 
 201            被创建 
 202            被采纳 
 203            非授权信息 
 204            无内容 
 205            重置内容 
 206            部分内容 
 300            多选项 
 301            永久地传送 
 302            找到 
 303            参见其他 
 304            未改动 
 305            使用代理 
 307            暂时重定向 
 400            错误请求 
 401            未授权 
 402            要求付费 
 403            禁止 
 404            未找到 
 405            不允许的方法 
 406            不被采纳 
 407            要求代理授权 
 408            请求超时 
 409            冲突 
 410            过期的 
 411            要求的长度 
 412            前提不成立 
 413            请求实例太大 
 414            请求URI太大 
 415            不支持的媒体类型 
 416            无法满足的请求范围 
 417            失败的预期 
 500            内部服务器错误 
 501            未被使用 
 502            网关错误 
 503            不可用的服务 
 504            网关超时 
 505            HTTP版本未被支持
 
### 二、HTTP头标 
头标由主键/值对组成。它们描述客户端或者服务器的属性、被传输的资源以及应该实现连接。 
四种不同类型的头标： 
>1.通用头标：即可用于请求，也可用于响应，是作为一个整体而不是特定资源与事务相关联。 
 2.请求头标：允许客户端传递关于自身的信息和希望的响应形式。 
 3.响应头标：服务器和于传递自身信息的响应。 
 4.实体头标：定义被传送资源的信息。即可用于请求，也可用于响应。 
 头标格式：<name>:<value><CRLF> 
 下表描述在HTTP/1.1中用到的头标 
 Accept       定义客户端可以处理的媒体类型，按优先级排序； 
                  在一个以逗号为分隔的列表中，可以定义多种类型和使用通配符。例如：Accept: image/jpeg,image/png,*/* 
 Accept-Charset  
                  定义客户端可以处理的字符集，按优先级排序； 
                  在一个以逗号为分隔的列表中，可以定义多种类型和使用通配符。例如：Accept-Charset: iso-8859-1,*,utf-8 
 Accept-Encoding        定义客户端可以理解的编码机制。例如：Accept-Encoding:gzip,compress 
 Accept-Language       定义客户端乐于接受的自然语言列表。例如：Accept-Language: en,de 
 Accept-Ranges  
              一个响应头标，它允许服务器指明：将在给定的偏移和长度处，为资源组成部分的接受请求。 
             该头标的值被理解为请求范围的度量单位。例如Accept-Ranges: bytes或Accept-Ranges: nonea 
 Age       允许服务器规定自服务器生成该响应以来所经过的时间长度，以秒为单位。 
             该头标主要用于缓存响应。例如：Age: 30 
 Allow            一个响应头标，它定义一个由位于请求URI中的次源所支持的HTTP方法列表。例如：Allow: GET,PUT 
 aUTHORIZATION 
             一个响应头标，用于定义访问一种资源所必需的授权（域和被编码的用户ID与口令）。 
             例如：Authorization: Basic YXV0aG9yOnBoaWw= 
 Cache-Control        一个用于定义缓存指令的通用头标。例如：Cache-Control: max-age=30 
 Connection           一个用于表明是否保存socket连接为开放的通用头标。例如：Connection: close或Connection: keep-alive 
 Content-Base 
             一种定义基本URI的实体头标，为了在实体范围内解析相对URLs。 
             如果没有定义Content-Base头标解析相对URLs，使用Content-Location URI（存在且绝对）或使用URI请求。 
             例如：Content-Base: http://www.baidu.com 
 Content-Encoding    一种介质类型修饰符，标明一个实体是如何编码的。例如：Content-Encoding: zip 
 Content-Language    用于指定在输入流中数据的自然语言类型。例如：Content-Language: en 
 Content-Length        指定包含于请求或响应中数据的字节长度。例如：Content-Length:382 
 Content-Location 
             指定包含于请求或响应中的资源定位（URI）。 
             如果是一绝。对URL它也作为被解析实体的相对URL的出发点。 
             例如：Content-Location: http://news.baidu.com/
 Content-MD5 
             实体的一种MD5摘要，用作校验和。 
             发送方和接受方都计算MD5摘要，接受方将其计算的值与此头标中传递的值进行比较。 
             例如：Content-MD5: <base64 of 128 MD5 digest> 
 Content-Range  
             随部分实体一同发送；标明被插入字节的低位与高位字节偏移，也标明此实体的总长度。 
             例如：Content-Range: 1001-2000/5000 
 Contern-Type        标明发送或者接收的实体的MIME类型。例如：Content-Type: text/html 
 Date                    发送HTTP消息的日期。例如：Date: Mon,10PR 18:42:51 GMT 
 ETag      一种实体头标，它向被发送的资源分派一个唯一的标识符。 
             对于可以使用多种URL请求的资源，ETag可以用于确定实际被发送的资源是否为同一资源。 
             例如：ETag: "208f-419e-30f8dc99" 
 Expires          指定实体的有效期。例如：Expires: Mon,05 Dec 2008 12:00:00 GMT 
 Form            一种请求头标，给定控制用户代理的人工用户的电子邮件地址。例如：From: webmaster@myweb.com 
 Host            被请求资源的主机名。对于使用HTTP/1.1的请求而言，此域是强制性的。例如：Host: www.myweb.com 
 If-Modified-Since    
             如果包含了GET请求，导致该请求条件性地依赖于资源上次修改日期。 
             如果出现了此头标，并且自指定日期以来，此资源已被修改，应该反回一个304响应代码。 
             例如：If-Modified-Since: Mon,10PR 18:42:51 GMT 
 If-Match            如果包含于一个请求，指定一个或者多个实体标记。只发送其ETag与列表中标记区配的资源。 
                        例如：If-Match: "208f-419e-308dc99" 
 If-None-Match  
            如果包含一个请求，指定一个或者多个实体标记。资源的ETag不与列表中的任何一个条件匹配，操作才执行。 
            例如：If-None-Match: "208f-419e-308dc99" 
 If-Range 
             指定资源的一个实体标记，客户端已经拥有此资源的一个拷贝。必须与Range头标一同使用。 
             如果此实体自上次被客户端检索以来，还不曾修改过，那么服务器只发送指定的范围，否则它将发送整个资源。 
             例如：Range: byte=0-499<CRLF>If-Range:"208f-419e-30f8dc99" 
 If-Unmodified-Since 
             只有自指定的日期以来，被请求的实体还不曾被修改过，才会返回此实体。 
             例如：If-Unmodified-Since:Mon,10PR 18:42:51 GMT 
 Last-Modified        指定被请求资源上次被修改的日期和时间。例如：Last-Modified: Mon,10PR 18:42:51 GMT 
 Location  
             对于一个已经移动的资源，用于重定向请求者至另一个位置。 
             与状态编码302（暂时移动）或者301（永久性移动）配合使用。
             例如：Location: http://www2.baidu.com
 Max-Forwards  
             一个用于TRACE方法的请求头标，以指定代理或网关的最大数目，该请求通过网关才得以路由。 
             在通过请求传递之前，代理或网关应该减少此数目。例如：Max-Forwards: 3 
 Pragma            一个通用头标，它发送实现相关的信息。例如：Pragma: no-cache 
 Proxy-Authenticate 
            类似于WWW-Authenticate，便是有意请求只来自请求链（代理）的下一个服务器的认证。 
            例如：Proxy-Authenticate: Basic realm-admin 
 Proxy-Proxy-Authorization 
             类似于授权，但并非有意传递任何比在即时服务器链中更进一步的内容。 
             例如：Proxy-Proxy-Authorization: Basic YXV0aG9yOnBoaWw= 
 Public            列表显示服务器所支持的方法集。例如：Public: OPTIONS,MGET,MHEAD,GET,HEAD 
 Range            指定一种度量单位和一个部分被请求资源的偏移范围。例如：Range: bytes=206-5513 
 Refener 
             一种请求头标域，标明产生请求的初始资源。对于HTML表单，它包含此表单的Web页面的地址。 
             例如：Refener:  http://www.baidu.com
 Retry-After  
            一种响应头标域，由服务器与状态编码503（无法提供服务）配合发送，以标明再次请求之前应该等待多长时间。 
            此时间即可以是一种日期，也可以是一种秒单位。例如：Retry-After: 18 
 Server                     一种标明Web服务器软件及其版本号的头标。例如：Server: Apache/2.0.46(Win32) 
 Transfer-Encoding     一种通用头标，标明对应被接受方反向的消息体实施变换的类型。例如：Transfer-Encoding: chunked 
 Upgrade  
             允许服务器指定一种新的协议或者新的协议版本，与响应编码101（切换协议）配合使用。 
             例如：Upgrade: HTTP/2.0 
 User-Agent 
             定义用于产生请求的软件类型（典型的如Web浏览器）。 
             例如：User-Agent: Mozilla/4.0(compatible; MSIE 5.5; Windows NT; DigExt) 
 Vary          一个响应头标，用于表示使用服务器驱动的协商从可用的响应表示中选择响应实体。例如：Vary: * 
 Via            一个包含所有中间主机和协议的通用头标，用于满足请求。例如：Via: 1.0 fred.com, 1.1 wilma.com 
 Warning    用于提供关于响应状态补充信息的响应头标。例如：Warning: 99 www.myweb.com Piano needs tuning 
 www-Authenticate 
             一个提示用户代理提供用户名和口令的响应头标，与状态编码401（未授权）配合使用。响应一个授权头标。 
             例如：www-Authenticate: Basic realm=zxm.mgmt