# 仓库-dx-game-texas

## 一句话定位

`dx-game-texas` 是德州扑克牌桌服务，承载德州游戏开始、结算、留座离桌、站起、钱包变更、鱿鱼和堆蘑菇等牌桌内核心逻辑。

## 基础事实

- 路径: `/Users/mac/IdeaProjects/dx-game-texas`
- 当前本地分支: `pre`
- 当前本地状态: 仅发现未跟踪 `.DS_Store` 与 `src/.DS_Store`
- 蘑菇开发分支族:
  - `feture-sun-16603`
  - `origin/16603-final`
  - `origin/duik-mushroom-temp-final`
  - `origin/merge-pre-feture-sun-16603-20260418`
- 需求关键词: 德州、德州扑克、Texas、蘑菇游戏、堆蘑菇、逃庄、留座离桌、结算后离桌、下一手庄位

## 当前蘑菇需求定位

当前“蘑菇游戏开发和蘑菇逃庄需求补充”不应定位到大厅服务。大厅只暴露 `stackMushroomSwitch` 等房间/牌桌展示配置；实际牌桌行为在 `dx-game-texas`。

关键源码入口:

- `src/main/java/com/dx/texas/command/userholdseat/UserHoldSeatCommand.java` — `TexasProto.USER_HOLD_SEAT` 留座离桌入口
- `src/main/java/com/dx/texas/command/userholdseat/UserHoldSeatHandler.java` — 留座离桌立即离开、结算后离开、限流和占座迁移
- `src/main/java/com/dx/texas/command/gamestart/handle/GameStartHandlerBase.java` — 开局检查、选庄、堆蘑菇调用
- `src/main/java/com/dx/texas/service/MushRoomGameService.java` — 蘑菇堆放、派彩、单人派奖、账变组装
- `src/main/java/com/dx/texas/model/v1/TableMushroom.java` — 牌桌蘑菇轮次状态
- `src/main/java/com/dx/texas/model/v1/UserItemMushroom.java` — 单个用户蘑菇轮次数据
- `src/main/java/com/dx/texas/service/FindUserService.java` — 下一手庄位、大小盲选择

## 分支差异提醒

`pre` 分支当前不包含完整蘑菇实现类；完整蘑菇对象在 `feture-sun-16603` / `origin/16603-final` 等分支可见。例如 `TableMushroom`、`UserItemMushroom`、`MushRoomGameService`、`MushroomRecordCommand` 等。

因此处理蘑菇相关需求时，必须先确认工作分支：

- 查当前线上 / 集成行为: 看 `pre`
- 查蘑菇需求实现: 看 `feture-sun-16603` 或 `origin/16603-final`
- 查逃庄补充是否已合入: 对比 `pre` 与蘑菇分支

## 来源

- `/Users/mac/IdeaProjects/dx-game-texas`
- `git branch --show-current` → `pre`
- `git branch --all --list '*mush*' '*16603*' '*pre*'`
- `git ls-tree -r --name-only feture-sun-16603`
- `git grep -n 'TableMushroom|UserItemMushroom|蘑菇|UserHoldSeat' feture-sun-16603 -- src/main/java`
