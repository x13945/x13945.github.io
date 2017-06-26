---
layout: single
title:  "Github Pages配置自定义域名"
date:   2017-06-24 19:34:32 +0800
categories: Github
---
使用github pages的时候，我们访问的域名一般是：`用户名.github.io`.不过，我们有时候希望显示自己的个性域名，例如我的`lstec.org`.

## 步骤

### 1. 在Github Pages中设置自定义域名
有两种方式可以做到这个：

1. 手动在pages项目的根目录下新建`CNAME`文件，并添加如下内容：
```
lstec.org
```
由于我把pages放在我的二级域名下了，所以`CNAME`文件的内容就是：
```
blog.lstec.org
```
2. 在github上pages工程的settings中，配置`Custom domain`，然后github会自动把配置的域名添加到工程的根目录下的`CNAME`文件中。

### 2. 在自己域名的DNS服务商那里设置域名解析 
像我这种二级域名，在dns那里设置的就是

|Type |Host          |Answer          |
|-----|--------------|----------------|
|CNAME|blog.lstec.org|x13945.github.io|
