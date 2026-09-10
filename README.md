<div align="center">

# LLMHubX

### 面向 AI 编程客户端的本地 Provider 与 Agent Host

集中管理上游 Provider、模型与凭证，通过统一的本地入口连接 Codex、Claude Code、Kiro 等客户端，并在请求执行链中提供路由、观测和受控 WASM 插件能力。

[**下载 macOS 版**](https://github.com/ykswang/LLMHubX/releases/download/app-v20260911.0014-3/LLMHubX_20260911.0014-3_aarch64.dmg) · [查看更新说明](https://github.com/ykswang/LLMHubX/releases/tag/app-v20260911.0014-3) · [Marketplace 索引](./marketplace.toml)

![macOS](https://img.shields.io/badge/macOS-Apple%20Silicon-111827?style=flat-square&logo=apple&logoColor=white)
![App](https://img.shields.io/badge/App-20260911.0014--3-2563eb?style=flat-square)
![Plugin ABI](https://img.shields.io/badge/Plugin%20ABI-Level%203-059669?style=flat-square)
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

1. 下载最新的 [Apple Silicon DMG](https://github.com/ykswang/LLMHubX/releases/download/app-v20260911.0014-3/LLMHubX_20260911.0014-3_aarch64.dmg)。
2. 打开 DMG，将 `LLMHubX.app` 拖入“应用程序”。
3. 在 LLMHubX 中配置 Provider、上游模型、逻辑模型和本地 API Key。
4. 在外部客户端中使用 LLMHubX 生成的本地地址与访问配置。

## App 下载

| 项目 | 当前版本 |
|---|---|
| 版本 | `20260911.0014-3` |
| 平台 | macOS · Apple Silicon |
| Plugin ABI | 当前 Level 3 · 最低兼容 Level 1 |
| 安装包 | [LLMHubX_20260911.0014-3_aarch64.dmg](https://github.com/ykswang/LLMHubX/releases/download/app-v20260911.0014-3/LLMHubX_20260911.0014-3_aarch64.dmg) |
| 更新说明 | [GitHub Release](https://github.com/ykswang/LLMHubX/releases/tag/app-v20260911.0014-3) |
| SHA-256 | [SHA256SUMS.txt](https://github.com/ykswang/LLMHubX/releases/download/app-v20260911.0014-3/SHA256SUMS.txt) |

下载后可在终端核对文件：

```bash
shasum -a 256 ~/Downloads/LLMHubX_20260911.0014-3_aarch64.dmg
```

将输出与 Release 中的 `SHA256SUMS.txt` 对比。

> [!IMPORTANT]
> 当前 `20260911.0014-3` 为 adhoc 签名构建，尚未使用 Apple Developer ID 签名或完成 notarization，macOS Gatekeeper 不会自动信任。安装前请先核对 SHA-256；首次启动如被系统阻止，请在“系统设置 → 隐私与安全”中确认 App 来源后再决定是否允许打开。

> [!WARNING]
> `20260831.1009` 和 `20260905.0836` 的已发布二进制无法解析自身内部 `.0` 版本；`20260907.0228-2`（界面显示 `20260907.228.2`）也存在前导零解析缺陷。上述版本请手动下载安装 `20260911.0014-3`。本版本不再把新密钥写入 macOS Keychain。首次读取旧配置时可选择一次性导入旧密钥；macOS 可能对每项旧密钥请求一次授权，导入完成后不再访问 Keychain。也可选择“重新配置”，完全跳过 Keychain，并在修改配置前保留备份。

### 本次更新

修复 DeepSeek 思考模式下 Main 已回复后，Focus 因继承历史缺少 reasoning_content 而被 HTTP 400 拒绝的问题。继承的历史作为带来源标记的参考资料，本次任务独立输入，Focus 自身工具回合仍保留实际思考内容。327 项 App 回归及实际 Host 的 15 次本地 HTTP 请求通过，真实服务与原生界面待安装后验收。

保留工具名转换与 JSON 错误正文捕获。本次只需更新 App，已安装下述 Pi Context 版本时无需重装。

补充当前摘要采用时间，复用不刷新，记录缺失不猜测；明确明细淘汰后的累计口径，多会话列表显示管家名称。

再次压缩时优先显示当前处理状态，避免被上一轮已采用摘要的状态遮盖；多会话列表分别更新各自状态。压缩阈值与可用预算分别展示，并通过真实插件边界测试。

修复用户取消在 WASM 中断路径被业务指标误计为超时失败的问题；取消与真正超时分别结算，未采用摘要不计成功。

插件观测改为插件声明的业务卡片，展示上下文占用、压缩效果和推理开销。折叠运行诊断保留最大内存、执行／等待明细及处理速率。需配套安装并启用新版 [Pi Context](./plugins/llmhubx.pi-context/20260910.2138.3/)。同时修复内部 DeepSeek 工具请求的自动参数冲突和本地失败诊断，以及新版插件的安装、市场下载校验与兼容绑定升级。保留现有工具执行和模型能力约束。

已完成本地确定性测试、真实 WASM 与旧版摘要升级验证；真实服务和原生界面仍待用户验收。详细变更见[更新说明](https://github.com/ykswang/LLMHubX/releases/tag/app-v20260911.0014-3)。

## 插件开发

当前公开契约为 **Plugin ABI Level 3**，并继续兼容 Level 1/2。Level 3 增加类型化业务指标声明与上报；SDK 包包含目标 ABI 的 WIT、生成绑定、模板和接入文档。新版 pi-context 已接入业务观测，其他旧插件仍可使用基础诊断。

### ABI

| ABI Level | 版本 | 下载 | 说明与变更 | 校验 |
|---:|---|---|---|---|
| 1 | `20260829.2102-1` | [tar.gz](./abi/1/20260829.2102-1/LLMHubX_Plugin_ABI_20260829.2102-1.tar.gz?raw=1) | [目录](./abi/1/20260829.2102-1/) · [CHANGELOG](./abi/1/20260829.2102-1/CHANGELOG.md) | [SHA256SUMS](./abi/1/20260829.2102-1/SHA256SUMS.txt) |
| 2 | `20260830.1046-2` | [tar.gz](./abi/2/20260830.1046-2/LLMHubX_Plugin_ABI_20260830.1046-2.tar.gz?raw=1) | [目录](./abi/2/20260830.1046-2/) · [CHANGELOG](./abi/2/20260830.1046-2/CHANGELOG.md) | [SHA256SUMS](./abi/2/20260830.1046-2/SHA256SUMS.txt) |
| 3 | `20260910.2138-3` | [tar.gz](./abi/3/20260910.2138-3/LLMHubX_Plugin_ABI_20260910.2138-3.tar.gz?raw=1) | [目录](./abi/3/20260910.2138-3/) · [CHANGELOG](./abi/3/20260910.2138-3/CHANGELOG.md) | [SHA256SUMS](./abi/3/20260910.2138-3/SHA256SUMS.txt) |

### SDK

| Runtime | 语言 | Target ABI | 版本 | 下载 | 文档 |
|---|---|---:|---|---|---|
| CMW | Rust | 1 | `20260831.1009-1` | [tar.gz](./sdks/cmw/rust/1/20260831.1009-1/LLMHubX_Plugin_SDK_CMW_Rust_20260831.1009-1.tar.gz?raw=1) | [目录与更新说明](./sdks/cmw/rust/1/20260831.1009-1/) |
| CMW | Rust | 2 | `20260831.1009-2` | [tar.gz](./sdks/cmw/rust/2/20260831.1009-2/LLMHubX_Plugin_SDK_CMW_Rust_20260831.1009-2.tar.gz?raw=1) | [目录与更新说明](./sdks/cmw/rust/2/20260831.1009-2/) |
| CMW | Rust | 3 | `20260910.2138-3` | [tar.gz](./sdks/cmw/rust/3/20260910.2138-3/LLMHubX_Plugin_SDK_CMW_Rust_20260910.2138-3.tar.gz?raw=1) | [目录与更新说明](./sdks/cmw/rust/3/20260910.2138-3/) |

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

维护滚动摘要与近期原文，并提供上下文占用、压缩效果和业务事件。需先安装 ABI 3 App，再安装并启用新版插件；详见[升级说明](./plugins/llmhubx.pi-context/20260910.2138.3/README.md)。

| 项目 | 内容 |
|---|---|
| 插件 ID | `llmhubx.pi-context` |
| 版本 | `20260910.2138.3` |
| Runtime | CMW |
| Agent contribution | `context:pi-context` |
| 依赖能力 | `resource.kv` |
| 权限 | `agent.context.inference`、`resource.kv.read`、`resource.kv.write` |
| 下载 | [pi-context_20260910.2138.3.lhxp](./plugins/llmhubx.pi-context/20260910.2138.3/pi-context_20260910.2138.3.lhxp?raw=1) |
| 版本信息 | [release.toml](./plugins/llmhubx.pi-context/20260910.2138.3/release.toml) · [CHANGELOG](./plugins/llmhubx.pi-context/20260910.2138.3/CHANGELOG.md) · [SHA256SUMS](./plugins/llmhubx.pi-context/20260910.2138.3/SHA256SUMS.txt) |

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
