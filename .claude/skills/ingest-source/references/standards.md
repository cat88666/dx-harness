# 摄入标准

## 来源类型

| 类型 | 典型输入 | 主要输出 | 次级输出 |
| --- | --- | --- | --- |
| `project` | 计划、工单、会议记录、里程碑、范围文档 | `wiki/entities/项目-<name>.md` 或最近的稳定对象页 | `wiki/summaries/主题-<name>.md`、`wiki/changes/变更-<name>.md` |
| `product` | PRD、功能说明、UX 流程、产品决策 | `wiki/entities/产品-<name>.md` | `wiki/summaries/主题-<name>.md`、`wiki/synthesis/对比-<name>.md` |
| `codebase` | 仓库树、README、`pom.xml`、配置、源码 | 先写 `raw/repos/<repo>/` 快照，再在后续或浅层同轮写 `wiki/entities/仓库-<repo>.md` | `wiki/entities/模块-<module>.md`、`wiki/entities/服务-<service>.md`、`wiki/entities/任务-<task>.md`、`wiki/runbooks/Runbook-<symptom>排查.md` |

## 命令模式

| 命令 | 目的 | 读取预算 | 主要输出 |
| --- | --- | --- | --- |
| `/ingest-map <source>` | 为项目 / 仓库建立粗粒度地图，用于路由 | README、构建文件、包 / 模块树、配置名、分支名，成本低时补热度图 | index 别名 + 一个粗粒度实体页 |
| `/ingest-deepen <object-or-page>` | 将已有粗粒度地图扩展为具体链路 / 模块 / 任务 | 先读已有 wiki 页，再读定向源码 | 模块 / 主题 / 任务 / runbook 页 |
| `/harness-locate <object-or-question>` | 低 token 定位方向 | `index.md`，再读一两个已链接页面 | 只给路由，不做大段解释 |

## 粗粒度地图字段

- 自然语言别名
- 真实仓库路径
- 当前分支和相关 feature 分支族
- 仓库 / 模块类型
- 启动入口或协议入口
- 顶层包 / 模块职责图
- 高价值源码入口
- 服务 / topic / RPC 粒度的外部依赖
- 已知活跃任务或 feature 分支
- 来源证据列表

## 细化字段

- 所属粗粒度页面
- 精确范围和非范围
- 源码入口
- 状态流转或调用链
- 分支 / 版本注意点
- 失败模式或测试场景
- 来源证据列表

## 必填字段

### 项目页

- 目标
- 范围
- 负责人
- 里程碑
- 风险
- 当前状态

### 产品页

- 问题陈述
- 目标用户
- 约束
- 决策点
- 相关功能

### 代码库页

- 仓库路径
- 启动入口
- 包结构
- 依赖栈
- 关键协议
- 高价值入口

## Raw 快照命名

对于 `codebase`，raw 快照放在 `raw/repos/<repo>/` 下，文件名带日期，例如：

- `YYYY-MM-DD-readme.md`
- `YYYY-MM-DD-pom-snapshot.md`
- `YYYY-MM-DD-package-tree.md`
- `YYYY-MM-DD-entrypoints.md`
- `YYYY-MM-DD-config-snapshot.md`
- `YYYY-MM-DD-doc-<topic>.md`
- `YYYY-MM-DD-git-heatmap.md`
- `YYYY-MM-DD-external-deps.md`
- `YYYY-MM-DD-structure-judgment.md`

## 接受 / 拒绝规则

- 只接受有助于定位、解释或操作来源的稳定事实。
- 拒绝临时聊天、重复笔记和推测性结论。
- 不能溯源的细节不要写入。
- 每个页面都必须能从 `index.md` 到达。
- raw 文件不得包含 wiki 层判断，只能包含证据和轻量观察。
- 不要让深层页面成为项目唯一入口；必须先把粗粒度路线加入 `index.md`。
