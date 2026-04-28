# 仓库-dx-game-texas

## 一句话定位

`dx-game-texas` 是德州扑克牌桌服务，承载德州房间内的入座、开局、下注、发牌、保险、结算、下一手推进、站起/退出、留座离桌、赛事桌、鱿鱼和堆蘑菇等牌桌内核心逻辑。

## 基础事实

- 路径: `/Users/mac/IdeaProjects/dx-game-texas`
- 仓库类型: 单 Maven module / Spring Boot 服务
- Maven 坐标: `com.dx:dx-game-texas:1.0-SNAPSHOT`
- parent: `com.dz:dz-parent:1.0.0-SNAPSHOT`
- Java 版本: 11
- 打包方式: `jar`
- 启动类: `com.dx.texas.DxGameTexasApplication`
- Spring 应用名: `dx-game-texas`
- 配置中心 / 服务发现: Nacos
- RPC: Dubbo
- 网关通信: NetBolt
- 消息: RocketMQ
- 缓存/分布式能力: Redis / Redisson / Guava 本地缓存
- 当前本地分支: `duik-mushroom-temp-final`
- 当前本地状态: 仅发现未跟踪 `.DS_Store` 与 `src/.DS_Store`
- 本次 map 不写 `raw/` 快照；来源直接指向真实仓库文件与 git 命令输出。

来源:
- `/Users/mac/IdeaProjects/dx-game-texas/pom.xml`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/DxGameTexasApplication.java`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/resources/application.yml`
- `/Users/mac/IdeaProjects/dx-game-texas/src/main/resources/bootstrap.yml`
- `git branch --show-current`

## 自然语言别名

- 德州
- 德州扑克
- Texas
- 德州牌桌
- 德州游戏
- 德州服务
- 蘑菇游戏 / 堆蘑菇 / 蘑菇逃庄
- 鱿鱼 / 鱿鱼模式
- 留座离桌 / 占座 / 站起 / 退出
- 赛事桌 / MTT / 比赛重进

## 当前活跃分支与任务信号

当前分支 `duik-mushroom-temp-final` 的最近提交集中在 `#SUN-46951`：

- `#SUN-46951-蘑菇逃庄-下一手庄位`
- `#SUN-46951-蘑菇逃庄-验证`
- `#SUN-46951-测试用例`
- 蘑菇相关历史提交包含单人蘑菇结算、showdown 圈盈亏展示、蘑菇记录、蘑菇逃庄等。

相关分支族:

- `duik-mushroom-temp-final`
- `origin/duik-mushroom-temp-final`
- `origin/duik-mushroom-temp`
- `feture-sun-16603`
- `origin/feture-sun-16603`
- `origin/16603-final`
- `origin/merge-pre-feture-sun-16603-20260418`
- `pre` / `origin/pre`

处理蘑菇需求时优先确认当前所在分支；当前本地已在 `duik-mushroom-temp-final`，不是 `pre`。

来源:
- `git log --oneline --decorate -15`
- `git branch --all --list '*mush*' '*16603*' '*pre*' '*duik*'`

## 顶层包职责地图

- `command/` — NetBolt 客户端协议入口，按协议拆分为入房、坐下、开局、下注、弃牌、保险、结算记录、留座离桌、站起、退出、房主操作、赛事、蘑菇记录、鱿鱼等命令。
- `service/` — 牌桌业务编排层，覆盖开局、选庄、发牌、下注、保险、结算、下一手、离桌、赛事、鱿鱼、蘑菇、回顾、补码、风控等。
- `model/`、`model/v1/` — 牌桌、手牌、玩家、蘑菇、鱿鱼等内存模型。
- `cache/` — 牌桌、玩家、配置、原始数据等运行时缓存入口。
- `notice/`、`notice/msg/` — 牌桌广播、玩家通知和协议消息 DTO。
- `task/`、`frame/context/` — 一次性任务、循环任务和任务上下文，如发牌、下注倒计时、结算、下一手、留座离桌超时。
- `rocketmq/consumer/`、`rocketmq/provider/` — MQ 消费和生产入口。
- `rpc/`、`rpc/texas/` — 对外暴露或调用的 Dubbo/RPC 门面。
- `listener/`、`event/` — Spring 事件监听和动作完成后的异步链路。
- `recover/` — 牌桌恢复、异常恢复和数据处理。
- `controller/` — HTTP/管理/调试入口，当前主要看到 `UpdateCardController`。
- `schedule/`、`monitor/` — 定时任务和监控入口。
- `config/`、`constant/`、`enums/`、`convert/`、`dto/`、`utils/` — 配置、常量、枚举、转换、DTO 和工具层。

来源:
- `find /Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas -maxdepth 2 -type d`

## 高价值协议入口

常用 `RequestCommand` 入口:

- 入房 / 坐下 / 退出:
  - `command/enterroom/EnterRoomCommand.java`
  - `command/usersitdown/UserSitDownCommand.java`
  - `command/userstand/UserStandCommand.java`
  - `command/userquit/UserQuitCommand.java`
  - `command/userholdseat/UserHoldSeatCommand.java`
  - `command/userback/UserBackCommand.java`
