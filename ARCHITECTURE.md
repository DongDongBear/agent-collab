# 🏗️ Architecture

## 网络拓扑

```
┌─────────────────────┐         SSH 反向隧道         ┌─────────────────────┐
│   🌰 核桃 (Mac)      │◄──────────────────────────►│   🐿️ 小小动 (VM)     │
│                     │    Mac:18789 ← VM:18790     │                     │
│  OpenClaw Gateway   │                             │  OpenClaw Gateway   │
│  :18789             │                             │  :18789             │
│                     │                             │                     │
│  Node Host ────────►│─── registers as node ──────►│  (接受 node 连接)    │
│  (connects to VM)   │                             │                     │
└─────────────────────┘                             └─────────────────────┘
```

## 通信方式

### 核桃 → 小小动
- 核桃的 gateway 可以通过 `nodes.run` 在小小动的机器上执行命令
- SSH 反向隧道保持连接（Mac:18789 → VM:18790）

### 小小动 → 核桃
- **待建设** — 目前小小动无法主动调用核桃
- 方案：小小动也运行 node host 连接到核桃的 gateway（通过 SSH 隧道）

### 共享状态
- **GitHub 仓库** — 这个项目本身就是共享状态
- **飞书消息** — 通过 DongDong 中转
- **文件系统** — 各自的 workspace 独立

## 基础设施

### 小小动 (VM-0-12-opencloudos)
- OS: OpenCloudOS 9 (Linux 6.6)
- Node.js: v22.22.0
- Gateway: port 18789 (loopback)
- Node Host Service: systemd (openclaw-node.service)
- 已安装: edge-tts, ffmpeg, nginx, rapfi (五子棋 AI)

### 核桃 (MacBook Pro)
- OS: macOS
- OpenClaw companion app + gateway
- 通过 SSH 隧道连接到 VM

## 待解决

- [ ] 修复 gateway token mismatch（nodes 工具无法使用）
- [ ] 建立双向 node 通信
- [ ] 定义 API/协议：两个 Agent 如何互相发任务
