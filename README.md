# DX Harness

DX Harness 是一个面向日常开发的个人工程记忆与 Agent 执行约束系统。

它不保存聊天记录，也不做学习笔记。它只解决一个问题：把真实工作项目的代码结构、排障经验、需求变更和事故复盘，沉淀成 Agent 可以检索、注入和执行的稳定上下文。

当前活跃实例：`llm-harness-project/`

## 一、稳定架构

```text
dx-harness/
├── AGENTS.md                 # Codex / Agent 协作规则
├── CLAUDE.md                 # 全局铁律与命令路由
├── README.md                 # 架构总纲
├── assets/                   # 图片与展示资源
├── llm-harness-project/      # 当前真实工作实例
│   ├── CLAUDE.md             # 实例规则
│   ├── index.md              # 全局索引，负责自然语言对象定位
│   ├── log.md                # append-only 变更日志
│   ├── raw/                  # 原始来源，只读
│   ├── wiki/                 # 编译后的工程记忆
│   └── harness/              # 当前实例的 Agent 执行约束
└── llm-harness-template/     # 可复制的空模板
    ├── CLAUDE.md
    ├── README.md
    ├── index.md
    ├── log.md
    ├── raw/
    ├── wiki/
    └── harness/
```

## 二、四层职责

### 1. Source Layer：`raw/`

只放原始来源或快照，不直接改写。

- `repos/`：仓库路径、模块树、`pom.xml`、README、配置快照
- `tickets/`：需求、Bug、聊天结论
- `logs/`：日志、异常栈、traceId 材料
- `sql/`：表结构、脚本、查询样例
- `incidents/`：事故原始材料

### 2. Memory Layer：`wiki/`

只放长期稳定、可复用的工程记忆。

- `entities/`：仓库、模块、服务、任务、表、配置项、MQ Topic
- `summaries/`：链路或主题聚合
- `runbooks/`：可执行排障手册
- `incidents/`：事故复盘
- `changes/`：需求、修复、重构记录
- `synthesis/`：对比、策略、判断

### 3. Index Layer：`index.md`

只做定位，不承载长解释。

自然语言对象名必须能从这里直达真实仓库和知识页。例如“大厅 / 比赛大厅 / 游戏大厅”必须定位到 `dx-game-hall`。

### 4. Execution Layer：`harness/`

只放 Agent 执行约束。

- `prompts/`：摄入、分析、回写等任务模板
- `queries/`：`query / locate / runbook` 输出边界
- `checklists/`：修改后必须检查的收尾清单

可复用的 skill 标准库放在 `.claude/skills/`，当前实例的运行约束放在 `llm-harness-project/harness/`。

## 三、核心原则

1. 真实代码仓是事实源，`wiki/` 是解释层。
2. `raw/` 只读，`wiki/` 才是可维护知识。
3. `index.md` 负责定位，知识页负责解释，`harness/` 负责执行约束。
4. 新页必须带类型前缀：`仓库-`、`模块-`、`服务-`、`任务-`、`主题-`、`Runbook-`、`Incident-`、`变更-`、`对比-`。
5. 任何 `wiki/` 实质修改后，必须同步更新 `index.md` 并追加 `log.md`。
6. 结论必须回指源码、配置、日志、SQL、工单或事故材料。

## 四、当前状态

当前实例已登记：

- 大厅 / 比赛大厅 / 游戏大厅 → `dx-game-hall` → `/Users/mac/IdeaProjects/dx-game-hall`

当前还未进入大规模内容建设阶段。下一步应先完善 `dx-game-hall` 的仓库页、核心模块页和 runbook，而不是继续扩散目录或规则。
