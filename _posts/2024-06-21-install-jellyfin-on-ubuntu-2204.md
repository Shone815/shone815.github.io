---
layout: post
title: "Ubuntu 2204 安装 配置Jellyfin"
subtitle: "jellyfin媒体服务器 配置"
author: "Shone815"
header-img: "img/2024-06-21_bg.jpg"
catalog: true
tags:
  - Ubuntu
  - NAS
  - Jellyfin
---

## 安装 Jellyfin
```
sudo apt install software-properties-common apt-transport-https ca-certificates gnupg curl -y
sudo add-apt-repository universe
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://repo.jellyfin.org/jellyfin_team.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/jellyfin.gpg
```

下面是一个命令
```
cat <<EOF | sudo tee /etc/apt/sources.list.d/jellyfin.sources
Types: deb
URIs: https://repo.jellyfin.org/$( awk -F'=' '/^ID=/{ print $NF }' /etc/os-release )
Suites: $( awk -F'=' '/^VERSION_CODENAME=/{ print $NF }' /etc/os-release )
Components: main
Architectures: $( dpkg --print-architecture )
Signed-By: /etc/apt/keyrings/jellyfin.gpg
EOF
```

接着
```
sudo apt update
sudo apt install jellyfin
sudo systemctl is-enabled jellyfin
sudo systemctl status jellyfin
```

若有报错，则需要重新启动jellyfin
```
sudo systemctl restart jellyfin
sudo systemctl status jellyfin
```

可以看到jellyfin是active状态，然后可以用浏览器打开127.0.0.1:8096 登录jellyfin网页。

## 生成SSL 证书
需要域名，暂时还没有，略过

## 问题
1. 若jellyfin无法访问/media/xxx/, 则考虑给予jellyfin相应权限
```
sudo chown -R jellyfin:jellyfin /media/shone
sudo systemctl restart jellyfin
```

## 参考
[如何在 Ubuntu 22.04 上安装 Jellyfin 媒体服务器](https://cn.linux-console.net/?p=30604)
