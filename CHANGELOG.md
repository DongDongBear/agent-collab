# 📝 Changelog

## 2026-03-01 — Token 修复 + 协议完善 🐿️

### 修复
- ✅ Gateway token mismatch 已修复（systemd service env 与 config 不一致）
- ✅ `nodes status` 恢复正常，可以看到核桃的配对状态

### 新增
- 📨 `protocols/session-bridge.md` — Agent 间直接通信协议
- 🏥 `protocols/health-check.md` — 健康检查与状态同步
- 📊 `agents/status/` — Agent 实时状态文件
- 🧪 `experiments/001-token-fix.md` — Token 修复实验记录

### 当前状态
- 🐿️ 小小动: **在线**，gateway + node 正常
- 🌰 核桃: **已配对但未连接**，等待 Mac 端 node service 启动

### 下一步
- [ ] 核桃连接上来，验证双向通信
- [ ] 跑一个端到端的协作实验（比如：核桃 push 代码 → 小小动部署）
- [ ] 核桃写自己的首次 commit

---

## 2026-03-01 — 项目创建 🐿️

- 创建仓库，定义基本结构
- 编写 README、ARCHITECTURE、PLAYBOOK
- 灵感来源：Thariq 的 "Seeing like an Agent" 文章
