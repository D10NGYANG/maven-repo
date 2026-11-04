# maven-repo
我的开源项目maven仓库

# 仓库地址
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


## DLSerialPortUtil 0.7.1

Kotlin Multiplatform 串口通讯库，使用上方 Maven 仓库地址。

```kotlin
// KMP commonMain
implementation("com.github.D10NGYANG:DLSerialPortUtil:0.7.1")
// 仅 JVM 或 Android 项目也可分别选择平台坐标，和根坐标择一
implementation("com.github.D10NGYANG:DLSerialPortUtil-jvm:0.7.1")
implementation("com.github.D10NGYANG:DLSerialPortUtil-android:0.7.1")
```

包含根模块及 Android、JVM、JS、WasmJS、Linux x64/arm64、macOS x64/arm64 制品。Android USB 驱动的传递依赖还需要 `maven("https://jitpack.io")`。

修复串口打开/关闭竞争、取消泄漏、Web 读错误恢复和 POSIX fd 复用/挂断问题；公共 Flow/Logger 依赖通过 api 暴露。Kotlin 2.2.21、Coroutines 1.11.0、DLLogUtil 0.3.0；保持 Android minSdk 26、Java 8 字节码和公共串口 API。日志采集最多缓冲 1024 条，慢消费者会丢弃旧诊断日志，不影响串口 RX 的 64 块 replay/背压语义。

[升级说明](https://github.com/D10NGYANG/DLSerialPortUtil/blob/0.7.1/MIGRATION_0.7.1.md) · [GitHub Release](https://github.com/D10NGYANG/DLSerialPortUtil/releases/tag/0.7.1)


## DLCryptoUtil 0.3.0

DLCryptoUtil 的 Maven 制品使用上面的仓库地址。

```kotlin
// KMP commonMain
implementation("com.github.D10NGYANG:DLCryptoUtil:0.3.0")
// 纯 JVM/Java
implementation("com.github.D10NGYANG:DLCryptoUtil-jvm:0.3.0")
```

包含 KMP 根模块、JVM、JS、iOS arm64、iOS simulator arm64 和 iOS x64 平台制品。

升级注意：CBC 新加密要求显式随机 IV；RSA 长文本输出和密钥格式已统一，先升级解密端再切换写入；新增 MGF SHA256，旧 iOS OAEP-SHA256 密文应按 SHA256/SHA256 读取。Kotlin 升级到2.4.21，BC 切换至 jdk18on:1.86（Java 8+）。

[完整升级说明](https://github.com/D10NGYANG/DLCryptoUtil/blob/main/docs/upgrade-0.3.0.md) · [GitHub Release](https://github.com/D10NGYANG/DLCryptoUtil/releases/tag/v0.3.0)


## DLBluetoothUtil 1.1.1

跨平台BLE通讯库，通过上方Maven地址安装。

```kotlin
implementation("com.github.D10NGYANG:DLBluetoothUtil:1.1.1")
// 仅Android项目可选平台坐标，与上面二者择一
implementation("com.github.D10NGYANG:DLBluetoothUtil-android:1.1.1")
```

支持Android、iOS arm64、iOS simulator arm64、JS、WasmJS。1.1.1升级DLLogUtil0.3.0，修复Apple日志输出与时间戳、改善日志并发安全；日志缓冲最多1024条，积压丢旧，全局等级影响后续Logger。BLE公共API保持不变。

[升级说明](https://github.com/D10NGYANG/DLBluetoothUtil/blob/1.1.1/docs/RELEASE_1.1.1.md) · [GitHub Release](https://github.com/D10NGYANG/DLBluetoothUtil/releases/tag/1.1.1)


## DLVoiceUtil 0.3.0

Android/iOS PCM 录音与播放工具，支持小端、16bit、单声道音频。

```kotlin
// KMP commonMain，由 Gradle 选择目标平台制品
implementation("com.github.D10NGYANG:DLVoiceUtil:0.3.0")
// 仅 Android 项目也可选择平台坐标，二者择一
implementation("com.github.D10NGYANG:DLVoiceUtil-android:0.3.0")
```

包含根模块、Android、iOS arm64 和 iOS simulator arm64 制品。新增可等待的录音停止 API 与错误 Flow，修复录放音数据、资源释放和会话问题。升级需匹配 Kotlin 2.4.21 元数据；Android minSdk 26、compileSdk 至少 37。

[升级说明](https://github.com/D10NGYANG/DLVoiceUtil/blob/v0.3.0/docs/migration/0.3.0.md) · [GitHub Release](https://github.com/D10NGYANG/DLVoiceUtil/releases/tag/v0.3.0)


## DLLogUtil 0.3.0

轻量级 Kotlin Multiplatform 日志库，Maven 制品使用上面的仓库地址。

```kotlin
// KMP commonMain，由 Gradle 选择目标平台制品
implementation("com.github.D10NGYANG:DLLogUtil:0.3.0")
// 纯 JVM/Java 工程可选择平台坐标，二者择一
implementation("com.github.D10NGYANG:DLLogUtil-jvm:0.3.0")
// 仅 Android 工程也可选择平台坐标
implementation("com.github.D10NGYANG:DLLogUtil-android:0.3.0")
```

包含根模块及 Android、JVM、JS、WasmJS、WasmWASI、Linux x64/arm64、macOS x64/arm64、iOS arm64/simulator arm64/x64 制品。

修复工厂并发访问和 Apple 日志输出；全局等级应用于后续新建 Logger；`getAll()` 返回注册表快照。日志流最多缓冲 1024 条，慢消费者积压时丢弃最旧消息。Kotlin 2.2.21、协程 1.11.0；保持 Java 8 字节码和 Android minSdk 26。

[升级说明](https://github.com/D10NGYANG/DLLogUtil/blob/0.3.0/docs/upgrade-0.3.0.md) · [GitHub Release](https://github.com/D10NGYANG/DLLogUtil/releases/tag/0.3.0)
