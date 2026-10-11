# ROLLBACK (回滚与应急方案)

本文档明确 OwnBox UI 重构过程中的紧急回滚步骤与故障应对策略。

## 1. 核心回退分支与基点

- **安全基准点 (Clean Base Tag/Commit)**:
  - 稳定 Commit: `89ec88c` (v3.0.9-preview)
- **快速回退命令**:
  ```bash
  # 若当前在 feature/bettbox-style-ui 分支发现严重回归：
  git checkout main
  git reset --hard 89ec88c
  # 强制同步回滚
  git push origin main --force
  ```

## 2. 局部模块应急回滚清单

| 异常情况 | 影响范围 | 应急操作命令 |
| :--- | :--- | :--- |
| 节点列表卡片排版异常 | `layout_profile.xml` | `git checkout 89ec88c -- app/src/main/res/layout/layout_profile.xml` |
| 底部控制坞/StatsBar 异常 | `layout_main.xml` | `git checkout 89ec88c -- app/src/main/res/layout/layout_main.xml` |
| 主题颜色解析崩溃 | `themes.xml`, `colors.xml` | `git checkout 89ec88c -- app/src/main/res/values/themes.xml app/src/main/res/values/colors.xml` |
| 尺寸间距溢出 | `dimens.xml` | `git checkout 89ec88c -- app/src/main/res/values/dimens.xml` |

## 3. 用户数据安全保证

1. **零触碰原则**: 数据库实体类 (`database/ProxyEntity.kt`, `database/ProxyGroup.kt` 等) 以及 Room Dao 层完全不做任何字段变更或删除。
2. **数据保留机制**: 所有 `SharedPreferences` 键名（如 `DataStore.selectedProxy`, `DataStore.theme` 等）完全保持原样，用户升级或降级时数据 100% 完整保留。
3. **出厂配置救援**: 若极端情况下特定主题配置冲突，提供在关于页面连击版本号触发的“重置 UI 偏好至默认”，保证永不锁死。
