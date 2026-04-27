# Repository Guidelines

## 项目结构与模块组织
本仓库是一个受约束的 Markdown 知识库工程，不是应用代码仓。当前活跃实例位于 `llm-harness-project/`；工作型 Harness 模板位于 `llm-harness-template/`；共享图片资源位于 `assets/`。

在 `llm-harness-project/` 中，将 `raw/` 视为原始资料层，将 `wiki/` 视为编译后的知识页：
- `raw/`：只读输入，如论文、产品资料、Prompt 材料
- `wiki/concepts/`：抽象概念、机制、方法、框架、体系
- `wiki/entities/`：人物、组织、工具、产品、模型等实体
- `wiki/summaries/`：按主题聚合的总结页
- `wiki/synthesis/`：比较、策略、判断或问题驱动的综合分析页

凡是对 wiki 做了实质修改，都要同步更新 `index.md`，并向 `log.md` 追加记录。

## 构建、测试与开发命令
本仓库没有应用构建流水线。常用协作命令如下：

- `rg --files llm-harness-project/wiki`：快速列出知识页
- `rg '\[\[.*\]\]' llm-harness-project/wiki`：检查 wiki 双链
- `git diff --stat`：查看本次内容改动范围
- `git status`：确认只改了预期的 Markdown 文件

工作流规则定义在 `CLAUDE.md` 和 `.claude/skills/*.md`。

## 编写风格与命名规范
统一使用 Markdown 编写，段落短、标题明确、结论需有来源支撑。不要编辑 `raw/` 下的文件。

文件名必须带类型前缀，格式统一为：`类型前缀-核心名称.md`。例如：
- `概念-Agent.md`
- `工具-Qdrant.md`
- `主题-RAG系统设计.md`
- `对比-RAG-vs-微调-vs-Agent.md`

命名规则以 `.claude/skills/naming/SKILL.md` 为准。优先更新已有页面，避免创建语义重复的新页。

## 测试指南
这里的“测试”主要指结构校验。提交 PR 前，请确认：
- 文件名符合前缀规范
- `index.md` 已同步新增或重命名页面
- 新页面已回链到 `raw/` 中相关来源
- `concepts/` 页面包含 `CLAUDE.md` 要求的 6 个固定部分

可手动执行一次 lint 检查，对照 `.claude/skills/lint/SKILL.md` 检查链接、孤立页面和命名一致性。

## 提交与 Pull Request 规范
现有提交历史多为 `init` 这类简短信息；后续新提交建议使用更清晰的祈使句，例如 `add prompt engineering summary` 或 `rename concept pages with required prefixes`。

PR 应包含：
- 本次知识变更的简要说明
- 受影响路径，例如 `llm-harness-project/wiki/summaries/`
- 已更新 `index.md` 与 `log.md` 的确认信息
- 仅当 `assets/` 或 Obsidian 展示效果发生变化时再附截图
