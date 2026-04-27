# LLM Harness Log

本文件 append-only，记录所有结构化更新。

格式：`## [YYYY-MM-DD] 操作类型 | 标题`

## [2026-04-27] Init | 三仓首批 10 页种子知识页

- 范围：`dx-game-core`、`dx-game-frame`、`dx-game-texas`
- 新增实体页 6 个：仓库 3 个、模块 1 个、任务 2 个
- 新增主题页 2 个：线程与事件分发骨架、Texas 牌局任务生命周期
- 新增 runbook 2 个：下注超时排查、结算后不开新手排查
- 更新 `index.md`
- 说明：本批以“结构地图 + 关键链路 + 高频排障入口”为主，尚未引入事故页和变更页

## [2026-04-27] Update | 固化 Harness 核心指令与全文索引规则

- 重写 `CLAUDE.md`，明确目标、铁律、全文索引原则、命名规则、核心指令和行为约束
- 新增 `harness/queries/QUERY_RULES.md`
- 新增 `harness/checklists/CHECKLIST-知识回写.md`
- 新增 `harness/prompts/PROMPT-INGEST-REPO.md`
- 更新 `index.md`

## [2026-04-27] Update | 先定结构并清理规则与内容混放

- 重写 `README.md`，只保留最小项目结构和目录职责
- 更新 `CLAUDE.md`，明确系统层与内容层边界
- 重写 `index.md`，改成系统入口 + 内容根目录 + 种子页导航
- 删除 `wiki/synthesis/对比-query-vs-locate-vs-runbook.md`，避免把规则文档混入知识页层

## [2026-04-27] Update | 合并重构方案到 README

- 将 `WORK_HARNESS_REDESIGN.md` 的目标、仓库映射、页面设计、起步策略合并进 `README.md`
- 删除重复的独立方案文件，保留单一结构入口
