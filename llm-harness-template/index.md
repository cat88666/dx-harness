# LLM Harness Index

> 总入口只做导航，不承载长解释。

## System

- [README.md](README.md) — 项目结构说明
- [CLAUDE.md](CLAUDE.md) — 规则、命名、核心指令
- [log.md](log.md) — append-only 结构化变更记录

## Harness

- [harness/prompts/PROMPT-INGEST-REPO.md](harness/prompts/PROMPT-INGEST-REPO.md) — `/ingest-repo` 的执行模板
- [harness/queries/QUERY_RULES.md](harness/queries/QUERY_RULES.md) — `/query`、`/locate`、`/runbook` 的边界
- [harness/checklists/CHECKLIST-知识回写.md](harness/checklists/CHECKLIST-知识回写.md) — 知识回写检查清单

## Content Roots

- `wiki/entities/` — 对象索引层
- `wiki/summaries/` — 主题聚合层
- `wiki/runbooks/` — 排障手册层
- `wiki/incidents/` — 事故复盘层
- `wiki/changes/` — 变更沉淀层
- `wiki/synthesis/` — 对比判断层

## Active Seeds

- [[仓库-dx-game-core]](wiki/entities/仓库-dx-game-core.md)
- [[仓库-dx-game-frame]](wiki/entities/仓库-dx-game-frame.md)
- [[服务-dx-game-texas]](wiki/entities/服务-dx-game-texas.md)
- [[模块-dx-game-frame-service-core]](wiki/entities/模块-dx-game-frame-service-core.md)
- [[任务-TableLoopTask]](wiki/entities/任务-TableLoopTask.md)
- [[任务-UserBetCountdownTask]](wiki/entities/任务-UserBetCountdownTask.md)
- [[主题-线程与事件分发骨架]](wiki/summaries/主题-线程与事件分发骨架.md)
- [[主题-Texas牌局任务生命周期]](wiki/summaries/主题-Texas牌局任务生命周期.md)
- [[Runbook-Texas下注超时链路排查]](wiki/runbooks/Runbook-Texas下注超时链路排查.md)
- [[Runbook-Texas结算后不开新手排查]](wiki/runbooks/Runbook-Texas结算后不开新手排查.md)
