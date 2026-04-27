# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 仓库用途

这是面向日常开发的个人 Work Harness。目标是把 `/Users/mac/IdeaProjects` 下真实工作项目的代码结构、排障经验、需求变更和事故复盘，编译成 Agent 可检索、可注入、可执行的工程记忆。

当前活跃实例：`llm-harness-project/`。

## 技能指令

| 指令 | 触发条件 |
|------|---------|
| `/ingest-repo <repo>` | 摄入工作代码仓结构和关键对象 |
| `/query <问题>` | 基于本地工程记忆回答问题 |
| `/locate <对象>` | 定位仓库、模块、服务、任务、类或配置 |
| `/runbook <症状>` | 返回排障步骤 |
| `/lint-work` | 检查索引、命名、失效引用和重复页 |

详细执行流水线见 `.claude/skills/` 对应 SKILL.md。
命名规则的唯一权威：`.claude/skills/naming/SKILL.md`。

## 铁律（任何操作均不可违反）

1. **`raw/` 只读**：绝对不写入、移动或修改 `raw/` 下任何文件
2. **操作后必须收尾**：每次 ingest / query 回写 / review / lint 后，必须更新 `llm-harness-project/index.md` 并追加 `llm-harness-project/log.md`
3. **新建页面前必须命名**：任何新文件落盘前，先按 `naming/SKILL.md` 规则确定文件名，禁止自由命名
4. **优先更新，不轻易新建**：新资料优先合并进已有页面，确实需要新主题时才新建
5. **工作项目优先索引**：自然语言对象名必须能从 `index.md` 直达真实仓库和知识页，例如“大厅”应定位到 `dx-game-hall`
6. **结论必须有来源**：项目页和排障页必须回指源码、配置、日志、SQL、工单或事故材料
