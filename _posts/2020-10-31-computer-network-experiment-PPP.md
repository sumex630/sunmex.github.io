---
layout: post
title: 计网实验记录-PPP协议
categories: 计网
description: 计网实验记录-ppp协议
keywords: PPP协议，
# topmost: true
---


# 计网实验 -- PPP协议实验过程

## 一、实验环境

- Cisco Packet Tracer

## 二、实验要求

- 将两个路由器使用PPP协议连接起来

## 三、实验步骤

### 第一步：连通路由器

1. 放置两个路由器，将这两个路由器连接起来，使用 se2/0 端口。
2. 修改路由器的配置。
   - 路由名称
   - 时钟速率 。如：128000
   - IP地址 。如：192.168.12.1
   - 接口状态 - 开
   - 保存
3. 模拟数据发送
   - 打开仿真面板
   - 在编辑过滤器中过滤ARP和ICMP协议
   - 模拟发送
   - 点开发送过来的数据包，可查看发送信息

### 第二步：配置路由器之间的ppp协议

1. 进入路由器(r1/r2)中 Serial2/0 的命令行界面

2. `(config-if)#encapsulation ppp`   #  配置 ppp 协议

3. `(config-if)#no shutdown`   # 确保ppp协议在此端口下不被关闭

4.  `(config-if)#do show int se2/0`  # 查看该端口是否被激活以及该链路协议是否启动

   ![image-20201025194648182](../images\posts\network\image-20201025194648182.png)

   > 注：只有将两个路由器都进行配置的情况下，才会显示 line protocol is up（链路协议已启动）。

### 第三步：配置PPP认证

1. 进入路由器(r1/r2)中 Serial2/0 的命令行界面

2.  `(config-if)#ppp ?` , `(config-if)#ppp authentication ? `  # 查看相关配置参数

   ![image-20201025201043569](../images\posts\network\image-20201025201043569.png)

   > 注：这里使用 PAP认证。
   >
   > 密码认证协议（PAP），是 PPP 协议集中的一种链路控制协议，主要是通过使用 2 次握手提供一种对等结点的建立认证的简单方法，这是建立在初始链路确定的基础上的。-- 来自百度

3.  `(config-if)#ppp au pap`  # 当前状态若为 down，则开启协议

4. （`(config-if)#no shutdown`）

5. `(config-if)#ppp pap sent-username r1 password 123456`  # 设置认证的用户名和密码

6. 退出当前配置环境，查看线路协议状态`#show int se2/0 `

   > 注：此时的链路状态为down，因为两个路由器都需要进行认证，并且进行连接登录

### 第四步：连接登录

1. r1路由器： `(config)#username r2 password 123456`
2. r2路由器： `(config)#username r1 password 123456`
3. 退出配置环境，查看链路协议状态 `#show int se2/0`

