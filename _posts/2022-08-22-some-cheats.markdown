---
title: Some Cheats
date: 2022-08-22 22:08:37 +0800
categories: [乱抄, cheats]
tags: [cheats]     # TAG names should always be lowercase
---

# vim cheats 
*global* replacement: *%* s/foo/bar/*g*

*global* delete: *%* s/foo

delete foo rows: g/foo/d

keep only foo rows: v/foo/d

# md cheats
hashtag-space: titles

1 star: *italic*

2 stars: **bold** 

3 stars: ***bold italic*** 

2 waves: ~~strikeout~~ 

2 equals: ==highlight==

- slash-space: list

1. num-dot-space: list with num

- [ ] - [ ] : check-list

- [x] - [x] : checked-list 

> greater-space: blockquote

    4 spaces: code

square-**name**-square-bracket-**url**-bracket: [URL](https://github.com/YJY1029/container/blob/main/linux.md) 

exclamatioin-ditto: ![image](null)

# git cheats 

## new branch
JUST REMEMBER TO RENAME PARENT DIR IF DUPLICATED

## change token
 1. find old remote: git remote -v
 2. remove old remote: git remote rm foo 
 3. add new remote: git remote add origin https: //oauth2:***token***@github.com/usr/repo.git

# scp cheats 
upload /foo to /bar: scp /foo usr@ip:/bar

download: simply reverse 

-r for directory, -P for port 

# tar cheats 
create foo.tar from ./bar: tar -cf foo.tar ./bar 

decompress: tar -xf foo.tar 

-c for create, -x for decompress, -t for view contents 

-v for verbose, -f for file(always the last one)

-g for gzip2
