---
title: Ubuntu+Win10 双系统硬盘安装 Kali linux
date: 2016-01-17 00:17:44
categories:
  - 网络日志
tags:
  - Linux
  - Kali
  - Ubuntu
  - Grub2
---

<!-- toc -->

> _背景：电脑上已经装了 Win10 和 Ubuntu 双系统，但是突然脑抽了想装下 kali 看看。但是手头的 U 盘最近出了些问题，所以只好硬盘安装了。但是由于当前双系统是由 grub2 来管理启动项，而这方面的经验又比较少，所有写个日志记录下。_

<!-- more -->

## 准备工作

1. 去[这里](https://www.kali.org/downloads/)下载需要的光盘镜像，根据需求下载 64 位或者 32 位的。
2. 然后，在硬盘上划出一块空间，来安放我们的 Kali linux。

## 安装

### 1. 准备 iso 文件

把下载的镜像重命名为`kali.iso`，然后放到我硬盘的第三个分区的根目录下。

### 2. 在 grub2 中添加一个用于安装 kali linux 的启动项

在 ubuntu 下，修改/boot/grub/grub.cfg 文件，添加下面的文字：

```shell
### BEGIN new install
menuentry 'New Install' {
    set root=(hd0,3)
    set iso="/kali.iso"
    set bootoptions="findiso=$iso boot=live noconfig=sudo username=root hostname=kali quiet splash"
    search --set -f $iso
    loopback loop (hd0,3)$iso
    linux (loop)/live/vmlinuz $bootoptions
    initrd (loop)/live/initrd.img
}
### END new install
```

然后重启电脑，就可以在开机后的系统选择菜单那里看到我们刚刚添加启动项`New Install`，选择这个启动项，就开始我们的正式安装过程了。

### 3. 安装 kali linux

首先进入的是 kali 的 live cd 界面，和 ubuntu 类似，我们可以在这里试用一下 kali，然后我们就要`Applications`中找到安装程序，开始安装。由于以前已经给 ubuntu 分了一个 swap 分区，而这个分区可以让 kali 和 ubuntu 共享，那么我就把事先准备好的空白分区都划给了 kali 作为跟分区了。其他就和一般的 linux 安装没啥大差异了。

## 使用

### 安装中文输入法

这里，我们安装 fcitx 作为我们的输入法框架：

```shell
apt-get install fcitx
```

然后根据需求安装搜狗拼音或者 google 拼音都可以啦

### 自动挂载其他分区

现在，我们可以知道，我的硬盘上至少有四个分区，分别是：`Win10 C盘`，`Win10 D盘`，`Ubuntu 所在分区`，`Kali 所在分区`，而每一次进入系统后再依次手动挂载其他分区实在太麻烦，于是我们来在 fstab 中配置自动挂载这些分区。
在`/etc/fstab`文件中加入如下内容：

```shell
/dev/sdb4       /mnt/winroot         auto                        0       0
/dev/sda2       /mnt/ubunturoot   ext4   defaults                        0       0
/dev/sda3       /mnt/xg              auto                        0       0
```

> 注意：ubuntu 所在分区的配置和其他两个分区不一样

### 更新 grub2 启动项类表（可选）

有时候，我们重装完系统，windows 的启动项就找不到了，我们可以通过下面的命令更新 grub2 启动项，重新把 windows 系统启动项找回来

```shell
update-grub
```

暂时就这么多吧
