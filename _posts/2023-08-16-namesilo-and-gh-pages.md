---
title: 购买自定义域名并部署GitHub个人页
date: 2023-8-16 21:29:30 +0100
categories: [剁椒派, 服务器]
tags: [CCLP]
---

## 购买域名

国内域名需要备案等手续，管理麻烦，首先排除。

国外较为良心的域名商有NameSilo，Google Domain，Domain.com。后两家价格一个比一个高，NameSilo口碑和用户量都很可观，所以选择了NameSilo。

需要重点考虑的附加服务有三项：

- WHOIS隐私：有点像匿名模式，好像是开了之后WHOIS查不到个人信息。必买，NameSilo赠送。
- Premium DNS：加快DNS解析（？），防止DDoS攻击。没人攻击我所以没用，没买。
- SSL证书：没有证书有些浏览器或者服务不允许访问，还会有不安全的小锁标志。必买，后期考虑换Let's Encrypt的免费证书，买了NameSilo的基础证书。

> 更新：像我一样的新手可能买个Premium DNS会好点，不然每次捣鼓都得等半个钟头，还不知道能不能成

## 将GitHub Pages部署至个人域名

1. 进入NameSilo域名管理后台，添加`CNAME`记录将个人域名指向原地址（`xxx.github.io`）。
2. 进入GitHub Pages repo设置，pages标签页，添加Custom domain为个人域名。
如果发布源不是主分支，该操作成功后会自动向发布分支提交`CNAME`文件。
3. 等待一段时间DNS生效。（这次是35分钟内）

[Et voilà!](https://blog.yanaerobe.top)
