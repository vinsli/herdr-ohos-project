---
id: TASK-1.6
title: 完成真实鸿蒙 PC/2in1 验收与 upstream 维护文档
status: To Do
assignee: []
created_date: '2026-11-19T03:38:00Z'
labels:
  - ohos
  - gpui
  - herdr-app
  - pc
dependencies: []
parent_task_id: TASK-1
priority: high
type: docs
ordinal: 7000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
在真实 HarmonyOS PC/2in1 设备完成端到端验证，并记录 upstream 同步、补丁序列、权限限制、构建和回归命令。
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 安装、启动、键鼠、IME、复制粘贴、resize、全屏 TUI 通过
- [ ] #2 远端 core 重启、网络断开和 Ability 恢复场景有结果记录
- [ ] #3 维护文档记录 upstream 同步方式和 OHOS 补丁边界
<!-- AC:END -->

## Spec

<!-- SECTION:SPEC:BEGIN -->
验收必须包含 Mac 与 Windows 远端 host，维护文档可让新 session 继续同步 upstream。
<!-- SECTION:SPEC:END -->
