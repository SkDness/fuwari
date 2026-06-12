---
title: Emby+OpenList+MediaWarp实现网盘320播放
published: 2026-06-13
description: Emby网盘302播放
tags: [影音]
category: 教程
draft: false
---


> 教程基于Linux Debian/Ubuntu系统
1. 安装
- 新建文件夹
```bash
sudo mkdir -p /usr/local/bin/mediawarp/config
```
- 打开文件夹
```bash
cd /usr/local/bin/mediawarp
```
- 下载文件，解压文件，赋予权限
```bash
wget https://github.com/AkimioJR/MediaWarp/releases/download/v0.2.4/MediaWarp_0.2.4_linux_amd64.tar.gz
```
```bash
tar -zxvf MediaWarp_0.2.4_linux_amd64.tar.gz
```
```bash
mv MediaWarp mediawarp
```
```bash
sudo chmod +x mediawarp
```
- 删除安装包
```bash
sudo rm MediaWarp_0.2.4_linux_amd64.tar.gz
```
2. 配置文件
- 新建配置文件
```bash
sudo nano /usr/local/bin/mediawarp/config/config.yaml
```
- 输入
```yaml
port: 9999

server:
  type: Emby
  addr: http://127.0.0.1:8096
  auth: 你的Emby API秘钥

log:
  access:
    console: true
    file: false
  service:
    console: true
    file: true

cache:
  enable: true
  http_strm_ttl: 1h
  image_ttl: 10m
  subtitle_ttl: 2h

http_strm:
  enable: true
  proxy: false
  final_url: true
  prefix_list:
    - /media/strm     # 改成你emby媒体库的路径

alist_strm:
  enable: false

web:
  enable: false

client:
  enable: false

subtitle:
  enable: false
```
- 保存退出
按`Ctrl+O`保存，然后按`Ctrl+X`退出
3. 配置生效 & 持久化
- 注册为系统服务
```bash
sudo nano /etc/systemd/system/mediawarp.service
```
- 填入:
```Ini
[Unit]
Description=MediaWarp
After=network.target

[Service]
ExecStart=/usr/local/bin/mediawarp/mediawarp
WorkingDirectory=/usr/local/bin/mediawarp
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```
4. 启动
```bash
sudo systemctl daemon-reload
```
```bash
sudo systemctl enable mediawarp
```
```bash
sudo systemctl start mediawarp
```
- 可以用下边的命令看下是否运行正常
```bash
sudo systemctl status mediawarp
```
5. 使用
- Emby正常使用，端口从8096改为前边设置的9999即可