---
title: 使用sshfs搭载内网目录
date: 2022-12-19 22:34:41 +0000
categories: [笔记, Linux]
tags: [sshfs]
---

## 需求

开发环境需要license无法本地编译，但服务端无法配置舒适的编辑环境。考虑使用`sshfs`将服务端目录挂载，本地编辑远程编译。 此外，还需要考虑服务器在内网这一因素。

设：本地机器A，proxy为B，服务器为C。

## ~~端口转发~~

1. 使用ssh进行TCP端口转发：A运行`ssh -NL TCP_PORT:C_IP:SSH_PORT B_USERNAME@B_IP`，开启正向SSH隧道，其中，`N`代表仅端口转发而不进入B的shell，`-L`代表进行TCP转发。`ssh`进程会在该终端内运行，使用`-f`可使其后台运行，但需要设置相关Interval保证连接稳定。
2. 设定文件权限并通过端口挂载目录：A运行

```shell
chmod 777 /A_TARGET_DIR # dunno what it does tho
sshfs -p TCP_PORT C_USERNAME@localhost:/C_SOURCE_DIR /A_TARGET_DIR
```

优缺点：通过`-R`也可以选择反向隧道，运行比较显式，并且全程不需要在不同机器之间转换。然而，端口转发设置与运行效率太低，需要（人肉或电子地）记录用户名、IP、命令等。

## ProxyJump

ProxyJump亦适用于一般的ssh链接，通用性高，使用`fstab`可在boot time自动搭载目录。（当然，密码的问题我还没整明白怎么搞）

1. A设置`~/.ssh/config`:

```shell
Host B_NAME
  HostName B_IP
  User B_USERNAME

Host C_NAME
  ProxyJump B_NAME
  HostName C_IP
  User C_USERNAME
```

2. A运行如下代码后，所有ssh操作直接向`C_NAME`发送即可。

```shell
chmod 777 /A_TARGET_DIR
sshfs C_NAME:/C_SOURCE_DIR /A_TARGET_DIR
```

3. 注意事项：不要使用`sudo`搭载目录，否则`A_TARGET_DIR`属于`root`，后者无法读取`~/.ssh/config`，再采用这一方法也就没有意义了。

***TODO: chmod，fstab***
