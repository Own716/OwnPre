# FILE-MIGRATION-MAP (文件级迁移映射)

记录 OwnBox 核心 UI 资源与布局文件的重构动作、实现要点、测试要点、风险等级及回滚方案。

| 文件/组件 | 当前职责 | 重构动作 | 实现要点 | 测试要点 | 风险等级 | 回滚方法 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `app/src/main/res/values/dimens.xml` | 尺寸与网格间距规范 | 扩展 Bettbox 风格设计 Token | 引入 `spacing_*` (4~32dp)、`card_radius_*` (8~20dp)、优化卡片外边距与内边距 | 检查所有卡片与列表排版是否紧凑和谐 | 低 | `git checkout -- app/src/main/res/values/dimens.xml` |
| `app/src/main/res/values/colors.xml` | 基础色值与调色板定义 | 补充 Bettbox 语义状态色 | 引入 `state_connected`, `state_disconnected`, `card_stroke`, 优化墨绿色主色调 | 浅色与深色对比度合规性 | 中 | 恢复原文件 |
| `app/src/main/res/values-night/colors.xml` | 深色模式基础色值 | 优化暗黑/AMOLED 卡片底色 | 优化深色卡片对比度，低反光柔和底色 | 深色模式下文字可读性 | 中 | 恢复原文件 |
| `app/src/main/res/drawable/bg_pill_protocol.xml` | 节点协议徽章底纹 | 新增可复用胶囊微章组件 | 6dp 圆角微透明底纹，使 VMess/Trojan 协议标精致呈现 | 各类协议长短文字排版 | 低 | 删除该 drawable |
| `app/src/main/res/drawable/bg_pill_latency.xml` | 延迟/握手状态微章 | 新增状态标签底纹组件 | 动态显示可用/超时/握手毫秒数卡片药丸 | 延迟数值超长时适配 | 低 | 删除该 drawable |
| `app/src/main/res/layout/layout_profile.xml` | 节点列表单条卡片布局 | 全面优化为 Bettbox 卡片风格 | 采用 16dp 圆角卡片，协议胶囊微章，紧凑优雅排版，圆角选中高亮框 | 节点切换、长按菜单、多选态 | 高 | 还原原布局 XML |
| `app/src/main/res/layout/layout_main.xml` | 主界面悬浮控制栏与容器 | 优化底部 StatsBar 与 FAB 胶囊坞 | 优雅圆角悬浮底部坞、双行速率大字体防截断、平滑启动按钮 | 服务启停、延迟刷新、流量跳动 | 高 | 还原原布局 XML |
| `app/src/main/res/layout/layout_group_item.xml` | 订阅分组卡片条目 | 升级卡片立体感与间距 | 统一 16dp 圆角，平滑更新进度条与操作按钮排版 | 订阅更新、重命名、节点数统计 | 中 | 还原原布局 XML |
| `app/src/main/res/layout/layout_route_item.xml` | 路由分流规则卡片 | 统一卡片风格与类型微章 | 路由卡片边距与阴影优化，规则开闭开关对齐 | 规则启停、编辑规则跳转 | 中 | 还原原布局 XML |
| `app/src/main/res/layout/item_dashboard.xml` | 仪表盘扩展卡片 | 提升卡片圆角与操作按钮间距 | 统一圆角边框，自适应诊断标签与操作按钮 | 仪表盘测试与删除交互 | 中 | 还原原布局 XML |
| `app/src/main/res/values/themes.xml` | 全局 MD3 与主题样式 | 微调 MaterialCardView 样式与圆角 | 确保 20+ 款主题均完美呈现 Bettbox 圆角风格 | 各颜色主题切换测试 | 高 | 恢复原主题文件 |
| `libcore/` (内核与底层服务) | 核心代理服务驱动 | **严禁修改** | 保持 Sing-box 1.15.0 原生驱动完全不变 | 代理数据流稳定性 | 极高 | 保护该目录不发生任何改动 |
