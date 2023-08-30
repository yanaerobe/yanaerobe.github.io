---
title: Neovim安装备忘
date: 2023-7-10 20:20:42 +0800
categories: [笔记, Linux]
tags: [Neovim]
---

以下均在Ubuntu 22.04进行。

Prerequisites

```shell
sudo apt-get install ninja-build gettext cmake unzip curl
```

git clone Neovim repo

```shell
git clone https://github.com/neovim/neovim\
cd neovim
```

```shell
# Optional stable version
# git checkout stable

# Optional download & build 3rd-party dependencies
# make deps
```

Download & build，Release/RelWithDebInfo/Debug

```shell
make CMAKE_BUILD_TYPE=Release
```

Check type

```shell
./build/bin/nvim --version | grep ^Build
```

Global installation into `/usr/local`

```shell
sudo make install
```

Or a specific location

```shell
make CMAKE_INSTALL_PREFIX=$HOME/local/nvim install
```

For updating, run the following commands and repeat the above (not verified)

```shell
make distclean
```

For uninstallation, run the follwing

```shell
make distclean\
sudo make uninstall
```

> 另：Linux根目录的`/usr`目录意思是Unix System Resources，一般安装预装软件。
> 用户软件一般安装在`$HOME`，为所有用户安装位置在`/usr/local`（即上）。
{:.prompt-tip}

> 又另：`/sbin`的意思是“super users才能用的`/bin`”
{:.prompt-tip}