- 开局 / 牌局动作:
  - `command/gamestart/GameStartCommand.java`
  - `command/userbet/UserBetCommand.java`
  - `command/userfoldcard/UserFoldCommand.java`
  - `command/usershowdown/UserShowdownCommand.java`
  - `command/usercheckpubliccard/UserCheckPublicCardCommand.java`
- 保险 / 延迟:
  - `command/buyinsure/BuyInsureCommand.java`
  - `command/buysmartinsure/`
  - `command/delaybet/DelayBetCommand.java`
  - `command/delaybuyinsure/DelayBuyInsureCommand.java`
- 牌桌管理:
  - `command/disband/DisbandCommand.java`
  - `command/homeownerhandler/HomeownerHandlerCommand.java`
  - `command/specifyStand/SpecifyStandCommand.java`
  - `command/specifyKick/SpecifyKickCommand.java`
  - `command/hallChangeTable/HallChangeTableCommand.java`
- 鱿鱼 / 蘑菇:
  - `command/squidjoin/SquidJoinCommand.java`
  - `command/squidrecord/SquidRecordCommand.java`
  - `command/squidwallet/UserSquidWalletCommand.java`
  - `command/mushroomRecord/MushroomRecordCommand.java`
- 赛事:
  - `command/racereenter/RaceReEnterCommand.java`
  - `command/pullrace/PullRaceCommand.java`
  - `command/pullracestandcheck/PullRaceStandCheckCommand.java`

来源:
- `find /Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/command -maxdepth 2 -name '*Command.java'`

## 高价值服务入口

- 开局 / 选庄 / 盲注:
  - `service/GameStartService.java`
  - `command/gamestart/handle/GameStartHandlerBase.java`
  - `service/FindUserService.java`
  - `service/ButtonBlindGameStartService.java`
  - `service/CollectPoolGameStartService.java`
- 手牌推进 / 结算:
  - `service/ProvisionalSettlementService.java`
  - `service/SettlementService.java`
  - `service/SettlementAfterService.java`
  - `service/SettlementRecordService.java`
  - `service/nexthand/BaseTableHandNextService.java`
  - `task/once/NextHandStartTask.java`
- 玩家离桌 / 占座:
  - `service/LeaveService.java`
  - `command/userholdseat/UserHoldSeatCommand.java`
  - `command/userholdseat/UserHoldSeatHandler.java`
  - `service/quit/UserQuitService.java`
  - `service/occpuy/UserOccupyService.java`
  - `task/once/UserLeaveTask.java`
  - `task/once/OccupyTimeOutTask.java`
- 蘑菇:
  - `service/MushRoomGameService.java`
  - `service/MushroomNextButtonService.java`
  - `model/v1/TableMushroom.java`
  - `model/v1/UserItemMushroom.java`
  - `command/mushroomRecord/MushroomRecordCommand.java`
- 鱿鱼:
  - `service/TableSquidService.java`
  - `service/SquidGameStartService.java`
  - `service/SquidSettlementService.java`
  - `service/SquidSettlementAfterService.java`
  - `service/ProvisionalSquidSettlementService.java`
- 赛事 / MTT:
  - `service/RaceMTTService.java`
  - `service/RaceMTTChangeTableService.java`
  - `service/RaceMTTDateService.java`
  - `service/RaceMTTReEnterService.java`
  - `service/RaceTableInitService.java`
  - `service/nexthand/RaceTableHandNextService.java`
- 保险 / 看牌 / 回顾:
  - `service/UserInsureService.java`
  - `service/ViewHandCardService.java`
  - `service/ViewHandCardCheckService.java`
  - `service/GameReviewService.java`
  - `service/CardReviewReplayService.java`
- 钱包 / 带入带出 / 审核:
  - `service/TransferService.java`
  - `service/TransferAuditService.java`
  - `service/UserBringOutService.java`

来源:
- `find /Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/service -maxdepth 2 -name '*Service.java'`

## 任务与状态推进入口

README 中已列出核心任务：

- `task/loop/TableLoopTask.java` — 游戏等待开始、房间解散，维度 `table`
- `task/once/SendHandCardTask.java` — 发手牌
- `task/loop/UserBetCountdownTask.java` — 用户下注超时倒计时
- `task/once/SendPublicCardTask.java` — 发送公牌
- `task/once/ProvisionalSettlementTask.java` — 触发结算条件后的临时结算
- `task/once/NextHandStartTask.java` — 结算完成后的下一手开始
- `task/once/OccupyTimeOutTask.java` — 占座超时处理
- `task/once/UserLeaveTask.java` — 留座离桌超时强制站起

源码中还可见：

- `task/once/SettlementTask.java`
- `task/once/SquidSettlementTask.java`
- `task/once/FillPublicCardTask.java`
- `task/once/OccupyToSitDownTask.java`
- `task/loop/UserInsureCountdownTask.java`
- `task/loop/UserSmartInsureCountdownTask.java`

