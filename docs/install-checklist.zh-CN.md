# 安装检查清单

## 语言与路径

- [ ] 已确认 `LANGUAGE` 为 `zh-CN`。
- [ ] 已确认中文模板内容和中文 comemo 文件名同步使用。
- [ ] 已确认 `CODEX_HOME`，默认建议为 `~/.codex`。
- [ ] 已确认 `MEMORY_PATH`，默认建议为 `~/comemo`。
- [ ] 如选择自定义 `MEMORY_PATH`，已确认生成的路由表和适配器说明都一致使用该路径。
- [ ] 已确认 `PROJECT_ROOT`。
- [ ] 已确认 `PROJECT_NAME`。
- [ ] 已确认日期 `YYYY-MM-DD`。
- [ ] 已将 `~` 解析为当前系统的真实 home 路径。

## 跨平台与编码

- [ ] 已确认 Markdown 文件按 UTF-8 读取和写入。
- [ ] 已确认当前解压方式能正确读取中文文件名。
- [ ] Windows 路径示例已按 `C:\Users\<user>\...` 理解。
- [ ] macOS 路径示例已按 `/Users/<user>/...` 理解。
- [ ] Linux 路径示例已按 `/home/<user>/...` 理解。

## 现有系统检测

- [ ] 已检查 `CODEX_HOME/AGENTS.override.md` 或 `CODEX_HOME/AGENTS.md` 是否存在。
- [ ] 已检查 `PROJECT_ROOT/AGENTS.override.md` 或 `PROJECT_ROOT/AGENTS.md` 是否存在。
- [ ] 已检查 `MEMORY_PATH` 是否存在。
- [ ] 已列出已存在的 comemo 文件。
- [ ] 已列出缺失的 comemo 文件。
- [ ] 已检查工具原生记忆文件，例如 `CLAUDE.md`、`.claude/`、`GEMINI.md`、`.gemini/`、`.cursor/rules/`、`.cursorrules`、`.aider.conf.yml`。
- [ ] 如果检测到已有系统，已先向用户展示当前记忆架构。
- [ ] 如果存在 `AGENTS.override.md`，已说明它在同一作用域优先级高于 `AGENTS.md`。

## 文件

- [ ] 空环境安装时，已创建或更新 `CODEX_HOME/AGENTS.md`。
- [ ] 空环境安装时，已创建或更新 `PROJECT_ROOT/AGENTS.md`。
- [ ] 已创建长期记忆目录 `MEMORY_PATH`。
- [ ] 已按安装模式创建 `MEMORY_PATH/偏好.md`。
- [ ] 已按安装模式创建 `MEMORY_PATH/目标.md`。
- [ ] 已按安装模式创建 `MEMORY_PATH/能力.md`。
- [ ] 已按安装模式创建 `MEMORY_PATH/经验.md`。
- [ ] 已按安装模式创建 `MEMORY_PATH/身份.md`。

## 安全确认

- [ ] 已有系统默认采用安装适配：只补缺失文件，不覆盖已有文件。
- [ ] 工具原生记忆系统默认桥接或保持不动，没有通过重写原生文件强行迁移。
- [ ] 如用户选择自定义安装，已按用户指定层级执行。
- [ ] 覆盖任何已有文件前，已向用户确认。
- [ ] 已有文件如需替换，已备份为 `.backup.YYYY-MM-DD`。
- [ ] 安装后逐个读取了新增或变更的目标文件。
- [ ] 所有新增或变更的目标文件非空。
- [ ] 所有新增或变更的目标文件没有残留 `{{...}}` 占位符。
- [ ] 全局层不包含项目事实、实验数据、结果、结论或下一步。
- [ ] 项目层明确项目事实和实验记录写入项目目录。
- [ ] 长期记忆层只放跨项目长期有效信息。
- [ ] 已向用户说明被跳过的已有文件和必要的合并建议。
