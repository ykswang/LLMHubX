# LLMHubX Plugin SDK CMW Rust 20260826.1021-1

- 面向 ABI Level 1 提供基于 Component Model/WIT 的 Rust 绑定。
- 支持六类强类型 Hook、顺序化修改、结构化观测与媒体副本导出 Host API。
- 与 Extism SDK 共享相同 WIT、权限、错误码、资源限制和 canonical fixtures。
- 附带最小 Component 插件模板、开发文档和冻结 WIT。
- 独立测试验证 ABI fixtures，并验证 wasm32-wasip2 模板构建和 Host conformance。

## 兼容性

- 生成的插件以 `target_abi_level = 1` 运行，需要 App 的兼容 ABI 区间包含 Level 1。
