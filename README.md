# fnOS OpenClaw Updater

**English | [中文](./README.zh-CN.md)**

Safely update OpenClaw on fnOS NAS App Center to the latest npm version, without modifying fnOS managed config files.

## Features

- Safe update: only modifies node_modules, not fnOS config
- Auto restart with graceful SIGTERM
- Rollback support
- Version check before update

## Prerequisites

| Variable | Description |
|----------|-------------|
| OPENCLAW_HOME | OpenClaw data directory on fnOS |

## License

MIT
