---
title: Some Cheats
date: 2022-08-22 22:08:37 +0800
categories: [笔记, cheats]
tags: [cheats]     # TAG names should always be lowercase
---

## vim cheats 
*global* replacement: `%s/foo/bar/g`

*global* delete: `%s/foo`

delete foo rows: `g/foo/d`

keep only foo rows: `v/foo/d`

## md cheats
2 waves: ~~strikeout~~ 

2 equals: ==highlight==

- slash-space: list

- [ ] - [ ] : check-list

- [x] - [x] : checked-list 

> greater-space:blockquote

\{:.prompt-tip/info/warning/danger}

    4 spaces: code

square-**name**-square-bracket-**url**-bracket: [URL](https://github.com/YJY1029/container/blob/main/linux.md)

exclamatioin-ditto: ![image](null)

## git cheats 

Remember to rename parent directory if duplicated. 

`git commit --amend -m "xxx" && git push -uf origin`: extremely useful to one-time forcifully fix last push. 

rebase.false: traditional merge

rebase.true: concatenate dev commits after main

## ssh-keygen

`ssh-keygen -t ed25519 -C "<comment>"`

`vim .ssh/id_ed25510.pub`

Although `ssh -T url` is ususally useful in testing and adding unknwon hosts, this is not strictly equal to `git clone` requests in that `ssh` (possibly) will call out a virtual terminal. 

## scp cheats 
upload /foo to /bar: `scp /foo usr@ip:/bar`

download: simply reverse 

-r for directory, -P for port 

## tar cheats 
create foo.tar from ./bar: `tar -cf foo.tar ./bar` 

decompress: `tar -xf foo.tar` 

-c for create, -x for decompress, -t for view contents 

-v for verbose, -f for file(always the last one)

-g for gzip2
