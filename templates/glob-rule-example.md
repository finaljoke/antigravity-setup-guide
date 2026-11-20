---
trigger: glob
globs: "*.sql, db/migrations/*.ts"
description: "数据库脚本与迁移变更守则（仅在读写匹配文件时自动激活）。"
---

# 数据库迁移与 SQL 变更守则

> [!CAUTION]
> **`.agents/rules/*.md` 语法红线（违反将被静默丢弃，不会报错）**：
> - 必须包含完整 YAML frontmatter 与合法 `trigger`；
> - `trigger` 严格使用 `snake_case`（`always_on`、`model_decision`、`glob`、`manual`），**禁止使用 camelCase**（如 `alwaysOn`、`modelDecision`）；
> - `globs` 必须为**带引号的逗号分隔字符串**（如 `"*.sql, db/migrations/*.ts"`），**禁止写成 YAML 数组**（如 `["*.sql"]`）；以 `*` 开头的模式必须加引号，避免被 YAML 解析为别名锚点；
> - `.agents/rules/` 默认仅扫描**一层深度**，若需按子目录归类，请在 `.agents/rules.json` 中显式注册路径。

## 示例约束（`trigger: glob`）

1. 严禁在单次部署中直接删除或重命名线上已有列，必须先走双写/扩展再收缩的兼容迁移。
2. 变更表结构或索引前，先核对现有迁移脚本命名与幂等约定，并本地验证回滚脚本。

---

## 其他按需触发模式参考

### 按语义按需加载（`trigger: model_decision`）

适合篇幅较长、仅在特定主题任务才需要读入的领域规范（平时只注入 `description` 索引）：

```markdown
---
trigger: model_decision
description: "编写或评审前端无障碍（a11y）与键盘导航交互时应用本规范。"
---

# 前端无障碍规范
...
```

### 仅手动点名加载（`trigger: manual`）

适合发版检查单或专项审计清单，仅在聊天中显式 `@` 引用该规则文件时注入（注意：Antigravity CLI 暂不支持 `@` 引用规则）：

```markdown
---
trigger: manual
description: "生产发版前人工复核清单。"
---

# 发版检查清单
...
```
