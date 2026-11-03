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
