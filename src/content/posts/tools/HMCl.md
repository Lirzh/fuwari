---
title: HMCL 简单指南
published: 2026-07-11
description: "记录了在 Debian 上使用 HMCL 的一些问题"
tags: [games,mc,hmcl]
category: games
draft: false
---

# 选择

PCL 2 官方版本并不支持 Linux，而社区版又没必要，所以选择使用 HMCL。

# 下载

本来是使用 hmcl.jar 和 自己编写的 .desktop 将其装成一个应用。

后来发现有 .deb 包，所以就用这个了。

::github{repo="HMCL-dev/HMCL"}

前往 [HMCL-dev/HMCL 的最新版本](httpshttps://github.com/HMCL-dev/HMCL/releases/latest) 里找最新的 .deb 包。

# 安装

都用 Linux 了，那应该都会使用 apt 或 dpkg 安装。

# 启动

可能有人会问，这一部分存在的意义是什么？不是直接启动 HMCL 吗？

没错，但是如果你使用的窗口系统是 Wayland 而非 X11，那么你的鼠标指针可能会出现一些问题，即指针会跑出游戏窗口。

所以，使用 X11 ~~或 全屏游玩（可能也有问题）~~ 吧。