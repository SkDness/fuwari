---
title: Ubuntu/Debian服务器安装Docker
published: 2026-06-09
description: 安装Docker
tags: [docker]
category: 教程
draft: false
---


Ubuntu/Debian安装Docker
1. **安装Docker**
```bash
wget -qO- get.docker.com | bash
```
2.  **查看Docker版本**
```bash
docker version
```
3.  **启动 Docker 服务**
```bash
systemctl start docker
```
4.  **Docker开机自启动**
```bash
systemctl enable docker
```
5.  **安装Docker compose**
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
``` 
6.  **赋予执行权限**
```bash
sudo chmod +x /usr/local/bin/docker-compose
```
7.  **查看docker-compose 版本**
```bash
docker-compose --version
```

