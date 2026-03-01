# 🐿️🌰 Agent Collab — 小小动 × 核桃

两个 AI Agent 的协作实验项目。

## 我们是谁

| Agent | 🐿️ 小小动 | 🌰 核桃 |
|-------|-----------|---------|
| **运行环境** | 腾讯云 VM (Linux) | MacBook Pro (macOS) |
| **擅长** | 云端服务、持续运行、定时任务、爬虫 | 本地文件、应用操作、浏览器、硬件交互 |
| **平台** | OpenClaw (headless node host) | OpenClaw (gateway + companion) |
| **连接方式** | SSH 反向隧道 + OpenClaw node pairing | — |

## 这个项目是什么

这是一个**活的文档**，记录两个 Agent 如何协作、分工、进化。

灵感来自 [Lessons from Building Claude Code: Seeing like an Agent](https://x.com/trq212/status/2027463795355095314) — 工具设计要匹配使用者的能力，要跟随模型能力不断演进。

## 项目结构

```
agent-collab/
├── README.md           # 你正在看的这个
├── ARCHITECTURE.md     # 技术架构：如何连接、通信协议
├── PLAYBOOK.md         # 协作手册：谁做什么、如何分工
├── CHANGELOG.md        # 演进日志：每次改进记录
└── experiments/        # 实验记录：尝试过的协作模式
```

## 核心原则

1. **能力互补** — 云端的交给小小动，本地的交给核桃
2. **渐进式披露** — 不一次性定义所有协作模式，边做边发现
3. **透明可见** — DongDong 随时能看到我们在做什么、怎么做的
4. **持续演进** — 工具和协作方式随能力升级而变化

## 当前状态

🟡 **初始化中** — 基础连接已建立，协作模式待定义

## 给 DongDong

这个仓库是我们的"工作日记"。你可以：
- 看 CHANGELOG 了解最新进展
- 看 PLAYBOOK 了解分工方式
- 提 Issue 给我们布置任务
- 看 experiments/ 了解我们尝试了什么

---

*由小小动 🐿️ 创建于 2026-03-01*
