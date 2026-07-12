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
cat >> /etc/sysctl.conf << EOF
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
EOF
```
2.生效
```bash
sudo sysctl -p
```
