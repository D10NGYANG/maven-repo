# maven-repo
我的开源项目maven仓库

# 镜像地址
```kotlin
maven("https://raw.githubusercontent.com/D10NGYANG/maven-repo/main/repository")
```

在你的 KMP 项目中添加仓库与依赖（Kotlin DSL）：

```kotlin
// settings.gradle.kts 或 build.gradle.kts 中的仓库（推荐）
dependencyResolutionManagement {
    repositories {
        maven("https://raw.githubusercontent.com/D10NGYANG/maven-repo/main/repository") {
          mavenContent {
            includeGroupAndSubgroups("com.github.D10NGYANG")
          }
        }
        google()
        mavenCentral()
    }
}
```


## DLCryptoUtil 0.3.0

本仓库是 DLCryptoUtil 提供给外部用户的 Maven 制品仓库；不依赖内网 Nexus。

```kotlin
// KMP commonMain
implementation("com.github.D10NGYANG:DLCryptoUtil:0.3.0")
// 纯 JVM/Java
implementation("com.github.D10NGYANG:DLCryptoUtil-jvm:0.3.0")
```

包含 KMP 根模块、JVM、JS、iOS arm64、iOS simulator arm64 和 iOS x64 平台制品。

升级注意：CBC 新加密要求显式随机 IV；RSA 长文本输出和密钥格式已统一，先升级解密端再切换写入；新增 MGF SHA256，旧 iOS OAEP-SHA256 密文应按 SHA256/SHA256 读取。Kotlin 升级到2.4.21，BC 切换至 jdk18on:1.86（Java 8+）。

[完整升级说明](https://github.com/D10NGYANG/DLCryptoUtil/blob/v0.3.0/docs/upgrade-0.3.0.md) · [GitHub Release](https://github.com/D10NGYANG/DLCryptoUtil/releases/tag/v0.3.0)


## DLBluetoothUtil 1.1.0

本仓库是 DLBluetoothUtil 面向外部用户的 Maven 制品仓库，使用上面的 `main/repository` 地址，无需内部 Nexus 或 JitPack。

```kotlin
// KMP commonMain（通过 Gradle 元数据选择平台）
implementation("com.github.D10NGYANG:DLBluetoothUtil:1.1.0")
// 仅 Android 项目也可直接选择平台坐标，二者择一
implementation("com.github.D10NGYANG:DLBluetoothUtil-android:1.1.0")
```

包含根模块、Android、iOS arm64、iOS simulator arm64、JS 和 WasmJS 制品。新增 Apple Silicon 模拟器支持；修复连接取消泄漏、队列异常和通知状态。Android payload 上限为 `minOf(MTU - 3, 512)`，超长写入立即失败；公共 BLE API 签名保持兼容，DLLogUtil 仍为 0.2.1。

[升级说明](https://github.com/D10NGYANG/DLBluetoothUtil/blob/1.1.0/docs/MIGRATION_1.1.0.md) · [GitHub Release](https://github.com/D10NGYANG/DLBluetoothUtil/releases/tag/1.1.0)
