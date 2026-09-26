# PrivacyHub 0.10.2-beta

## 更新内容

- 修复切换到安全箱时，数据加载期间短暂闪现“新建安全箱内容”操作的问题。
- 设置页进入与返回不再使用横向页面转场，和中转、安全箱导航保持一致。
- 将通知操作“关闭通知栏按钮”改为“关闭通知按钮”，让同组操作按钮尺寸更协调。

本次为 0.10.1-beta 的小型修整版本，不修改安全箱数据、保存流程或业务逻辑。

## APK

- 文件：`PrivacyHub-0.10.2-beta.apk`
- versionCode：`130`
- 大小：`23619902` bytes
- SHA-256：`95892E58B99FBF00CE56FDDF1C0E81DB84C1FBFE411DBC8E7F1D2672F4FF39810`
- 正式签名证书 SHA-256：`FAFCDDCE1E680A685C9C0B222D996C99ACE9E1EC3F755BD238F6ED1C5D2D1709`
- APK Signature Scheme v2 / v3：均有效
- `debuggable=false`、`allowBackup=false`；未声明 `INTERNET`、`ACCESS_NETWORK_STATE` 或 `QUERY_ALL_PACKAGES`

最低支持 Android 8.0（API 26），targetSdk 35。正式签名沿用前版证书，已安装公开 Release 可覆盖升级。不要为切换 Debug/Release 签名线而直接卸载含有数据的 App。

## 验证边界

Debug / Release JVM tests 各 200/200 通过；Debug / Release Lint 0 errors（34/35 warnings）。Debug APK、正式签名 Release APK/AAB 和 AndroidTest APK 构建通过。本轮未重跑完整 Android instrumentation 或多 ROM 设备矩阵。

详细 APK 复核命令与权限清单见 [安全与构建证据](SecurityEvidence.md)。
