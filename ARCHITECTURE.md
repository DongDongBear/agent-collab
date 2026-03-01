# 🏗️ Architecture

## 设计目标

支持 **N 个 Agent** 协作，而不只是两个。新 Agent 加入应该是低成本的。

## 整体架构

```
                    ┌──────────────┐
                    │  🧑 DongDong  │
                    │  (Human)     │
                    └──────┬───────┘
                           │ 飞书 / GitHub Issues
                    ┌──────▼───────┐
                    │   Agent Hub   │
                    │  (this repo)  │
                    └──────┬───────┘
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        ┌───────────┐┌───────────┐┌───────────┐
        │ 🐿️ 小小动  ││ 🌰 核桃    ││ 🤖 Agent N │
        │ Cloud VM  ││ MacBook   ││ ???       │
        └───────────┘└───────────┘└───────────┘
```

## 通信层

### 层级

1. **直接通信** — OpenClaw node pairing (nodes.run / sessions_send)
2. **异步同步** — Git 仓库（push/pull）
3. **人工中转** — 飞书消息（降级方案）

### 当前网络

```
🌰 核桃 (Mac)  ◄── SSH 反向隧道 ──►  🐿️ 小小动 (VM)
   :18789                              :18789 (gateway)
                                        :18790 (tunnel endpoint)
```

### 新 Agent 接入方式

1. **云端 Agent** — 直接 SSH / VPN 连接
2. **本地 Agent** — SSH 反向隧道 + OpenClaw node host
3. **移动端 Agent** — OpenClaw companion app
4. **临时 Agent** — 子 Agent (sessions_spawn)，任务完成后销毁

## Agent 注册

每个 Agent 在 `agents/registry.json` 中注册：
- id, name, emoji
- environment (type, os, always_on)
- capabilities (能力列表)
- connection (通信方式)
- status (online / offline / pending)

## 共享状态

| 状态类型 | 存储位置 | 说明 |
|---------|---------|------|
| Agent 注册 | agents/registry.json | 谁在、能做什么 |
| 协作协议 | protocols/ | 怎么协作 |
| 实验记录 | experiments/ | 尝试了什么 |
| 演进日志 | CHANGELOG.md | 什么时候变了什么 |

## 待建设

- [ ] 修复 gateway token mismatch
- [ ] 双向 node 通信
- [ ] Agent 自动发现与注册
- [ ] 任务队列与调度
- [ ] 健康检查与心跳
