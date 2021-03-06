---
layout: default
title: 解决Nginx疑似端口被占用无法启动问题
subtitle: 10013 An attempt was made to access a socket in a way forbidden by its access permissions
apptitle: 10013 An attempt was made to access a socket in a way forbidden by its access permissions
category: tech
description: 解决Nginx疑似端口被占用无法启动问题 Hyper-V共享网络 防火墙正常 Fix Nginx error 10013 An attempt was made to access a socket in a way forbidden by its access permissions
permalink: /:categories/:year/:month/:day/:title
author: ROCEYS
date: 2019/11/19
tags:
    - tech
    - nginx
    - rtmp
---

## 系统环境

 **`Windows10`** **`Nginx-rtmp`**
 
 <br>

## 错误描述

```bash
2019/11/19 15:01:36 [emerg] 70712#97132: bind() to 0.0.0.0:1935 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
2019/11/19 15:04:47 [emerg] 67592#63044: bind() to 0.0.0.0:1935 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
2019/11/19 15:11:27 [emerg] 61036#61540: bind() to 0.0.0.0:1935 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
2019/11/19 15:14:00 [emerg] 65020#27996: bind() to 0.0.0.0:1935 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
2019/11/19 15:14:37 [emerg] 93428#21940: bind() to 0.0.0.0:1935 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
2019/11/19 15:15:16 [emerg] 67772#17516: bind() to 0.0.0.0:1936 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
2019/11/19 15:16:41 [emerg] 68992#25508: bind() to 0.0.0.0:1935 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
2019/11/19 15:16:43 [emerg] 18916#92192: bind() to 0.0.0.0:1935 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
2019/11/19 15:25:15 [emerg] 53048#58936: bind() to 0.0.0.0:1935 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
2019/11/19 15:25:30 [emerg] 36060#90476: bind() to 0.0.0.0:1935 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
2019/11/19 15:31:54 [emerg] 17220#51996: bind() to 0.0.0.0:8089 failed (10013: An attempt was made to access a socket in a way forbidden by its access permissions)
```
<br>

## 原因分析

昨天还正常启动的，啥也没动。

<br>

修改了conf配置里的服务器端口号也是同样错误。

<br>

查看了并没运行nginx.exe进程及相关端口号也没被占用。

<br>

```bash
netstat -ano | findstr "1935"
```

<br>

WFC防火墙也是正常的。

<br>

## 问题解决

经过一番折腾，原来是 `Hyper-V Virtual Ethernet Adapter` #3虚拟交换机自启导致的，**禁用**这些网络适配器后再启动就正常了。

```cpp
2019/11/19 15:56:43 [notice] 26948#69132: using the "select" event method
2019/11/19 15:56:43 [notice] 26948#69132: nginx/1.13.12
2019/11/19 15:56:43 [info] 26948#69132: OS: 260200 build:9200, "", suite:100, type:1
2019/11/19 15:56:43 [notice] 26948#69132: start worker processes
2019/11/19 15:56:43 [notice] 26948#69132: start worker process 52244
2019/11/19 15:56:44 [notice] 52244#13580: nginx/1.13.12
2019/11/19 15:56:44 [info] 52244#13580: OS: 260200 build:9200, "", suite:100, type:1
2019/11/19 15:56:44 [notice] 52244#13580: create thread 76628
2019/11/19 15:56:44 [notice] 52244#13580: create thread 98812
2019/11/19 15:56:44 [notice] 52244#13580: create thread 98868
2019/11/19 15:56:45 [info] 52244#76628: *1 client connected '127.0.0.1'
2019/11/19 15:56:45 [info] 52244#76628: *1 connect: app='live' args='' flashver='FMLE/3.0 (compatible; FMSc/1.0)' swf_url='rtmp://localhost/live' tc_url='rtmp://localhost/live' page_url='' acodecs=0 vcodecs=0 object_encoding=0, client: 127.0.0.1, server: 0.0.0.0:1935
2019/11/19 15:56:45 [info] 52244#76628: *1 createStream, client: 127.0.0.1, server: 0.0.0.0:1935
2019/11/19 15:56:45 [info] 52244#76628: *1 publish: name='' args='' type=live silent=0, client: 127.0.0.1, server: 0.0.0.0:1935
2019/11/19 15:56:45 [info] 52244#76628: *1 relay: create push name='' app='' playpath='' 
```

