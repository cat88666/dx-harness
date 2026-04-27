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
