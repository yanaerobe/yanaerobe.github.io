---
title: CCLP上手与初步配置
date: 2023-7-9 20:35:42 +0800
categories: [剁椒派, 配置]
tags: [CCLP, Linux]
---

本文主要给重新在128Gb TF/SSD上配置更好系统作备忘。

![OPi5](/assets/posts/20230711113748.jpg){: w="500"}

## 烧写系统并ssh

香橙派到了几天了，但中通挂了所以TF卡今天才到。

烧写的香橙派官网Ubuntu服务端系统，以太网连接并通过路由器管理查询到IP后顺利连上了，没什么说的。`git`版本甚至是最新的，不错。

![Boot](/assets/posts/2023-07-09203906.png){: w="500"}

查了查资料，直接烧写Ubuntu官网系统应该不是个好选择。这样外设应该是需要自己找/开发驱动，没必要，乖乖安装的香橙派版。

## 连接WiFi

3.6.4：`orangepi-config`或`/boot/orangepiEnv.txt`启用硬件模块。

3.6.2：`nmcli`服务器端无GUI连接并测试WiFi

3.6.3: 设置静态IP地址放在设置服务器上说

## 设置其它用户

使用`adduser`跟随系统指引即可。

顺便使用`sudo auto_login_cli.sh username`修改了登陆用户。

TODO：用户组位于1001而非1000，需要了解其含义并制定更好的用户组策略

## TODO: VPN

## 配置ZSH与Neovim

使用`cat /etc/shells`查看可用shell，`chsh`修改登录shell。

系统自带了oh-my-zsh，但是在`/etc/`目录下，所以把root的shell也改成了zsh，这样su可以直接更新omz。

TODO: 傻逼防火墙连接不上`raw.githubusercontent.com`这个网站，暂时先改hosts好了，下一步得把VPN装上。

Neovim搞了半天才装上，`make`各种报网络错误，跑了不下十遍才全部下载好，佛了。

## 配置其它开发环境

### Prerequisites

略，要啥装啥就是了

### Node.js

安装流程和WSL中不一样。

```shell
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```

## 个性化起步

### [thefuck](https://github.com/nvbn/thefuck)

```shell
sudo apt update
sudo apt install python3-dev python3-pip python3-setuptools
pip3 install thefuck --user
```

不会把自己添加进`$PATH`，需要手动添加`$HOME/.local/bin`。

### auto_suggestions

将[repo](https://github.com/zsh-users/zsh-autosuggestions)拷贝进`$ZSH_CUSTOM/plugins`

### autojump

将[repo](https://github.com/wting/autojump/tree/master)拷贝至本地后`./install.py`
