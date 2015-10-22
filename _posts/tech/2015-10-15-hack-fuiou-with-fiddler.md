---
layout:     post
categories: "tech"
tags:       [android,fiddler]
title:      "利用Fiddler完成对富友收件宝应用的网络请求解析"
subtitle:   "hack-fuiou-with-fiddler"
author:     "Charles"
---

## 文章目地
讲述如何利用[Fiddler](http://www.telerik.com/fiddler)实现对Android设备的网络访问嗅探，同时以富友收件宝为例，描述了如何分析Fiddler的网络请求。

## 工具
[Fiddler](http://www.telerik.com/fiddler)是一款与Wireshark、Charles类似的网络数据抓包(嗅探)软件，可以实现对网络的监听。[下载地址](http://www.telerik.com/download/fiddler)
[富友收件宝](https://www.fuiou.com/)是一款社区智能收寄取快递的设备，用于社区中自助收件服务。实验版本

## 初衷
在笔者所住的小区内安装了富友收件宝的快递箱，类似超市的寄存箱。快递员将快递放入寄存箱内，富友的系统下发短信告知收件人有快递待收取，收件人可以凭借手机号和取件密码/手机应用开箱操作两种方式取件。

刚开始的时候，收件人收到的通知短信内会包含有取件密码，而后来只有通知短信告知有快递，必须安装富友收件宝的手机应用才能查看到取件密码或者手机开箱。而富友收件宝的手机应用使用体验相当糟糕，经常强制升级，强行广告。
因此有了分析其应用接口API，自己通过一个轻量的页面或者微信公众号来完成其应用核心功能的想法。

## 实验原理
原理其实很简单，首先将PC和Android手机连到同一个局域网内，在PC上开启Fiddler作为网络代理，而Android设备网络手动代理连接到这台PC。从而达到Android设备所有网络请求都经过PC上的Fiddler的目地。

## 步骤
1.  如何安装和使用Fiddler请参见[Android利用Fiddler进行网络数据抓包](http://www.trinea.cn/android/android-network-sniffer/),注意其中的PC IP地址应该查看Fiddler右上角中Online的信息，从ipconfig中有可能无法获取到PC在局域网中的地址。
2.  打开富友收件宝完成一次登录操作，可以故意输错密码。在Fiddler中查看结果。
3.  返回成功格式
`
<FM>
    <Rcd>0000</Rcd>
    <RDesc>成功</RDesc>
    <Ust/>
    <InsCd>08A0000083</InsCd>
    <MchntCd/>
    <SessionID>EB82B8D828BDA74887698C2FA677143F.jvm62</SessionID>
    <CommBindSt>1</CommBindSt>
    <CommunityName>江南景苑北区</CommunityName>
    <CommunityCd>A100009607</CommunityCd>
    <Cells>
        <ProvCd>330</ProvCd>
        <CityCd>3320</CityCd>
        <CountyCd>3322</CountyCd>
        <RowId>201435593530</RowId>
        <DetailAddr>宁波市新舟路55弄监控室旁边</DetailAddr>
        <CommunityCd>A100009607</CommunityCd>
        <CommunityName>江南景苑北区</CommunityName>
        <Latitude>29.898608</Latitude>
        <Longitude>121.638575</Longitude>
        <CheckSt>1</CheckSt>
    </Cells>
    <UUrl>https://fly.fuiou.com/jf.csv</UUrl>
    <UVer>20131128</UVer>
    <Cno/>
    <Ctp>0</Ctp>
    <Cnm/>
    <AcntBalance>0</AcntBalance>
    <AcntCfBalance>0</AcntCfBalance>
    <AcntTxBalance>0</AcntTxBalance>
    <Ast/>
    <IsUpdPwd>0</IsUpdPwd>
    <IsOpenNoPay>0</IsOpenNoPay>
    <PerCenterData>
        <AcntBalance>0</AcntBalance>
        <AcntCfBalance>0</AcntCfBalance>
        <AcntTxBalance>0</AcntTxBalance>
        <CardBindCount>0</CardBindCount>
        <VoucherCount>0</VoucherCount>
        <AvatarUrl/>
        <IsOpenNoPay/>
        <VoucherData>
            <actionAddr>kaquanbao.html</actionAddr>
            <showBar>0</showBar>
            <isInvokeNative>1</isInvokeNative>
            <barName>voucher</barName>
            <folder>o2o</folder>
            <type>1</type>
        </VoucherData>
    </PerCenterData>
    <MbNoticeData>
        <Snum>0</Snum>
        <Unum>0</Unum>
    </MbNoticeData>
    <VoucherData>
        <actionAddr>kaquanbao.html</actionAddr>
        <showBar>0</showBar>
        <isInvokeNative>1</isInvokeNative>
        <barName>voucher</barName>
        <folder>o2o</folder>
        <type>1</type>
    </VoucherData>
</FM>
`
