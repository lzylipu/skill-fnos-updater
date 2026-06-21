---
name: fnos-openclaw-updater
description: "飞牛NAS应用中心版OpenClaw安全更新到最新版本。触发词：更新、激活"
metadata:
  trigger: "更新|升级龙虾|更新龙虾|update openclaw"
---

# 飞牛 OpenClaw 更新技能

将飞牛NAS应用中心安装的 OpenClaw（managed-openclaw）安全更新到 npm 最新版。

## 触发词

- 更新 / 激活
- 升级龙虾 / 更新龙虾
- update openclaw

## 前提条件

1. **飞牛 NAS 应用中心**安装的 OpenClaw
2. openclaw 主程序在 `/vol1/@apphome/trim.openclaw/data/openclaw/node_modules/`
3. npm registry：`https://registry.npmmirror.com/`

## 安全路线

**不修改飞牛配置：**
- `/vol1/@appcenter/trim.openclaw/config/openclaw-version.env`
- `/var/apps/trim.openclaw/cmd/`
- `/vol1/@appcenter/trim.openclaw/server/`

**只修改：**
- `/vol1/@apphome/trim.openclaw/data/openclaw/package.json`
- `/vol1/@apphome/trim.openclaw/data/openclaw/node_modules/openclaw/`

## 更新流程

### 1. 检查版本
```bash
/vol1/@apphome/trim.openclaw/data/openclaw/node_modules/.bin/openclaw --version
npm view openclaw version --registry=https://registry.npmmirror.com
```

### 2. 安装最新版
```bash
cd /vol1/@apphome/trim.openclaw/data/openclaw
npm install openclaw@latest --registry=https://registry.npmmirror.com
```

### 3. 重启生效
```bash
# 找到 openclaw 进程 PID
ps aux | grep openclaw | grep -v grep | grep -v "trim_server\|trim_open"
# 发送 SIGTERM 优雅退出（飞牛 server 自动重启子进程）
kill -TERM <PID>
```

或用飞牛应用中心 → OpenClaw → 停止→启动。

### 4. 验证
```bash
/vol1/@apphome/trim.openclaw/data/openclaw/node_modules/.bin/openclaw --version
```

## 回滚
```bash
cd /vol1/@apphome/trim.openclaw/data/openclaw
# 改 package.json 版本为旧版
npm install --registry=https://registry.npmmirror.com
# 重启同上
```