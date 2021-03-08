---
title: Mac安装OpenJDK
date: 2021-03-08 12:03:27
tags:
	- macOS
	- Java
	- brew
categories:
	- 网络日志
---

## 前言

由于工作需要，需要在 Mac 系统中安装多个版本的`JDK`，并且需要可以方便的版本切换。

找了半天方案，最终还是选择 `AdoptOpenJDK` 作为`JDK`的载体。然后用`Homebrew`来管理它的升级、卸载等。

<!-- more -->

## 安装

### Requirement

- MacOS
- Homebrew [The Missing Package Manager for macOS (or Linux) — Homebrew](https://brew.sh/)

### 步骤

#### 1. 只使用最新版本

如果对 JDK 的版本没有要求，而且想要 JDK 可以自动更新到最新，可以直接使用下面的命令安装

```zsh
$ brew install --cask adoptopenjdk
```

#### 2. 需要特定版本或者多个版本

1. 为`brew`安装`AdoptOpenJDK`的库

   这样，我们就可以用`brew`来安装`AdoptOpenJDK`库下的`OpenJDK`的任意版本了。

   ```
   brew tap AdoptOpenJDK/openjdk
   ```

2. 安装自己需要的`JDK`

   ```
   brew install --cask adoptopenjdk14
   ```

   至于可用的版本号，可以查询官方文档。或者使用`brew search adoptopenjdk`来检索。

#### 3. 管理多个版本

当我们在 Mac 上安装多个版本的 JDK 的时候，系统会默认使用最新的版本。因此我们可以用`java_home`命令在多个版本之间切换。为了便于操作，我们可以在 shell 的配置文件中添加一个 `jdk` 函数，用于快捷切换.

1.  在 `~/.bashrc` 或者 `~/.zshrc`中，添加下面的代码（如果你用的是`bash`，就修改`bashrc`；如果用的是`zsh`，则需要修改`zshrc`）

```shell
jdk() {
      version=$1
      export JAVA_HOME=$(/usr/libexec/java_home -v"$version");
      java -version
}
```

2.  通过`source`命令，把上面的修改生效

3.  在命令后中，直接通过 `jdk`命令，切换版本

```shell
jdk 1.8
# 或者
jdk 9
```
