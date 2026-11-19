---
id: TASK-1
title: 将 herdr-app 移植为鸿蒙 PC 客户端
status: To Do
assignee: []
created_date: '2026-11-19T03:38:00Z'
labels:
  - ohos
  - gpui
  - herdr-app
  - pc
dependencies: []
references:
  - https://github.com/herdrdev/herdr-app
  - https://github.com/ohos-rs/gpui-ohos
priority: high
type: feature
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
将 herdr-app 的 spaces、tabs、panes、terminal view 和 command 层移植到 HarmonyOS PC/2in1，复用 herdr-core OHOS 远端能力并保持与 upstream herdr-app 的持续同步。鸿蒙设备作为远端客户端，终端和进程由远端 core 承载。
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 herdr-app Rust workspace 可面向 HarmonyOS PC/2in1 构建并启动 GPUI 原生窗口
- [ ] #2 spaces、tabs、split panes、machine 和 command 模型可用，业务代码保持可同步
- [ ] #3 远端 terminal view 支持 framed stream、VT/ANSI、键盘输入、IME、复制粘贴、滚动和 resize
- [ ] #4 Ability 重建、后台恢复、远端 core 重启和断线重连保持正确生命周期
- [ ] #5 真实 HarmonyOS PC/2in1 完成 Mac/Windows 远端验收
- [ ] #6 文档记录 upstream 同步方式、OHOS 补丁边界、平台限制和验证命令
<!-- AC:END -->

## Spec

<!-- SECTION:SPEC:BEGIN -->
以 upstream herdr-app Rust 业务代码为主体，平台差异集中在 gpui-ohos、OHOS platform module、hc transport、Ability/NAPI 和 HAP packaging。不得引入 pyt 或在鸿蒙本地依赖 PTY、fork、exec、child process。
<!-- SECTION:SPEC:END -->
