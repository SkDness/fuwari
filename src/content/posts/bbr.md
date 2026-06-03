---
title: 服务器开启BBR+FQ
published: 2026-06-03
description: BBR+FQ，上网更给力
tags: [网络]
category: 教程
draft: false
---

1.开启
```bash
echo "net.core.default_qdisc=fq" | sudo tee -a /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" | sudo tee -a /etc/sysctl.conf
```
2.生效
```bash
sudo sysctl -p
```
