# llm-harness-project 实例配置

本文件仅记录 `llm-harness-project` 实例的特定配置。
通用规范见根目录 `CLAUDE.md`；当前实例的执行约束见 `llm-harness-project/harness/`。

## 实例路径

| 路径 | 用途 |
|------|------|
| `llm-harness-project/raw/` | 原始资料（只读） |
| `llm-harness-project/wiki/` | 结构化知识库 |
| `llm-harness-project/harness/` | 当前实例的 Agent 执行约束 |
| `llm-harness-project/index.md` | 全局索引 |
| `llm-harness-project/log.md` | 操作日志（append-only） |

## 当前实例定位

`llm-harness-project` 是当前真实工作项目的工程记忆实例。它只保留与 `/Users/mac/IdeaProjects` 下工作代码仓有关的知识，不再承载 LLM 学习笔记。

当前已登记项目：

- 大厅 / 比赛大厅 / 游戏大厅 → `dx-game-hall` → `/Users/mac/IdeaProjects/dx-game-hall`

## 目录结构

```text
llm-harness-project/raw/          ← 原始资料（只读）
├── repos/                ← 仓库路径、模块树、pom.xml、README、配置快照
├── tickets/              ← 需求、Bug、聊天结论
├── logs/                 ← 日志、异常栈、traceId 资料
├── sql/                  ← 表结构、脚本、查询样例
└── incidents/            ← 事故原始材料

llm-harness-project/wiki/         ← 编译后的工程记忆
├── entities/             ← 仓库、模块、服务、任务、表、配置项
├── summaries/            ← 链路或主题聚合
├── runbooks/             ← 排障手册
├── incidents/            ← 事故复盘
├── changes/              ← 需求、修复、重构记录
└── synthesis/            ← 对比、策略、判断

llm-harness-project/harness/      ← 当前实例执行约束
├── prompts/              ← ingest / review / 回写模板
├── queries/              ← query / locate / runbook 输出边界
└── checklists/           ← 收尾检查清单
```

## 当前稳定边界

- `index.md` 只登记真实可用的工作知识页，不索引模板、规则或不存在的页面
- `wiki/` 只保留与当前工作项目有关的页面
- `harness/` 可以定义规则，但不得承载项目知识
- `.claude/skills/` 是技能标准库，负责定义摄入标准和页面切分规则
- 新增项目必须先进入 `index.md` 的自然语言定位区
- 命名规则由目录职责和类型前缀共同决定，不依赖外部规则文件
- 除非用户明确要求其他语言，当前实例所有回复、知识回写、规则说明和日志记录始终使用中文

## 三段式摄入命令

| 命令 | 用途 | 输出边界 |
|------|------|----------|
| `/ingest-map <source>` | 自动摄入项目/仓库粗粒度地图，包括自然语言索引、仓库卡、分支/模块/入口定位 | 只建方向，不展开深链路 |
| `/ingest-deepen <object-or-page>` | 在已有粗粒度地图基础上扩展细粒度模块、任务、链路、runbook | 一次只扩一个对象或问题簇 |
| `/harness-locate <object-or-question>` | 最少 token 定位方向，先查 `index.md`，再查已链接知识页 | 返回去哪看，不做大段分析 |

执行顺序固定为：先 `/harness-locate` 判断是否已有路线；没有路线则 `/ingest-map`；已有路线但知识不够才 `/ingest-deepen`。
