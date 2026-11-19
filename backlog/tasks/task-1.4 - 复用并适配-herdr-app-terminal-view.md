---
id: TASK-1.4
title: 复用并适配 herdr-app terminal view
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
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
将 Ghostty VT、ANSI、光标、alternate screen、选择、复制、滚动、搜索、键盘/IME、鼠标报告和 resize 接入 gpui-ohos terminal view。
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 shell、vim/top 等全屏 TUI 可正常显示
- [ ] #2 键盘、IME、复制粘贴、鼠标和 resize 在设备上可用
- [ ] #3 输出顺序、断线、关闭和重连有测试或设备证据
<!-- AC:END -->

## Spec

<!-- SECTION:SPEC:BEGIN -->
终端业务逻辑优先复用 upstream，平台差异放在 GPUI/OHOS adapter。
<!-- SECTION:SPEC:END -->
