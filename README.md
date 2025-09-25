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
