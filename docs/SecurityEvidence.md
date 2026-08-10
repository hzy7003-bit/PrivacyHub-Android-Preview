# 安全与构建证据

> 核对版本：`v0.9.27-beta`
>
> 核对日期：2026-08-10

本文记录公开 Release APK 可以独立复查的构建信息。它不是对 Android 系统或第三方 App 行为的绝对安全承诺。

## 发布文件

- 文件：`PrivacyHub-v0.9.27-beta-release.apk`
- [GitHub Release 下载页](https://github.com/hzy7003-bit/PrivacyHub-Android-Preview/releases/tag/v0.9.27-beta)
- SHA-256：`36EEE6449DD6300C02E4924B4826F2983B869CAB9258C86DDD6F5E38E6C31EF6`

## 签名证书

- 证书主题：`CN=Privacy Hub, O=Privacy Hub`
- 证书 SHA-256：`FAFCDDCE1E680A685C9C0B222D996C99ACE9E1EC3F755BD238F6ED1C5D2D1709`

后续版本应继续使用同一正式发布证书。证书摘要变化时，不应在未说明原因的情况下继续安装。

## APK 权限清单

使用 Android Build Tools `aapt2 dump permissions` 核对当前 APK，得到以下权限：

```text
android.permission.POST_NOTIFICATIONS
android.permission.RECEIVE_BOOT_COMPLETED
android.permission.FOREGROUND_SERVICE
android.permission.FOREGROUND_SERVICE_SPECIAL_USE
android.permission.USE_BIOMETRIC
android.permission.USE_FINGERPRINT (maxSdkVersion=28)
```

清单中没有：

```text
android.permission.INTERNET
android.permission.ACCESS_NETWORK_STATE
```

APK 还声明了由 Android 系统绑定的 Quick Settings Tile、Autofill 和可选无障碍服务。它们不是联网权限；其中网盘提取码辅助的无障碍服务默认关闭，只能由用户在系统设置中主动开启。

## 自行复查

安装 Android SDK Build Tools 后，可以执行：

```powershell
Get-FileHash .\PrivacyHub-v0.9.27-beta-release.apk -Algorithm SHA256
aapt2 dump permissions .\PrivacyHub-v0.9.27-beta-release.apk
apksigner verify --print-certs .\PrivacyHub-v0.9.27-beta-release.apk
```

核对重点：

1. 文件 SHA-256 与本页一致。
2. 权限输出中没有 `INTERNET` 和 `ACCESS_NETWORK_STATE`。
3. 签名证书 SHA-256 与本页一致。

## 数据边界

- 安全箱使用 Room + SQLCipher 保存本地数据。
- 数据库密钥由 Android Keystore 保护。
- 加密离线备份使用 PBKDF2-HMAC-SHA256 派生密钥和 AES-256-GCM 加密。
- App 不接入广告、统计或云同步服务。
- App 不读取 IMEI、手机号或 SIM 信息。
- 本地诊断不记录安全箱正文。

## 已知边界

- 厂商 ROM 可以限制通知常驻、磁贴和后台剪贴板读取。
- 系统长按文本菜单是否展示入口由来源 App 和 ROM 决定。
- App 无法控制输入法历史、厂商云剪贴板或第三方 App 自身的数据处理。
- 无网络权限能阻止 App 直接联网，但不能代替对设备系统和第三方输入法的安全管理。
