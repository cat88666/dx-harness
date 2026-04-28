# DX Harness

DX Harness 是一个面向日常开发的个人工程记忆与 Agent 执行约束系统。

它不保存聊天记录，也不做学习笔记。它只解决一个问题：把真实工作项目的代码结构、排障经验、需求变更和事故复盘，沉淀成 Agent 可以检索、注入和执行的稳定上下文。

当前活跃实例：`llm-harness-project/`

## 工作空间清单

> 以下按仓库名和现有 README、目录结构整理，是一版面向日常协作的初始定位。

### 核心业务与共享框架

| 项目 | 核心内容 |
| --- | --- |
| `dx-account` | 账号中心与用户基础能力，偏身份、登录、账号相关流程 |
| `dx-b-chat-server` | 聊天服务，负责消息、会话和聊天相关接口 |
| `dx-common-facades` | 跨服务公共 DTO / Facade / RPC 接口共享层 |
| `dx-game-cn-poker` | 国标扑克业务服务，承载对应玩法主流程 |
| `dx-game-core` | 游戏运行时核心能力，偏任务、事件、状态推进和通用游戏逻辑 |
| `dx-game-frame` | 游戏框架层，承载公共协议、RPC、repository 和通用支撑能力 |
| `dx-game-guandan` | 掼蛋业务服务，承载该玩法的房间与牌局流程 |
| `dx-game-hall` | 比赛大厅 / 游戏大厅服务，负责登录、房间/牌桌列表、比赛、报名、用户状态、钱包、广播、排队 |
| `dx-game-http` | HTTP 接口层 / 聚合层，含 controller、filter、interceptor、service 等入口 |
| `dx-game-mahjong` | 麻将业务服务，承载该玩法的房间与牌局流程 |
| `dx-game-race-hall` | 赛事大厅 / 比赛入口服务，偏赛事列表、详情、报名和赛桌能力 |
| `dx-game-replay` | 回放与复现工具，偏机器人流程回放、问题复盘和压测支撑 |
| `dx-game-texas` | 德州业务服务，承载牌局状态机、下注、发牌、结算和下一手推进 |
| `dx-hub-server` | 中枢 / 聚合服务，负责跨业务编排和共享入口 |
| `dx-net-bolt` | Bolt 通信相关封装，偏网络协议、客户端/服务端接入 |
| `dx-net-gateway` | 网络网关层，偏接入、转发和协议桥接 |
| `dx-robot` | 机器人与压测套件，按游戏拆分多个子模块，并带脚本、报告和 GTO 求解辅助 |
| `dx-game-robot` | 轻量机器人服务 / 实验仓，保留独立 `src`、`doc` 和基础自动化入口 |
| `dz-framework` | 基础设施封装层，偏 Redis、MQ、Nacos、日志等通用支撑 |
| `dz-game-framework` | 另一套游戏框架仓，通常承载通用能力和历史架构遗留 |

### 实验、样例与源码快照

| 项目 | 核心内容 |
| --- | --- |
| `dx-ace-snake` | 独立游戏 / 演示项目，偏样例工程或小型玩法实验 |
| `dx-game-test` | 测试壳 / 空仓，当前内容很少，主要是占位或实验入口 |
| `netty-netty-4.2.6.Final` | Netty 源码快照，偏第三方依赖源码参考 |
| `sofa-bolt` | SOFA Bolt 源码快照，偏第三方依赖源码参考 |

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
7. 新项目先 `/ingest-map` 建粗粒度地图；已有地图再 `/ingest-deepen` 扩细节；定位类问题先 `/harness-locate`，不要直接全仓扩散。

## 四、当前状态

当前实例已登记：

- 大厅 / 比赛大厅 / 游戏大厅 → `dx-game-hall` → `/Users/mac/IdeaProjects/dx-game-hall`
- 德州 / 德州扑克 / Texas → `dx-game-texas` → `/Users/mac/IdeaProjects/dx-game-texas`

当前还未进入大规模内容建设阶段。下一步应先用 `/ingest-map` 补齐核心仓库粗粒度地图，再按实际需求用 `/ingest-deepen` 扩展链路、任务和 runbook。
