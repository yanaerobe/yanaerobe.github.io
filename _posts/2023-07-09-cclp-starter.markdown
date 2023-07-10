---
title: CCLP上手与初步配置
date: 2023-7-9 20:35:42 +0800
categories: [剁椒派, 配置]
tags: [CCLP, Linux]
---

## 烧写系统并ssh

香橙派到了几天了，但中通挂了所以TF卡今天才到。

烧写的香橙派官网Ubuntu服务端系统，以太网连接并通过路由器管理查询到IP后顺利连上了，没什么说的。`git`版本甚至是最新的，不错。

![Boot](/assets/posts/2023-07-09203906.png)

查了查资料，直接烧写Ubuntu官网系统应该不是个好选择。这样外设应该是需要自己找/开发驱动，没必要，乖乖安装的香橙派版。

## 连接WiFi

3.6.4：`orangepi-config`或`/boot/orangepiEnv.txt`启用硬件模块。

3.6.2：`nmcli`服务器端无GUI连接并测试WiFi

3.6.3: 设置静态IP地址放在设置服务器上说

## 设置其它用户

使用`adduser`跟随系统指引即可。

TODO：用户组位于1001而非1000，需要了解其含义并制定更好的用户组策略

## TODO: VPN

## 配置ZSH与Neovim

使用`cat /etc/shells`查看可用shell，`chsh`修改登录shell。

系统自带了oh-my-zsh，但是在`/etc/`目录下，所以把root的shell也改成了zsh，这样su可以直接更新omz。

傻逼防火墙连接不上raw.githubusercontent.com这个网站，暂时只能先改hosts了，下一步得把VPN装上。

Neovim也是半天还没装上，make各种报网络错误，佛了。`apt`安装了一个先凑用着了。

## TODO: 配置其它开发环境

## TODO: 个性化起步
