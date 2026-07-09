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

## 不使用的权限

- 不申请 `INTERNET`
- 不申请 `ACCESS_NETWORK_STATE`
- 不申请无障碍权限
- 不申请 Root
- 不申请后台高耗电白名单