来源:
- `/Users/mac/IdeaProjects/dx-game-texas/README.md`
- `find /Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/task -maxdepth 2 -name '*Task.java'`

## RPC 与 MQ 入口

RPC 入口候选:

- 对内/外 RPC 门面:
  - `rpc/GameTableDetailRpcServiceImpl.java`
  - `rpc/DxGameTrackRpcServiceImpl.java`
  - `rpc/texas/GameTexasTableDetailRpcServiceImpl.java`
  - `rpc/texas/GameReviewRpcServiceImpl.java`
  - `rpc/texas/TexasInsuranceRpcServiceImpl.java`
  - `rpc/texas/TexasUpdateCardRpcServiceImpl.java`
  - `rpc/texas/TexasMockExceptionRpcServiceImpl.java`
  - `rpc/texas/TableUpgradeRpcServiceImpl.java`
  - `rpc/texas/EventRetryServiceRpcImpl.java`
- 上游依赖门面:
  - `DxGameAccountRpcServiceInter`
  - `DxTableInfoRpcServiceInter`
  - `GameHallMatchRpcServiceInter`
  - `RaceRpcServiceInter`
  - `WalletOperatorRpcService`
  - `HallRoomRpcService`
  - `GameReviewHandRpcServiceInter`

主要 MQ consumer:

- 配置 / 基础数据: `GlobalConfigChangeConsumer`、`GlobalDataChangeConsumer`、`UserInfoChangeConsumer`、`MerchantChangeConsumer`、`ClubChangeConsumer`
- 牌桌维护 / 解散 / 风控: `TableMaintainConsumer`、`DisbandMqConsumer`、`ProxyLockUserKickerConsumer`
- 赛事: `TexasRaceInitTableRpcServiceConsumer`、`RaceStatusAggConsumer`、`RaceUpBlindConsumer`、`RaceCommonUpdateConsumer`
- 牌桌跨节点 / 审核: `CrossNodeNoticeConsumer`、`TableTransferAuditConsumer`
- 机器人 / 游客 / 商城: `RobotRoomEndConsumer`、`TouristConfigConsumer`、`UserMallGoodsConsumer`

来源:
- `find /Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/rpc -maxdepth 2 -name '*.java'`
- `find /Users/mac/IdeaProjects/dx-game-texas/src/main/java/com/dx/texas/rocketmq/consumer -maxdepth 1 -name '*.java'`
- `rg -n '@RocketMQMessageListener|topic =|selectorExpression' .../rocketmq/consumer`

## 配置入口

- `src/main/resources/application.yml` — `spring.application.name = dx-game-texas`
- `src/main/resources/bootstrap.yml` — Nacos discovery/config 配置，依赖 `${spring.cloud.nacos.discovery.*}`
- `src/main/resources/env/` — `dev`、`dev1`、`local`、`pre`、`prod`、`test`、`test1`、`test2`、`uat` 环境参数
- `src/main/resources/spy.properties` — 运行时探针/监控相关配置候选

来源:
- `find /Users/mac/IdeaProjects/dx-game-texas/src/main/resources -maxdepth 2 -type f`
- `rg -n 'spring.application.name|spring.cloud.nacos|nacos' .../application.yml .../bootstrap.yml .../env/pre.properties`

## 改动热度

近 6 个月 Top 热点文件:

1. `service/RaceMTTService.java` — 125
2. `command/gamestart/handle/RaceGameStartHandler.java` — 117
3. `service/RaceMTTChangeTableService.java` — 87
4. `service/TransferService.java` — 78
5. `command/enterroom/EnterRoomCommand.java` — 71
6. `service/SettlementRecordService.java` — 63
7. `service/MushRoomGameService.java` — 59
8. `command/usersitdown/handle/SitDownHandlerBase.java` — 59
9. `listener/UserRaceCompleteActionListener.java` — 58
10. `convert/TexasTableConvert.java` — 58

判断:

- 赛事 / MTT、开局、转入、入房、结算记录、蘑菇是当前高改动区域。
- 蘑菇开发已进入活跃分支，`MushRoomGameService` 位列近 6 个月热点文件。

来源:
- `git log --since='6 months ago' --name-only --pretty=format: -- src/main/java`

## 后续可 `/ingest-deepen` 的对象

- `主题-德州开局与下一手推进链路`
- `主题-德州留座离桌与占座链路`
- `主题-德州蘑菇逃庄留座离桌链路`（已有，可继续细化实现与测试）
- `主题-德州结算与账变链路`
- `主题-德州赛事MTT重进与合桌链路`
- `模块-德州任务调度`
- `模块-德州MQ消费者`
- `Runbook-德州牌桌卡结算排查`
- `Runbook-德州玩家无法站起或离桌排查`

## 已知不确定点

- 本页是 `/ingest-map` 粗粒度地图，不展开具体业务状态机。
- 当前本地分支是 `duik-mushroom-temp-final`；若切回 `pre`，蘑菇相关类和提交状态可能不同。
- 本次未写 `raw/` 快照，因为当前仓库规则要求 `raw/` 作为只读输入层。
