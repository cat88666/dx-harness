# LLM Harness

这是一个面向日常开发的个人 Harness。

它保留受约束的 Karpathy LLM Wiki / Obsidian 工程记忆模型，但目标不是记学习笔记，而是为真实研发工作提供：

- 代码结构索引
- 工程记忆沉淀
- 排障与复盘入口
- Agent 执行约束

## 目标

这套结构要解决 3 个实际问题：

1. 让 Agent 知道代码在哪一层、问题落在哪一层
2. 让知识沉淀按仓库结构和问题类型发生，而不是按聊天记录堆积
3. 让调试、改代码、回顾事故、做需求时复用同一套上下文

你的真实工作环境不是单仓，而是 `/Users/mac/IdeaProjects` 下的多仓体系：

- 框架层：`dx-game-frame`、`dz-framework`、`dx-game-core`
- 业务层：`dx-game-texas`、`dx-game-mahjong`、`dx-game-guandan`
- 基础设施层：`dx-net-bolt`、`dx-hub-server`、`dx-common-facades`

## 最小结构

```text
llm-harness-template/
├── README.md           ← 结构说明，只解释“这套系统是什么”
├── CLAUDE.md           ← 系统规则、核心指令、命名约束
├── index.md            ← 总入口，只做导航，不承载长解释
├── log.md              ← append-only 变更记录
├── raw/                ← 原始来源层，只读
├── cleaned/            ← 整理层，放脱敏/归一化后的材料
├── wiki/               ← 工程记忆层
└── harness/            ← Agent 执行层
```

## 目录职责

### `raw/`

只保存原始来源：

- `repos/`：仓库路径、模块树、关键 `pom.xml`、README、配置快照
- `tickets/`：需求、Bug、聊天结论
- `logs/`：日志、异常栈、traceId 资料
- `sql/`：表结构、脚本、查询样例
- `incidents/`：事故原始材料

### `cleaned/`

只放整理后的中间材料，例如脱敏日志、归一化调用链、修正格式后的文本。

### `wiki/`

只放稳定的工程记忆：

- `concepts/`：通用工程概念，如幂等、延迟任务、事件驱动、缓存一致性
- `entities/`：仓库、模块、服务、任务、表、配置项
- `summaries/`：链路或主题聚合
- `runbooks/`：排障手册
- `incidents/`：事故复盘
- `changes/`：需求、修复、重构记录
- `synthesis/`：对比、策略、判断

规则文档不要放进 `wiki/`。

### `harness/`

只放 Agent 约束材料：

- `prompts/`
- `queries/`
- `checklists/`

这里是执行层，不是知识页层。

## 页面设计

学习型 wiki 里的 `concepts / entities / summaries / synthesis` 仍然保留，但工作场景必须补齐 3 类：

- `runbooks/`：标准排障动作
- `incidents/`：一次事故一页
- `changes/`：一次需求、修复或重构一页

推荐命名：

- `entities/仓库-dx-game-frame.md`
- `entities/模块-dx-game-frame-service-core.md`
- `entities/服务-dx-game-texas.md`
- `entities/任务-UserBetCountdownTask.md`
- `runbooks/Runbook-Texas下注超时链路排查.md`
- `incidents/Incident-牌局未结算导致房间卡死.md`
- `changes/变更-德州发牌链路重构.md`
- `summaries/主题-Texas任务调度模型.md`
- `synthesis/对比-Disruptor-vs-线程池任务派发.md`

## 与当前代码库的映射

第一步不是全量导入，而是先建立系统地图：

- `dx-game-frame`：通用框架层，优先沉淀线程模型、任务调度、RPC、Repository、Proto
- `dx-game-core`：运行时核心能力层，优先沉淀事件、队列、线程、延迟事件
- `dz-framework`：基础设施封装层，优先沉淀 Redis、MQ、Nacos、日志、优雅停机
- `dx-game-texas`：业务样板层，优先沉淀任务链路、牌局状态机、配置驱动行为
- `dx-hub-server` / `dx-common-facades`：外围协作层，沉淀跨服务依赖

第一批最值得编译进来的不是所有代码，而是：

1. `pom.xml` 和模块树
2. 启动类、配置目录、环境 profile
3. 核心任务链路，如 `TableLoopTask`、`UserBetCountdownTask`
4. 常见故障日志与 traceId 排查路径
5. 高频改动点和易踩坑配置

## 起步策略

不要一上来全量导入 `/Users/mac/IdeaProjects`。

第一阶段只做 3 个仓：

1. `dx-game-frame`
2. `dx-game-core`
3. `dx-game-texas`

第一周只产出 10-15 页高价值页面：

- 3 个仓库/模块地图
- 2 个任务链路 summary
- 2 个 runbook
- 2 个 incident
- 1 个架构对比 synthesis

先进入可用状态，再逐步扩充。

## 当前原则

1. 先定结构，再扩内容
2. `wiki/` 只写长期有复用价值的内容
3. 规则写在 `CLAUDE.md` 和 `harness/`，不混进知识页
4. `index.md` 只做入口，不做大段说明
