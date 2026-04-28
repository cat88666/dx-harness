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

## [2026-04-28] Update | 固化三段式 harness skill 命令
- 更新 `.claude/skills/ingest-source/SKILL.md`，定义 `/ingest-map`、`/ingest-deepen`、`/harness-locate`
- 更新 `.claude/skills/ingest-source/references/standards.md`，补充三种命令模式、粗粒度地图字段和细粒度扩展字段
- 新增 `llm-harness-project/harness/prompts/PROMPT-INGEST-DEEPEN.md`
- 更新根 `CLAUDE.md`、实例 `CLAUDE.md`、`README.md`、`PROMPT-INGEST-REPO.md` 和 `QUERY_RULES.md`，统一三段式摄入与定位流程

## [2026-04-28] Update | 增加始终中文全局规则
- 更新根 `CLAUDE.md`，增加语言规则和铁律：除非用户明确要求其他语言，所有输出和回写都使用中文
- 更新 `llm-harness-project/CLAUDE.md`，同步当前实例语言规则

## [2026-04-28] Update | 中文化 ingest-source skill
- 将 `.claude/skills/ingest-source/SKILL.md` 中刚新增的三段式命令说明改为中文
- 将 `.claude/skills/ingest-source/references/standards.md` 中命令模式、字段标准和接受/拒绝规则改为中文

## [2026-04-28] Ingest | ingest-map dx-game-texas 粗粒度地图
- 更新 `wiki/entities/仓库-dx-game-texas.md` 为粗粒度仓库地图，覆盖基础事实、分支族、包职责、协议入口、服务入口、任务入口、RPC/MQ、配置入口、热点文件和后续 deepen 候选
- 更新 `index.md`，将德州蘑菇游戏当前本地分支修正为 `duik-mushroom-temp-final`，并补充 `PROMPT-INGEST-DEEPEN.md` 系统入口
- 本次未写 `raw/` 快照；依据当前仓库规则，将 `raw/` 作为只读输入层，来源直接指向 `/Users/mac/IdeaProjects/dx-game-texas` 文件和 git 命令

## [2026-04-28] Ingest | ingest-deepen 德州蘑菇逃庄留座离桌链路
- 更新 `wiki/summaries/主题-德州蘑菇逃庄留座离桌链路.md`，从旧的候选拦截点说明深化为当前分支 `MushroomNextButtonService` 实现地图
- 更新 `wiki/changes/任务-德州蘑菇逃庄需求补充.md`，将当前上下文修正为 `duik-mushroom-temp-final`，补充已接入出口、验收要点和持续关注项
- 更新 `index.md`，补充 `MushroomNextButtonService`、`nextButtonUserId`、蘑菇防逃庄回归测试点的自然语言入口
- 本次未写 `raw/` 快照；来源直接指向 `/Users/mac/IdeaProjects/dx-game-texas` 当前源码、`docs/蘑菇防逃庄功能回归测试点.md` 与 `docs/handleNextButton需求分析.md`

## [2026-04-28] Query | harness-locate 蘑菇逃庄留座离桌
- 从 `index.md` 自然语言入口定位到 `wiki/entities/仓库-dx-game-texas.md`、`wiki/changes/任务-德州蘑菇逃庄需求补充.md`、`wiki/summaries/主题-德州蘑菇逃庄留座离桌链路.md`
- 复核真实仓库 `/Users/mac/IdeaProjects/dx-game-texas` 当前分支为 `duik-mushroom-temp-final`，工作区仅有未跟踪 `.DS_Store` 与 `src/.DS_Store`
- 源码命中 `MushroomNextButtonService`、`UserHoldSeatHandler`、`UserLeaveTask`、`HandOverListener`、`GameStartHandlerBase` 等开发定位入口

## [2026-04-28] Query | harness-locate 普通预站起 蘑菇逃庄
- 从主题页中的普通预站起风险点定位到 `PrepStandCommand`、`SpecifyService`、`MushroomNextButtonService` 与 `UserStandHander`
- 确认普通预站起设置阶段不直接调用 `MushroomNextButtonService`；手牌进行中由结算后 `SpecifyService.collectPreStandUsers` 收集并在 `handleForcedUserAction` 拦截，非手牌进行中则同步触发 `handleForcedUserAction`
- 回写 `wiki/summaries/主题-德州蘑菇逃庄留座离桌链路.md` 与 `wiki/changes/任务-德州蘑菇逃庄需求补充.md`，将“需确认”改为已确认链路
