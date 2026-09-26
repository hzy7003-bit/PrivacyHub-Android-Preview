# 隐私与权限说明

隐私中转站的设计目标是让分享链接和本地安全箱尽量在设备本地完成。

## 网络

`0.10.1-beta`（versionCode `129`）采用 local-first / offline 设计，Release APK 不声明 `INTERNET` 或 `ACCESS_NETWORK_STATE` 权限，不接入广告 SDK、统计 SDK 或云同步服务。

## 本地数据

用户保存的内容保存在本地安全箱中。正式数据库使用 Room + SQLCipher，数据库密钥由 Android Keystore 管理。本版提升了数据库密钥持久化可靠性，改进加密离线备份的合并与替换恢复一致性。

Release APK 设置 `allowBackup=false`、`debuggable=false`；用户可主动使用 Pro 加密离线备份功能。诊断记录进一步脱敏，提交反馈前仍应检查截图和文字，避免包含账号、设备码、激活码或安全箱正文。

## 已使用权限

- `POST_NOTIFICATIONS`：显示用户主动开启的通知栏保存入口
- `RECEIVE_BOOT_COMPLETED`：用户同时开启通知栏入口与开机恢复选项后，重启设备时尝试恢复入口
- `FOREGROUND_SERVICE` / `FOREGROUND_SERVICE_SPECIAL_USE`：维持用户主动开启的通知栏快捷入口
- `USE_BIOMETRIC` / `USE_FINGERPRINT`：敏感模块可选安全验证

## 可选系统服务

- Android Autofill：仅在用户主动将隐私中转站设为系统自动填充服务后生效
- 网盘提取码辅助：仅在 Pro 用户主动开启专用无障碍服务后生效，默认关闭

网盘提取码辅助只执行用户已保存提取码的一次性文本填入，不自动点击确认、登录、下载或支付。基础保存、分享接收、安全箱和链接路由均不依赖无障碍服务。

本版加强 Autofill 网站作用域隔离与网盘提取码目标网站限制；这些 Beta 功能仍受目标页面和浏览器兼容性影响。

## 后台与电量策略

通知栏入口启用后，后台服务只负责维持系统前台通知。空闲期间不轮询剪贴板、不发起网络请求、不执行定时扫描、不重复写入数据库，也不持有唤醒锁。读取、解析和保存只在用户点击通知动作后短暂执行。

服务使用 `START_STICKY` 提高被系统回收后的恢复机会；App 更新时尝试刷新已开启的通知栏入口，设备重启后的恢复由单独的开机恢复选项控制。这些机制旨在兼顾长时间可用性与低后台占用，不绕过 Android 电量管理，也不保证在所有厂商 ROM 上永久存活。

## 不使用的权限

- 不申请 `INTERNET`
- 不申请 `ACCESS_NETWORK_STATE`
- 不申请 `QUERY_ALL_PACKAGES`
- 基础功能不要求开启无障碍服务
- 不申请 Root
- 不申请后台高耗电白名单

最新版 APK 的完整权限清单、哈希和签名证书摘要见：[安全与构建证据](SecurityEvidence.md)。
