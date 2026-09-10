# Level 3 兼容边界

- Level 1/2 包继续沿原 world 加载，无需重编译。
- Level 3 包须声明 CMW Level 3，并实现业务观测 world；包声明的能力仍须分别通过原有 conformance。
- 仅 Context 的 Level 3 包不依赖 Workflow world；声明 Workflow 的包仍须通过 Workflow conformance。
- 未支持 Level 3 的宿主应在安装检查中拒绝包，不能等到调用时才暴露缺失 import。
- 使用业务观测插件前，应确认 App 的支持区间包含 Level 3。宿主可同时支持 `[1,3]`；这不表示所有 Manifest v2 能力均已实现对应的调用入口。
