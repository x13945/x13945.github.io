---
title: Ubuntu+Nginx证书续签
tags:
  - Ubuntu
  - Nginx
  - Let's Entrypt
  - acme
categories:
  - 网络日志
---


## 步骤

### 1. 停用 nginx

```plain
nginx -s quit
```



### 2. 生成证书

```plain
acme.sh --issue --standalone -d lstec.org -d happy.lstec.org -d pan.lstec.org -d l2d.lstec.org -d l2y.lstec.org -d tj.lstec.org --force
```

### 3. 安装证书

```plain
acme.sh  --installcert -d lstec.org -d happy.lstec.org -d pan.lstec.org -d l2d.lstec.org -d l2y.lstec.org -d tj.lstec.org  --key-file /etc/nginx/ssl/lstec.org.key --fullchain-file /etc/nginx/ssl/fullchain.cer --reloadcmd  "service nginx force-reload"
```

### 4. 重启服务

```plain
sudo service nginx restart
```

