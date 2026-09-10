# CMW Rust SDK：ABI Level 3 业务观测

此 SDK 使用独立的 `business-observation` world，为插件提供类型化声明和业务上报。Level 1 基础能力通过 `level_one` 重导出；需要 Workflow 的插件另行组合 Level 2 SDK，不强迫 Context 插件实现 Workflow。

实现 `BusinessObservationDispatch`，返回与包内 `observation/metrics.toml` 相同的声明，并分别执行基础 world 和本 SDK 的 `bindings::export!`。包使用 Manifest v2、CMW `target_abi_level = 3`，增加 `[observation]` 的 `schema_revision = 1` 和 `declarations = "observation/metrics.toml"`。

`template/` 是一个非 Context 请求观测示例，只上报最终请求的消息条目数量，不复制消息正文。`begin_operation` 返回可用句柄后可上报阶段和完成结果；未采集、无效或配额拒绝不能改变插件业务返回。句柄只在当前调用有效，宿主负责归属、执行事实和最终结算。

```sh
cargo build --manifest-path template/Cargo.toml --target wasm32-wasip2 --release
```

发布压缩包附带 `level1/` 依赖，可直接构建，无需取得 App 源码。生成的 Component 可用于宿主 `business_observation` 集成测试。

使用时需要支持 ABI Level 3 的 App。本次实际接入 Context 调用；非 Context 模板用于验证相同的声明、WASM 上报和宿主结算契约，不代表 Manifest v2 Hook/Resource 已接入 App 的网关执行入口。旧宿主会拒绝新版包，请先更新 App。
