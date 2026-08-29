# Pi Context 20260830.0010-1

## 修复

- 图片等不可压缩 Context Source 始终保留为原始来源，不再被滚动摘要错误覆盖或丢弃。
- 滚动摘要按实际已摘要的 Source ID 计算活跃来源，允许摘要序列范围内保留不可压缩来源。
- 插件升级或 Context 配置变化后丢弃不兼容的派生 checkpoint，并从 Kernel 保存的原始消息安全重建。
- checkpoint 实现 revision 与 Bundle 发布版本分离，避免普通版本发布造成错误的不兼容判断。
