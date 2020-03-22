# x13945.github.io

这是蹲墙角的猫放置个人博客的地方，或者说是一个树洞。

<!-- TOC -->

- [x13945.github.io](#x13945githubio)
  - [常用命令](#%e5%b8%b8%e7%94%a8%e5%91%bd%e4%bb%a4)
    - [1. 在本地查看博客](#1-%e5%9c%a8%e6%9c%ac%e5%9c%b0%e6%9f%a5%e7%9c%8b%e5%8d%9a%e5%ae%a2)
      - [1. 查看博客，不包括草稿箱](#1-%e6%9f%a5%e7%9c%8b%e5%8d%9a%e5%ae%a2%e4%b8%8d%e5%8c%85%e6%8b%ac%e8%8d%89%e7%a8%bf%e7%ae%b1)
      - [2. 查看博客，包括草稿箱](#2-%e6%9f%a5%e7%9c%8b%e5%8d%9a%e5%ae%a2%e5%8c%85%e6%8b%ac%e8%8d%89%e7%a8%bf%e7%ae%b1)
    - [2. 新建草稿](#2-%e6%96%b0%e5%bb%ba%e8%8d%89%e7%a8%bf)
    - [3. 新建文章](#3-%e6%96%b0%e5%bb%ba%e6%96%87%e7%ab%a0)
- [FAQ](#faq)

<!-- /TOC -->

## 常用命令

由于该博客是用过`hexo`来生成静态文件的，所以有一些常用命令需要谨记

### 1. 在本地查看博客

#### 1. 查看博客，不包括草稿箱

```shell
npm start
```

#### 2. 查看博客，包括草稿箱

```shell
npm run dev
```

### 2. 新建草稿

草稿箱的位置在`$PROJECT_DIR/source/_drafts`，当我们的文章还处于未完成时，可以暂时把文章放到草稿箱中。新建草稿的命令是：

```shell
hexo new draft 文章标题
```

> 注：如果标题中有空格，则会自动加上引号

### 3. 新建文章

当我们想要发表一篇文章的时候，可以通过下面的命令创建一篇文章，这样的文章会被自动编译成 `html` 格式放到博客站中

```shell
hexo new 文章标题
```

# FAQ

1. 使用 hexo 命令碰到如下的异常应该怎么办：

   ```shell
   command not found: hexo
   ```

   解决办法：通过下面的命令安装`hexo`

   ```shell
   npm install hexo-cli -g
   ```
