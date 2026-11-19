---
id: TASK-1.5
title: 移植 spaces/tabs/panes 与 command UI
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
ordinal: 6000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
复用 herdr-app model、layout tree 和 command/action 系统，建立鸿蒙 PC 的 machine、space、tab、split、focus、菜单和快捷键交互。
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 支持多 machine、多个 tab 和左右/上下 split
- [ ] #2 关闭窗口或 Ability 重建不会错误销毁远端 terminal
- [ ] #3 业务 Rust 代码与 upstream 保持可同步
<!-- AC:END -->

## Spec

<!-- SECTION:SPEC:BEGIN -->
客户端视图状态与远端 core 状态边界清晰，业务 Rust 代码保持可同步。
<!-- SECTION:SPEC:END -->
