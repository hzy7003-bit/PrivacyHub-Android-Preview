# PrivacyHub 0.10.4-beta

发布时间：2026-09-27
Git tag：`v0.10.4-beta`
版本：`0.10.4-beta` / versionCode `132`

## 本版变更

- 原生 Android Autofill 凭据绑定目标包名与该应用当前安装签名身份；无法可信验证请求来源时 fail-closed。
- 网页 Autofill 当前 fail-closed。网页来源无法独立可信验证，因此本版不会自动向网页填入凭据；已有网页凭据数据不会因升级删除。
- Room schema v9 增加 nullable 的应用签名身份字段。加密离线备份格式升级为 v5，同时兼容读取 v1–v4；恢复时仅在本机已安装应用签名匹配时保留 Autofill 绑定。
- 明确排除 Android 系统云备份与设备迁移数据域；用户主动创建的加密离线备份不受影响。
- 增补第三方组件许可文本和离线查看入口。

## 正式 APK

- 文件：`PrivacyHub-0.10.4-beta.apk`
- 大小：`23709961` bytes
- SHA-256：`6474D4F2D67E33EFB639BBCC579D81D875532DB9A5B9CFB11A2B0D73B9217FC4`
- 签名证书 SHA-256：`FAFCDDCE1E680A685C9C0B222D996C99ACE9E1EC3F755BD238F6ED1C5D2D1709`
- APK Signature Scheme v2 / v3：均验证通过
- 包名：`com.privacyhub`；minSdk `26`；targetSdk `35`
- `debuggable=false`；`allowBackup=false`
- 未声明 `INTERNET`、`ACCESS_NETWORK_STATE` 或 `QUERY_ALL_PACKAGES`
- Release 仅提供正式 APK；AAB 不作为公开下载附件。

## 验证范围与限制

- Debug / Release JVM：各 220 项通过，0 failures / errors / skipped。
- Debug / Release Lint：0 errors；分别 33 / 34 warnings，各 1 informational。
- API 35 专用测试 AVD：全量 instrumentation 28/28；Room migration 8/8（v1→v9 至 v8→v9）。通知 acceptance、数据库密钥失败边界、诊断隐私和备份 Merge / Replace smoke 在候选功能源码验证阶段完成。
- `assembleDebug`、正式签名 `assembleRelease`、`bundleRelease`、`assembleDebugAndroidTest` 通过。版本元数据定稿后未重建 APK；线上附件应与已验收 APK 字节完全一致。
- 未完成多品牌 ROM、真实第三方 Autofill 页面或完整实体设备矩阵；Beta 不承诺所有应用和 ROM 均兼容。网页 Autofill 的 fail-closed 行为是本版明确限制。
