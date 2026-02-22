---
title: Nodejs 的 Docker 指北
published: 2026-02-22
description: "记录了自用的nodejs相关docker用法"
tags: [tools,nodejs,docker]
category: tools
draft: false
---

# 版本

这是我自己选择的版本，并不保证满足所有要求，不过一般够了

| 架构      | 版本信息                     | 镜像名字 |
|----------|------------------------------|-----------------------------|
| amd64    | node24（基于 alpine）| node:24-alpine |
| arm64    | node24（基于 alpine）| node:24-alpine |
| arm32    | node22（基于 alpine）| arm32v7/node:22-alpine |
| s390x    | node24（基于 alpine）| s390x/node:24-alpine AS |
| amd32    | 不支持 | none |
| ppc64le  | node24（基于 debian）| ppc64le/node:24-slim |
| riscv64  | 要自己弄 | riscv64/ubuntu |

# Dockerfile 怎么用
'
我没有选择每一个架构都单独弄一个 'Dockerfile'，而是用环境变量决定

这是我的 'Dockerfile' 的重要部分，不过 's390x' 和 'ppc64le' 有点奇怪的兼容性问题，所以我一般会把它们注释了，应该是能用的

```yaml
# 预定义各架构的运行时镜像
FROM node:24-alpine AS runtime-amd64
FROM node:24-alpine AS runtime-arm64
FROM arm32v7/node:22-alpine AS runtime-arm
FROM s390x/node:24-alpine AS runtime-s390x
FROM ppc64le/node:24-slim AS runtime-ppc64le

# 根据 TARGETARCH 选择对应的运行时镜像
FROM runtime-${TARGETARCH} AS runtime
```

这是 'Github Action' 的关键部分
```yaml
- name: Set up QEMU
        uses: docker/setup-qemu-action@v3
        with:
          platforms: linux/amd64,linux/arm/v7,linux/arm64,linux/ppc64le,linux/s390x # 这是重点
中间省略...
- name: Extract metadata (tags, labels) for Docker
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
          tags: |
            type=raw,value=latest,enable={{is_default_branch}}
            type=ref,event=branch
            type=ref,event=pr
            # 使用从package.json提取的完整版本号
            type=raw,value=${{ steps.extract-version.outputs.full-version }}
            # 使用主版本.次版本格式
          push: ${{ github.event_name != 'pull_request' }}
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
          platforms: linux/amd64,linux/arm/v7,linux/arm64,linux/ppc64le,linux/s390x  # 这是重点
          cache-from: type=gha
          cache-to: type=gha,mode=max
```

# riscv64 的 Nodejs Docker 基础镜像

还没找到合适的，我的计划是：再解决完 's390x' 和 'ppc64le' 的兼容性问题后，自己做一个基础镜像托管到 ghcr上。

当然，如果官方有的话，那肯定是万事大吉了