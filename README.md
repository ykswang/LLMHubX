# LLMHubX

这是 LLMHubX 的公开分发仓库，不是源码仓库。

- App 通过 GitHub Release 分发。
- 插件 ABI、各语言 SDK 和插件包直接保存在本仓库的不可变版本目录中。
- App 内更新检查、插件市场和 SDK 下载以 [`marketplace.toml`](./marketplace.toml) 为机器可读索引。

## App

最新版本：`20260826.1259-1`，当前 ABI Level 1，最低兼容 ABI Level 1。

- [下载 Apple Silicon DMG](https://github.com/ykswang/LLMHubX/releases/download/app-v20260826.1259-1/LLMHubX_20260826.1259-1_aarch64.dmg)
- [查看 Release](https://github.com/ykswang/LLMHubX/releases/tag/app-v20260826.1259-1)
- [更新日志](https://github.com/ykswang/LLMHubX/releases/download/app-v20260826.1259-1/app-CHANGELOG.md)

## 插件 ABI

| ABI Level | 版本 | 下载 | 更新日志 | 校验文件 |
|---|---|---|---|---|
| 1 | `20260826.1021-1` | [tar.gz](./abi/1/20260826.1021-1/LLMHubX_Plugin_ABI_20260826.1021-1.tar.gz?raw=1) | [CHANGELOG](./abi/1/20260826.1021-1/CHANGELOG.md) | [SHA256SUMS](./abi/1/20260826.1021-1/SHA256SUMS.txt) |

## 插件 SDK

| Runtime | 语言 | Target ABI | 版本 | 下载 | 更新日志 |
|---|---|---:|---|---|---|
| Extism v1 | Rust | 1 | `20260826.1021-1` | [tar.gz](./sdks/extism/v1/rust/1/20260826.1021-1/LLMHubX_Plugin_SDK_Extism_Rust_20260826.1021-1.tar.gz?raw=1) | [CHANGELOG](./sdks/extism/v1/rust/1/20260826.1021-1/CHANGELOG.md) |
| Extism v1 | JavaScript | 1 | `20260826.1021-1` | [tar.gz](./sdks/extism/v1/javascript/1/20260826.1021-1/LLMHubX_Plugin_SDK_Extism_JavaScript_20260826.1021-1.tar.gz?raw=1) | [CHANGELOG](./sdks/extism/v1/javascript/1/20260826.1021-1/CHANGELOG.md) |
| Extism v1 | TypeScript | 1 | `20260826.1021-1` | [tar.gz](./sdks/extism/v1/typescript/1/20260826.1021-1/LLMHubX_Plugin_SDK_Extism_TypeScript_20260826.1021-1.tar.gz?raw=1) | [CHANGELOG](./sdks/extism/v1/typescript/1/20260826.1021-1/CHANGELOG.md) |
| CMW v1 | Rust | 1 | `20260826.1021-1` | [tar.gz](./sdks/cmw/v1/rust/1/20260826.1021-1/LLMHubX_Plugin_SDK_CMW_Rust_20260826.1021-1.tar.gz?raw=1) | [CHANGELOG](./sdks/cmw/v1/rust/1/20260826.1021-1/CHANGELOG.md) |

每个 SDK 包都包含目标 ABI 的 WIT 快照、生成绑定、Markdown 接入文档、最小模板、示例和本地 conformance 工具。

## 插件

### 最小化思考

在实际 Route 成员支持关闭思考时关闭思考；否则选择该成员公开的最低思考档位。插件同时提供 Extism v1 和 CMW v1 两种 Rust 产物，目标 ABI Level 1。

- 插件 ID：`llmhubx.minimize-reasoning`
- 最新版本：`20260826.1021-1`
- 权限：`request.reasoning.write`、`observation.annotate`
- Hook：`member-request-transform`
- [下载插件](./plugins/llmhubx.minimize-reasoning/20260826.1021-1/minimize-reasoning_20260826.1021-1.lhxp?raw=1)
- [版本元数据](./plugins/llmhubx.minimize-reasoning/20260826.1021-1/release.toml)
- [更新日志](./plugins/llmhubx.minimize-reasoning/20260826.1021-1/CHANGELOG.md)
- [校验文件](./plugins/llmhubx.minimize-reasoning/20260826.1021-1/SHA256SUMS.txt)

## 目录规则

```text
abi/ABI_LEVEL/VERSION/
sdks/RUNTIME/LANGUAGE/ABI_LEVEL/VERSION/
plugins/PLUGIN_ID/PLUGIN_VERSION/
```

ABI、SDK 和插件的已发布版本目录不可覆盖。历史 GitHub Release 仅作为旧分发记录保留；新的非 App 版本不会再创建 GitHub Release。
