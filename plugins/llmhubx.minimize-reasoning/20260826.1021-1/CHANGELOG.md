# 最小化思考插件 20260826.1021-1

- 将官方“最小化思考”插件重写为 ABI Level 1 插件。
- 同一 `.lhxp` Bundle 同时包含 Extism Rust 与 CMW Rust 产物，用户可选择 Runtime。
- 在实际 Route 成员支持关闭思考时设置为关闭；否则选择该成员公开的最低思考档位。
- 只实现 `member-request-transform`，只声明 Reasoning 修改与结构化观测权限。
- 两个 Runtime 产物通过同一组 canonical conformance vectors，保持相同用户可见行为。
- Marketplace 目录保留 Bundle 的完整纯文本介绍，不再退回一行摘要。

## 兼容性与迁移

- 本插件以 `target_abi_level = 1` 运行，需要 App 的兼容 ABI 区间包含 Level 1。
- 这是新的 `.lhxp` 版本线，不继承或迁移旧 `1.0.0` 插件状态。
