# 隐私中转站公开进度

> 核对日期：2026-09-30
>
> 当前公开版本：`0.10.5-beta` / versionCode `133`，状态：Beta

## 0.10.5-beta 安全与可靠性加固

- 收紧分享输入与无障碍自动填码边界，降低数据库操作对界面的阻塞，并加强异步任务生命周期管理。
- 加强备份/恢复隔离、分类跨存储失败恢复和设置异步渲染稳定性。设置页回归在 Release → Release 验证中被发现并修复后，完整 API 35 instrumentation 通过 39/39。
- Debug / Release JVM 各 255/255；Debug / Release Lint 均 0 errors。0.10.4-beta → 0.10.5-beta Release 覆盖升级后，安全箱内容、分类、Home tag 和设置值均保留。
- Room schema v9、Backup payload v5；未新增 INTERNET、ACCESS_NETWORK_STATE 或 QUERY_ALL_PACKAGES。
- 当前最新经过审计的 Source Available 快照仍为 0.10.4-beta；0.10.5-beta 源码快照将在独立审计后发布。

## 0.10.4-beta 身份边界与备份保护

- 原生 Autofill 凭据按目标包名与当前安装应用签名身份共同约束；来源无法可信验证时 fail-closed。网页 Autofill 暂停自动填入，已有网页凭据数据保留。
- Room schema v9 增加 nullable signer digest；加密离线备份 v5 兼容读取 v1–v4，恢复时仅在本机签名匹配时保留绑定。
- 系统备份和设备迁移规则排除应用数据存储域；`allowBackup=false` 保持不变，用户主动加密离线备份继续可用。
- Debug / Release JVM 各 220/220；API 35 instrumentation 28/28，migration 8/8；Debug / Release Lint 均 0 errors。正式包使用已验收功能源码和沿用的正式签名；仪器测试在候选功能源码阶段完成。
- 产物 SHA-256、签名、权限及覆盖限制见 [安全与构建证据](SecurityEvidence.md) 与 [0.10.4 发布说明](Release-0.10.4.md)。真实第三方 Autofill 页面、多 ROM / 实体设备完整矩阵未覆盖。

## 0.10.3-beta 百度网盘通知栏流程修正

- 对含有效百度网盘提取码的通知栏“保存并跳转”，在网盘自动化、Pro 权益、无障碍服务和支持浏览器均符合条件时，显式打开浏览器并准备一次性填码，避免 Android App Link 跳过浏览器页面。
- 仅执行一次性文本填入；不自动确认、登录、下载或支付。host / 浏览器校验失败时保留原有路由。
- 版本 `0.10.3-beta / 131`，沿用此前正式签名；APK 哈希与完整权限证据见 [安全与构建证据](SecurityEvidence.md)。

## 0.10.2-beta 增量更新

- 修复安全箱异步加载时短暂显示“新建安全箱内容”的闪现。
- 设置页进入和返回不再出现与另外两个主页面不一致的横向转场。
- 通知栏关闭操作使用更短的“关闭通知按钮”文案。
- 沿用 0.10.1-beta 的功能、安全边界与正式签名证书；新包可以覆盖升级。

## 0.10.1-beta 本地安全与使用稳定性

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
