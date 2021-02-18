---
title: 用youtube-dl下载油管视频
date: 2021-02-18 11:03:39
categories:
  - 网络日志
tags:
  - Youtube
  - 油管
  - youtube-dl
---

### 简介

youtube-dl 是一个用python开发的命令行工具，可以用来下载油管上的视频

### 使用

### 1. 选择视频格式和分辨率

视频被上传到油管之后，会被转换成多种格式和分辨率。我们在下载的时候，需要指定特定的分辨率。可以用下面这两个命令查看格式：

```bash
youtube-dl -F [url]
# or
youtube-dl --list-formats [url]
```

输出的内容大致如下：

```bash
[info] Available formats for YkUgNrW3j6U:
format code  extension  resolution note
139          m4a        audio only DASH audio   50k , m4a_dash container, mp4a.40.5 (22050Hz), 7.34MiB
251          webm       audio only tiny  106k , opus @106k (48000Hz), 16.08MiB
140          m4a        audio only tiny  129k , mp4a.40.2@129k (44100Hz), 19.49MiB
278          webm       256x144    DASH video   95k , webm_dash container, vp9, 30fps, video only
18           mp4        640x360    360p  215k , avc1.42001E, 30fps, mp4a.40.2 (44100Hz), 32.49MiB
22           mp4        1280x720   720p  370k , avc1.64001F, 30fps, mp4a.40.2 (44100Hz) (best)
```

### 2. 下载特定分辨率的视频

根据上面的输出，就可以用`-f`参数指定特定分辨率进行下载了。

```bash
youtube-dl -f 137 https://www.youtube.com/playlist\?list\=PL54herq3DAICshHvaJlpZ6QOvvC4_JP2m
```

