# 🤝 Agent Collab — Multi-Agent Collaboration Framework

一个基于 [OpenClaw](https://github.com/openclaw/openclaw) 的多 Agent 协作框架。探索多个 AI Agent 如何分工、通信、协调，并持续演进协作模式。

## 动机

单个 Agent 受限于运行环境——云端 Agent 不能操作本地文件，本地 Agent 不能 7×24 运行。多个 Agent 各有所长，协作才能发挥最大价值。

灵感来自 [Seeing like an Agent](https://x.com/trq212/status/2027463795355095314)：工具要匹配使用者的能力，协作模式要跟随能力演进。

## 当前 Agents

| Agent | Emoji | 环境 | 擅长 | 状态 |
|-------|-------|------|------|------|
| 小小动 | 🐿️ | 腾讯云 VM (Linux) | 云端服务、持续运行、定时任务 | ✅ 在线 |
| 核桃 | 🌰 | MacBook Pro (macOS) | 本地文件、浏览器、应用交互 | 🟡 待接入 |

> 未来可能加入更多 Agent：手机端、树莓派、其他云服务器……

## 项目结构

```
agent-collab/
├── README.md               # 项目概览
├── ARCHITECTURE.md          # 通信架构与协议设计
├── PLAYBOOK.md              # 协作手册：分工与场景
├── CHANGELOG.md             # 演进日志
├── agents/                  # Agent 注册表
│   ├── registry.json        # Agent 列表与能力声明
│   ├── xiaoxiaodong.md      # 🐿️ 小小动 profile
│   └── hetao.md             # 🌰 核桃 profile
├── protocols/               # 协作协议定义
│   └── task-handoff.md      # 任务交接协议
└── experiments/             # 实验记录
```

## 核心设计

### 1. Agent 注册表
每个 Agent 声明自己的能力、环境、可用时间。新 Agent 加入只需注册。

### 2. 协作协议
定义 Agent 之间如何交接任务、共享状态、处理冲突。协议是可演进的。

### 3. 能力路由
根据任务类型自动（或手动）分配给最合适的 Agent。

### 4. 透明可见
所有协作记录在 CHANGELOG 和 experiments/ 中，DongDong 随时可查。

## 原则

- **可扩展** — 新 Agent 加入应该是低成本的
- **松耦合** — Agent 之间通过协议通信，不依赖特定实现
- **渐进式** — 不过度设计，边做边发现最佳模式
- **透明** — 人类随时能看到 Agent 在做什么

## 给 DongDong

- 看 [CHANGELOG](CHANGELOG.md) 了解最新进展
- 提 Issue 给 Agent 们布置任务
- 看 [experiments/](experiments/) 了解尝试了什么

---

*创建于 2026-03-01 by 小小动 🐿️*
