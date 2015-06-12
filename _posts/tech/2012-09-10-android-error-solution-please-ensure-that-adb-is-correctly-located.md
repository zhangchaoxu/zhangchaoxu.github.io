---
layout:     post
category:   "tech"
title:      "Android Error Solution: Please ensure that adb is correctly located"
subtitle:   "android-error-solution-please-ensure-that-adb-is-correctly-located"
date:       2012-09-10 08:53
author:     "Charles"
header-img: "img/post-bg-01.jpg"
---

<p>&#160;&#160;&#160; Android开发环境奔溃的概率太大，当使用sqlite的时候，莫名其妙的问题更多。</p>  <p>&#160;&#160;&#160; 今天遇到一个问题</p>  <pre><code>The connection to adb is down, and a severe error has occured.<br />You must restart adb and Eclipse.<br />Please ensure that adb is correctly located at 'C:\&lt;sdk-directory&gt;\platform-tools\adb.exe' and can be executed.</code></pre>

<p>&#160;&#160; </p>

<p>&#160; 问题简单说就是找不到adb了，可是路径肯定没问题，再stackoverflow上找到老外们的<a href="http://stackoverflow.com/questions/5035456/the-connection-to-adb-is-down-and-a-severe-error-has-occurred" target="_blank">讨论</a>，解决方案简单说就是以下几招：</p>

<p><strong>方案一</strong></p>

<p>&#160;&#160;&#160;&#160; 关闭Eclipse—&gt;adb kill-server—&gt;adb start-server--&gt;任务栏中关闭adb.exe--&gt;重启Eclipse</p>

<p><strong>方案二</strong></p>

<p>&#160;&#160;&#160;&#160; 将platform-tools目录和tools目录加到Path环境变量中。</p>

<p><strong>方案三</strong></p>

<p>&#160;&#160;&#160;&#160; restart computer</p>

<p>&#160;</p>

<p>&#160;&#160;&#160; 折腾去吧，总有一款方案适合你。</p>