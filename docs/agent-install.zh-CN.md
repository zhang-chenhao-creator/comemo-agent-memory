> 本文档给 AI Agent 阅读和执行。执行前必须向用户展示计划并等待确认。

# comemo Agent 安装说明

comemo 的核心记忆系统只依赖 Markdown，不包含脚本或平台安装器。推荐流程是：

```text
下载或解压本仓库，把它交给 Agent，并说：
「阅读 docs/agent-install.zh-CN.md，并帮我安装 comemo。」
```

## 0. Agent 基础规则

- 不运行脚本。本项目刻意不提供 `.sh`、`.ps1`、`.py`、二进制安装器或平台专用安装器。
- 所有 Markdown 文件和归档文件名按 UTF-8 处理。
- 写入前把 `~` 解析为当前系统真实 home 目录。
- 不静默覆盖已有记忆文件。
- 如需替换已有文件，先展示准确路径，征求确认，并备份为 `filename.backup.YYYY-MM-DD`。
- 已有记忆系统默认采用安装适配：只创建缺失文件，并给出合并建议。
- 除非用户明确要求某个具体变更，否则不要移动、重命名、删除或重写其他 Agent 的原生记忆文件。
- 安装完成前替换所有占位符。
- 安装后逐个读取目标文件，确认文件存在、非空、没有残留 `{{...}}` 占位符。

## 1. 选择语言

让用户选择一个 `LANGUAGE`：

- `zh-CN`：中文模板正文和中文长期记忆文件名。
- `en`：英文模板正文和英文长期记忆文件名。

语言同时控制模板内容和 `MEMORY_PATH` 下的文件名。

`zh-CN` 使用：

```text
templates/zh-CN/
MEMORY_PATH/偏好.md
MEMORY_PATH/目标.md
MEMORY_PATH/能力.md
MEMORY_PATH/经验.md
MEMORY_PATH/身份.md
```

`en` 使用：

```text
templates/en/
MEMORY_PATH/preference.md
MEMORY_PATH/goals.md
MEMORY_PATH/ability.md
MEMORY_PATH/experience.md
MEMORY_PATH/identity.md
```

目录名 `comemo` 是所有语言的推荐默认值。`AGENTS.md` 是固定文件名，不要改成 `AGENT.md`。

## 2. 解析路径

询问或推断这些值：

- `CODEX_HOME`：默认 `~/.codex`
- `CLAUDE_HOME`：默认 `~/.claude`，仅在用户需要 Claude Code 支持或检测到 Claude Code 文件时使用
- `MEMORY_PATH`：默认 `~/comemo`
- `PROJECT_ROOT`：当前项目根目录
- `PROJECT_NAME`：当前项目名
- `DATE`：今天日期，格式 `YYYY-MM-DD`
- `LANGUAGE`：`zh-CN` 或 `en`

派生的 Claude Code 桥接目标：

- `CLAUDE_GLOBAL`：`CLAUDE_HOME/CLAUDE.md`
- `CLAUDE_PROJECT`：`PROJECT_ROOT/CLAUDE.md` 或 `PROJECT_ROOT/.claude/CLAUDE.md`

如果用户选择自定义 `MEMORY_PATH`，后续所有位置都使用该路径：模板占位符替换、路由表、验证步骤和适配器说明。路径解析后不要再写死 `~/comemo`。

跨平台示例：

```text
Windows CODEX_HOME: C:\Users\<user>\.codex
Windows CLAUDE_HOME: C:\Users\<user>\.claude
Windows MEMORY_PATH: C:\Users\<user>\comemo

macOS CODEX_HOME: /Users/<user>/.codex
macOS CLAUDE_HOME: /Users/<user>/.claude
macOS MEMORY_PATH: /Users/<user>/comemo

Linux CODEX_HOME: /home/<user>/.codex
Linux CLAUDE_HOME: /home/<user>/.claude
Linux MEMORY_PATH: /home/<user>/comemo
```

## 2.1 判断当前目标工具

安装前，Agent 应判断当前正在服务的目标工具，但不能只依赖自报身份。

判断依据包括：

- 当前 Agent 自报类型：Codex、Claude Code、Cursor、Aider、Gemini CLI 或其他。该信息只作为参考。
- 用户当前明确要求的目标工具。
- 已存在的工具路径和文件：
  - `CODEX_HOME/AGENTS.md`
  - `CODEX_HOME/AGENTS.override.md`
  - `CLAUDE_HOME/CLAUDE.md`
  - `PROJECT_ROOT/AGENTS.md`
  - `PROJECT_ROOT/AGENTS.override.md`
  - `PROJECT_ROOT/CLAUDE.md`
  - `PROJECT_ROOT/.claude/CLAUDE.md`
  - `.cursor/rules/`
  - `.cursorrules`
  - `.aider.conf.yml`
  - `GEMINI.md`
  - `.gemini/`

