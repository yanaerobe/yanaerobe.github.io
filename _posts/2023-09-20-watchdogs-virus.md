---
title: watchdogs病毒查杀与使用ssh秘钥预防
date: 2023-9-20 20:25:01 +0100
categories: [笔记, Linux]
tags: [CCLP, Linux, virus]
---

上网习惯不好，CCLP中了个病毒。这篇笔记简要记录一下查杀过程，算是给自己提个醒了。

## 症状

CCLP开机启动1-2天后在极低负载的情况下CPU使用率异常地高（仅开启TeamSpeak 3服务器与DDNS脚本，CPU占用率在0-15%之间跳动）。

使用`htop`查看发现若干个名为`watchdogs ssh a watchdog kthread`的进程占用了这些异常资源。

## 排查

一开始以为是长期开启服务器与脚本导致软硬件异常，开门狗程序使能。但多次重启后台与CCLP均无法排除这一问题，香橙派提供的开门狗测试程序也返回了正常的结果。

不得不求助万能的搜索引擎，直接搜索`watchdogs ssh a watchdog kthread`。语言隔阂还真有点正面影响，谷歌有关`watchdogs`的搜索结果全被某U姓游戏公司的三流游戏污染了，百度[高匹配的结果](https://zhuanlan.zhihu.com/p/81798241)表明`watchdogs`是一个挖矿病毒程序。

> 无差别攻击是真的牛批，单板机都给黑了挖矿。转发22端口确实是非常不好的习惯，侥幸心理也真不好。

简而言之（其它的我也不懂），`watchdogs`是一个有若干变种的经由`ssh`暴力破解弱密码入侵与传播的挖矿病毒。

## 手动查杀

为了这个病毒给CCLP下一套Linux杀毒套件显然太业余也太不值当了，所以我参考了[这个网页](https://juejin.cn/post/7222052147596460093)手动进行了查杀。

```shell
# find malware processes pid
ps -ef | grep watchdogs

# find process location
ll /proc/$pid

# forcibly kill malware processes
kill -9 $pid

# remove malware scripts (just an example)
# Other possible directories exist. Also rm `ksoftirqds`, `.lsdpid`, etc.
rm -rf /dev/shm/watchdogs

# check scheduled tasks
crontab -l
```

## 可选的后续处理

1. 删除用户
2. 使用强密码
3. 修改默认端口
4. 使用ssh秘钥，关闭高权限用户的`ssh`远程登录

## `ssh`秘钥生成与使用

> 部分参考[此页面](https://cloud.tencent.com/developer/article/1780788)
{:.prompt-info}

首先，在客户端生成一对ssh秘钥。

```shell
ssh-keygen -t type -f filename -N passphrase
```

使用passphrase可以提高安全性，但在`scp`时可能需要多次输入passphrase，比较麻烦。更适合在单纯的ssh中使用。

TODO: 使用`ssh-agent`解决此问题

随后使用如下命令，或`ssh-copy-id`，或直接登陆主机将`filename.pub`中的内容加入需登陆用户的`~/.ssh/authorized_keys`中。

```shell
cat ~/.ssh/id_rsa.pub | ssh user@host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

另：要禁止某一用户的ssh登陆权限，在`/etc/ssh/sshd_config`中添加`DenyUsers user`一行即可。
