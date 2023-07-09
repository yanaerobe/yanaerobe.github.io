---
title: CCLP上手与初步配置
date: 2023-7-9 20:35:42 +0800
categories: [剁椒派, 配置]
tags: [CCLP, Linux]
---

## 烧写系统并ssh

香橙派到了几天了，但中通挂了所以TF卡今天才到。

烧写的香橙派官网Ubuntu服务端系统，以太网连接并通过路由器管理查询到IP后顺利连上了，没什么说的。

![Boot](/assets/posts/2023-07-09203906.png)

查了查资料，直接烧写Ubuntu官网系统应该不是个好选择。这样外设应该是需要自己找/开发驱动，没必要，乖乖安装的香橙派版。

## 连接WiFi

3.6.4：`orangepi-config`或`/boot/orangepiEnv.txt`启用硬件模块。

3.6.2：`nmcli`服务器端无GUI连接并测试WiFi

TODO: 3.6.3: 设置静态IP地址，还不明确必要性和需要注意的地方。

## TODO：设置其它用户

## TODO：配置ZSH与Neovim

## TODO：配置其它开发环境

## TODO：个性化起步
