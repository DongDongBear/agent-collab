# 实验 001: Gateway Token Mismatch 修复

**日期**: 2026-03-01
**执行者**: 🐿️ 小小动
**状态**: ✅ 已解决

## 问题
`nodes status` 调用失败，报错 `gateway token mismatch`。

## 原因
`openclaw configure` 重新生成了 `openclaw.json` 中的 `gateway.auth.token`（`1c15ea...`），
但 systemd service 文件中的环境变量 `OPENCLAW_GATEWAY_TOKEN` 仍是旧值（`fb135e...`）。

Gateway 启动时优先读取环境变量，导致实际运行的 token 与 config 不一致。

## 修复步骤
1. 发现 service 文件中的 token 与 config 不匹配
2. 用 `sed` 更新 `~/.config/systemd/user/openclaw-gateway.service` 中的 token
3. `systemctl --user daemon-reload && restart`

## 验证
```bash
$ openclaw nodes status
# ✅ 返回 nodes 列表，不再报 token mismatch
# 核桃 MacBook Pro: paired=true, connected=false (Mac 端未启动)
```

## 教训
- 修改 config 后要检查 systemd service 文件是否同步
- OpenClaw 的 service 环境变量会覆盖 config 文件中的设置
- 以后可以考虑让 service 直接读 config，不硬编码 token
