# 工作版 Harness Wiki 规则

## 目标

这是一个面向日常开发的个人 Harness，同时保留受约束的 Wiki / Obsidian 工程记忆模型。

目标不是记录聊天，而是把代码仓、日志、配置、需求、事故和变更，编译成可被人和 Agent 稳定消费的结构化工程记忆。

## 铁律

1. `raw/` 只读，保存来源或快照，不直接篡改原始材料
2. 真实代码仓是事实源，`wiki/` 是解释层，不替代源码
3. 新建页面前先判断类型和命名，禁止自由命名
4. 优先更新已有页面，避免“同一问题多页并存”
5. 每次 ingest / query 回写 / review / lint 后，必须更新 `index.md` 和 `log.md`
6. 结论必须能回指到源码、日志、SQL、配置、工单或事故材料
7. 页面写稳定知识，不写临时聊天过程
8. 任何排障结论都应尽量沉淀为 `runbooks/`、`incidents/` 或 `changes/`

## 全文索引原则

1. `index.md` 是总入口，必须登记所有有效知识页
2. 页名要直接暴露对象或问题，不允许抽象空标题
3. 每页必须出现可检索的关键字：
   - 仓库名
   - 模块名
   - 关键类名
   - 关键任务名
   - 关键事件键、配置项、traceId 模式或症状词
4. `query` 用主题页和综合页回答问题，`locate` 用实体页和 runbook 直达对象
5. 索引层次固定：先 `Entities`，再 `Summaries`，再 `Runbooks`，最后 `Incidents / Changes / Synthesis`
6. `README.md`、`CLAUDE.md`、`harness/` 属于系统层，不进入 `wiki/` 内容索引

## 页面分类

- `wiki/concepts/`：工程抽象概念，如幂等、串行分组、延迟事件
- `wiki/entities/`：仓库、模块、服务、任务、表、配置项、MQ Topic
- `wiki/runbooks/`：可执行操作手册
- `wiki/incidents/`：事故复盘
- `wiki/changes/`：需求、修复、重构记录
- `wiki/summaries/`：链路或主题聚合
- `wiki/synthesis/`：对比、策略、判断

## 结构边界

- `README.md`：解释项目结构
- `CLAUDE.md`：定义规则与核心指令
- `harness/`：放 Agent 约束材料
- `wiki/`：只放工程记忆本身

不要把“规则解释文档”写成 `wiki/synthesis/` 页面。

## 命名规则

统一用 `类型-核心名称.md`：

- `仓库-<repo>.md`
- `模块-<module>.md`
- `服务-<service>.md`
- `任务-<task>.md`
- `主题-<链路或主题>.md`
- `Runbook-<症状>排查.md`
- `Incident-<事故标题>.md`
- `变更-<需求或修复标题>.md`
- `对比-<方案A>-vs-<方案B>.md`

## 核心指令

- `/ingest-repo <repo>`：摄入仓库结构、模块、关键类、README、`pom.xml`
- `/ingest-issue <text|file>`：摄入需求、Bug、聊天结论
- `/ingest-log <traceId|file>`：摄入日志、异常栈、调用链
- `/query <question>`：基于本地工程记忆回答问题
- `/locate <symbol|class|task|table>`：直达代码对象、链路或知识页
- `/runbook <symptom>`：按症状返回排障步骤
- `/incident <title|traceId>`：生成事故页
- `/review <change>`：基于知识库做变更审查
- `/lint-work`：检查索引、命名、失效引用、重复页、过期 runbook

## 指令行为约束

### `/ingest-repo`

- 先生成或更新仓库页
- 再生成模块页和主题页
- 不做全量导入，优先导入高频链路和高价值对象

### `/query`

- 优先读取 `summaries/`、`synthesis/`、`runbooks/`
- 回答必须带出对应页面或源码对象
- 若知识缺失，应补写页面而不是只返回口头结论

### `/locate`

- 优先命中 `entities/`
- 若命中任务或链路，应同时给出对应 summary / runbook

### `/runbook`

- 输出症状、排查顺序、高概率原因、关键源码
- 若已有事故页，应优先关联事故页

### `/incident`

- 结构固定：现象、影响、时间线、根因、证据、修复、预防

### `/lint-work`

- 检查未索引页面
- 检查失效来源路径
- 检查重复页和空泛标题
- 检查 runbook 是否缺少“适用症状”和“排查顺序”
