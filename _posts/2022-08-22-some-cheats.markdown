---
title: Some Cheats
date: 2022-08-22 22:08:37 +0800
categories: [笔记, cheats]
tags: [cheats]     # TAG names should always be lowercase
---

> Adding & removing based on my personal memory.
{:.prompt-info}

## md cheats

2 equals: ==highlight==

- slash-space: list

\{:.prompt-tip/info/warning/danger}

    4 spaces: code

## Python venv

```shell
# virtual env creation
py -m venv $env_name

# activation, check & deactivate
source $env_name/bin/activate
echo $VIRTUAL_ENV
deactivate

# print current packages
pip3 freeze > requirements.txt
```

## git cheats

Remember to rename parent directory if duplicated.

rebase.false: traditional merge

rebase.true: concatenate dev commits after main

## [git-filter-repo](https://github.com/newren/git-filter-repo)

*Recommend install via package manager*

```shell
# Analysis is also used in online repo cleanup
git-filter-repo --analyze

# Choose specific files and filter history
# Multiple paths should be specified separately
git-filter-repo --path <dir_or_file> --path <dir_or_file>

# Filter out specific files and filter history
git-filter-repo --path <dir_or_file> --invert-paths
```

## git subtree

```shell
# Under top-level repo directory
# --prefix= -P

# Suggest add subtree upstream
git remote add subtree_upstream subtree_upstream_url

# To split a dir into a subtree branch
git subtree split --prefix=subdir -b subtree_branch

# To add a subtree to this repo
git subtree add --prefix=subdir subtree_upstream subtree_branch

# To pull from/push to a subtree
# The working tree shall be very clean
git subtree pull/push --prefix=subdir subtree_upstream subtree_branch
```

## ssh-keygen

`ssh-keygen -t ed25519 -C "<comment>"`

`vim .ssh/id_ed25510.pub`

Although `ssh -T url` is ususally useful in testing and adding unknwon hosts, this is not strictly equal to `git clone` requests in that `ssh` (possibly) will call out a virtual terminal.

## scp cheats

upload /foo to /bar: `scp /foo usr@ip:/bar`

download: simply reverse

-r for directory, -P for port

## tar cheats

> Would recommend using shell plugins instead
{:.prompt-tip}

create foo.tar from ./bar: `tar -cf foo.tar ./bar`

decompress: `tar -xf foo.tar`

-c for create, -x for decompress, -t for view contents

-v for verbose, -f for file(always the last one)

-g for gzip2
