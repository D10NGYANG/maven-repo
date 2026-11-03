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

## DLCommonUtil 1.1.0

本仓库是 DLCommonUtil 对外 Maven 制品的分发仓库，源码与版本说明位于 [DLCommonUtil](https://github.com/D10NGYANG/DLCommonUtil)。

```kotlin
// KMP commonMain
implementation("com.github.D10NGYANG:DLCommonUtil:1.1.0")
// 纯 JVM
implementation("com.github.D10NGYANG:DLCommonUtil-jvm:1.1.0")
```

1.1.0 制品包含 KMP 根模块、Android、JVM、JS、iOS Arm64/Simulator Arm64/X64、macOS Arm64、Linux X64/Arm64。建议下游对齐 Kotlin 2.4.21；JVM 仍面向 Java 8。

升级前请查看 [1.1.0 升级说明](https://github.com/D10NGYANG/DLCommonUtil/blob/1.1.0/doc/Upgrade-1.1.0.md)：Apple GBK 的 GB18030 超集行为保留，但畸形字节解码改为显式异常；轨迹投影和 JS 数字转换已修正。
