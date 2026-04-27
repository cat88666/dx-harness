# llm-harness-project 实例配置

本文件仅记录 `llm-harness-project` 实例的特定配置。
通用规范（铁律 / 命名规则 / 操作流水线）见：
- 根目录 `CLAUDE.md` → 铁律与技能路由
- `.claude/skills/naming/SKILL.md` → 命名规则（唯一权威）
- `.claude/skills/<skill>/SKILL.md` → 各操作流水线

## 实例路径

| 路径 | 用途 |
|------|------|
| `llm-harness-project/raw/` | 原始资料（只读） |
| `llm-harness-project/wiki/` | 结构化知识库 |
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
```

## 已知技术债

当前实例刚从学习型 wiki 清理为工作 Harness。新增内容必须遵守命名规则，不得重新引入与工作项目无关的 LLM 学习页。
