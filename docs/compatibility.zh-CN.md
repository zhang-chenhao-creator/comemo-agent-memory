# 兼容性说明

comemo 是 Markdown 模板，不是运行时集成层。这里的兼容，指目标 Agent 可以读取相关 Markdown 文件，或能通过轻量适配器指向这些文件。

## 操作系统

文档和模板里用 `~` 表示跨平台 home 目录。

```text
Windows: C:\Users\<user>
macOS: /Users/<user>
Linux: /home/<user>
```

推荐路径：

```text
~/.codex/AGENTS.md
~/comemo/
<project-root>/AGENTS.md
```

`~/comemo/` 只是推荐默认值。安装器和 Agent 应把长期记忆目录视为 `MEMORY_PATH`，如果用户选择自定义路径，生成的路由表和适配器说明都要保持一致。

所有 Markdown 文件按 UTF-8 处理。英文模板使用 ASCII 文件名。中文模板在 `MEMORY_PATH` 下使用 UTF-8 中文文件名。

## 集成方式

| Agent | 集成方式 | 说明 |
| --- | --- | --- |
| Codex | 主要目标 | 直接使用 `AGENTS.md` |
| Claude Code | 桥接 | 用 `CLAUDE.md` 导入 `AGENTS.md` |
| Cursor | 手动 / 共享项目规则 | 使用项目级 `AGENTS.md` 作为共享上下文 |
| Aider | adapter 示例 | 把 `AGENTS.md` 加为只读上下文 |
| Gemini CLI | adapter 示例 | 把 `AGENTS.md` 加入上下文发现范围 |

## 验证状态

工具行为会随版本变化。comemo 记录的是预期集成模式，不是保证永久稳定的运行时契约。

Last verified: 2026-05-25

| Tool | Status | Note |
| --- | --- | --- |
| Codex | Primary target | 使用 `AGENTS.md` 作为主要指令文件 |
| Claude Code | Bridge example | `CLAUDE.md` 导入 `AGENTS.md` |
| Cursor | Partial / manual | 使用 `AGENTS.md` 作为共享项目指令；项目规则可能需要手动设置 |
| Aider | Example adapter | 把 `AGENTS.md` 作为只读上下文读取 |
| Gemini CLI | Example adapter | 把 `AGENTS.md` 加入上下文发现范围 |

## Agent 说明

### Codex

Codex 是主要目标。使用：

```text
~/.codex/AGENTS.md
<project-root>/AGENTS.md
MEMORY_PATH/
```

见 `adapters/codex/README.md`。

### Claude Code

Claude Code 通常使用 `CLAUDE.md` 作为项目指令文件。适配器保持 `AGENTS.md` 作为共享事实源，只增加一个 `CLAUDE.md` 桥接：

```md
@AGENTS.md
```

见 `adapters/claude/CLAUDE.md`。

### Cursor

使用项目级 `AGENTS.md` 作为共享项目规则。comemo v0.1.0 不生成 `.cursor/rules`，因为那会复制一套记忆系统，增加维护成本。

Cursor 支持把 `AGENTS.md` 放在项目根目录，作为简单项目指令使用，但细粒度作用域可能仍需要手动配置 Cursor project rules。如果项目需要按目录或文件类型做细粒度规则，应使用 Cursor project rules 做轻量指向，而不是复制完整 comemo 模板。

见 `adapters/cursor/README.md`。

### Aider

适配器提供一个最小 `.aider.conf.yml` 示例，把 `AGENTS.md` 作为只读上下文文件。

见 `adapters/aider/.aider.conf.yml`。

### Gemini CLI

适配器提供一个最小 settings 示例，把 `AGENTS.md` 加入 Gemini CLI 的上下文文件发现范围。

见 `adapters/gemini/settings.json`。

## 参考链接

- AGENTS.md open format: https://agents.md/
- OpenAI Codex AGENTS.md: https://developers.openai.com/codex/guides/agents-md
- Claude Code memory: https://docs.anthropic.com/en/docs/claude-code/memory
- Cursor rules: https://docs.cursor.com/en/context
- Aider YAML config: https://aider.chat/docs/config/aider_conf.html
- Gemini CLI configuration: https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/configuration.md

## 边界

- 适配器是示例，不是完整安装器。
- 工具行为可能随版本变化。
- 如果某个 Agent 有自己的原生记忆文件，保持该文件轻量，只引用 `AGENTS.md`，不要复制完整 comemo 模板。
- 不要假设所有 Agent 的指令优先级完全一致。
- 已有原生记忆文件应视为用户资产。安装时优先桥接到 `AGENTS.md` 或给合并建议，默认不重写。
- 如果同一作用域存在 Codex `AGENTS.override.md`，它优先于 `AGENTS.md`；不要在未说明优先级的情况下创建竞争性规则。
