# 隐私与权限说明

隐私中转站的设计目标是让分享链接和本地安全箱尽量在设备本地完成。

## 网络

当前测试版默认不申请 `INTERNET` 权限，不接入广告 SDK、统计 SDK 或云同步服务。

## 本地数据

用户保存的内容保存在本地安全箱中。正式数据库使用 SQLCipher 加密，数据库密钥由 Android Keystore 管理。

## 已使用权限

- `POST_NOTIFICATIONS`：显示用户主动开启的通知栏保存入口
- `RECEIVE_BOOT_COMPLETED`：用户开启通知栏入口后，重启设备时尝试恢复入口
- `FOREGROUND_SERVICE` / `FOREGROUND_SERVICE_SPECIAL_USE`：维持用户主动开启的通知栏快捷入口
- `USE_BIOMETRIC` / `USE_FINGERPRINT`：敏感模块可选安全验证

## 可选系统服务

- Android Autofill：仅在用户主动将隐私中转站设为系统自动填充服务后生效
- 网盘提取码辅助：仅在 Pro 用户主动开启专用无障碍服务后生效，默认关闭

网盘提取码辅助只执行用户已保存提取码的一次性文本填入，不自动点击确认、登录、下载或支付。基础保存、分享接收、安全箱和链接路由均不依赖无障碍服务。

## 不使用的权限

- 不申请 `INTERNET`
- 不申请 `ACCESS_NETWORK_STATE`
- 基础功能不要求开启无障碍服务
- 不申请 Root
- 不申请后台高耗电白名单

最新版 APK 的完整权限清单、哈希和签名证书摘要见：[安全与构建证据](SecurityEvidence.md)。
