# CLAUDE.md

## 仓库用途

这是面向日常开发的个人 Work Harness。目标是把 `/Users/mac/IdeaProjects` 下真实工作项目的代码结构、排障经验、需求变更和事故复盘，编译成 Agent 可检索、可注入、可执行的工程记忆。

当前活跃实例：`llm-harness-project/`。

## 架构边界

- `README.md`：架构总纲，只定义系统怎么分层
- `AGENTS.md`：Codex / Agent 协作规则
- `CLAUDE.md`：全局铁律与命令路由
- `llm-harness-project/`：当前真实工作实例
- `llm-harness-template/`：无项目绑定模板
- `raw/`：原始来源，只读
- `wiki/`：稳定工程记忆
- `harness/`：Agent 执行约束，不放业务知识页

## 技能指令

| 指令 | 触发条件 |
|------|---------|
| `/ingest-source <source>` | 摄入项目资料、产品资料或代码库 |
| `/ingest-repo <repo>` | 摄入工作代码仓结构和关键对象 |
| `/ingest-map <source>` | 自动摄入项目/仓库粗粒度地图，补齐索引和知识结构，用最少 token 支持后续定位 |
| `/ingest-deepen <object-or-page>` | 基于已有粗粒度页面继续扩展细粒度模块、链路、任务或 runbook |
| `/harness-locate <object-or-question>` | 低 token 定位入口，先走 `index.md`，返回目标仓库、分支、知识页和源码入口 |
| `/query <问题>` | 基于本地工程记忆回答问题 |
| `/locate <对象>` | 定位仓库、模块、服务、任务、类或配置 |
| `/runbook <症状>` | 返回排障步骤 |
| `/lint-work` | 检查索引、命名、失效引用和重复页 |

`.claude/skills/` 是本仓库的技能标准库；`llm-harness-project/harness/` 是当前实例的执行约束层。

## 语言规则

除非用户明确要求其他语言，所有回复、知识回写、规则说明和日志记录始终使用中文。

## 铁律（任何操作均不可违反）

1. **`raw/` 只读**：绝对不写入、移动或修改 `raw/` 下任何文件
2. **操作后必须收尾**：每次 ingest / query 回写 / review / lint 后，必须更新 `llm-harness-project/index.md` 并追加 `llm-harness-project/log.md`
3. **新建页面前必须定型命名**：任何新文件落盘前，先判断目录类型和文件前缀，禁止自由命名
4. **优先更新，不轻易新建**：新资料优先合并进已有页面，确实需要新主题时才新建
5. **工作项目优先索引**：自然语言对象名必须能从 `index.md` 直达真实仓库和知识页，例如“大厅”应定位到 `dx-game-hall`
6. **结论必须有来源**：项目页和排障页必须回指源码、配置、日志、SQL、工单或事故材料
7. **规则不进 wiki**：`wiki/` 只放工程记忆，规则、提示词、检查清单放 `harness/`
8. **技能先行**：摄入前先选择对应 skill，再决定页面类型和回写路径
9. **先地图后细节**：新项目必须先 `/ingest-map` 建立粗粒度索引；已有地图再用 `/ingest-deepen` 扩展；定位类问题先 `/harness-locate`，避免无索引全仓扫描
10. **始终中文**：除非用户明确要求其他语言，所有输出和回写都使用中文
