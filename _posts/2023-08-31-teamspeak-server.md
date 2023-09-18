---
title: 香橙派TeamSpeak 3服务器搭建、连接与使用
date: 2023-8-31 19:26:23 +0100
categories: [剁椒派, 服务器]
tags: [CCLP, TeamSpeak]
---

> 使用方法可直接转到[这里](#连接teamspeak-3服务器并调整设置)。
> 联系我获取我的TeamSpeak 3服务器地址与密码 :smirk:
{:.prompt-info}

## 概述

国内语音软件生态令人非常反感，在此点名批评某K姓流氓软件。

自己动手丰衣足食，使用ARMv8（64位）架构的香橙派搭建x86架构的TeamSpeak 3服务器并将其穿透至公网。

## Box64

[Box64](https://github.com/ptitSeb/box64)是一款用户层模拟器，通过直接将x86指令翻译成ARM64指令实现跨架构应用的运行。

### 安装

git clone

```shell
git clone https://github.com/ptitSeb/box64
```

编译Box64并安装。

```shell
cd box64
mkdir build
cd build
# For RK3588/RK3588S
cmake .. -D RK3588=1 -D CMAKE_BUILD_TYPE=RelWithDebInfo
make -j4  
sudo make install
```

重启`systemd-binfmt`服务，以更新系统可以支持的架构。

```shell
sudo systemctl restart systemd-binfmt
```

重启香橙派。

```shell
sudo reboot
```

## TeamSpeak 3服务器搭建

需要公网IP并进行穿透，随后运行服务器。

### 设置端口转发

TeamSpeak不同的服务需要不同的端口，详细列表与功能[见此页面](https://support.teamspeak.com/hc/en-us/articles/360002712257-Which-ports-does-the-teamspeak-3-server-use-)。其中最为重要的是UDP协议的9987端口，此为语音服务器端口。

| 服务              | 协议 | 端口  |
|-------------------|------|-------|
| 语音              | UDP  | 9987  |
| 文件传输          | TCP  | 30033 |
| ServerQuery (raw) | TCP  | 10011 |
| ServerQuery (ssh) | TCP  | 10022 |
| WebQuery (hhtp)   | TCP  | 10080 |
| WebQuery (https)  | TCP  | 10443 |
| TSDNS             | TCP  | 41144 |

> 语音端口（9987）不要同时开启TCP与UDP协议，ref [here](https://community.teamspeak.com/t/solved-hosting-a-ts3-server-at-home/3402/16)
{:.prompt-danger}

> TeamSpeak无证书情况下支持单个最多32人在线的虚拟服务器。
> 如果使用付费证书的多个虚拟服务器，端口号自9987递增。
{:.prompt-info}

### 下载并运行服务器

进入官网`wget`对应的服务器端版本。

```shell
wget https://files.teamspeak-services.com/releases/server/3.13.7/teamspeak-server_linux_amd64-3.13.7.tar.bz2
```

解压压缩包。

```shell
# Or use `extract` under oh-my-zsh
tar -xvf teamspeak-server_linux_amd64-3.13.7.tar.bz2
```

```shell
# Optional 
rm teamspeak-server_linux_amd64-*
mv teamspeak-server_linux_amd64 teamspeak
```

接受用户协议

```shell
cd teamspeak
touch .ts3server_license_accepted
```

运行服务器

```shell
./ts3server_startscript.sh start
```

如果成功运行服务器，终端会依次输出Box64与TeamSpeak 3的prompt，随后输出两个block，分别为服务器密码与管理员授权token。

首次登陆服务器后，输入管理员授权token即可获取管理员权限。

## 连接TeamSpeak 3服务器并调整设置

进入[官网](https://teamspeak.com/en/downloads/#client)（可能需要VPN）或其他途径下载客户端并安装。

安装过程中，Overwolf是一个可选的游戏内覆盖组件（用起来一般般）。TeamSpeak账户亦可不填，该账户仅用于TeamSpeak官方社区而非客户端。

启动客户端，从Connections下拉菜单中选择Connect。

![connect](/assets/posts/2023-08-31-200603.png){: w="500"}

输入服务器地址、密码与用户名，点击Connect。

![server-info](/assets/posts/2023-08-31-200842.png){: w="500"}

成功后即可进入服务器，have fun!

使用Connections下拉菜单中的Disconnect或直接使用Ctrl+D退出服务器。

### 如果连接出现问题

可能的问题包括但不限于：无法连接服务器，语音中连接超时掉线，通话电流音大。

TeamSpeak 3所需资源极少，上传下载速率仅需若干Kb每秒，硬件与网速不太可能出问题。大部分情况下，这些都是网络环境或配置问题。

个人建议的调试方法有：

1. 召唤一个好兄弟尝试连接，排除服务器问题。
2. 点击Bookmark下拉菜单中的TeamSpeak Public，连接至官方服务器，排查自身网络问题。
3. 如果前两条无法复现问题，Windows下在`:C/Users/username/AppData/Roaming/TS3Client/logs`中查找日志文件排查问题。
4. 如果还是不能解决问题，施展进阶召唤术寻求服务器运营/管理员甚或网络运营商的帮助。

亦可参考[本TeamSpeak社区页面](https://community.teamspeak.com/t/you-cant-connect-to-a-server/8530/1)的解决方案。

### 调整设置

在Tools下拉菜单中选择Options进入设置界面。

![options](/assets/posts/2023-08-31-200853.png){: w="500"}

设置界面中，Playback为语音接收设置。据我所知，默认声音设置比较小，建议适当调高Voice Volume Adjustment。其它可根据个人需求调整。

![playback](/assets/posts/2023-08-31-200926.png){: w="500"}

Capture为语音捕获设置。建议检查并调整Capture Device，打开Typing attenuation（消除键盘音）。Echo
cancellation在某些条件下（e.g., 垃圾麦）可能使得语音捕获不完整，可以考虑改用Echo reduction并调节减益量。其他可根据个人需求调整。

![capture](/assets/posts/2023-08-31-200930.png){: w="500"}

> Begin Test是个好功能
{:.prompt-tip}

### 汉化

进入[汉化包repo](https://github.com/VigorousPro/TS3-Translation_zh-CN/releases)（GitHub页面，可能需要VPN）或[这里](/assets/Chinese_Translation_zh-CN.ts3_translation)下载TeamSpeak汉化包。下载后直接运行并重启客户端即可完成客户端汉化。

汉化包卸载可在工具->设置->附加组件->翻译中进行。
