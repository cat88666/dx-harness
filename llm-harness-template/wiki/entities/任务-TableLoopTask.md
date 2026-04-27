# 任务-TableLoopTask

## 定位

`TableLoopTask` 是德州牌桌的常驻轮询任务，负责等待开局、解散检测、在线状态刷新、异常监控、风控检查和版本维护类逻辑。

## 触发方式

- 事件键：`TABLE_TASK_{tableId}`
- 来源：玩家进入房间后建立轮询；下一手开始时也会立即执行一次
- 类型：`LoopEventTypeEnum.TABLE_TASK`

## 主要职责

- 牌桌解散与到时处理
- 用户在线状态维护
- 卡死和异常牌桌监控
- 风控定时检查
- 比赛换桌与维护逻辑
- 在 `EVENT_WAIT` 状态下发送房间等待通知

## 排障提示

- 若牌桌“卡在等待态”，优先看 `tableHand.getEvent()` 是否一直停留在 `EVENT_WAIT`
- 若任务消失，检查 `TableCache.getTable(tableId)` 是否为空，任务会主动移除自身

## 来源

- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/task/loop/TableLoopTask.java`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/task/enums/LoopEventTypeEnum.java`
