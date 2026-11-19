# herdr-ohos-project

This repository is the project control plane for the HarmonyOS ports.

- `herdr-core-ohos` contains the OpenHarmony `herdr-core` fork and its `ohos-port` branch.
- `herdr-app` contains the `herdr-app` fork and its `ohos-port` branch.
- `backlog/` contains the migration tasks, architecture notes, device validation records, and upstream synchronization guidance.

The HarmonyOS client remains a remote client. Terminal processes and PTY ownership stay in the remote `herdr-core` host. The project does not introduce `pyt` or local PTY/fork/exec/child-process dependencies.
