# fnOS OpenClaw 更新器

**[English](./README.md) | 中文**

安全更新 fnOS NAS 应用中心的 OpenClaw 到最新 npm 版本，不修改 fnOS 托管的配置文件。

## 功能

- 安全更新：只修改 node_modules，不改 fnOS 配置
- 自动重启（优雅 SIGTERM）
- 支持回滚
- 更新前版本检查

## 前置条件

| 变量 | 说明 |
|------|------|
| OPENCLAW_HOME | fnOS 上 OpenClaw 的数据目录 |

## License

MIT
