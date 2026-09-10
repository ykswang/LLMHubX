# Plugin ABI Level 3：业务观测

本级新增独立包 `llmhubx:plugin-level-3` 的 `business-observation` world，导入 `observation-host` 并导出 `observation-declarations`。已有 Level 1/2 WIT 文件保持冻结。组件组合基础 `plugin` world 与实际所需的其他 world；仅有 Context 的组件不要求 Workflow world。

声明、报告均为 WIT record/variant，不使用自由 JSON。声明返回值必须与 Manifest v2 中 `[observation]` 指定的 TOML 完全一致。指标与状态 ID 不得重复，不能覆盖 `host.*`。同一报告最多 32 个指标，编码后最多 16 KiB；所有数值有限，值类型和单位由声明校验。

操作句柄为宿主发出的不透明 u64，只在宿主绑定的当前调用内使用；数字相同不能授权跨调用或跨观测代次访问。`begin-operation`、`report` 和 `finish-operation` 的拒绝只影响采集。宿主在实际调用结束时独立结算已登记操作；插件完成声明不等于 ContextView 已被采用。

宿主最多接受每插件 8 项操作、32 项指标、6 组核心展示；单次调用最多 16 项操作、2 层父子关系及 100 条业务报告。运行中调用／句柄最多 256 个；观测保留最近 1,000 条事件和 100 个上下文，每页最多 50 条。超限只影响采集，宿主仍须将操作结算为明确终态。

本级实际接入 Context 调用；非 Context 模板用于验证通用上报契约。其他能力须由宿主实现对应的执行入口，不因 Component 能实例化就视为已支持。
