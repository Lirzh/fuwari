---
title: Hydro 系列 - Raid 简单指南
published: 2026-02-26
description: "记录了 raid 的基础用法"
tags: [tools,raid,hydro]
category: tools
draft: false
---
# 这是断篇

由于资金链不足（硬盘没凑够），该篇章不想续写了。。。

# raid 介绍

[什么是磁盘阵列？15种RAID优缺点详解 · 科技宅小明](https://www.bilibili.com/video/BV1vA411W7yU/)

![raid介绍](raid-introduce.png)

以下是常见的RAID级别：

```
RAID 0：条带化（数据分块）但没有冗余，提供较高的读写性能。
RAID 1：镜像，数据完全复制到另一个驱动器，提供容错能力。
RAID 5：条带化加分布式奇偶校验，提供数据冗余和读取性能。
RAID 6：类似于RAID 5，但提供更高级别的容错能力。
RAID 10：RAID 1+0，将RAID 1镜像组合成RAID 0条带化，提供较高的容错能力和读写性能。
RAID 50：RAID 5组合成RAID 0，提供较高的性能和容错能力。
RAID 60：RAID 6组合成RAID 0，提供更高级别的性能和容错能力。
```

多的不说，因为我对速度无要求，但对容错有极高的要求，预计数据会有 600G 左右，所以选择 RAID 1。

# raid 环境

## 硬件选择

硬盘选择 3 块相同型号的希捷 1T 机械硬盘（`ST1000DM003`，运行`5.9W`/闲置`3.36W`/待机`0.63W`，读写速度能有 `210 ~ 185 MB/s`），1 块固体装系统电脑硬件选择 `i3 5100 + 4G ddr3` （很牢了）。

由于资金不足，只能选择 软Raid，也就是软件模拟 Raid，因此系统选择 `Ubuntu 24.04 LTS` （这个搭配属于很猎奇了）。

工具则选择 `mdadm` 以及 `cockpit` 。

## 性能估算

预计一下，小文件读写能力算 `100MB/s` 的话，总文件大小算 `500G` ，完整读写一次保持在 `85 minutes` 左右，后期因为会使用增量备份，时间应该不超过 `2 minutes` ，而完整拉取一次（大小算 `600G` ）耗时应该在 `102 minutes` 左右，属于能接受的范畴。

## 磁盘 URE 估算

[关于磁盘URE的担忧 · fangpsh's blog](https://fangpsh.github.io/posts/2024/2024-03-19.html)

首先，URE 的概率本身是极低的，而且我采用了 3 块硬盘做 `raid1`，正常来说 当且仅当 同时有两块及以上的硬盘在同一个扇区发生 URE 时才会造成数据损坏，就算坏了，其他数据也还是好的，而且我将其作为 题目的测试数据 的存档仓库，其实丢一两个测试数据无伤大雅，`Hydro` 会忽略掉不可用的测试数据（应该吧）。

# 具体操作

## 系统安装

这不必多说...

## mdadm 安装

```bash
sudo apt install mdadm
```

## 对应硬盘到系统中

查看所有硬盘的型号、序列号、盘符

```bash
lsblk -o NAME,SIZE,TYPE,MODEL,SERIAL
```

你会看到类似：

```bash
sda   1TB  disk  ST1000DM003-XXXX  Z1DXXXXXX
sdb   1TB  disk  ST1000DM003-XXXX  Z1DYYYYYY
sdc   1TB  disk  ST1000DM003-XXXX  Z1DZZZZZZ
```

`SERIAL` 那一列就是硬盘唯一序列号，在硬盘的标签上。
