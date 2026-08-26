# Fake User Agent 20260826.1554-1

首个正式版本。

- 新增“虚拟身份”官方插件，可使用用户配置的 User-Agent 替换客户端原始 User-Agent 后再发送给 Provider。
- 首次启用时要求填写 User-Agent；启用后可在插件编辑界面继续修改，保存后从下一次请求开始生效。
- 权限限定为 `request.headers.write` 的 `user-agent` 精确范围，不读取或修改认证 Header。
- 同时提供 Extism v1 与 CMW v1 两个 Rust Runtime 产物，目标 ABI Level 1。
- 插件停用后恢复 LLMHubX 默认的客户端 User-Agent 继承行为；虚拟值不会改变当前请求用于插件匹配的原始身份。
