# 安全与构建证据

> 核对版本：`v0.10.2-beta`（versionCode 130）
>
> 核对日期：2026-09-27

本文记录公开 Release APK 可以独立复查的构建信息。它不是对 Android 系统或第三方 App 行为的绝对安全承诺。

## 发布文件

- 文件：`PrivacyHub-0.10.2-beta.apk`
- 大小：`23619902` bytes
- [GitHub Release 下载页](https://github.com/hzy7003-bit/PrivacyHub-Android-Preview/releases/tag/v0.10.2-beta)
- SHA-256：`95892E58B99FBF00CE56FDDF1C0E81DB84C1FBFE411DBC8E7F1D2672F4FF39810`
- 构建启用 R8 混淆、压缩及资源收缩，非 debuggable；不公开源码或 mapping 文件。混淆不等于加密，也不保证不可逆向。

## APK 元数据

| 项目 | 核对值 |
| --- | --- |
| packageName | `com.privacyhub` |
| versionName | `0.10.2-beta` |
| versionCode | `130` |
| minSdk | `26`（Android 8.0 / API 26+） |
| targetSdk | `35` |
| debuggable | `false` |
| allowBackup | `false` |

## 签名证书

- 证书主题：`CN=Privacy Hub, O=Privacy Hub`
- 证书 SHA-256：`FAFCDDCE1E680A685C9C0B222D996C99ACE9E1EC3F755BD238F6ED1C5D2D1709`
- APK Signature Scheme v2：`true`，验证通过。
- APK Signature Scheme v3：`true`，验证通过。

后续版本应继续使用同一正式发布证书。证书摘要变化时，不应在未说明原因的情况下继续安装。

## APK 权限清单

使用 Android SDK `apkanalyzer manifest permissions` 与 `manifest print` 核对当前 APK，得到以下权限：

```text
android.permission.POST_NOTIFICATIONS
android.permission.RECEIVE_BOOT_COMPLETED
android.permission.FOREGROUND_SERVICE
android.permission.FOREGROUND_SERVICE_SPECIAL_USE
android.permission.USE_BIOMETRIC
android.permission.USE_FINGERPRINT (maxSdkVersion=28)
com.privacyhub.DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION (应用自定义 signature 权限)
```

清单中没有：

```text
android.permission.INTERNET
android.permission.ACCESS_NETWORK_STATE
android.permission.QUERY_ALL_PACKAGES
```

APK 还声明了由 Android 系统绑定的 Quick Settings Tile、Autofill 和可选无障碍服务。它们不是联网权限；其中网盘提取码辅助的无障碍服务默认关闭，只能由用户在系统设置中主动开启。

## 自行复查

安装 Android SDK Build Tools 与 Command-line Tools 后，可以执行：

```powershell
Get-FileHash .\PrivacyHub-0.10.2-beta.apk -Algorithm SHA256
aapt2 dump permissions .\PrivacyHub-0.10.2-beta.apk
apksigner verify --verbose --print-certs .\PrivacyHub-0.10.2-beta.apk
apkanalyzer manifest print .\PrivacyHub-0.10.2-beta.apk
apkanalyzer manifest debuggable .\PrivacyHub-0.10.2-beta.apk
```

核对重点：

1. 文件 SHA-256 与本页一致。
2. 权限输出中没有 `INTERNET`、`ACCESS_NETWORK_STATE` 和 `QUERY_ALL_PACKAGES`。
3. v2 / v3 均验证通过，签名证书 SHA-256 与本页一致。
4. 包名、版本与 SDK 信息匹配上表；`allowBackup=false`、`debuggable=false`。Manifest 未显式声明 debuggable 时，使用 `manifest debuggable` 核对其有效值。

## 数据边界

- 安全箱使用 Room + SQLCipher 保存本地数据。
- 数据库密钥由 Android Keystore 保护。
- 加密离线备份使用 PBKDF2-HMAC-SHA256 派生密钥和 AES-256-GCM 加密。
- App 不接入广告、统计或云同步服务。
- App 不读取 IMEI、手机号或 SIM 信息。
- 本版进一步脱敏诊断记录，诊断报告不展示安全箱正文；反馈截图与文字前仍应检查个人信息。

## 已知边界

- 厂商 ROM 可以限制通知常驻、磁贴和后台剪贴板读取。
- 系统长按文本菜单是否展示入口由来源 App 和 ROM 决定。
- App 无法控制输入法历史、厂商云剪贴板或第三方 App 自身的数据处理。
- 无网络权限能阻止 App 直接联网，但不能代替对设备系统和第三方输入法的安全管理。
