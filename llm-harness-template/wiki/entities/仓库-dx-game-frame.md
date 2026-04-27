# 仓库-dx-game-frame

## 定位

`dx-game-frame` 是德州等游戏服务的通用框架层，负责把命令、事件、RPC、Repository、Socket、通用业务骨架拆成多模块，并给具体游戏仓复用。

## 模块地图

- `dx-game-frame-common`：线程、事件、公共工具
- `dx-game-frame-cmd`：命令入口层
- `dx-game-frame-service-core`：默认业务实现骨架
- `dx-game-frame-socket`：业务插口，供具体游戏覆写
- `dx-game-frame-repository`：数据访问层
- `dx-game-frame-rpc-consumer` / `rpc-provider`：远程调用边界
- `dx-game-frame-test`：测试模块

## 架构特征

- `cmd` 不直接依赖 `service-core`
- `service-core` 继承并填充 `socket` 的空实现
- 具体游戏仓在此基础上继续覆写默认行为

## 工作价值

- 是阅读 `dx-game-texas` 前必须先建立的“框架地图”
- 排查业务问题时，先判断问题属于 `cmd`、`service`、`repository` 还是 `socket` 扩展点

## 来源

- `/Users/mac/IdeaProjects/dx-game-frame/pom.xml`
- `/Users/mac/IdeaProjects/dx-game-frame/README.md`
- `/Users/mac/IdeaProjects/dx-game-frame/dx-game-frame-service-core/README.md`
- `/Users/mac/IdeaProjects/dx-game-frame/dx-game-frame-socket/README.md`
