---
title: Yarn使用手册
date: 2021-02-18 11:46:11
categories:
  - 网络日志
tags:
  - Yarn
  - Node.js
  - JavaScript
  - JS
---

## 简介

Yarn 是npm的一个替代工具，具有并发下载等功能。

## 使用

### 查看帮助文档

可以使用 help 命令查看 Yarn 的帮助文档

``` 
yarn help # 查看帮助文档的简介

yarn help [command] # 查看特定 command 的帮助文档
```



### 升级依赖

我们通常可以用`upgrade` 来升级依赖，但是这个命令默认只会根据`package.json`中定义的版本号，来更新版本依赖。但是如果想要把依赖更新到最新版本，则需要加上 `--latest` 或者 `-L`参数，让 Yarn 更新package.json中的版本号。

```bash
yarn upgrade -L
```