Agent 自报的软件类型不能作为唯一依据。最终安装目标必须以用户确认和实际文件路径为准。

如果目标工具不明确，不要猜测。展示检测结果，让用户选择目标工具和写入位置。

如果检测到多个工具，不迁移、不删除、不覆盖任何已有工具原生文件。保留共享 `AGENTS.md` 作为事实源，再按用户选择安装对应桥接。

Cursor 默认只检测和提示，或给出轻量适配建议。不要把完整 comemo 模板复制进 `.cursor/rules/` 或 `.cursorrules`。

安装前必须展示：

```text
当前 Agent 自报类型：
用户指定目标工具：
检测到的 Codex 文件：
检测到的 Claude Code 文件：
检测到的 Cursor 文件：
检测到的其他 Agent 文件：
推荐安装目标：
需要用户确认的写入：
```

## 3. 检查现有记忆系统

写入任何文件前，先检查并展示当前状态：

- `CODEX_HOME/AGENTS.override.md` 或 `CODEX_HOME/AGENTS.md` 是否存在。
- `CLAUDE_HOME/CLAUDE.md` 是否存在。
- `PROJECT_ROOT/AGENTS.override.md` 或 `PROJECT_ROOT/AGENTS.md` 是否存在。
- `PROJECT_ROOT/CLAUDE.md` 或 `PROJECT_ROOT/.claude/CLAUDE.md` 是否存在。
- `MEMORY_PATH` 是否存在。
- 哪些预期 comemo 文件已经存在。
- 哪些预期 comemo 文件缺失。
- 是否存在可能冲突，例如已有全局规则、项目规则、不同命名的记忆文件。
- 是否存在已生效的工具原生记忆文件，例如 `CLAUDE.md`、`.claude/`、`GEMINI.md`、`.gemini/`、`.cursor/rules/`、`.cursorrules`、`.aider.conf.yml` 或其他明显的 Agent 指令文件。

环境分类：

- 空环境：没有任何目标记忆文件。
- 已有 comemo 兼容系统：至少一个目标文件或相关 `AGENTS.md`/comemo 文件已经存在。
- 工具原生记忆系统：某个受支持 Agent 已有自己的记忆文件，但 comemo 目标文件缺失。
- 混合系统：comemo 兼容文件和工具原生记忆文件都已经存在。

非空环境下，提出改动前先展示一段简短架构摘要：

```text
检测到的全局文件：
检测到的项目文件：
检测到的长期记忆目录：
检测到的工具原生记忆文件：
可能冲突：
推荐安装模式：
```

## 4. 选择安装模式

### 空环境

如果是空环境：

1. 展示完整安装计划。
2. 请求用户确认。
3. 安装所有目标文件。

### 已有系统

如果检测到已有系统，先展示当前架构，再让用户选择：

1. 安装适配：只创建缺失文件，并提供已有文件的合并建议。默认推荐。
2. 自定义安装：用户选择安装哪些层，例如只安装全局层、项目层、comemo 层、Claude Code 桥接，或只预览。
3. 替换已有文件：必须用户明确确认；每个被替换文件备份为 `.backup.YYYY-MM-DD`。

安装适配模式下，不替换已有 `AGENTS.md` 或 comemo 文件。

如果存在工具原生记忆系统，优先桥接，不直接迁移：

- 工具支持导入或只读上下文文件时，让原生文件保持轻量，只指向共享 `AGENTS.md`。
- 不要把完整 comemo 模板复制进 `CLAUDE.md`、`GEMINI.md`、`.cursor/rules` 或 `.aider.conf.yml`。
- 如果原生文件里已经有有用规则，保留原文件，只给合并建议，不重写。
- Claude Code 项目级桥接中，只有安装后的 `CLAUDE.md` 与 `AGENTS.md` 位于同一目录时，`@AGENTS.md` 才有效。
- Claude Code 全局桥接写入 `CLAUDE_HOME/CLAUDE.md` 时，应使用解析后的 `CODEX_HOME/AGENTS.md` 绝对路径导入。除非 `AGENTS.md` 也在 `CLAUDE_HOME`，否则不要原样写入 `@AGENTS.md`。
- 如果存在 `AGENTS.override.md`，把它视为比 `AGENTS.md` 更高优先级；不要在同一作用域创建竞争性的 `AGENTS.md`，除非先说明优先级关系。

