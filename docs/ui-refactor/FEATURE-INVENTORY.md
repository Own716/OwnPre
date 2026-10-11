# FEATURE-INVENTORY (功能清单)

记录 OwnBox 核心业务模块、触发入口、底层类及数据持久化架构。重构期间严禁改动任何业务持久化层与服务接口。

| 功能模块 | 触发入口 | 关键实现类/文件 | 数据来源 | 持久化方式 |
| :--- | :--- | :--- | :--- | :--- |
| **代理服务启动/停止** | 首页 FAB 按钮 / 系统快捷磁贴 / 桌面 Widget | `bg/BaseService.kt`, `bg/VpnService.kt`, `SagerNet.kt` | 用户点击触发 | `DataStore.serviceState`, `SharedPreferences` |
| **节点管理与选择** | `ConfigurationFragment.kt` 节点卡片点击 | `ProfileManager.kt`, `ConfigurationFragment.kt` | Room 数据库 (`ProxyEntity`) | Room SQLite (`SagerDatabase.proxyDao`) |
| **订阅与分组管理** | `GroupFragment.kt`, `GroupUpdater.kt` | `GroupManager.kt`, `RawUpdater.kt` | 远程 HTTP(S) 订阅链接 | Room SQLite (`SagerDatabase.groupDao`) |
| **实时流量统计** | 首页 StatsBar / 状态栏通知 / Widget | `TrafficLooper.kt` (libcore), `StatsBar.kt` | Sing-box 内核流量回调通道 | 内存动态流，历史记录存入数据库 |
| **延迟/速度测试** | 节点卡片延迟测速 / 工具箱批量测速 | `SpeedTest.kt`, `SpeedTestOutcome.kt` | TCP / ICMP / HTTPS 握手测量 | 缓存于 `ProxyEntity.ping` 及内存 |
| **路由规则管理** | `RouteFragment.kt` 规则列表与开关 | `RouteRuleEditor.kt`, `RouteRule.kt` | 用户自定义规则与 GeoIP/GeoSite 规则集 | Room SQLite (`SagerDatabase.routeDao`) |
| **应用分流 (App Proxy)**| 路由设置 -> 分流应用选择 | `AppManagerActivity.kt`, `PackageCache.kt` | Android PackageManager 应用清单 | `DataStore.proxyApps` (`SharedPreferences`) |
| **主题与外观切换** | 设置 -> 外观设置 -> 主题选择 | `Theme.kt`, `ThemedActivity.kt` | 用户选择的主题样式 (20+ 调色板) | `DataStore.theme` (`SharedPreferences`) |
| **WebDAV 远端备份** | 备份页面 -> WebDAV 同步 | `BackupHelper.kt`, `WebDAVSettingsActivity.kt` | 数据库全量加密 JSON 导出包 | 远端 WebDAV 服务器文件存储 |
| **Sing-box 配置生成** | 启动代理时触发 | `ConfigBuilder.kt`, `SingBoxOptionsUtil.kt` | 当前选中节点 + 路由规则 + DNS 设置 | 动态组装为 sing-box 运行时 JSON/二进制 |
| **DNS 与探测设置** | 设置 -> 核心与网络设置 | `SettingsPreferenceFragment.kt` | 用户指定 Remote/Direct DNS 与嗅探选项 | `DataStore` 首选项存储 |
| **快捷通知与磁贴** | Android 系统通知栏 / 下拉控制中心 | `ServiceNotification.kt`, `QuickToggleShortcut.kt` | 服务运行状态广播 | Android 系统系统级通知服务 |
