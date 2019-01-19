---
title: Android+Gradle+Jenkins持续集成
tags:
  - Android
  - Gradle
  - Jenkins
---

## 1.准备工作

1. 下载 tomcat
2. 下载 jenkins[这里](https://jenkins.io/)

## 2.启动 jenkins

将下载的 jenkins.war 包直接放到 tomcat 下的 webapps 目录，启动 tomcat 即可安装完成。

## 3.配置 jenkins

从[http://localhost:8080/jenkins](http://localhost:8080/jenkins)访问 jenkins.第一次启动,为了验证是本人操作,会让输入一个验证密钥.位置就在本机上:

```shell
╰$ cat /home/xiao/.jenkins/secrets/initialAdminPassword
```

然后,就会提示安装一些插件,如果不是很了解,可以选择"安装推荐插件",或者自己手动选取需要安装的插件.然后开始安装,这个时间或比较长,安心等待.
