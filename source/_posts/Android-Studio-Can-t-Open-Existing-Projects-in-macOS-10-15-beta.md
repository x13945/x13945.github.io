---
title: Android Studio Can't Open Existing Projects in macOS 10.15 beta
date: 2019-08-07 18:19:16
categories:
  - 网络日志
tags:
  - macOS
  - macOS 10.15 beta
  - macOS Catalina
---
![](https://raw.githubusercontent.com/x13945/image-bucket/master/img/jamie-street-hBzrr6m6-pc-unsplash.jpg)

又到了今年的七(hua)夕(qian)之夜，先祝大家节日快乐。**：）**

最近呀，有些使用**Mac**开发`Android`的小伙伴会发现如下现象：升级`macOS Catalina 10.15beta`版本后，你的`Android Studio`既无法打开现有工程，也没办法导入工程到`Android Studio`了。这个问题在`Android Studio 3.5 RC 2`和`Android Studio 3.4.`版本中均是**百分百**出现。

至今，广大网友也不知道这个锅应该是`macOS`的开发团队，还是`Android Studio`的开发团队来背了。（咱也不知道，咱也不敢问 **XD**）

百般捣鼓之后，我试出了一个权宜办法，就是**在命令行中打开现有工程**。

这个办法有两种方式来实现：

### 1. 用`Android Studio`自带的`command-line launcher`打开现有工程

命令如下：

```shell
$ studio "project的位置"
```

### 2. 用`Mac`自带的`open`命令来打开现有工程

命令如下：

```shell
$ open -a /Applications/Android\ Studio.app "project的位置"
或者是下面这种
$ open -a /Applications/Android\ Studio\ 3.5\ Preview.app "project的位置"
```

### 结语

今天的文章到这里就结束了。不过有些小伙伴会说：博主只提供了打开现有工程的办法，怎么没有说怎么解决无法导入工程的问题呀。原因就是，博主要过七夕呀，没有这么多时间来试探这个问题了。而且，当前的解决办法，应该已经可以满足一小撮遇到这个问题的小伙伴快乐的**过(qiao)七(dai)夕(ma)**了。如果想要追踪这个这俩问题的进度，可以关注这个问题的回复情况[Android Studio: Can't Open Existing Projects - Stack Overflow](https://stackoverflow.com/questions/57361744/android-studio-cant-open-existing-projects)
