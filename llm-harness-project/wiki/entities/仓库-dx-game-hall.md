# 仓库-dx-game-hall

## 1. 一句话定位
24 微服务体系中的大厅入口与赛事接入服务，承接大厅登录、房间/牌桌、比赛、报名、重进、用户状态与广播入口。[推断]

## 2. 基础事实
- 路径: `/Users/mac/IdeaProjects/dx-game-hall`
- 仓库类型: `单 Maven module`
- parent pom / 共享 BOM: `com.dz:dz-parent:1.0.0-SNAPSHOT`
- Java 版本: `11`
- 启动类: `com.dx.hall.DxGameHallApplication`
- 服务名 (Nacos): `dx-game-hall`
- 部署形态: `独立 Jar 部署` [推断]
- 来源:
  - `raw/repos/dx-game-hall/2026-04-27-pom-snapshot.md`
  - `raw/repos/dx-game-hall/2026-04-27-config-snapshot.md`
  - `raw/repos/dx-game-hall/2026-04-27-structure-judgment.md`

## 3. 顶层包结构(职责 + 入口)
- `cache` — 用户广播、状态等缓存入口 — `UserBroadcastDataCache`
- `command` — 大厅协议命令入口 — `HallLoginCommand`、`RaceSignUpCommand`、`RaceReEnterCommand`
- `config` — 应用与中间件装配入口 — `[缺]`
- `constant` — 常量定义 — `[缺]`
- `consumer` — MQ 消费入口 — `HallBroadcastMessageNoticeConsumer`、`RaceStartNoticeConsumer`
- `controller` — HTTP / 管理入口 — `HallController`、`TexasController`、`MahjongController`、`PokerController`、`RaceController`
- `convert` — DTO / VO 转换 — `[缺]`
- `dto` — 数据传输对象 — `RaceDetailDto`
- `enums` — 枚举定义 — `[缺]`
- `interceptor` — 请求拦截 / 鉴权入口 — `[缺]`
- `notice` — 通知消息封装 — `[缺]`
- `rocketmq` — MQ 生产与封装入口 — `RocketMqProvider`
- `rpc` — RPC 门面与实现入口 — `RpcServiceImpl`、`RaceRpcServiceImpl`、`HallRaceReEnterRpcServiceImpl`
- `schedule` — 定时任务入口 — `[缺]`
- `service` — 业务编排入口 — `HallRoomService`、`RoomInfoService`、`TableInfoService`、`LoginTexasService`、`Race*Service`
- `utils` — 通用工具 — `[缺]`

来源:
- `raw/repos/dx-game-hall/2026-04-27-package-tree.md`
- `raw/repos/dx-game-hall/2026-04-27-entrypoints.md`

## 4. 对外依赖(上游)
- RPC 调用的其他服务:
  - `dx-common-facades` 侧：`MemberRPCService`、`PlayerConfigRpcService`、`IDxGameConfigService`、`ClubTableWhiteListRpcService`、`IDxTableInfoService`、`WalletRPCService`、`HallRoomRpcService`、`GameRecommendationRpcService`、`BroadcastIntegratedRpcService`、`MerchantRpcService` 等 [推断]
  - `dx-game-frame-rpc-provider` 侧：`ITexasRaceInitTableRpcService`、`IDxGamePersonalInfoQueryRpcService`、`RaceInfoRpcService`、`RaceProcessRpcService`、`RaceQueryRpcService`、`OnlineMemberRpcService`、`IGameTableDetailService`、`HandPlayersRpcService`、`TableDetailRpcService`、`GameReviewRpcService` 等 [推断]
  - `dx-common-game-api` 侧：`ITexasInsuranceRpcService`、`ITexasMockExceptionRpcService`、`ITexasUpdateCardRpcService`、`IPokerIntelligentCardRpcService`、`IPokerUpdateCardRpcService`、`IPokerMockExceptionRpcService` 等 [推断]
