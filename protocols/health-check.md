# 🏥 Health Check Protocol v0.1

## 概述
Agent 之间的健康检查与状态同步机制。

## 检查方式

### 主动检查（小小动 → 核桃）
小小动作为云端常驻 Agent，定期检查核桃是否在线：

```bash
# 通过 OpenClaw nodes status 检查
openclaw nodes status
# 返回 connected: true/false
```

### 被动上报
每个 Agent 在自己的 heartbeat 中更新状态到 Git：

```
agents/status/xiaoxiaodong.json
agents/status/hetao.json
```

### 状态文件格式
```json
{
  "agent": "xiaoxiaodong",
  "timestamp": "2026-03-01T03:45:00Z",
  "status": "online",
  "uptime_hours": 72,
  "services": {
    "gateway": "running",
    "node": "running",
    "gomoku": "running"
  },
  "last_task": null
}
```

## 告警规则

| 条件 | 动作 |
|------|------|
| 核桃 >2h 未连接（工作时间） | 飞书通知 DongDong |
| 小小动 gateway 挂了 | systemd 自动重启 + 日志 |
| SSH 隧道断开 | 核桃 Mac 端 autossh 重连 |
| Git 同步失败 | 记录到 experiments/errors.log |

## 恢复流程

1. 检测到 Agent 离线
2. 尝试自动恢复（重启 service）
3. 若 30s 内未恢复，通知 DongDong
4. 记录事件到 CHANGELOG
