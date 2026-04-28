# Work Harness Index

> 总入口只做导航。这里登记当前实例中真实可用的工作项目知识页。

## Projects

### 大厅 / 比赛大厅 / 游戏大厅

- [[仓库-dx-game-hall]](wiki/entities/仓库-dx-game-hall.md) — 比赛大厅后端仓库卡，真实仓库 `/Users/mac/IdeaProjects/dx-game-hall`

### 德州 / 德州扑克 / Texas

- [[仓库-dx-game-texas]](wiki/entities/仓库-dx-game-texas.md) — 德州游戏后端仓库卡，真实仓库 `/Users/mac/IdeaProjects/dx-game-texas`
- [[任务-德州蘑菇逃庄需求补充]](wiki/changes/任务-德州蘑菇逃庄需求补充.md) — 当前蘑菇游戏开发 / 提测第三轮中的逃庄 BUG 补充需求
- [[主题-德州蘑菇逃庄留座离桌链路]](wiki/summaries/主题-德州蘑菇逃庄留座离桌链路.md) — 当前分支 `MushroomNextButtonService`、保护窗口和离桌出口定位链路

## Active Work

### 德州蘑菇游戏

- 当前本地分支: `/Users/mac/IdeaProjects/dx-game-texas` → `duik-mushroom-temp-final`
- 蘑菇开发分支族: `feture-sun-16603`、`origin/16603-final`、`origin/duik-mushroom-temp-final`
- 自然语言入口:
  - “德州” / “德州扑克” / “Texas” → [[仓库-dx-game-texas]](wiki/entities/仓库-dx-game-texas.md)
  - “蘑菇游戏” / “堆蘑菇” / “蘑菇逃庄” / “逃庄 BUG” / “第三轮提测” → [[任务-德州蘑菇逃庄需求补充]](wiki/changes/任务-德州蘑菇逃庄需求补充.md)
  - “留座离桌” / “结算留座离桌” / “下一手庄位不能离开” → [[主题-德州蘑菇逃庄留座离桌链路]](wiki/summaries/主题-德州蘑菇逃庄留座离桌链路.md)
  - “MushroomNextButtonService” / “nextButtonUserId” / “蘑菇防逃庄回归测试点” → [[主题-德州蘑菇逃庄留座离桌链路]](wiki/summaries/主题-德州蘑菇逃庄留座离桌链路.md)

## Content Roots

- `wiki/entities/` — 仓库、模块、服务、任务、表、配置项等对象索引
- `wiki/summaries/` — 跨对象主题聚合
- `wiki/runbooks/` — 可执行排障手册
- `wiki/incidents/` — 事故复盘
- `wiki/changes/` — 需求、修复、重构记录
- `wiki/synthesis/` — 对比、策略、判断

## System

- [CLAUDE.md](CLAUDE.md) — 当前实例规则
- [harness/queries/QUERY_RULES.md](harness/queries/QUERY_RULES.md) — 查询、定位、排障输出边界
- [harness/prompts/PROMPT-INGEST-REPO.md](harness/prompts/PROMPT-INGEST-REPO.md) — 仓库摄入模板
- [harness/prompts/PROMPT-INGEST-DEEPEN.md](harness/prompts/PROMPT-INGEST-DEEPEN.md) — 细粒度扩展模板
- [harness/checklists/CHECKLIST-知识回写.md](harness/checklists/CHECKLIST-知识回写.md) — 知识回写检查清单
- [log.md](log.md) — append-only 变更记录
