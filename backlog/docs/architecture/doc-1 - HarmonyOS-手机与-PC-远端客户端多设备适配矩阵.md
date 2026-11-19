---
id: doc-1
title: HarmonyOS 手机与 PC 远端客户端多设备适配矩阵
type: specification
created_date: '2026-11-19T03:36:00Z'
updated_date: '2026-11-19T03:37:00Z'
---
---
id: doc-6
title: HarmonyOS 手机与 PC 远端客户端多设备适配矩阵
type: specification
created_date: '2026-11-16T16:06:00Z'
updated_date: '2026-11-16T16:07:00Z'
---
# HarmonyOS 手机与 PC 远端客户端多设备适配矩阵

## 目标

TASK-6 采用一套工程、按 phone 与 PC/2in1 设备形态部署的远端客户端架构。两端复用 herdr-core 的 machine、JSON-RPC、SSH transport、framed terminal stream、凭据抽象和远端状态模型。鸿蒙手机与 PC 本地 TUI、PTY、holder、shell、host 的差异不在本阶段解决；PC 本地能力由 TASK-6.5 低优先级跟踪。

## 官方依据

- [一次开发，多端部署概览](https://developer.huawei.com/consumer/cn/doc/doccenter-multi-device/bpta-multi-device-overview/)：工程、功能、界面三层适配；支持手机、PC/2in1 等设备。
- [电脑应用开发](https://developer.huawei.com/consumer/cn/doc/doccenter-multi-device/bpta-pc-guide/)：PC/2in1 原生部署、兼容运行、键鼠、大屏和多窗口差异。
- [API 跨设备兼容性](https://developer.huawei.com/consumer/cn/doc/guidebook/develop-once-deploy-everwhere-4--3-0000002625192365/)：通过 SystemCapability 判断 API 能力，避免仅凭 SDK 声明使用不支持的能力。

## 设备矩阵

| 能力 | 手机 profile | PC/2in1 profile | 本阶段策略 |
|---|---|---|---|
| UI | ArkUI 触摸、小屏、竖横屏 | ArkUI 大屏、键鼠、窗口 | 共用页面模型，按设备形态响应式布局 |
| 远端 machine | 支持 | 支持 | 共用 machine/RPC/SSH |
| terminal attach | 支持 | 支持 | 共用 framed stream 与 fallback |
| 凭据 | app sandbox / 安全存储适配 | app sandbox / 安全存储适配 | 共用抽象，按产品配置存储 |
| 本地 PTY | 禁用 | 本阶段不交付 | 留给 TASK-6.5 |
| 本地 holder/shell | 禁用 | 本阶段不交付 | 留给 TASK-6.5 |
| 本地 TUI | 不适用 | 本阶段不交付 | 留给 TASK-6.5 |
| 生命周期 | Ability 重建、断线重连 | 窗口/Ability 重建、断线重连 | 共用远端状态恢复语义，分别验证 |
| 网络 | INTERNET 权限、SSH 到 Mac/Windows | INTERNET 权限、SSH 到 Mac/Windows | 共用 SSH transport |

## 工程部署

- Entry Module 声明 `phone` 与 `2in1`，避免 PC 被当作手机兼容运行。
- Rust 公共能力保持在 herdr-core / OHOS client 层；UI 与输入适配在 ArkTS product 层。
- 若 PC 与手机功能差异扩大，使用产品配置生成不同 HAP；不复制远端协议实现。
- 需要记录每个设备 profile 的 HAP 产物、ABI、签名、安装命令和验证结果。

## 验证矩阵

1. 配置：module.json5、build-profile.json5 和 product 配置能解析 phone/2in1。
2. 构建：手机与 PC/2in1 目标的 HAP 构建成功，公共 native library 只实现一次。
3. 手机回归：安装、machine.add、terminal attach、输出、输入、resize、interrupt、Ability 重建。
4. PC 回归：键盘、鼠标、窗口变化、resize、terminal attach 和 Mac/Windows 远端连接。
5. 能力保护：不支持的 SystemCapability 进入明确降级或错误路径。
6. 边界：PC 本地 TUI、PTY、holder、shell、host 不作为 TASK-6 的完成条件。
