---
title: 中望3D Linux 简单指南
published: 2026-04-6
description: "记录了在 Ubuntu 上使用 中望3D Linux 的一些问题"
tags: [tools,3d]
category: tools
draft: false
---

## 下载

[中望3D Linux](https://www.zwsoft.cn/product/zw3d/linux#downfile)

下载 统信UOSV20/深度V20 的版本。

## 安装

```bash
apt install ./zw3d-linux-20.04.0.0.deb # 名字可能会不同
```

安装完先别启动，因为是 Ubuntu ，中望 3D 自带的 libfreetype 库版本太老，和系统库冲突了，所以要改一下 libfreetype 库再用。

```bash
sudo mv /opt/apps/com.zwsoft.zw3d2026/files/lib3rd/libfreetype.so.6 /opt/apps/com.zwsoft.zw3d2026/files/lib3rd/libfreetype.so.6.bak
```
