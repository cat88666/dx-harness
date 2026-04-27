# 服务-dx-game-hall

## 定位

`dx-game-hall` 是比赛大厅 / 游戏大厅服务，工作目录位于：

`/Users/mac/IdeaProjects/dx-game-hall`

它不是前端大厅，也不是通用大厅匹配框架；它是一个 Spring Boot + Dubbo + Nacos + NetBolt 的后端服务，负责大厅登录、房间列表、牌桌列表、比赛列表、比赛报名、用户状态、钱包信息、广播通知、排队等大厅侧入口能力。

## 快速识别

| 项 | 信息 |
|---|---|
| 仓库名 | `dx-game-hall` |
| Maven artifactId | `dz-game-hall` |
| Spring 应用名 | `dx-game-hall` |
| 主包名 | `com.dx.hall` |
| 启动类 | `com.dx.hall.DxGameHallApplication` |
| Java 版本 | 11 |
| 配置中心 | Nacos |
| RPC | Dubbo |
| 网关通信 | NetBolt |
| 消息 | RocketMQ |
| 缓存/锁 | Redis / Redisson |

## 架构入口

- `DxGameHallApplication`：服务启动入口，开启 `@EnableDiscoveryClient`、`@EnableDubbo`，扫描 `com.dx` 和 `com.dz`。
- `command/`：客户端大厅协议命令入口，覆盖 `halllogin`、`hallmatch`、`roomlist`、`tablelist`、`raceList`、`raceSignUp`、`walletinfo`、`userinfo` 等。
- `controller/`：HTTP / 管理类接口入口，包含比赛列表、比赛详情、房间列表、维护接口，以及 Texas / Mahjong / Guandan / Poker 调试与管理接口。
- `service/`：业务编排层，核心包括 `HallRoomService`、`RoomInfoService`、`TableInfoService`、`RaceTableService`、`LoginTexasService`、`GameRecommendService`、`UserOnlineService`。
- `cache/`：大厅侧本地缓存，包含大厅房间、牌桌、比赛规则、用户登录、广播、版本配置等缓存。
- `consumer/`：MQ 事件消费入口，处理配置变更、俱乐部变更、钱包变更、广播、邀请、牌桌变化、用户状态变化等事件。
- `rpc/`：对外或内部 RPC 门面，包含 `GameHallMatchRpcService`、`HallBroadcastRpcService`、`RaceRpcService`。
- `schedule/`：定时刷新入口，包含房间、牌桌、俱乐部成员、排队任务等。

## 关键依赖

`dx-game-hall` 依赖三类能力：

- 游戏框架层：`dx-game-frame-proto`、`dx-game-frame-rpc-provider`、`dx-game-frame-repository`
- 业务核心层：`dz-game-biz`、`dz-game-core`、`dx-common-facades`
- 基础设施层：Dubbo、Nacos、RocketMQ、Redisson、NetBolt、MyBatis-Plus、Log4j2

这说明大厅服务本身不应承载底层匹配 Redis 细节；大厅匹配与牌桌人数等底层状态主要通过 `dx-game-frame-repository` 中的大厅匹配服务访问。

## 大厅相关核心目录

```text
src/main/java/com/dx/hall/
├── command/      # 客户端协议命令入口
├── controller/   # HTTP / 管理接口
├── service/      # 大厅业务编排
├── cache/        # 本地缓存
├── consumer/     # MQ 消费
├── rpc/          # RPC 门面
├── schedule/     # 定时任务
├── config/       # Dubbo / NetBolt / Redisson / 线程配置
└── dto/          # 大厅返回与中间 DTO
```

## 典型问题定位

- 查大厅登录：先看 `command/halllogin/`，再看 `LoginTexasService`。
- 查大厅匹配：先看 `command/hallmatch/`，再看 `service/match/`，再追 `dx-game-frame-repository` 的 `HallMatch*Service`。
- 查房间列表：先看 `command/roomlist/`、`RoomListV2Controller`、`HallRoomService`。
- 查牌桌列表：先看 `command/tablelist/`、`TableListQueryService`、`TableInfoService`。
- 查比赛列表 / 报名：先看 `command/raceList/`、`command/raceSignUp/`、`service/race/`。
- 查人数刷新：先看 `schedule/RoomInfoSchedule`、`schedule/TableInfoSchedule`、`HallDataCache`。
- 查广播通知：先看 `notice/`、`HallBroadcastService`、`consumer/HallBroadcastMessageNoticeConsumer`。

## 来源

- `/Users/mac/IdeaProjects/dx-game-hall/pom.xml`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/java/com/dx/hall/DxGameHallApplication.java`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/resources/application.yml`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/resources/bootstrap.yml`
- `/Users/mac/IdeaProjects/dx-game-hall/doc/大厅.md`
