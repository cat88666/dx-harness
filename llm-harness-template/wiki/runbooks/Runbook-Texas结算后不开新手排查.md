# Runbook-Texas结算后不开新手排查

## 适用症状

- 这一手结算结束了，但牌桌迟迟不进入下一手
- `NextHandStartTask` 似乎发布了，但没有真正起新局
- 老 `handCode` 已结束，新 `handCode` 没生成

## 排查顺序

1. 确认 `BaseTableHandNextService.handle()` 是否发布 `NextHandStartTask`
2. 检查 `TABLE_NEXT_HAND_START_TASK_{tableId}` 是否存在或被消费
3. 检查 `NextHandStartTask.run()` 中是否命中了鱿鱼强制结算分支
4. 检查是否触发了 `NEXT_HAND_EXCEPTION` mock 异常
5. 检查 `HandGenerationUtils.generateHand(...)` 后 `TableCache` 是否写入了新 `handCode`
6. 检查末尾是否成功执行了 `new TableLoopTask(context).run()`

## 高概率原因

- 结算后又被鱿鱼逻辑拦住
- 下一手启动过程抛异常，随后回退到 `GameModelEnum.NEXT_HAND`
- 新 `handCode` 已生成，但 `EVENT_WAIT` 没有正确回写

## 关键源码

- `BaseTableHandNextService.handle`
- `NextHandStartTask.run`
- `TableLoopTask.run`

## 来源

- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/service/nexthand/BaseTableHandNextService.java`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/task/once/NextHandStartTask.java`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/task/loop/TableLoopTask.java`
