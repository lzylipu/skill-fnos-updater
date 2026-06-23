---
name: skill-fnos-updater
description: "Update Hermes Agent on fnOS NAS App Center to latest npm version safely"
version: 1.0.0
author: lzylipu
license: MIT
platforms: [linux]
prerequisites:
  env_vars: [OPENCLAW_HOME]
  services:
    - name: fnOS NAS
      description: "fnOS App Center with managed OpenClaw installation"
metadata:
  hermes:
    tags: [fnos, hermes, update, nas, npm, 更新]
    related_skills: []
    homepage: https://github.com/lzylipu/skill-fnos-updater
    category: personal
    skill_type: automation
---

# 飞牛 OpenClaw 更新技能

将飞牛NAS应用中心安装的 OpenClaw（managed-openclaw）安全更新到 npm 最新版。

## 触发词

- 更新 / 激活
- 升级龙虾 / 更新龙虾
- update openclaw

## 前提条件

1. **飞牛 NAS 应用中心**安装的 OpenClaw
2. openclaw 主程序在 `${OPENCLAW_HOME}/openclaw/node_modules/`
3. npm registry：`https://registry.npmmirror.com/`

## 安全路线

**不修改飞牛配置：**
- `${OPENCLAW_CONFIG}/openclaw-version.env`
- `${OPENCLAW_CMD}/`
- `${OPENCLAW_SERVER}/`

**只修改：**
- `${OPENCLAW_HOME}/openclaw/package.json`
- `${OPENCLAW_HOME}/openclaw/node_modules/openclaw/`

## 更新流程

### 1. 检查版本
```bash
${OPENCLAW_HOME}/openclaw/node_modules/.bin/openclaw --version
npm view openclaw version --registry=https://registry.npmmirror.com
```

### 2. 安装最新版
```bash
cd ${OPENCLAW_HOME}/openclaw
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
${OPENCLAW_HOME}/openclaw/node_modules/.bin/openclaw --version
```

## 回滚
```bash
cd ${OPENCLAW_HOME}/openclaw
# 改 package.json 版本为旧版
npm install --registry=https://registry.npmmirror.com
# 重启同上
```