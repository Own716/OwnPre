# SCREEN-INVENTORY (页面清单)

本文档记录 OwnBox Android 客户端所有 Activity、Fragment 页面及对应布局文件与触发入口。

| 页面名称 | 对应类 | 布局文件 (`res/layout/`) | 入口来源 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| **主页 / 容器** | `MainActivity.kt` | `layout_main.xml` | 应用启动 / 点击常驻通知 / 磁贴跳转 | 主界面容器，包含底部悬浮 StatsBar、FAB 启动按钮与侧边栏抽屉导航 |
| **配置与节点页** | `ConfigurationFragment.kt` | `layout_profile_list.xml`, `layout_profile.xml` | 主界面默认页 / 导航抽屉 | 核心节点列表、分组切换、测速、添加节点入口 |
| **分组管理页** | `GroupFragment.kt` | `layout_group_list.xml`, `layout_group_item.xml` | 导航抽屉 / 订阅分组设置 | 订阅链接管理、节点分组与更新控制 |
| **分组编辑页** | `GroupSettingsActivity.kt` | `layout_edit_group.xml` | 分组列表点击编辑 | 分组属性、正则过滤、自动测速与排序设置 |
| **路由规则页** | `RouteFragment.kt` | `layout_route.xml`, `layout_route_item.xml` | 导航抽屉「路由」项 | 路由规则列表、分流策略、开闭状态控制 |
| **路由规则编辑** | `RouteSettingsActivity.kt` | `layout_route.xml` | 路由列表点击规则项 | 单条分流规则详细配置（域名、IP、应用、协议） |
| **网络工具箱** | `ToolsFragment.kt` | `layout_tools.xml` | 导航抽屉「工具」项 | 包含 STUN 测试、延迟测试、测速工具集合 |
| **设置主页** | `SettingsPreferenceFragment.kt` | `layout_settings_activity.xml` | 导航抽屉「设置」项 | 外观主题、内核参数、连接模式等偏好设置 |
| **备份与恢复** | `BackupFragment.kt` | `layout_backup.xml` | 设置 -> 备份与恢复 | 本地备份导入导出、WebDAV 远端同步 |
| **WebDAV 设置** | `WebDAVSettingsActivity.kt` | `layout_webdav_settings.xml` | 备份页面 WebDAV 配置 | 服务器 URL、用户名、密码与路径配置 |
| **流量统计图表** | `TrafficChartActivity.kt` | `activity_traffic_chart.xml` | StatsBar 点击或侧边栏 | 实时上传/下载速率与历史流量曲线 |
| **STUN 测试** | `StunActivity.kt` | `layout_stun.xml` | 工具箱 -> STUN 测试 | NAT 类型与公网 IP 诊断检测 |
| **应用分流管理** | `AppManagerActivity.kt`, `AppListActivity.kt` | `layout_apps.xml`, `layout_app_list.xml` | 路由设置 -> 应用分流 | 手机已安装应用多选与分流策略标记 |
| **二维码扫描** | `ScannerActivity.kt` | `layout_scanner.xml` | 节点页右上角添加 -> 扫描二维码 | 摄像头扫码识别节点与订阅链接 |
| **局域网共享** | `LanSharingActivity.kt` | `activity_lan_sharing.xml` | 工具箱 -> 局域网代理共享 | 代理端口共享、热点共享与设备连接监控 |
| **节点选择弹窗** | `NodeSelectDialogActivity.kt` | `activity_node_select_dialog.xml` | 快捷方式 / 外部 Intent | 快速切换目标节点对话框 |
| **日志查看** | `LogcatFragment.kt` | `layout_logcat.xml` | 导航抽屉「日志」项 | Sing-box 内核运行日志与调试排查 |
| **关于页面** | `AboutFragment.kt` | `layout_about.xml` | 导航抽屉「关于」项 | 版本信息、内核版本、开源声明与许可 |
| **协议节点编辑** | `ui/profile/*SettingsActivity.kt` | `layout_edit_config.xml` 等 | 节点卡片编辑按钮 | 支持 Shadowsocks, VMess, VLESS, Trojan, Hysteria, Tuic 等配置编辑 |
| **桌面小组件** | `OwnBoxWidgetProvider.kt` | `widget_proxy_1x1.xml`, `widget_proxy_2x2.xml`, `widget_proxy_4x1.xml`, `widget_proxy_4x2.xml` | 桌面长按添加小部件 | 1x1 状态开关、2x2、4x1、4x2 流量与节点监控部件 |
