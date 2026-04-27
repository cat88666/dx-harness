# 主题-Texas牌局任务生命周期

## 主题结论

`dx-game-texas` 的主链路可以概括成：`TableLoopTask` 等待开局，`SendHandCardTask` 发手牌，`UserBetCountdownTask` 约束行动时限，`SendPublicCardTask` 推进圈层，`ProvisionalSettlementTask` 触发结算，`NextHandStartTask` 开始下一手。

## 主链路

1. `TableLoopTask` 轮询牌桌状态与等待逻辑
2. `GameStartService` 发布 `SendHandCardTask`
3. `UserBetNotice` 通知当前玩家下注，并发布 `UserBetCountdownTask`
4. `HandRoundOverListener` 在本圈平衡后发布 `SendPublicCardTask`
5. `HandOverListener` 在整手结束时发布 `ProvisionalSettlementTask`
6. `BaseTableHandNextService` 发布 `NextHandStartTask`

## 任务分层

- `loop`：常驻轮询，如牌桌等待、下注超时
- `once`：一次性推进节点，如发牌、公牌、结算、下一手

## 排障视角

- “卡在等待”看 `TableLoopTask`
- “玩家没行动就停住”看 `UserBetNotice` 和 `UserBetCountdownTask`
- “圈结束不发公牌”看 `HandRoundOverListener`
- “结算后不开新手”看 `BaseTableHandNextService` 和 `NextHandStartTask`

## 来源

- `/Users/mac/IdeaProjects/dx-game-texas/README.md`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/service/GameStartService.java`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/notice/UserBetNotice.java`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/listener/HandRoundOverListener.java`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/listener/HandOverListener.java`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/service/nexthand/BaseTableHandNextService.java`