- 直接共享依赖: `dx-game-frame-proto`、`dx-game-frame-rpc-provider`、`dx-game-frame-repository`、`dx-common-facades`
- 业务共享依赖: `dz-game-biz`、`dz-game-core`、`dz-game-common`、`dz-common-api`
- 监听的 MQ topic:
  - `dx-game-texas-table-change-topic`
  - `dx_texas_topic`
  - `hall_server_topic`
  - `dx-global-config-change-topic`
  - `bw_club_info_topic`
  - `bw_merchant_topic`
  - `proxy-lock-player-topic`
  - `proxy_mttstatus_venues_list_info_topic`
  - `dx_account_table_fee_change_topic`
  - `dx_game_shutdown_maintenance_topic`
  - `dx_game_player_upload_logs_topic`
  - `dx_game_bring_in_review_topic`
  - `dx_snake_app_version`
- producer 是谁:
  - `RocketMqProvider`
  - `UserLoginRecordService`
  - `UserDailyActiveService`
  - `BringInReviewService`
  - `HallUploadAppLogCommand`
- 依赖的 Redis key 前缀 / DB schema:
  - `noAcceptByCurrentDayCacheKey_YYYYMMDD`
  - `hall:invitationLimitCache`
  - `wallet_change_userId:%s_walletType:%s`
  - `GameFrameRedisKeyEnum.INVITATION_SUCCESS_KEY` [推断]
  - DB / Mapper 证据在 raw 中未扫出 [实测无]

来源:
- `raw/repos/dx-game-hall/2026-04-27-external-deps.md`
- `raw/repos/dx-game-hall/2026-04-27-pom-snapshot.md`

## 5. 对外暴露(下游)
- 自己暴露的 RPC 接口:
  - `HallMatchRpcService`
  - `HallBringInReviewRpcService`
  - `HallTableUpgradeRetryRpcService`
  - `UserOnlineInfoService`
  - `GameTableDetailRpcService`
  - `HallRaceUserRankRpcService`
  - `OnlineMemberRpcService`
- 自己 produce 的 MQ topic:
  - `dx_user_login_hall_info_topic:dx_user_login_hall_info_tag`
  - `dx_game_player_upload_logs_topic:dx_player_logs_upload_success_tag`
  - `dx_texas_race_over_topic:dx_game_texas_race_over_confirm_tag`
  - `dz_user_vister_record_topic:dz_user_vister_record_tag`
  - `dx_robot_race_add_robot_topic:dx_robot_race_add_robot_tag`
  - `hall_server_topic:dx_hall_invitation_tag`
  - `dx_hall_line_up_success_topic:dx_hall_line_up_success_tag`
  - `dx_game_bring_in_review_topic:dx_game_bring_in_review_tag`
  - `DX_TEXAS_RACE_TABLE_INIT_TOPIC:DX_GAME_TEXAS_RACE_TABLE_INIT_TAG` [实测无]
- HTTP / WS 端点:
  - `/online/race/list`
  - `/online/race/raceRuleDetail`
  - `/online/race/raceUserList`
  - `/online/race/raceUserSignUpList`
  - `/online/race/raceTableList`
  - `/online/roomList/info`
  - `/online/maintenance/list`
  - `/test/lineup/waitAndOnlineNum`
  - `/texas/insurance/insuranceMock`
  - `/texas/exception/addMockException`
  - `/texas/updateCard/updateCards`、`/texas/updateCard/updateNextCards`、`/texas/updateCard/updateHandCards`、`/texas/updateCard/getTableUser`
  - `/guandan/exception/addMockException`
  - `/guandan/updateCard/getTableUser`、`/guandan/updateCard/updatePlayerCards`
  - `/mahjong/exception/addMockException`
  - `/mahjong/updateCard/checkReady`、`/mahjong/updateCard/checkWinType`、`/mahjong/updateCard/updatePlayerCards`、`/mahjong/updateCard/restart`、`/mahjong/updateCard/getTableUser`
  - `/poker/exception/addMockException`
  - `/poker/updateCard/intelligentCards`、`/poker/updateCard/compareHand`、`/poker/updateCard/updatePlayerCards`、`/poker/updateCard/getTableUser`
