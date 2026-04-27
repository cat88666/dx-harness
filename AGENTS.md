# Repository Guidelines

## 项目结构与模块组织
本仓库是一个受约束的 Markdown 工程记忆库，不是应用代码仓。当前活跃实例位于 `llm-harness-project/`；可复用模板位于 `llm-harness-template/`；共享图片资源位于 `assets/`。

在 `llm-harness-project/` 中，将 `raw/` 视为原始资料层，将 `wiki/` 视为编译后的工作知识页：
- `raw/`：只读输入，如仓库快照、工单、日志、SQL、配置
- `wiki/entities/`：仓库、模块、服务、任务、表、配置项
- `wiki/summaries/`：链路或主题聚合总结
- `wiki/runbooks/`：可执行排障手册
- `wiki/incidents/`：事故复盘
- `wiki/changes/`：需求、修复、重构记录
- `wiki/synthesis/`：比较、策略、判断

凡是对 wiki 做了实质修改，都要同步更新 `index.md`，并向 `log.md` 追加记录。

## 构建、测试与开发命令
本仓库没有应用构建流水线。常用协作命令如下：

- `rg --files llm-harness-project/wiki`：快速列出知识页
- `rg '\[\[.*\]\]' llm-harness-project/wiki`：检查 wiki 双链
- `git diff --stat`：查看本次内容改动范围
- `git status`：确认只改了预期的 Markdown 文件

工作流规则定义在 `CLAUDE.md`、`llm-harness-project/CLAUDE.md` 和 `llm-harness-project/harness/`。模板规则只用于创建新实例。

## 编写风格与命名规范
统一使用 Markdown 编写，段落短、标题明确、结论需有来源支撑。不要编辑 `raw/` 下的文件。

文件名必须带类型前缀，格式统一为：`类型前缀-核心名称.md`。例如：
- `仓库-dx-game-hall.md`
- `服务-dx-game-hall.md`
- `模块-大厅匹配.md`
- `任务-大厅房间人数刷新.md`
- `主题-大厅匹配链路.md`
- `Runbook-大厅匹配失败排查.md`

优先更新已有页面，避免创建语义重复的新页。自然语言对象名必须能从 `index.md` 直达，例如“大厅”应定位到 `dx-game-hall`。

规则、提示词、检查清单不要写进 `wiki/`，应放在 `harness/`。

## 测试指南
这里的“测试”主要指结构校验。提交 PR 前，请确认：
- 文件名符合前缀规范
- `index.md` 已同步新增或重命名页面
- 新页面已回链到源码、配置、日志、SQL、工单或事故材料
- `index.md` 中没有指向不存在文件的旧链接

可手动执行一次结构检查，重点看链接、孤立页面、命名一致性和失效来源路径。

## 提交与 Pull Request 规范
现有提交历史多为 `init` 这类简短信息；后续新提交建议使用更清晰的祈使句，例如 `add prompt engineering summary` 或 `rename concept pages with required prefixes`。

PR 应包含：
- 本次知识变更的简要说明
- 受影响路径，例如 `llm-harness-project/wiki/entities/`
- 已更新 `index.md` 与 `log.md` 的确认信息
- 仅当 `assets/` 或 Obsidian 展示效果发生变化时再附截图
