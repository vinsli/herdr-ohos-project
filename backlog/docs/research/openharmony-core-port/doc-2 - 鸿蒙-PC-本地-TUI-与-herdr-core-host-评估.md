---
id: doc-2
title: 鸿蒙 PC 本地 TUI 与 herdr-core host 评估
type: specification
created_date: '2026-11-19T03:36:00Z'
updated_date: '2026-11-19T03:37:00Z'
---
---
id: doc-7
title: 鸿蒙 PC 本地 TUI 与 herdr-core host 评估
type: specification
created_date: '2026-11-16T16:32:00Z'
updated_date: '2026-11-16T16:33:00Z'
---
# 鸿蒙 PC 本地 TUI 与 herdr-core host 评估

## 结论

TASK-6 继续交付远端客户端，不把鸿蒙 PC 本地 TUI 或 host 作为阻塞条件。PC/2in1 具备比手机更宽的子进程能力，但这不等价于已经具备 herdr-tui 所需的交互式 PTY、raw mode、ANSI 输入和稳定窗口 resize 生命周期。当前工程保留远端 SSH/RPC/terminal stream 作为唯一产品路径。

## 官方能力

- [HarmonyOS process model](https://developer.huawei.com/consumer/en/doc/harmonyos-guides/process-model-overview/)：PC/2in1 和 tablet 可以通过 childProcessManager 创建子进程；子进程生命周期跟随父进程。
- [Native child process](https://developer.huawei.com/consumer/en/doc/HarmonyOS-references/capi-native-child-process-h/)：原生子进程按 Ability API 和动态库入口启动，适用设备与 API 版本有差异。
- [Seccomp symbols](https://developer.huawei.com/consumer/en/doc/harmonyos-references/seccomp-symbol/)：fork/execve 的系统调用可见，但调用可用不代表应用沙箱、PTY、终端设备和分发审核条件满足。
- [PC/2in1 bin deployment](https://developer.huawei.com/consumer/en/doc/harmonyos-guides/hap-bin/)：PC/2in1 可随 HAP 部署 bin 并由 native 代码启动，但示例仍要求自建 fork/exec 生命周期。

## 对 herdr-tui/host 的评估

| 问题 | 结论 | 依据/后续 |
|---|---|---|
| stdin/stdout、raw mode、ANSI | 未在当前 PC 设备上实机确认；官方子进程 API 只证明 I/O 流和进程启动，不证明控制终端 | 需要真实 HarmonyOS PC/2in1 设备与最小 native PTY probe |
| 窗口大小与 PTY resize | ArkUI 窗口 resize 已可转换为远端 terminal resize；本地 PTY resize 未验证 | 远端路径已实现 `terminalStreamResize`，本地 host 暂不启用 |
| PTY、holder、shell 生命周期 | 当前 OHOS `herdr_core_session_new` 明确返回 `-95`；OHOS machine transport 使用纯 Rust russh，不 spawn 本地 ssh/child | 不改变手机安全边界；若启动 spike，单独实现 native child/PTY prototype |
| herdr-tui 抽取 | 暂不抽取；TUI 依赖真实 terminal ownership、raw mode、signal、window resize 和 process lifecycle | 先完成 PC 设备 probe，再决定抽取边界 |
| PC 本地 host | 暂不支持；PC product 是远端客户端，host/holder/PTY 仍由 Mac/Windows 承载 | 另建任务并要求 PC 实机、ABI、签名、生命周期和崩溃恢复证据 |

## 可执行后续方案

1. 用真实 HarmonyOS PC/2in1 创建最小 native child process + PTY probe：启动 shell，读写 stdin/stdout，切换 raw mode，发送 ANSI，观察 window resize，验证 Ability 重启后的子进程收敛。
2. 只有 probe 同时通过且系统能力/分发要求明确后，才设计 `herdr-tui` 的 PC adapter；复用远端状态模型但不复制 wire 协议。
3. 在此之前，PC/2in1 HAP 只提供远端 SSH/RPC/framed stream；手机继续禁止本地 PTY/fork/exec/child。
