---
id: TASK-1.3
title: 接入鸿蒙 hc transport 与现有 herdr-core 远端协议
status: To Do
assignee: []
created_date: '2026-11-19T03:38:00Z'
labels:
  - ohos
  - gpui
  - herdr-app
dependencies: []
parent_task_id: TASK-1
priority: high
type: task
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
把 herdr-app 的 hc client 接到 OHOS core service、SSH machine、JSON-RPC 和 framed terminal stream，保留 herdr-app machine/space/terminal API 语义。
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 可创建远端 machine、space、tab 和 terminal
- [ ] #2 Mac 远端 framed stream 可收发数据
- [ ] #3 Ability 重建后可恢复连接或报告可恢复错误
<!-- AC:END -->

## Spec

<!-- SECTION:SPEC:BEGIN -->
鸿蒙本地不运行 PTY、fork、exec 或 child process，复用 herdr-core OHOS transport。
<!-- SECTION:SPEC:END -->