## 5. 目标文件

全局层：

```text
CODEX_HOME/AGENTS.md
```

如果 `CODEX_HOME/AGENTS.override.md` 已存在，不要假设 `CODEX_HOME/AGENTS.md` 会生效。先说明优先级，再让用户选择：不安装全局 comemo、只给 override 文件合并建议，或明确安装一个低优先级参考用的 `AGENTS.md`。

可选 Claude Code 全局桥接：

```text
CLAUDE_HOME/CLAUDE.md
```

这个文件应保持轻量。它应导入解析后的 `CODEX_HOME/AGENTS.md` 绝对路径，不应复制完整 comemo 模板。

长期记忆层：

```text
MEMORY_PATH/*
```

项目层：

```text
PROJECT_ROOT/AGENTS.md
```

如果 `PROJECT_ROOT/AGENTS.override.md` 已存在，同样先说明优先级，再决定是否创建 `PROJECT_ROOT/AGENTS.md`；未获明确确认前不要编辑 override 文件。

可选 Claude Code 项目桥接：

```text
PROJECT_ROOT/CLAUDE.md
PROJECT_ROOT/.claude/CLAUDE.md
```

除非用户明确要求两处都安装，否则只选择一个项目桥接目标。默认使用 `PROJECT_ROOT/CLAUDE.md`，结构最简单。

## 6. 复制模板

复制并替换占位符：

| Source | Target |
| --- | --- |
| `templates/<LANGUAGE>/AGENTS.global.template.md` | `CODEX_HOME/AGENTS.md` |
| `templates/<LANGUAGE>/AGENTS.project.template.md` | `PROJECT_ROOT/AGENTS.md` |
| `templates/<LANGUAGE>/comemo/*` | `MEMORY_PATH/*` |

可选 Claude Code 桥接文件：

| Source | Target | 必要改动 |
| --- | --- | --- |
| `adapters/claude/CLAUDE.global.md` | `CLAUDE_HOME/CLAUDE.md` | 把占位导入替换为解析后的 `CODEX_HOME/AGENTS.md` 绝对路径。 |
| `adapters/claude/CLAUDE.project.md` | `PROJECT_ROOT/CLAUDE.md` 或 `PROJECT_ROOT/.claude/CLAUDE.md` | 仅在 `AGENTS.md` 与安装后的 `CLAUDE.md` 位于同一目录时使用。 |

替换每个 comemo 模板文件中的这些占位符：

- `{{CODEX_HOME}}`
- `{{MEMORY_PATH}}`
- `{{PROJECT_ROOT}}`
- `{{PROJECT_NAME}}`
- `{{DATE}}`
- `{{LANGUAGE}}`

已有系统安装适配时，只复制缺失文件，除非用户明确批准替换。

## 7. 验证安装

读取每个新增或变更的目标文件，并检查：

- 文件存在。
- 文件非空。
- 没有残留 `{{...}}` 占位符。
- 如安装或替换了 `CODEX_HOME/AGENTS.md`，其中包含记忆候选确认规则。
- 如安装或替换了 `PROJECT_ROOT/AGENTS.md`，其中说明项目事实、记录、参数、数据、结果、结论、下一步写入项目目录。
- 如安装了 `CLAUDE_HOME/CLAUDE.md`，它应导入解析后的 `CODEX_HOME/AGENTS.md` 绝对路径；除非 `AGENTS.md` 也在 `CLAUDE_HOME`，否则不应是普通 `@AGENTS.md`。
- 如安装了项目级 `CLAUDE.md`，它要么与 `AGENTS.md` 同目录并使用 `@AGENTS.md`，要么使用能正确解析的显式路径。
- `MEMORY_PATH` 默认命名为 `comemo`，除非用户另选路径。
- `zh-CN` 模式下中文 comemo 文件名可正常读取。
- `en` 模式下英文 comemo 文件名和路由表一致。

使用匹配语言的检查清单：

- 中文：`docs/install-checklist.zh-CN.md`
- 英文：`docs/install-checklist.en.md`

## 8. 结束时说明

告诉用户：

- 安装了哪些文件。
- 因已有文件而跳过了哪些文件。
- 哪些已有文件被备份，如果有。
- 对已有文件有什么合并建议。
- 是否安装了 Claude Code 桥接文件，以及它是全局桥接还是项目级桥接。
- 未来「记住」类请求应先给记忆候选，不静默写入。
- 项目事实和实验记录应写入项目目录，而不是全局记忆。