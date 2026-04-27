# 服务-dx-game-texas

## 定位

`dx-game-texas` 是德州业务实现仓，承接具体牌局状态、命令处理、通知广播、定时任务、结算和跨服务协作。

## 关键结构

- `command/`：用户动作与房间动作入口
- `service/`：业务处理和链路编排
- `notice/`：广播与用户通知
- `listener/`：牌局阶段事件监听
- `task/loop` 与 `task/once`：轮询任务和一次性任务
- `cache/` / `model/`：运行态数据与领域对象

## 关键判断

- 这是任务驱动型业务，不是单次请求型业务
- 排障时必须同时看 `service -> notice/listener -> task -> cache`
- 大量流程是“先发事件，再由事件继续推进牌局”

## 首批重点区域

- `GameStartService`
- `UserBetNotice`
- `HandRoundOverListener`
- `HandOverListener`
- `service/nexthand/`

## 来源

- `/Users/mac/IdeaProjects/dx-game-texas/pom.xml`
- `/Users/mac/IdeaProjects/dx-game-texas/README.md`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas`
