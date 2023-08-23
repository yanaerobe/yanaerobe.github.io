---
title: 香橙派内网穿透笔记
date: 2023-8-22 20:39:41 +0100
categories: [剁椒派, 服务器]
tags: [CCLP]
---

> WIP
{:.prompt-warning}

localhost vs 127.0.0.1 vs 0.0.0.0 vs IP

localhost只是一个域名，通过修改hosts文件可以解析到其它地址

127.* 是loopback地址，和它们有关的操作经过虚拟网卡而根本不和外界交互

0.0.0.0类似一个空地址，没有实际意义；但将服务导向它即可本地与外网都访问到（TODO: 可以再严谨地了解一下）。
从而可以用在jekyll测试上：CCLP运行jekyll至0.0.0.0，局域网内访问CCLP地址的4000（默认）端口

IP则是路由器分配的公网用的

## 分割线

成功地实现了nginx的内网穿透，证明家里的路由器确实（应该？）是公网IP

nginx默认使用80端口TCP协议，在路由器里设置端口转发（80端口转到80端口）后，直接访问路由器的地址就会导航到nginx默认界面了