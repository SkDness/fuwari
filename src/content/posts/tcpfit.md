---
title: TCPfit网络调优
published: 2026-09-14
description: 服务器网络调优
tags: [网络]
category: 教程
draft: false
---


```bash
bash <(curl -fsSL https://raw.githubusercontent.com/Kylin010/tcpfit/main/tcpfit.sh)
```
跑完出菜单，选 `1` 全自动。只问三个问题：

1. **带宽多少** —— 不想扫拐点就填 `0`，已知限速值输入 `m` 直接指定
2. **测速对端** —— 回车用免费公共节点，或填自己另一台机器的 IP
3. **机器用途** —— 代理 / 大文件传输
装好之后敲 `tcpfit` 进菜单。