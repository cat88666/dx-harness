# Wiki Log

本文件记录所有操作，append-only，禁止修改历史记录。

格式：`## [YYYY-MM-DD] 操作类型 | 标题`
操作类型：`Init` / `Ingest` / `Query` / `Lint` / `Update`

---

## [2026-04-27] Update | 增加 dx-game-hall 工作项目索引
- 新增 `wiki/entities/服务-dx-game-hall.md`
- 在 `index.md` 增加 `Work Projects`，将“大厅 / 比赛大厅 / 游戏大厅”映射到 `/Users/mac/IdeaProjects/dx-game-hall`

## [2026-04-27] Update | 稳定 Work Harness 架构边界
- 重写根 `README.md`，明确 Source / Memory / Index / Execution 四层职责
- 补齐 `llm-harness-project/harness/` 执行层规则
- 更新 `CLAUDE.md`、`AGENTS.md`、实例 `CLAUDE.md` 与 `index.md`，统一系统层、实例层、知识层和执行层边界
- 补齐当前实例 `raw/` 与 `wiki/` 的工作型目录骨架

## [2026-04-27] Ingest | raw 摄入: dx-game-hall 第一刀，产物 9 份，wiki 待后续轮次
- 仅写入 `llm-harness-project/raw/repos/dx-game-hall/`
- 产物覆盖 README、POM、包树、入口、配置、文档、git 热度、外部依赖、结构判断

## [2026-04-27] Ingest | wiki 摄入: dx-game-hall 仓库卡(第二刀)
- 仅产出 `llm-harness-project/wiki/entities/仓库-dx-game-hall.md`
- 来源为 `llm-harness-project/raw/repos/dx-game-hall/` 下 9 份快照
- `index.md` 已将“大厅 / 比赛大厅 / 游戏大厅”补到仓库卡
- 模块页 / runbook 待第三刀

## [2026-04-27] Update | raw 重做 + 仓库卡修订(第二刀补丁)
- `raw/repos/dx-game-hall/2026-04-27-external-deps.md` 重做为 A-F 六节扫描结果
- `wiki/entities/仓库-dx-game-hall.md` 仅修订第 4 / 5 / 7 / 9 节
- `index.md` 未更新，对象关系不变

## [2026-04-28] Update | 补齐德州蘑菇逃庄需求索引
- 新增 `wiki/entities/仓库-dx-game-texas.md`，将“德州 / 德州扑克 / Texas”定位到 `/Users/mac/IdeaProjects/dx-game-texas`
- 新增 `wiki/changes/任务-德州蘑菇逃庄需求补充.md`，登记蘑菇游戏第三轮提测中的逃庄 BUG 补充需求
- 新增 `wiki/summaries/主题-德州蘑菇逃庄留座离桌链路.md`，沉淀 `USER_HOLD_SEAT` 到结算后蘑菇庄位拦截链路
- 更新 `index.md`，增加德州、蘑菇游戏、逃庄、留座离桌和第三轮提测的自然语言入口
