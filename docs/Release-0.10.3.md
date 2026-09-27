# PrivacyHub 0.10.3-beta

## 更新内容

- 修正通知栏“保存并跳转”处理带有效百度网盘提取码的分享时，Android App Link 可能直接打开百度网盘、绕过浏览器输入页面的问题。
- 仅当网盘自动化、Pro 权益、无障碍服务、精确百度网盘 host 和支持浏览器都通过校验时，显式在该浏览器打开并准备一次性填码。
- 条件不足时保留原有路由；不会自动确认、登录、下载或支付。

## 下载与校验

- 文件：`PrivacyHub-0.10.3-beta.apk`
- versionCode：`131`
- 大小：`23619902` bytes
- SHA-256：`E433CA1F61B0BC2A073F2EEE18D2661FB621C0A72BEC39442C3ACE64302FBFBF`
- 正式签名证书 SHA-256：`FAFCDDCE1E680A685C9C0B222D996C99ACE9E1EC3F755BD238F6ED1C5D2D1709`
- APK Signature Scheme v2 / v3：均验证通过
- 包名：`com.privacyhub`；minSdk `26`；targetSdk `35`
- `debuggable=false`；`allowBackup=false`
- 未声明 `INTERNET`、`ACCESS_NETWORK_STATE` 或 `QUERY_ALL_PACKAGES`

详细权限清单和复查命令见 [安全与构建证据](SecurityEvidence.md)。此 Beta 不代表所有 ROM、浏览器或百度网盘版本均完成端到端兼容验证。
