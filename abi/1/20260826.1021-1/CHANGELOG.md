# LLMHubX Plugin ABI Level 1 20260826.1021-1

- 发布首个正式 ABI Level 1，共享给 Extism 与 CMW 插件体系。
- 冻结五份规范 WIT：package、types、hooks、host 与 world，并提供生成后的 ABI 文档和兼容说明。
- 定义六类 Hook、中立请求与响应、顺序化修改、逻辑模型选择、私有调用状态、结构化观测和媒体副本导出契约。
- 定义权限、共享错误码、fail-open、超时、fuel、内存、输入输出和异步队列边界。
- 提供覆盖 record、variant、option、list、result、bytes、整数和 RFC 8785 边界的 canonical fixtures。
- 固定 Extism UTF-8 JSON wire 与 CMW Component Model 对相同 WIT 值的等价语义。

## 兼容性

- 这是首个正式 ABI Level，不与旧 `api_version = "1.0.0"` 包格式建立映射或兼容关系。
