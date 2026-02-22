---
title: Nodejs 简单指南
published: 2026-02-21
description: "记录了自用的nodejs相关脚本"
tags: [tools，nodejs]
category: tools
draft: false
---

:::note
以下都会保持用户一致性，即与非 执行命令的用户 无关
:::

# 安装

[官方网址](https://nodejs.org/zh-cn/download)

下面是我自己用的脚本

```bash
# 下载并安装 nvm：
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
# 代替重启 shell
\. "$HOME/.nvm/nvm.sh"
# 下载并安装 Node.js：
nvm install 24
# 下载并安装 Yarn:
corepack enable yarn
# 下载并安装 pnpm：
corepack enable pnpm
# 验证 pnpm 版本：
pnpm -v
# 验证 Yarn 版本：
yarn -v
# 验证 npm 版本：
npm -v # Should print "11.8.0".
# 验证 Node.js 版本：
node -v # Should print "v24.13.1".
```

# 换源

我选择了淘宝源

```bash
# npm 换源
npm config set registry https://registry.npm.taobao.org
# yarn 换源
yarn config set registry https://registry.npmmirror.com
# pnpm 换源
pnpm config set registry https://registry.npmmirror.com
```