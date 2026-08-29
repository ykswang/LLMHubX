# SQLite Resource Provider 20260829.1024-1

- 首次发布官方 CMW-only SQLite Resource Provider。
- 提供完整的 `resource.kv` 与 `resource.relational` 能力。
- 通过 Kernel 分配的 scoped Workspace 持久化 SQLite 数据，不获得任意文件、网络、DNS、环境变量或 DSN。
- 通过与 Native SQLite Provider 相同的共享 conformance，并支持双向迁移和 Component 重建读回。
