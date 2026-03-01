# 🌉 Session Bridge Protocol v0.1

## 概述
通过 OpenClaw 的 `sessions_send` 和 `nodes.run` 实现 Agent 间直接通信。

## 通信模式

### 1. 命令执行（同步）
适合简单的跨环境操作。

**小小动 → 核桃：**
```
nodes.run(node="DongDong's MacBook Pro", command=["ls", "-la", "/Users/dongdong/Desktop"])
```

**核桃 → 小小动：**
```
nodes.run(node="VM-0-12-opencloudos", command=["systemctl", "--user", "status", "openclaw-gateway"])
```

### 2. 消息通信（异步）
适合复杂任务交接、讨论。

```
sessions_send(label="hetao-main", message="需要你帮我在 Mac 上截个图")
```

### 3. 子 Agent 派遣
适合一次性任务，用完即销毁。

```
sessions_spawn(task="检查五子棋网站是否正常", runtime="subagent")
```

## 消息格式约定

Agent 间通信用结构化前缀，方便解析：

```
[TASK] 需要你执行的任务描述
[STATUS] 当前状态更新
[RESULT] 任务执行结果
[QUESTION] 需要对方回答的问题
[HANDOFF] 任务交接，附带上下文
```

## 示例场景

### 场景：部署代码到云端
```
🌰 核桃: [TASK] 我已经 push 了新代码到 gomoku 仓库，请 pull 并重启服务
🐿️ 小小动: [STATUS] 正在 pull...
🐿️ 小小动: [RESULT] 部署完成，服务正常运行。测试 URL: http://hetaogomoku.uk
```

### 场景：获取本地文件
```
🐿️ 小小动: [TASK] 需要 Mac 桌面上的 design.png，请上传到 /tmp/shared/
🌰 核桃: [STATUS] 正在处理...
🌰 核桃: [RESULT] 文件已放到 /tmp/shared/design.png (142KB)
```

## 前置条件
- [x] OpenClaw node 配对完成
- [x] Gateway token 一致
- [ ] 双向 node 通信验证
- [ ] sessions_send 互通测试
