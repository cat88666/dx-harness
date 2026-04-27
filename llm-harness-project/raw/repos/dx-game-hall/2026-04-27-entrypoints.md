# dx-game-hall Entrypoints Snapshot

来源：
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/java/com/dx/hall/DxGameHallApplication.java`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/java/com/dx/hall/command`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/java/com/dx/hall/controller`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/java/com/dx/hall/service`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/java/com/dx/hall/rpc`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/java/com/dx/hall/consumer`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/java/com/dx/hall/schedule`

## 启动入口

- `com.dx.hall.DxGameHallApplication`

## 主要入口目录

- `command/`：大厅协议命令入口，含 `halllogin`、`hallmatch`、`roomlist`、`tablelist`、`raceList`、`raceSignUp`、`walletinfo` 等
- `controller/`：HTTP / 管理类入口，含 `hall`、`texas`、`mahjong`、`poker`、`race` 相关控制器
- `service/`：业务编排层，含 `HallRoomService`、`RoomInfoService`、`TableInfoService`、`LoginTexasService`、`Race*Service`
- `rpc/`：RPC 服务门面，含 `RpcServiceImpl`、`RaceRpcServiceImpl`、`HallRaceReEnterRpcServiceImpl`
- `consumer/`：MQ 消费入口，含 `HallBroadcastMessageNoticeConsumer`、`RaceStartNoticeConsumer` 等
- `schedule/`：定时任务入口，含房间、牌桌、俱乐部成员、排队相关任务
