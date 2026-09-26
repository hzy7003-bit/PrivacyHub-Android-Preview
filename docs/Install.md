# 安装说明

当前公开测试版为 `0.10.2-beta`（versionCode `130`），最低支持 Android 8.0 / API 26+。

1. 打开 [v0.10.2-beta Release 页面](https://github.com/hzy7003-bit/PrivacyHub-Android-Preview/releases/tag/v0.10.2-beta)。
2. 下载 `PrivacyHub-0.10.2-beta.apk`，并按 [安全与构建证据](SecurityEvidence.md) 核对 SHA-256 和正式签名证书。
3. 在 Android 系统中允许“安装未知来源应用”。
4. 安装后根据需要开启通知权限。

公开 Release 版本沿用同一正式证书，可以覆盖升级；升级不要求卸载或清除数据。

如果设备已安装 Debug 测试包，不能直接覆盖安装 Release 包。请优先继续使用同签名 Debug 更新；需要换签名线时，先确认加密备份和恢复方案，再自行决定是否卸载。卸载会删除本地数据，不要为解决图标或签名提示贸然卸载。

APK 采用正式签名、R8 混淆和资源收缩，直接安装即可，不需要解压密码。混淆不是源码加密。文件哈希和证书摘要见 [安全与构建证据](SecurityEvidence.md)。

本版 APK 大小为 `23619902` bytes，SHA-256 为 `95892E58B99FBF00CE56FDDF1C0E81DB84C1FBFE411DBC8E7F1D2672F4FF39810`。文件哈希或签名证书不一致时，请停止安装并重新核对下载来源。
