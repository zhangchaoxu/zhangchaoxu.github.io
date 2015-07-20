---
layout:     post
categories: "tech"
title:      "Android Error Solution: Please ensure that adb is correctly located"
subtitle:   "android-error-solution-please-ensure-that-adb-is-correctly-located"
date:       2012-09-10 08:53
author:     "Charles"
---

Android开发环境奔溃的概率太大，当使用sqlite的时候，莫名其妙的问题更多。
今天遇到一个问题
~~~
The connection to adb is down, and a severe error has occured. 
You must restart adb and Eclipse. 
Please ensure that adb is correctly located at 'C:\&lt;sdk-directory&gt;\platform-tools\adb.exe' and can be executed.
~~~

问题简单说就是找不到adb了，可是路径肯定没问题，再stackoverflow上找到老外们的[讨论](http://stackoverflow.com/questions/5035456/the-connection-to-adb-is-down-and-a-severe-error-has-occurred),解决方案简单说就是以下几招:

- **方案一**

关闭Eclipse->adb kill-server->adb start-server->;
任务栏中关闭adb.exe->重启Eclipse

- **方案二**

将platform-tools目录和tools目录加到Path环境变量中;

- **方案三**

restart computer

折腾去吧，总有一款方案适合你。