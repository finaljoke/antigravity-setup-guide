# Personal Core

跨项目通用协作原则、轻量 SDD 交付纪律、中文文案规范与四层知识分流准则（纯净跨平台版）。全部规则均不依赖外部脚本或特定操作系统路径，可直接部署到全新 Antigravity 环境开箱使用。

## 包含组件

- [`plugin.json`](./plugin.json)：插件清单（符合 `https://antigravity.google/schemas/v1/plugin.json` 规范，含 `displayName`、`logo` 与 3 个开箱即用 `suggestedPrompts`）。
- [`assets/logo.svg`](./assets/logo.svg)：128×128 矢量图标（透明边距、双主题高对比配色）。
- [`rules/AGENTS.md`](./rules/AGENTS.md)：纯 Markdown 常驻全局规则（无 YAML frontmatter，严格控制在 4 KB 以内），涵盖：
  - 身份、简体中文沟通与低追问决策边界（含 scope delta 与线上高风险确认门禁）
  - 轻量 SDD、先核实先例与生效渲染路径、测试根因排查、换行编码保护与工具单一职责
  - 通用中文文案规范（改前先指错、用词统一、去翻译腔、事实对齐代码）
  - 四层知识分流（源码/`codegraph_explore`、仓根 `AGENTS.md` + `.agents/rules/*.md`、Skills、`/learn` 或项目记忆目录）与沉淀三门禁

## 安装与跨机同步方式

以下三种方式任选其一即可：

### 方式一：Git 仓库免拷贝同步（推荐）

将本仓库克隆到本地固定路径后，在 `~/.gemini/config/plugins.json` 中配置 `entries` 指向克隆目录下的 `plugins` **绝对路径**（可参考 [`templates/plugins.json`](../../templates/plugins.json)）：

```json
{
  "entries": [
    {
      "path": "/Users/yourname/dotfiles/antigravity-setup-guide/plugins"
    }
  ]
}
```

> [!IMPORTANT]
> **`plugins.json` 不会自动展开 `~`**，Windows（如 `C:/Users/yourname/...`）与 macOS/Linux 均必须填写完整绝对路径。后续跨机更新只需执行 `git pull`。

### 方式二：官方 CLI 校验与安装

在仓库根目录执行官方校验与本地安装命令：

```bash
agy plugin validate --strict ./plugins/personal-core
agy plugin install ./plugins/personal-core
```

### 方式三：手动复制或目录链接

将 `plugins/personal-core/` 放置或链接到 `~/.gemini/config/plugins/personal-core/`：

- **macOS / Linux**：
  ```bash
  ln -s /path/to/antigravity-setup-guide/plugins/personal-core ~/.gemini/config/plugins/personal-core
  ```
- **Windows（无需管理员权限，推荐使用目录联接 `/J`）**：
  ```cmd
  mklink /J "%USERPROFILE%\.gemini\config\plugins\personal-core" "C:\path\to\antigravity-setup-guide\plugins\personal-core"
  ```
  > 避免使用 `mklink /D`，普通用户权限下会要求管理员提权。

安装或注册完成后，在 Antigravity **Customizations > Installed** 中确认 `Personal Core`（`personal-core`）处于开启状态即可（热重载即时生效，无需重启）。

> [!NOTE]
> 如需在「个人背景边界」中补充所在地区、业务范围或专属前提，请仅在本地保留或同步至私有仓库，**切勿将个人隐私、密钥或公司敏感规则提交到公开仓库**。
