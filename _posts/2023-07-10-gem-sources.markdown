---
title: 使用gem镜像源
date: 2023-7-10 17:47:02 +0800
categories: [笔记, Linux]
tags: [gem]
---

科学上网不能解决连接到ruby源卡死的问题，如`jekyll`本地编译。原因不明。

需要清空gem源并重新设置为`https://gems.ruby-china.com/`。

> 不是`.org`
{: .prompt-warning }

```shell
# Check current gem sources
gem sources --list
# Remove obsolete gem sources
gem sources --remove https://rubygems.org/
# Add the mirror site
gem sources --add https://gems.ruby-china.com/
# Clear and update gem sources
gem sources --clear && gem sources --update
```

> 注意，如果托管在GitHub上Gemfile不要修改镜像，否则容易出现连接错误
{:.prompt-warning}
