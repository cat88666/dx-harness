# Wiki Log

本文件记录所有操作，append-only，禁止修改历史记录。

格式：`## [YYYY-MM-DD] 操作类型 | 标题`
操作类型：`Init` / `Ingest` / `Query` / `Lint` / `Update`

---

## [2026-04-22] Init | 初始化 wiki 目录结构
- 创建 `raw/`、`wiki/`、`CLAUDE.md`
- 创建 `wiki/index.md`、`wiki/log.md`
- 创建 `wiki/concepts/`、`wiki/entities/`、`wiki/synthesis/`、`wiki/summaries/`

## [2026-04-27] Update | 增加 dx-game-hall 工作项目索引
- 新增 `wiki/entities/服务-dx-game-hall.md`
- 在 `index.md` 增加 `Work Projects`，将“大厅 / 比赛大厅 / 游戏大厅”映射到 `/Users/mac/IdeaProjects/dx-game-hall`

## [2026-04-27] Update | 清理旧 LLM 学习型索引内容
- 重写 `index.md`，移除与当前工作项目无关的 LLM 学习页索引
- 更新根 `CLAUDE.md`、`AGENTS.md` 与实例 `CLAUDE.md`，统一为 Work Harness 语义
- 保留当前唯一有效项目页 `wiki/entities/服务-dx-game-hall.md`

## [2026-04-27] Update | 稳定 Work Harness 架构边界
- 重写根 `README.md`，明确 Source / Memory / Index / Execution 四层职责
- 补齐 `llm-harness-project/harness/` 执行层规则
- 更新 `CLAUDE.md`、`AGENTS.md`、实例 `CLAUDE.md` 与 `index.md`，统一系统层、实例层、知识层和执行层边界
- 补齐当前实例 `raw/` 与 `wiki/` 的工作型目录骨架

## [2026-04-27] Ingest | raw 摄入: dx-game-hall 第一刀，产物 9 份，wiki 待后续轮次
- 仅写入 `llm-harness-project/raw/repos/dx-game-hall/`
- 产物覆盖 README、POM、包树、入口、配置、文档、git 热度、外部依赖、结构判断
