# LLMHubX Plugin SDK Extism JavaScript 20260826.1021-1

- 面向 ABI Level 1 提供 JavaScript 类型声明、Hook 调用封装和 Extism JSON wire 编解码。
- 支持六类 Hook、类型化顺序变更、结构化观测与媒体副本导出 Host API。
- 使用安全字符串表示可能超过 JavaScript 安全整数范围的 WIT 整数，并固定 base64url bytes 编码。
- 附带最小插件模板、开发文档、冻结 WIT 和 canonical fixtures。
- 独立测试验证 canonical 编码及可直接生成 wasm32-unknown-unknown 插件的构建流程。

## 兼容性

- 生成的插件以 `target_abi_level = 1` 运行，需要 App 的兼容 ABI 区间包含 Level 1。
