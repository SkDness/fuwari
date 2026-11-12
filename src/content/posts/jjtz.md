---
title: 极简探针安装文档
published: 2026-11-13
description: 装个探针，以针会友
tags: [探针]
category: 教程
draft: false
---

# 安装

<details>
<summary>本页内容</summary>

- [1. 装 hub](#1-装-hub)
  - [一键脚本](#一键脚本)
  - [Docker](#docker)
- [2. 配反向代理](#2-配反向代理)
- [3. 进面板](#3-进面板)
- [4. 接入节点](#4-接入节点)

</details>

## 1. 装 hub

### 一键脚本

需要 systemd（Debian、Ubuntu、RHEL 系等）。Alpine 这类 OpenRC 系统用下面的 Docker。

```bash
curl -fsSL -o install-hub.sh \
  https://github.com/monitor-probe/monitor/releases/latest/download/install-hub.sh
chmod +x install-hub.sh
sudo ./install-hub.sh
```

菜单里选「安装 / 升级」，端口回车即用默认的 28080。装完显示应急密码，记下来。参数、目录与升级见安装 hub。

### Docker

```bash
docker run -d --name monitor --restart unless-stopped \
  -p 127.0.0.1:28080:28080 -v monitor-data:/data -e TZ=Asia/Shanghai \
  stqfdyr/monitor
```

TZ 设成 hub 所在的时区。应急密码在容器日志里：

```bash
docker logs monitor | grep Emergency
```

compose 写法见 Docker 部署。密码忘了见重置应急密码。

这时面板还打不开：hub 只在本机监听，公网访问不到。下一步配反向代理。

## 2. 配反向代理

用 caddy 的话，Caddyfile 里加三行：

```caddyfile
hub.example.com {
    reverse_proxy 127.0.0.1:28080
}
```

nginx、宝塔、Cloudflare 隧道的写法，以及四项必需的设置，见反向代理。

hub 的参数不用改：面板按浏览器地址栏里的地址生成安装命令，域名通了，命令就是对的。

## 3. 进面板

- 打开 `https://hub.example.com/admin`，用应急密码登录。
- 安全页改掉应急密码，按需配 GitHub 单点登录，见登录与安全
- 设置页填站点名称、上传站点图标，决定公开状态页是否开放

## 4. 接入节点

节点页点「添加节点」填一个名字，再点这一行的安装按钮（下载图标），复制命令到被监控的机器上以 root 执行，几秒后节点上线。一次装很多台用批量安装。
