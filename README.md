# DX Harness

> 把工程沉淀为 LLM 可执行的 Agent Runtime。模型决定能力上限，Harness 决定可用性。

DX Harness 是一套基于 **Karpathy LLM Wiki + Obsidian + Harness 编程**的工程知识系统，面向长期维护的复杂项目（如 4 年期、10+ 模块的产品级代码库），把分散的产品资料、代码材料和工程经验，编译为 AI 可检索、可注入、可执行的结构化记忆。

核心判断：**AI 编程的瓶颈不在模型，而在工程知识能否被结构化、被检索、被注入。** 给同一个模型不同的知识上下文，产出质量差异巨大；让 AI 不漂移的关键，不是更聪明的 prompt，而是更有结构的知识。

---

## 1. 解决三个工程问题

| 场景 | 没有 Harness | 有 Harness |
| --- | --- | --- |
| 拿到需求 → 开发 | AI 不知道影响哪些模块，自由发挥 | AI 先定位模块卡 → 出影响面 → 按 API 契约改 |
| 出现 BUG → 定位 | AI 在源码里大海捞针 | AI 沿双链回溯：现象 → 模块卡 → 依赖链 → 已知问题 |
| 模块迭代 | 改完代码,知识断层 | 模块卡是 SSOT,改代码前先反向更新卡片 |

---

## 2. 三层架构

```text
记忆层 (Karpathy Wiki)   — 知识沉淀：业务规则、模块归纳、排障经验
   ↓
视图层 (Obsidian)        — 实时查看与导航：双链、索引、模块定位
   ↓
执行层 (Harness)         — Agent Runtime：工具、上下文、权限、Loop
```

三层共享同一份 Markdown 源,各自独立运转：

- **记忆层（Wiki）** — 按 `raw/` / `wiki/` 分层、按类型分型,结论回链原始来源,变更落 log。
- **视图层（Obsidian）** — 用 `[[ ]]` 双链串联模块、概念、BUG。开发时左侧索引定位模块,右侧并排打开模块卡 + 关联排障卡。Obsidian 不是知识本身,是操作面板。
- **执行层（Harness）** — Agent Runtime 的最小完备闭环：

  ```text
  Agent = LLM + Harness

  Harness =
        Tools           (读写文件、搜索、执行、联网)
      + Agent Loop      (推理 → 工具调用 → 接收结果 → 继续推理)
      + Context Manager (历史压缩、近期保留、规则重注入)
      + Prompt System   (Control Plane: 工具策略、错误处理、安全边界)
      + Permission System
      + Hooks
  ```

  Prompt 在这里是 Control Plane,不是一次性指令——用来注入模块卡、约束工具策略、补丁模型缺陷。

---

## 3. 目录结构

```text
dx-harness/
├── AGENTS.md                   # Codex / Agent 协作规则
├── CLAUDE.md                   # Claude Code 协作规则
├── README.md
├── assets/                     # 共享图片资源
├── llm-harness-project/        # 当前活跃实例
│   ├── CLAUDE.md               # 实例路径配置
│   ├── index.md                # 全局索引(每次实质修改后同步)
│   ├── log.md                  # append-only 操作日志
│   ├── raw/                    # 只读原始资料
│   └── wiki/
│       ├── concepts/           # 抽象概念、业务规则、机制、方法
│       ├── entities/           # 人物、组织、工具、产品、模型
│       ├── modules/            # ★ 模块卡(一等公民)
│       ├── summaries/          # 跨模块主题聚合
│       └── synthesis/          # 对比、策略、排障 playbook
└── llm-harness-template/       # 可复用 Harness 模板
```

> `modules/` 与 `entities/` 分离是关键设计:模块的信息密度(依赖图、API 契约、已知 BUG、性能基线)远高于普通实体,混在一起会稀释 AI 检索时的上下文质量。

---

## 4. 知识类型与命名规范

