---
title: 安装并使用Linux下的clash
date: 2023-7-13 11:09:04 +0800
categories: [笔记, Linux]
tags: [clash, VPN]
---

使用clash进行配置。实际上网上许多教程都比较全面简洁，并不难。

## 获取文件

[clash release](https://github.com/Dreamacro/clash/releases)页面`wget`最新的ARM64 `.gz`文件。

> ARM64即ARMv8，因为它是第一版真正支持64位的指令集。
{:.prompt-tip}

使用`gunzip`解压该文件，更改名字为clash并`chmod u+x clash`获取权限。zsh的`extract`在这里不好用，它一直在尝试将其解压为一个文件夹，不知道为什么。

尝试运行clash，如果`.mmdb`文件下载失败，前往[另一repo](https://github.com/Dreamacro/maxmind-geoip/releases)下载该文件，用以识别IP地址。

从机场的订阅链接`curl -O config.yaml URL`即可下载配置文件，或者也可以从clash的GUI右键配置文件`scp`过来。它长得大概像[这样](https://dreamacro.github.io/clash/configuration/configuration-reference.html)

## 配置

> 以下操作均需`sudo`
{:.prompt-tip}

把clash `cp` 到`/usr/local/bin`，`.mmdb``config.yaml` `cp`到`/etc`下的新文件夹，如`/etc/clash`。

将以下内容添加为`/etc/systemd/system/clash.service`：

```ini
[Unit]
Description=Clash daemon, A rule-based proxy in Go.
After=network-online.target

[Service]
Type=simple
Restart=always
# The executable, and file dir
ExecStart=/usr/local/bin/clash -d /etc/clash

[Install]
WantedBy=multi-user.target
```

## 运行代理

```shell
# Reload systemd
systemctl daemon-reload

# Launch clash-daemon on startup
systemctl enable clash

# Launch clash
systemctl start clash

# Status and log check
systemctl status clash
journalctl -xe

# 启用代理
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890

# 禁用代理
unset  http_proxy  https_proxy  all_proxy
```

## 其它

不妨试试[这个封装好的项目](https://github.com/wanhebin/clash-for-linux)

如果53端口被`systemd-resolved`或`dnsmasq`占用，修改`config.yaml`中的DNS监听端口为其它数值即可。

> TODO: 为什么？
{:.prompt-info}

使用`ping`来测试代理并不合适，或者说根本没用。`curl -L`一个原本无法访问的网站比较可靠。

> TODO: 为什么？
{:.prompt-info}
