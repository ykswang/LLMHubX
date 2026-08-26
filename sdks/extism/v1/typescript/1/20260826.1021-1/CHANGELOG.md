# LLMHubX Plugin SDK Extism TypeScript 20260826.1021-1

- 面向 ABI Level 1 提供由规范 WIT 生成的 TypeScript 类型和六类 Hook API。
- 提供类型化顺序变更、HostApiError、结构化观测与媒体副本导出调用。
- 固定 JavaScript 安全整数、base64url bytes 与 canonical JSON 编码规则。
- 附带最小插件模板、开发文档、冻结 WIT 和 canonical fixtures。
- 独立测试和 typecheck 验证 canonical 编码及 wasm32-unknown-unknown 插件构建。

## 兼容性

- 生成的插件以 `target_abi_level = 1` 运行，需要 App 的兼容 ABI 区间包含 Level 1。
