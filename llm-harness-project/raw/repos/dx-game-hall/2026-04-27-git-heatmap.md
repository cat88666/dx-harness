# dx-game-hall Git Heatmap

来源：`git -C /Users/mac/IdeaProjects/dx-game-hall log --since='6 months ago'`

## 总体统计

- 过去 6 个月提交总数：`1841`
- 作者数：`21`
- 最近一次提交时间：`2026-04-19 17:08:04 +0800`

## 顶层包提交热度

按 `src/main/java/com/dx/hall/` 下路径聚合：

1. `command` - `949`
2. `service` - `891`
3. `dto` - `212`
4. `rpc` - `201`
5. `consumer` - `195`
6. `cache` - `71`
7. `rocketmq` - `31`
8. `controller` - `31`
9. `notice` - `28`
10. `config` - `23`
11. `convert` - `18`
12. `schedule` - `16`
13. `enums` - `16`
14. `utils` - `10`
15. `interceptor` - `10`
16. `constant` - `8`

## Top 20 文件

1. `src/main/java/com/dx/hall/service/race/RaceInitService.java` - `123`
2. `src/main/java/com/dx/hall/service/race/RaceListService.java` - `97`
3. `src/main/java/com/dx/hall/command/raceDetail/RaceRuleDetailCommand.java` - `81`
4. `src/main/java/com/dx/hall/service/LoginTexasService.java` - `70`
5. `src/main/java/com/dx/hall/command/invitationSelect/InvitationSelectCommand.java` - `63`
6. `src/main/java/com/dx/hall/rpc/impl/HallRaceReEnterRpcServiceImpl.java` - `54`
7. `src/main/java/com/dx/hall/command/raceuserdetail/RaceUserDetailCommand.java` - `44`
8. `src/main/java/com/dx/hall/service/race/RaceReEnterService.java` - `41`
9. `src/main/java/com/dx/hall/service/race/RaceBizService.java` - `41`
10. `src/main/java/com/dx/hall/command/raceUserList/RaceUserListCommand.java` - `41`
11. `src/main/java/com/dx/hall/command/raceSignUp/RaceSignUpCommand.java` - `39`
12. `src/main/java/com/dx/hall/rpc/impl/RaceRpcServiceImpl.java` - `35`
13. `src/main/java/com/dx/hall/dto/race/RaceDetailDto.java` - `35`
14. `src/main/java/com/dx/hall/command/racereenter/RaceReEnterCommand.java` - `35`
15. `src/main/java/com/dx/hall/rpc/provider/HallRaceRankServiceImpl.java` - `33`
16. `src/main/java/com/dx/hall/command/userRaceList/handler/UserRaceListHandler.java` - `32`
17. `src/main/java/com/dx/hall/cache/UserBroadcastDataCache.java` - `32`
18. `src/main/java/com/dx/hall/rocketmq/provider/RocketMqProvider.java` - `31`
19. `src/main/java/com/dx/hall/service/UserOnlineStatusService.java` - `29`
20. `src/main/java/com/dx/hall/service/race/RaceRewardService.java` - `28`

## 死掉目录

过去 6 个月内未见提交痕迹、或提交极弱的顶层目录可先视为低热度：

- `constant`
- `interceptor`
- `utils`
- `schedule`
- `convert`
- `config`
- `notice`
- `rocketmq`

## 说明

这里的“热度”只反映 6 个月内的 git 改动频率，不等价于业务重要性。
