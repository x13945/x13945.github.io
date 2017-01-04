# Android+Gradle+Jenkins持续集成
[TOC]

# 1.准备工作
1. 下载tomcat
2. 下载jenkins[这里](https://jenkins.io/)

# 2.启动jenkins
将下载的jenkins.war包直接放到tomcat下的webapps目录，启动tomcat即可安装完成。

# 3.配置jenkins
从[http://localhost:8080/jenkins](http://localhost:8080/jenkins)访问jenkins.第一次启动,为了验证是本人操作,会让输入一个验证密钥.位置就在本机上:
```shell
╰$ cat /home/xiao/.jenkins/secrets/initialAdminPassword
```
然后,就会提示安装一些插件,如果不是很了解,可以选择"安装推荐插件",或者自己手动选取需要安装的插件.然后开始安装,这个时间或比较长,安心等待.