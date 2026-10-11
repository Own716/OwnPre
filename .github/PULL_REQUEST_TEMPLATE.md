### 概要
- 本次改动将 OwnBox 客户端全面重构升级为 Bettbox 现代化卡片式 UI 风格，同时保证底层 Sing-box 内核逻辑与所有网络配置行为 100% 等价兼容。

### 更改列表
- **设计系统 (Design Tokens)**:
  - 引入 Bettbox 风格 `spacing_*` (4dp~32dp) 间距规范与 `card_radius_*` (8dp~20dp) 圆角规范。
  - 补充 `colors.xml` 与 `values-night/colors.xml` 中的语义化状态色 (`state_connected`, `state_disconnected`, `card_stroke`, `bettbox_pill_*`)。
  - 新增 `bg_pill_protocol.xml` 与 `bg_pill_latency.xml` 徽章胶囊背景，实现精致的节点协议与测速标签展示。
- **页面与条目卡片现代化**:
  - `layout_profile.xml`: 节点卡片采用 16dp 圆角、紧凑排版、自适应协议微章与延迟药丸。
  - `layout_group_item.xml`: 订阅分组卡片升级为卡片式布局，优化进度条与操作按键对齐。
  - `layout_route_item.xml`: 路由规则卡片化，强化分流类型显示与开关交互。
  - `item_dashboard.xml`: 仪表盘卡片优化圆角与操作按钮间距。
  - `themes.xml`: 全局卡片风格规范化，兼容全部 20+ 款调色板主题。
- **基线与测试文档**:
  - 交付完整 `docs/ui-refactor/` 系列文档 (`BASELINE.md`, `SCREEN-INVENTORY.md`, `FEATURE-INVENTORY.md`, `FILE-MIGRATION-MAP.md`, `TEST-PLAN.md`, `ROLLBACK.md`)。

### 影响范围
- 应用核心列表界面、卡片条目与设置样式。
- **无任何业务逻辑或网络内核变更**，`libcore` 与数据库层零触碰。

### 验证情况
- Gradle 编译通过: `:app:processPreviewDebugResources` SUCCESSFUL。
- Kotlin 编译通过: `:app:compilePreviewDebugKotlin` SUCCESSFUL。
- 单元测试通过: `:app:testPreviewDebugUnitTest` 100% PASS。
- 打包成功: `OwnBox-3.1.0-arm64-v8a-preview-debug.apk` 生成完毕。
