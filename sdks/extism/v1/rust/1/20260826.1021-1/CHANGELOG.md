# LLMHubX Plugin SDK Extism Rust 20260826.1021-1

- 面向 ABI Level 1 提供由规范 WIT 生成的 Rust 类型和 Extism JSON wire 包装。
- 提供六类 Hook 的输入、输出与变更类型，并保留未知 Host 错误码。
- 提供类型化媒体副本导出 Host API，不向插件暴露真实文件路径或媒体二进制。
- 附带最小插件模板、开发文档、冻结 WIT 和 canonical fixtures。
- 独立测试验证 canonical 编码、错误边界及 wasm32-unknown-unknown 模板构建。

## 兼容性

- 生成的插件以 `target_abi_level = 1` 运行，需要 App 的兼容 ABI 区间包含 Level 1。
