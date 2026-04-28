# Prompt-Ingest-Repo

用于 `/ingest-repo <repo>` 与 `/ingest-map <repo>`。

## 输入

- 真实仓库路径
- 用户给出的自然语言项目名或别名
- 可选：本次关注的链路、模块、问题或任务

## 执行顺序

1. 读取仓库 `README`、`pom.xml`、启动类、配置目录和顶层包结构
2. 判断仓库类型：服务、模块库、框架库、工具库、前端或脚本仓
3. 生成或更新 `entities/仓库-<repo>.md` 或 `entities/服务-<service>.md`
4. 补齐 `index.md` 的自然语言别名、真实路径、当前分支、重要 feature 分支族
5. 更新 `index.md` 的自然语言定位入口
6. 追加 `log.md`

## 粗粒度边界

`/ingest-map` 只回答“这是什么、去哪看、哪些入口最可能相关”。不要展开完整业务链路。

必须捕获：

- 自然语言别名
- 真实仓库路径
- 当前分支和活跃 feature 分支
- 顶层模块 / 包职责
- 启动类、协议入口、Controller、RPC、MQ、Schedule 等粗入口
- 最高价值源码入口
- 后续可 `/ingest-deepen` 的候选对象

## 禁止

- 一次性全量导入所有类
- 没有来源就写结论
- 把临时观察写成事故结论
- 把规则文档写入 `wiki/`
