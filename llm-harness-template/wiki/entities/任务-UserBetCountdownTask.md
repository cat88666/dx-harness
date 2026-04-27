# 任务-UserBetCountdownTask

## 定位

`UserBetCountdownTask` 是当前行动玩家的下注超时轮询任务，用来在超时后触发系统代操作，并推动牌局继续前进。

## 触发方式

- 事件键模式：`USER_BET_COUNT_DOWN_TASK_{tableId}_UID_{userId}`
- 由 `UserBetNotice.handleNotice()` 在通知下注后发布
- 实际初始延迟为 `betTotalMillisTime + 200ms`

## 核心行为

- 先校验当前手牌、当前用户、当前状态是否仍有效
- 到时后调用 `userBetService.systemHandle()` 执行系统 check/fold
- 再触发 `BET_TIME_OUT` 模型处理
- 成功后停止自己的轮询任务

## 风险点

- 托管玩家会被直接视为超时
- 任何异常都会进入 `stopTask`，所以“任务不见了”不一定代表业务正常结束
- 手动 Mock 的一般异常会主动抛错并停任务

## 来源

- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/task/loop/UserBetCountdownTask.java`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/notice/UserBetNotice.java`
