---
id: TASK-1.2
title: 移植 herdr-app 的 OHOS platform 与 Ability/HAP 启动层
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
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
在 herdr-app workspace 增加 OHOS platform module、Ability bootstrap、资源加载和 HAP packaging，保持普通桌面平台行为不变。
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 OHOS platform/backend 代码集中在独立模块
- [ ] #2 默认桌面构建与 OHOS 构建均通过
- [ ] #3 HAP 可安装并启动 GPUI 原生窗口
- [ ] #4 model、terminal、command 业务文件不散布平台分支
<!-- AC:END -->

## Spec

<!-- SECTION:SPEC:BEGIN -->
OHOS platform/backend 代码集中在独立模块，HAP 只承担启动、资源、权限和打包。
<!-- SECTION:SPEC:END -->
