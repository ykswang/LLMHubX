<div align="center">

# LLMHubX

### 面向 AI 编程客户端的本地 Provider 与 Agent Host

集中管理上游 Provider、模型与凭证，通过统一的本地入口连接 Codex、Claude Code、Kiro 等客户端，并在请求执行链中提供路由、观测和受控 WASM 插件能力。

[**下载 macOS 版**](https://github.com/ykswang/LLMHubX/releases/download/app-v20260905.1321-2/LLMHubX_20260905.1321-2_aarch64.dmg) · [查看更新说明](https://github.com/ykswang/LLMHubX/releases/tag/app-v20260905.1321-2) · [Marketplace 索引](./marketplace.toml)

![macOS](https://img.shields.io/badge/macOS-Apple%20Silicon-111827?style=flat-square&logo=apple&logoColor=white)
![App](https://img.shields.io/badge/App-20260905.1321--2-2563eb?style=flat-square)
![Plugin ABI](https://img.shields.io/badge/Plugin%20ABI-Level%202-059669?style=flat-square)
![WASM](https://img.shields.io/badge/Plugins-CMW-7c3aed?style=flat-square)

</div>

> [!NOTE]
> 这是 LLMHubX 的官方公开分发仓库，用于发布 App、插件 ABI、SDK 和插件包，不存放产品源码。

## 为什么使用 LLMHubX

| | 能力 | 说明 |
|---|---|---|
| 🔐 | 集中管理凭证 | 上游 API Key 保留在 LLMHubX 中，客户端只使用本地地址和本地访问凭证。 |
| 🧭 | 统一模型入口 | 将客户端使用的逻辑 Model ID 映射到 Provider Route，集中维护模型与路由配置。 |
| 🔎 | 请求观测 | 在独立观测窗口查看请求、执行链路、延迟和插件队列状态。 |
| 🧩 | 受控插件 | 通过 CMW 运行 WASM 插件，并在安装时明确展示 Hook、Resource 能力与数据权限。 |
| 🤖 | Agentic Workflow | 管家可以把较长任务放到后台，由 Focus 规划并交给 Expert 分步完成。 |
| 🛠️ | 开发工具链 | 提供版本化 ABI、CMW Rust SDK、模板与 conformance 工具。 |

## 快速开始

1. 下载最新的 [Apple Silicon DMG](https://github.com/ykswang/LLMHubX/releases/download/app-v20260905.1321-2/LLMHubX_20260905.1321-2_aarch64.dmg)。
2. 打开 DMG，将 `LLMHubX.app` 拖入“应用程序”。
3. 在 LLMHubX 中配置 Provider、上游模型、逻辑模型和本地 API Key。
4. 在外部客户端中使用 LLMHubX 生成的本地地址与访问配置。

## App 下载

| 项目 | 当前版本 |
|---|---|
| 版本 | `20260905.1321-2` |
| 平台 | macOS · Apple Silicon |
| Plugin ABI | 当前 Level 2 · 最低兼容 Level 1 |
| 安装包 | [LLMHubX_20260905.1321-2_aarch64.dmg](https://github.com/ykswang/LLMHubX/releases/download/app-v20260905.1321-2/LLMHubX_20260905.1321-2_aarch64.dmg) |
| 更新说明 | [GitHub Release](https://github.com/ykswang/LLMHubX/releases/tag/app-v20260905.1321-2) |
| SHA-256 | [SHA256SUMS.txt](https://github.com/ykswang/LLMHubX/releases/download/app-v20260905.1321-2/SHA256SUMS.txt) |

下载后可在终端核对文件：

```bash
shasum -a 256 ~/Downloads/LLMHubX_20260905.1321-2_aarch64.dmg
```

将输出与 Release 中的 `SHA256SUMS.txt` 对比。

> [!IMPORTANT]
> 当前 `20260905.1321-2` 为 adhoc 签名构建，尚未使用 Apple Developer ID 签名或完成 notarization，macOS Gatekeeper 不会自动信任。安装前请先核对 SHA-256；首次启动如被系统阻止，请在“系统设置 → 隐私与安全”中确认 App 来源后再决定是否允许打开。

> [!WARNING]
> `20260831.1009` 和 `20260905.0836` 的已发布二进制无法解析自身内部 `.0` 版本，请手动下载安装 `20260905.1321-2`。本版本不再把新密钥写入 macOS Keychain。首次读取旧配置时可选择一次性导入旧密钥；macOS 可能对每项旧密钥请求一次授权，导入完成后不再访问 Keychain。也可选择“重新配置”，完全跳过 Keychain，并在修改配置前保留备份。

## 插件开发

当前公开契约为 **Plugin ABI Level 2**，并继续兼容 Level 1。Level 2 增加 Workflow 与 Expert Agent contribution；SDK 包包含目标 ABI 的 WIT 快照、生成绑定和接入文档。

### ABI

| ABI Level | 版本 | 下载 | 说明与变更 | 校验 |
|---:|---|---|---|---|
| 1 | `20260829.2102-1` | [tar.gz](./abi/1/20260829.2102-1/LLMHubX_Plugin_ABI_20260829.2102-1.tar.gz?raw=1) | [目录](./abi/1/20260829.2102-1/) · [CHANGELOG](./abi/1/20260829.2102-1/CHANGELOG.md) | [SHA256SUMS](./abi/1/20260829.2102-1/SHA256SUMS.txt) |
| 2 | `20260830.1046-2` | [tar.gz](./abi/2/20260830.1046-2/LLMHubX_Plugin_ABI_20260830.1046-2.tar.gz?raw=1) | [目录](./abi/2/20260830.1046-2/) · [CHANGELOG](./abi/2/20260830.1046-2/CHANGELOG.md) | [SHA256SUMS](./abi/2/20260830.1046-2/SHA256SUMS.txt) |

### SDK

| Runtime | 语言 | Target ABI | 版本 | 下载 | 文档 |
|---|---|---:|---|---|---|
| CMW | Rust | 1 | `20260831.1009-1` | [tar.gz](./sdks/cmw/rust/1/20260831.1009-1/LLMHubX_Plugin_SDK_CMW_Rust_20260831.1009-1.tar.gz?raw=1) | [目录与更新说明](./sdks/cmw/rust/1/20260831.1009-1/) |
| CMW | Rust | 2 | `20260831.1009-2` | [tar.gz](./sdks/cmw/rust/2/20260831.1009-2/LLMHubX_Plugin_SDK_CMW_Rust_20260831.1009-2.tar.gz?raw=1) | [目录与更新说明](./sdks/cmw/rust/2/20260831.1009-2/) |

## 官方插件

### 最小化思考

在实际 Route 成员支持关闭思考时关闭思考；否则选择该成员公开的最低思考档位。

| 项目 | 内容 |
|---|---|
| 插件 ID | `llmhubx.minimize-reasoning` |
| 版本 | `20260829.2102-1` |
| Runtime | CMW |
| Hook | `member-request-transform` |
| 权限 | `request.reasoning.write`、`observation.annotate` |
| 下载 | [minimize-reasoning_20260829.2102-1.lhxp](./plugins/llmhubx.minimize-reasoning/20260829.2102-1/minimize-reasoning_20260829.2102-1.lhxp?raw=1) |
| 版本信息 | [release.toml](./plugins/llmhubx.minimize-reasoning/20260829.2102-1/release.toml) · [CHANGELOG](./plugins/llmhubx.minimize-reasoning/20260829.2102-1/CHANGELOG.md) · [SHA256SUMS](./plugins/llmhubx.minimize-reasoning/20260829.2102-1/SHA256SUMS.txt) |

### Fake User Agent · 虚拟身份

使用用户配置的 User-Agent 替换客户端原始身份，再将请求发送给 Provider。首次启用时填写身份，之后可以在插件编辑界面继续修改。

| 项目 | 内容 |
|---|---|
| 插件 ID | `llmhubx.fake-user-agent` |
| 版本 | `20260829.2102-1` |
| Runtime | CMW |
| Hook | `request-transform` |
| 权限 | `request.headers.write`，授权范围限定为 `user-agent` |
| 下载 | [fake-user-agent_20260829.2102-1.lhxp](./plugins/llmhubx.fake-user-agent/20260829.2102-1/fake-user-agent_20260829.2102-1.lhxp?raw=1) |
| 版本信息 | [release.toml](./plugins/llmhubx.fake-user-agent/20260829.2102-1/release.toml) · [CHANGELOG](./plugins/llmhubx.fake-user-agent/20260829.2102-1/CHANGELOG.md) · [SHA256SUMS](./plugins/llmhubx.fake-user-agent/20260829.2102-1/SHA256SUMS.txt) |

### SQLite Resource Provider

在受限 Workspace 中使用 SQLite 提供中性的 KV 与关系数据能力。

| 项目 | 内容 |
|---|---|
| 插件 ID | `llmhubx.resource-sqlite` |
| 版本 | `20260829.2102-1` |
| Runtime | CMW |
| 提供能力 | `resource.kv`、`resource.relational` |
| 权限 | `resource.provider.workspace` |
| 下载 | [resource-sqlite_20260829.2102-1.lhxp](./plugins/llmhubx.resource-sqlite/20260829.2102-1/resource-sqlite_20260829.2102-1.lhxp?raw=1) |
| 版本信息 | [release.toml](./plugins/llmhubx.resource-sqlite/20260829.2102-1/release.toml) · [CHANGELOG](./plugins/llmhubx.resource-sqlite/20260829.2102-1/CHANGELOG.md) · [SHA256SUMS](./plugins/llmhubx.resource-sqlite/20260829.2102-1/SHA256SUMS.txt) |

### Basic Steward

提供 LLMHubX 官方基础管家模型和稳定的 Agent 定义。

| 项目 | 内容 |
|---|---|
| 插件 ID | `llmhubx.basic-steward` |
| 版本 | `20260829.2102-1` |
| Runtime | CMW |
| Agent contribution | `steward:basic-steward` |
| 权限 | 无 |
| 下载 | [basic-steward_20260830.1046-2.lhxp](./plugins/llmhubx.basic-steward/20260830.1046-2/basic-steward_20260830.1046-2.lhxp?raw=1) |
| 版本信息 | [release.toml](./plugins/llmhubx.basic-steward/20260830.1046-2/release.toml) · [CHANGELOG](./plugins/llmhubx.basic-steward/20260830.1046-2/CHANGELOG.md) · [SHA256SUMS](./plugins/llmhubx.basic-steward/20260830.1046-2/SHA256SUMS.txt) |

### Basic Workflow

让管家把较长任务拆成步骤，在 BotX 保持可聊天的同时持续推进后台 Task。

| 项目 | 内容 |
|---|---|
| 插件 ID | `llmhubx.basic-workflow` |
| 版本 | `20260830.1046-2` |
| Runtime | CMW |
| Agent contribution | `workflow:basic-workflow` |
| 权限 | 无 |
| 下载 | [basic-workflow_20260830.1046-2.lhxp](./plugins/llmhubx.basic-workflow/20260830.1046-2/basic-workflow_20260830.1046-2.lhxp?raw=1) |
| 版本信息 | [release.toml](./plugins/llmhubx.basic-workflow/20260830.1046-2/release.toml) · [CHANGELOG](./plugins/llmhubx.basic-workflow/20260830.1046-2/CHANGELOG.md) · [SHA256SUMS](./plugins/llmhubx.basic-workflow/20260830.1046-2/SHA256SUMS.txt) |

### General Expert

在没有更匹配的专业 Expert 时，处理不依赖外部工具的通用分析、总结、转换与文本生成步骤。

| 项目 | 内容 |
|---|---|
| 插件 ID | `llmhubx.general-expert` |
| 版本 | `20260830.1046-2` |
| Runtime | CMW |
| Agent contribution | `expert:general-expert` |
| 权限 | 无 |
| 下载 | [general-expert_20260830.1046-2.lhxp](./plugins/llmhubx.general-expert/20260830.1046-2/general-expert_20260830.1046-2.lhxp?raw=1) |
| 版本信息 | [release.toml](./plugins/llmhubx.general-expert/20260830.1046-2/release.toml) · [CHANGELOG](./plugins/llmhubx.general-expert/20260830.1046-2/CHANGELOG.md) · [SHA256SUMS](./plugins/llmhubx.general-expert/20260830.1046-2/SHA256SUMS.txt) |

### Pi Context

为 Steward Agent 提供滚动摘要与近期原文组成的时间顺序 ContextView。

| 项目 | 内容 |
|---|---|
| 插件 ID | `llmhubx.pi-context` |
| 版本 | `20260830.0010-1` |
| Runtime | CMW |
| Agent contribution | `context:pi-context` |
| 依赖能力 | `resource.kv` |
| 权限 | `agent.context.inference`、`resource.kv.read`、`resource.kv.write` |
| 下载 | [pi-context_20260830.0010-1.lhxp](./plugins/llmhubx.pi-context/20260830.0010-1/pi-context_20260830.0010-1.lhxp?raw=1) |
| 版本信息 | [release.toml](./plugins/llmhubx.pi-context/20260830.0010-1/release.toml) · [CHANGELOG](./plugins/llmhubx.pi-context/20260830.0010-1/CHANGELOG.md) · [SHA256SUMS](./plugins/llmhubx.pi-context/20260830.0010-1/SHA256SUMS.txt) |

## 发布与目录规则

- App 通过 GitHub Release 分发；只有 App Release 会标记为 GitHub `Latest`。
- ABI、SDK 和插件使用仓库内不可变版本目录，已发布版本不会覆盖或改写。
- [`marketplace.toml`](./marketplace.toml) 是 App 更新、插件市场及开发资源发现使用的机器可读索引。

```text
abi/ABI_LEVEL/VERSION/
sdks/RUNTIME/LANGUAGE/ABI_LEVEL/VERSION/
plugins/PLUGIN_ID/PLUGIN_VERSION/
```

历史 GitHub Release 作为旧分发记录保留；新的 ABI、SDK 和插件版本不再创建 GitHub Release。
