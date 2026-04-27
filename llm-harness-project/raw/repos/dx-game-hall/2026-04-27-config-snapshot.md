# dx-game-hall Config Snapshot

来源：
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/resources/application.yml`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/resources/bootstrap.yml`
- `/Users/mac/IdeaProjects/dx-game-hall/src/main/resources/env/*.properties`

## 关键配置

- `spring.application.name: dx-game-hall`
- `spring.main.allow-circular-references: true`
- `spring.main.allow-bean-definition-overriding: true`
- `spring.messages.basename: i18n/messages`
- Nacos discovery / config 使用同一套 `server-addr`、`namespace`、`username`、`password`
- `shared-configs` 里包含 `dz-common.yaml` 与 `dx-game-hall.yaml`

## 环境文件

- `dev.properties`
- `dev1.properties`
- `local.properties`
- `pre.properties`
- `prod.properties`
- `test.properties`
- `test1.properties`
- `test2.properties`
- `uat.properties`

## 观察

配置中心和环境文件齐全，说明该仓库不是单纯的样例工程。
