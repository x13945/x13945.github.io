---
title: 使用NodeJs递归清理本地Git仓库
date: 2019-01-19 19:05:32 +0800
categories:
  - 网络日志
tags:
  - NodeJs
  - Git
---

<!-- TOC -->

- [背景](#背景)
- [工作环境](#工作环境)
- [方案](#方案)
  - [解决思路](#解决思路)
  - [工具](#工具)
  - [步骤](#步骤)
    - [1.找出所有`.git`文件夹的位置](#1找出所有git文件夹的位置)
    - [2.获得仓库位置](#2获得仓库位置)
    - [3.清理仓库](#3清理仓库)
- [结语](#结语)

<!-- /TOC -->

## 背景

由于常年混迹`Github`，所以在我电脑上有很多 clone 下的`Git Repo`，而这些 repo 使用中生成的临时文件占用了大量空间。粗略看了下空间占用，居然有`23G`。所以决定通过`git clean`命令把每一个仓库清理一下。但是先进入每一个仓库，然后执行上面的命令就太 low 了，于是决定写个脚本处理一下。最近 nodejs 用的多一些，因此决定用 nodejs 来处理这件事。

<!-- more -->

## 工作环境

我的电脑是 mac 系统，理论上这个解决方案也可以在 linux 和 win10 中的 linux 子系统中运行。

## 方案

### 解决思路

鉴于每个`Git Repo`的根目录中，都有一个名字叫做`.git`的文件夹。因此可以通过查找`.git`文件夹的位置，间接知道`Git Repo`的位置，类似下面这种：

```shell
/a/b/repo1/.git
/z/repo2.git
/repo3/.git
```

之后进入每个`Git Repo`,执行 `git clean`命令。

### 工具

- `NodeJs`中的`child_process`。用于在 js 中执行`unix`系统的命令行程序
- `NodeJs`中的`path`。用于处理路径
- `find`命令。用于查找文件位置
- `cd`命令。用于切换执行`unix`命令的目录位置
- `git`命令。 用于执行`git clean`命令

### 步骤

#### 1.找出所有`.git`文件夹的位置

通过`child_process`， 执行`find . -type d -name .git`命令，。

```javascript
const process = require("child_process");

const find = process.spawn("find", ". -type d -name .git".split(" "));

find.stdout.on("data", data => {

  // dirs中包含所有.git文件夹的位置
  const dirs = data.toString().split(/\r?\n/));
});

find.stderr.on("data", data => {
  console.log(`stderr: ${data}`);
});

find.on("close", code => {
  console.log(`child process exited with code ${code}`);
});
```

最后得到的`dirs`是一个字符串数组，包含所有找到的`.git`文件夹的位置，类似`['/a/b/repo1/.git', '/b/c/repo2/.git']`

#### 2.获得仓库位置

通过`path`获得`.git`目录所在`Git Repo`的路径

```javascript
for (const i of dirs) {
  const repo = path.dirname(i);
}
```

现在得到的`repo`变量中存储的就是`Git Repo`的路径

#### 3.清理仓库

切换到`repo`目录，执行`git clean -xdf` 命令

```javascript
const cleanRes = process.exec(
  "cd " + repo + " && git clean -xdf .",
  {},
  (error, stdout, stderr) => {
    console.log(`\nTry to clean up ${repo} by: '${cleanCommand}'`);
    if (error) {
      console.log(`error: ${error}`);
    } else {
      console.log(stdout);
    }
  }
);
```

## 结语

思路和解决方案都比较简单，本文仅作为记录。完整代码被我放到[这里](https://gist.github.com/44492b93fc37e3902f725dfd7bd981fb.git)了。想要使用的同学可以把这个文件放到你要清理的文件夹下，然后用`node`执行即可。
