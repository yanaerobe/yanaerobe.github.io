---
title: 香橙派备份方法
date: 2023-8-30 21:45:39 +0100
categories: [剁椒派, 配置]
tags: [CCLP, Linux]
---

用`dd`尝试了若干次，卡在了启动时的自动登陆(auto authentication)上，肯定是没能完整地复制磁盘，但不清楚具体原因。
其它不可靠的猜测包括使用了静态IP地址或者修改了默认用户的密码。

作为妥协，改用`tar`完成了一次比较成功的备份。

```shell
# On Pi
su root

# Backup to backup.tar.gz
sudo tar -cvpzf backup.tar.gz --exclude=/backup.tar.gz --exclude=/mnt --exclude=/sys --exclude=/proc --one-file-system /

# On PC
scp root@x.x.x.x:/root/backup.tar.gz ~/backup.tar.gz
```

```shell
# Change booter, on PC
scp ~/backup.tar.gz root@x.x.x.x:/root/backup.tar.gz

# Might need to remove previous ssh fingerprint
ssh-keygen -R x.x.x.x

# Restore
tar -xvpfz backup.tar.gz -C /
```

> `dd`可能仍然是一个更正经的磁盘映像制作手段，毕竟不需要将boot分区和filesystem分开恢复
> 主要问题依然是auto authentication和可能存在的片段损坏
{:.prompt-tips}
