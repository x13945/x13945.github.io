---
title: Github Pages 配置自定义域名
date: 2017-06-24 19:34:32 +0800
categories:
  - 网络日志
tags:
  - Github Pages
  - 域名
---

<!-- toc -->

使用 github pages 的时候，我们访问的域名一般是：`用户名.github.io`.不过，我们有时候希望显示自己的个性域名，例如我的`lstec.org`.

<!-- more -->

## 步骤

### 1. 在 Github Pages 中设置自定义域名

有两种方式可以做到这个：

1. 手动在 pages 项目的根目录下新建`CNAME`文件，并添加如下内容：

```plain
lstec.org
```

由于我把 pages 放在我的二级域名下了，所以`CNAME`文件的内容就是：

```plain
blog.lstec.org
```

2. 在 github 上 pages 工程的 settings 中，配置`Custom domain`，然后 github 会自动把配置的域名添加到工程的根目录下的`CNAME`文件中。

### 2. 在自己域名的 DNS 服务商那里设置域名解析

像我这种二级域名，在 dns 那里设置的就是

| Type  | Host           | Answer           |
| ----- | -------------- | ---------------- |
| CNAME | blog.lstec.org | x13945.github.io |
