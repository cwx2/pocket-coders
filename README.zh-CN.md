<p align="center">
  <img src="docs/assets/icon.png" width="80" alt="Pocket Coder" />
</p>

<h1 align="center">Pocket Coder</h1>

<p align="center">
  <strong>手机上的 AI 编程助手 — 用手机操控电脑上的 AI Agent 写代码。</strong>
</p>

<p align="center">
  <a href="../../releases">下载</a> •
  <a href="#功能">功能</a> •
  <a href="#快速开始">快速开始</a> •
  <a href="README.md">English</a>
</p>

---

## Pocket Coder 是什么？

Pocket Coder 让你用手机连接电脑上的 AI 编程工具。AI 对话、浏览文件、编辑代码、终端命令、Git 管理 — 全部在手机上完成。

代码始终在你的电脑上，Pocket Coder 只是遥控器。

## 功能

| | 功能 | 说明 |
|---|---|---|
| 🤖 | **AI 对话** | 支持 Claude Code、Codex、Gemini CLI、Copilot、Aider 等 |
| 📁 | **文件浏览** | 浏览项目、查看代码（100+ 语言高亮）、直接编辑 |
| 🔀 | **Git** | Diff、暂存、提交、推送、拉取、切换分支、查看日志 |
| 💻 | **终端** | 手机上的完整终端模拟器 |
| 🔒 | **加密** | 端到端 AES-256 加密，不经过任何第三方服务器 |
| 📡 | **灵活连接** | 局域网直连、远程中继、自建隧道 |


## 截图

<p align="center">
  <img src="docs/screenshots/chat.png" width="200" alt="AI 对话" />
  <img src="docs/screenshots/files.png" width="200" alt="文件浏览" />
  <img src="docs/screenshots/terminal.png" width="200" alt="终端" />
</p>

## 快速开始

### 1. 安装电脑端（Agent）

从 [Releases](../../releases) 下载：

| 平台 | 文件 |
|------|------|
| Windows | `mobileflow-agent-windows.exe` |
| macOS | `mobileflow-agent-macos` |
| Linux | `mobileflow-agent-linux` |

### 2. 安装手机端（App）

| 平台 | 下载 |
|------|------|
| Android | [Releases 页面下载 APK](../../releases) |
| iOS | 即将上线 |

### 3. 安装一个 AI 工具

电脑上至少需要安装一个 AI CLI 工具：

```bash
# 选一个（或多个）：
npm i -g @anthropic-ai/claude-code    # Claude Code
npm i -g @openai/codex                # Codex
npm i -g @google/gemini-cli           # Gemini CLI（有免费额度）
```

### 4. 连接

1. 电脑上启动 Agent → 从系统托盘查看 IP 和密码
2. 手机打开 App → 输入 IP、端口（9600）和密码
3. 搞定，开始写代码。


## 架构

```
┌─────────────┐     WebSocket      ┌─────────────┐
│   手机 App  │◄──────────────────►│   电脑端    │
│  (Flutter)  │    端到端加密       │   Agent     │
│             │                    │  (Python)   │
│ • AI 对话   │                    │ • AI CLI    │
│ • 文件      │                    │ • 文件      │
│ • 终端      │                    │ • 终端      │
│ • Git       │                    │ • Git       │
└─────────────┘                    └─────────────┘
```

- **App** — Flutter 手机端 UI，零数据存储
- **Agent** — Python 守护进程，管理 AI 工具、文件、终端、Git
- **Protocol** — WebSocket + AES-256 加密

## 连接模式

| 模式 | 适用场景 | 延迟 |
|------|---------|------|
| **局域网直连** | 同一 WiFi 网络 | < 10ms |
| **远程中继** | 不同网络 | ~50-100ms |
| **隧道直连** | 自建服务器 | 取决于服务器 |

> 📖 详细配置指南：[远程连接指南](docs/远程连接指南.md)

## 安全

- 所有代码始终在你的电脑上
- AES-256 消息级加密（局域网）/ NaCl SecretBox 端到端加密（中继）
- 暴力破解保护：3 次失败 → 锁定 60 秒
- 会话令牌机制 — 认证后密码不再传输