| 类型目录 | 前缀 | 用途 | 示例 |
| --- | --- | --- | --- |
| `concepts/` | `概念-` | 抽象规则、算法、机制 | `概念-牌型比较.md` |
| `entities/` | `工具-` / `人物-` / `产品-` | 实体记录 | `工具-Redis.md` |
| `modules/` | `模块-` | 单个 module 卡 | `模块-下注引擎.md` |
| `summaries/` | `主题-` | 跨模块主题聚合 | `主题-性能基线.md` |
| `synthesis/` | `对比-` / `策略-` / `排障-` | 综合分析 | `排障-断线重连卡顿.md` |

### 4.1 模块卡固定模板（7 段必填）

```markdown
# 模块-<名称>

## 职责
<一句话定位>

## 依赖
- 上游: [[模块-A]] [[模块-B]]
- 下游: [[模块-C]]

## 关键路径
- 源码入口: <path/to/entry>
- 核心类: <ClassName>

## 对外 API
| 方法 | 入参 | 出参 | 契约 |
| --- | --- | --- | --- |

## 数据模型
<核心结构说明 / 链接 raw 中的 schema>

## 变更历史
- 2025-xx-xx: <变更摘要> → log.md#<anchor>

## 已知问题
- [[排障-xxx]]
```

**模块卡缺段不接收**——这是约束 AI 不漂移的核心机械手。

### 4.2 concepts 卡固定 6 段

一句话定义 / 第一性原理 / 核心机制 / 关键权衡 / 与其他概念的关系 / 应用边界。

---

## 5. 核心约束（防漂移机制）

控制 AI 编程漂移的本质,是约束 **写入路径** 与 **上下文边界**:

- `raw/` 只读,不修改、不移动、不重命名其中资料。
- `wiki/` 优先更新已有页,避免语义重复的新页。
- 任何 `wiki/` 实质修改 → 必须同步更新 `index.md` + 追加 `log.md`。
- 新页必须带类型前缀,否则拒收。
- 模块卡 7 段必须完整,不接收部分提交。
- **AI 生成代码前,必须先打开对应模块卡**(通过 Prompt 注入 / Hook 强制)。
- **代码改动前,先反向更新模块卡**——卡片漂移就是知识漂移。

---

## 6. 工作流

### 6.1 需求开发

1. 原始需求落 `raw/specs/<需求名>.md`。
2. AI 读需求 → 检索 `modules/` → 输出**影响面分析**(影响哪些模块卡 / API / 数据模型)。
3. 人确认影响面 → AI 按模块卡的 API 契约和数据模型生成补丁。
4. 提交后:更新被影响模块卡的"变更历史" + 追加 `log.md`。

### 6.2 BUG 定位

1. 现象先落 `wiki/synthesis/排障-<现象>.md`(初版只写现象 + 复现路径)。
2. AI 沿双链回溯:现象 → 涉及模块卡 → 依赖链 → 历史已知问题。
3. 定位根因后:
    - 根因落到对应**模块卡的"已知问题"**段。
    - 修复策略落到 `synthesis/排障-xxx.md` 的"修复方案"段。
4. 修复完成 → 追加 `log.md`。

### 6.3 模块演进

**改代码前先改模块卡。** 卡片是 SSOT(单一事实源),代码是卡片的实现。允许代码先动、卡片后补的项目,三个月后必然退化回"AI 不知道细节"的初始状态。

---

## 7. 协作入口

- Codex / Agent 协作规则:`AGENTS.md`
- Claude Code 协作规则:`CLAUDE.md`、`llm-harness-project/CLAUDE.md`
- 当前知识库导航:`llm-harness-project/index.md`
- 变更记录:`llm-harness-project/log.md`

---

## 8. 常用命令

```bash
# 列出所有 wiki 页
rg --files llm-harness-project/wiki

# 列出所有模块卡
rg --files llm-harness-project/wiki/modules

# 找所有双链(用于检查孤儿节点)
rg '\[\[.*\]\]' llm-harness-project/wiki

# 找未链接的模块卡(应为 0)
rg -L '\[\[模块-' llm-harness-project/wiki/modules

# 工程态检查
git status && git diff --stat
```

---

## 9. 一句话总结

> **Claude Harness = LLM 的操作系统 + 工具链 + 调度器。**  
> 没有 Harness,模型只是会说话;有 Harness,模型才能在 4 年的复杂工程里持续干活。