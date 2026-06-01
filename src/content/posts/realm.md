---
title: Realm流量转发安装教程
published: 2026-06-01
description: 流量转发，一看就会
tags: [网络]
category: 教程
draft: false
---

# 创建一个专门的目录并进入
```
mkdir -p /etc/realm && cd /etc/realm
```

# 下载官方编译好的最新稳定版（适用于绝大多数 Linux 服务器）
```
wget https://github.com/zhboner/realm/releases/latest/download/realm-x86_64-unknown-linux-gnu.tar.gz
```

# 解压并赋予执行权限
```
tar -xvf realm-x86_64-unknown-linux-gnu.tar.gz
```
```
chmod +x realm
```
# 把 realm 复制到系统全局路径，方便直接调用
```
cp realm /usr/local/bin/
```
# 创建并编辑配置文件在/etc/realm 目录下创建一个名为 config.toml 的配置文件
```
nano /etc/realm/config.toml
```
# 把下面的内容粘贴进去。注意：请把 2.2.2.2:443 修改为你真实的节点 B 的 IP 和端口！
```
[network]
no_delay = true

[[endpoints]]
listen = "0.0.0.0:54321"
remote = "111.111.111.111:12345"
```
(粘贴完成后，按 Ctrl + O 保存，按 Enter 确认，再按 Ctrl + X 退出 nano 编辑器)
# 配置 Systemd 开机自启服务（强烈推荐）为了防止服务器重启后中转失效，我们把它做成系统服务：
```
nano /etc/systemd/system/realm.service
```
粘贴以下内容：
```
[Unit]
Description=Realm Port Forwarding Service
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/etc/realm
ExecStart=/usr/local/bin/realm -c /etc/realm/config.toml
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```
保存并退出
# 启动并检查服务
```
systemctl daemon-reload
```

```
systemctl enable --now realm
```

```
systemctl status realm
```
# 重要提醒（放行防火墙）： > 很多服务商（如甲骨文、外包 VPS）有系统防火墙，请务必在节点 A 上放行你监听的端口（如 54321）的 TCP 和 UDP 流量。如果是用 ufw，运行：
```
ufw allow 54321
```