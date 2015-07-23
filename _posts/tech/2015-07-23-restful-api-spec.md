---
layout:     post
categories: tech
tags:       Android
title:      Restful API 规范
subtitle:   Restful API Spec
author:     "Charles"
---

在移动开发中移动端不可避免的会从服务器端拉取数据，并且进行交互，而

## 接口规范定义

### 原则
接口定义尽量符合Restful规范
1.  路径中应该只包含resource名称，而不是动作名称。
2.  对于不同的操作采用URL Params, 如验单中的承运商验单还是收货验单，IoT设备中的车牌号等
3.  采用GET为数据获取请求，Put最为幂等数据修改操作请求，Post为数据的提交请求，Delete为数据的删除请求；
4.  用不同状态码HttpStatus作为不同操作结果的区分


## 全局定义
返回数据为不含 BOM 的 UTF-8标准的JSON格式。格式定义如下
`
{
    "status": 200,
    "msg": "OK",
    "queryTs": 1400000000
    "page":0/1,
    "pageInfo":{
      "no":1,
      "size":20,
      "total":100
    },
    "data": []
}
`

### 全局参数说明

## 附录 

### 附录1 返回状态码
返回码参考[HttpStatusCode](http://httpstatus.es/)
其中1000+为自定义码段


### Ref:
