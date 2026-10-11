# OwnBox UI Refactor Baseline

| 字段 | 内容 |
| :--- | :--- |
| **项目版本号** | 3.0.9-preview (versionCode 359) |
| **内核版本** | Sing-box v1.15.0 Alpha (libcore submodule) |
| **原始仓库** | `https://github.com/Own716/OwnBoxForAndroid` |
| **目标仓库** | `https://github.com/Own716/OwnPre.git` |
| **基线分支** | `main` |
| **重构分支** | `feature/bettbox-style-ui` |
| **基准 Commit** | `89ec88c` (feat(security): comprehensive repository audit, vulnerability remediation, and test hardening) |
| **Gradle 版本** | 8.10.2 |
| **Kotlin 版本** | 1.9.24 |
| **JDK 版本** | Eclipse Adoptium OpenJDK 17 |
| **minSdkVersion** | 24 (Android 7.0+) |
| **targetSdkVersion**| 34 (Android 14) |
| **构建命令** | `./gradlew assembleDebug` / `gradlew.bat assembleRelease` |
| **测试命令** | `./gradlew test` / `./gradlew lint` |
| **自动化测试覆盖** | 覆盖核心加密解析、配置生成与网络工具单元测试 |
| **已知问题** | 初始安装默认零分组模式；多主题在老旧极端尺寸屏下个别边距需统一 |
