# Query Rules

## 目标

让 `query / locate / runbook` 三类操作输出稳定，不退化成随意聊天。

## `/query`

适用：

- “Texas 的下注超时是怎么推进的？”
- “dx-game-frame 和 dx-game-core 的线程分发差异是什么？”

要求：

1. 先找 `summaries/` 和 `synthesis/`
2. 再补 `entities/` 中的具体对象
3. 输出里必须给出至少一个可直达页面或源码对象

## `/locate`

适用：

- “定位 UserBetCountdownTask”
- “定位下一手开始链路”

要求：

1. 先命中 `entities/`
2. 再补相关 `runbooks/` 或 `summaries/`
3. 输出重点是“去哪看”，不是完整解释

## `/runbook`

适用：

- “玩家超时后没自动弃牌怎么查？”
- “结算完不开新手怎么查？”

要求：

1. 直接返回检查顺序
2. 必须包含高概率原因
3. 必须给出关键源码入口
