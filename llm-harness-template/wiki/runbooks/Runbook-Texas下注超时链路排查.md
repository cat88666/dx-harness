# Runbook-Texas下注超时链路排查

## 适用症状

- 玩家界面已收到下注提示，但服务端没有继续推进
- 玩家超时后没有自动 check/fold
- 下注倒计时任务看起来被创建了，但没有生效

## 排查顺序

1. 确认 `UserBetNotice.handleNotice()` 是否执行到发布 `UserBetCountdownTask`
2. 确认当前事件键是否已生成：`USER_BET_COUNT_DOWN_TASK_{tableId}_UID_{userId}`
3. 检查 `tableHand.getCurrentUserBetInfo()` 是否包含 `betStartTime` 和 `betTotalMillisTime`
4. 检查 `userBetService.betTaskCheck()` 是否提前返回
5. 检查玩家是否已被设置为托管，托管会直接进入超时逻辑
6. 检查异常日志里是否走到了 `stopTask(..., \"下注倒计时error\")`

## 高概率原因

- 当前手牌或当前用户上下文已失效
- 下注通知发出后，牌局已提前结束或换圈
- 计时参数为空，导致超时判断始终不成立
- 任务执行异常后被主动停掉

## 关键源码

- `UserBetNotice.handleNotice`
- `UserBetCountdownTask.run`
- `UserBetCountdownTask.checkUserBetCountDownTimeIsTimeOut`

## 来源

- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/notice/UserBetNotice.java`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/task/loop/UserBetCountdownTask.java`