- 其他可见入口:
  - `HallUploadAppLogCommand` -> `HallProto.HALL_UPLOAD_APP_LOG`
  - `InvitationSelectCommand` -> `HallProto.HALL_INVITATION_SELECT_LIST`
  - `ClientInfoCommand` -> `HallProto.HALL_CLIENT_INFO`

来源:
- `raw/repos/dx-game-hall/2026-04-27-external-deps.md`
- `raw/repos/dx-game-hall/2026-04-27-entrypoints.md`

## 6. 改动热度(过去 6 个月)
- 总提交数: `1841`
- 活跃作者数: `21`
- 最近一次提交: `2026-04-19 17:08:04 +0800`
- Top 5 改动最频繁的包:
  1. `command` — `949`
  2. `service` — `891`
  3. `dto` — `212`
  4. `rpc` — `201`
  5. `consumer` — `195`
- Top 5 改动最频繁的具体文件:
  1. `src/main/java/com/dx/hall/service/race/RaceInitService.java` — `123`
  2. `src/main/java/com/dx/hall/service/race/RaceListService.java` — `97`
  3. `src/main/java/com/dx/hall/command/raceDetail/RaceRuleDetailCommand.java` — `81`
  4. `src/main/java/com/dx/hall/service/LoginTexasService.java` — `70`
  5. `src/main/java/com/dx/hall/command/invitationSelect/InvitationSelectCommand.java` — `63`
- 6 个月零提交的死目录: `constant`、`interceptor`、`utils`、`schedule`、`convert`、`config`、`notice`、`rocketmq`

来源:
- `raw/repos/dx-game-hall/2026-04-27-git-heatmap.md`

## 7. 关键链路(初步识别,不展开)
- 赛事初始化链路 — `RaceInitService` 121 — 已在 Top 5 [推断]
- 赛事列表 / 规则详情链路 — `RaceListService` 97 + `RaceRuleDetailCommand` 81 — 已在 Top 5 [推断]
- 大厅登录链路 — `LoginTexasService` 64 — 已在 Top 5 [推断]
- 邀请选择链路 — `InvitationSelectCommand` 62 — 已在 Top 5 [推断]
- 报名 / 重进链路 — `RaceSignUpCommand` 34 + `RaceReEnterService` 40 — 未进 Top 5 [推断]
- 房间 / 牌桌查询链路 — `TableListCommand` 9 + `HallRoomService` 4 + `RoomListCommandV2Handler` 1 — 未进 Top 5 [推断]
- 广播 / 在线状态链路 — `HallBroadcastMessageNoticeConsumer` 24 + `UserOnlineService` 18 — 未进 Top 5 [推断]

## 8. 已知不确定点
- `RPC 调用的其他服务` 未从 raw 中抽出具体对象名 `[缺]`
- `监听的 MQ topic` 与 `producer` 身份未抽出 `[缺]`
- `Redis key 前缀 / DB schema` 未抽出 `[缺]`
- `HTTP / WS 端点` 未抽出 `[缺]`
- `config`、`constant`、`convert`、`enums`、`interceptor`、`notice`、`schedule`、`utils` 的关键入口类未抽出 `[缺]`
- `自己暴露的 RPC 接口` 的注解归属与方法级签名仅作类级反推 `[推断]`
- `独立 Jar 部署` 由单模块 Spring Boot 构建形态反推 `[推断]`
- `属于德州扑克项目 24 微服务之一` 由结构判断快照反向印证 `[推断]`

## 9. 后续待办
- 待建模块页候选:
  - 赛事初始化
  - 赛事列表 / 规则详情
  - 大厅登录
  - 邀请选择
  - 报名 / 重进
  - 房间 / 牌桌查询
  - 广播 / 在线状态
- runbook 候选必须基于 `raw/incidents/` 或 `raw/tickets/` 真实事故，目前不登记
