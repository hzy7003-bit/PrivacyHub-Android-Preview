# 隐私中转站公开进度

> 核对日期：2026-09-27
>
> 当前公开版本：`0.10.1-beta` / versionCode `129`，状态：Beta

## 本次更新

- 提升本地数据库密钥持久化可靠性，改进加密备份合并 / 替换恢复一致性。
- 加强 Autofill 网站作用域隔离、网盘提取码目标网站限制与诊断记录脱敏。
- 改进通知栏 / 磁贴保存、后台通知恢复，以及 Pro / 设置异常状态保护。
- 完成 Material 3 UI 一致性收尾；保留中转 / 安全箱 / 设置三入口和花形标识。
- 支持 Android 8.0 / API 26+，沿用同一正式签名证书；具体权限和 APK 哈希见 [安全证据](SecurityEvidence.md)。

## 已实现的免费功能

- 系统分享和长按文本处理入口。
- 通知栏“保存到安全箱”和“保存并跳转”。
- 控制中心磁贴辅助保存。
- 本地加密安全箱、搜索、收藏、最近保存和分类管理。
- 淘宝、京东、拼多多、小红书、抖音、快手、B 站、微博和普通网页识别。
- 百度、夸克、迅雷、阿里、蓝奏、123、天翼和移动网盘识别。
- 淘宝购物口令、普通代付、闪购代付以及 `m.tb.cn`、`e.tb.cn` 短链路由。
- 浅色、深色、跟随系统、可选安全锁、可选禁止截图和后台隐藏。
- 完全本地的脱敏诊断报告。

## 已实现的 Pro 功能

- ECDSA P-256 离线永久 License 和设备绑定。
- AES-256-GCM 加密离线备份与跨设备恢复。
- Android Autofill 系统自动填充 Beta。
- 网盘提取码辅助 Beta，只执行用户授权的一次性填入。

## 隐私与安全

- APK 不声明 `INTERNET`、`ACCESS_NETWORK_STATE` 或 `QUERY_ALL_PACKAGES`。
- 无广告、无统计 SDK、无云同步。
- 安全箱使用 Room + SQLCipher。
- 数据库密钥、License 和敏感设置使用 Android Keystore 保护。
- Release APK 启用 R8/ProGuard 混淆压缩和资源收缩，并使用正式证书签名。
- `allowBackup=false`、`debuggable=false`，继续 local-first / offline 运行。

## 已知系统边界

- Android 10+ 和厂商 ROM 会限制后台剪切板读取、通知常驻和磁贴行为。
- 系统强制停止后的后台恢复受 Android / ROM 控制。
- 系统长按文本菜单是否展示入口由来源 App 和 ROM 决定。
- 第三方 App 可随版本改变 Deep Link 和 Autofill 支持。
- App 无法清除输入法自己的历史或厂商私有云剪切板。
- Debug 与 Release 证书不同，不能直接覆盖安装。

## 当前验证状态

- 本次正式 Release APK 的大小、SHA-256 与正式签名证书摘要已独立复核，v2 / v3 签名验证通过。
- 包名、版本、minSdk / targetSdk、非调试与禁用系统备份标志已从 APK 复核。
- Manifest 未声明 `INTERNET`、`ACCESS_NETWORK_STATE` 或 `QUERY_ALL_PACKAGES`。
- 公开文件与复查命令见 [安全与构建证据](SecurityEvidence.md)。这不代表全 ROM 或所有第三方业务均已兼容。

## 未完成

- 高级搜索、高级标签、批量导入导出和高级路由规则尚未作为可用功能发布。
- 抖音代付没有可靠公开 Deep Link，当前不提供不稳定的自动跳转。
- 三星、HyperOS、ColorOS、HarmonyOS/EMUI 和 MagicOS 的完整兼容矩阵仍在扩展。
