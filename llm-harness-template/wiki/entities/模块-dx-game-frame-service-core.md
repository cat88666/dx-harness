# 模块-dx-game-frame-service-core

## 定位

`dx-game-frame-service-core` 是通用业务默认实现层，作用是在 `socket` 空接口之上提供可继承的默认业务，再让具体游戏仓覆写差异逻辑。

## 在整体中的位置

- 上游被具体游戏仓复用
- 下游依赖 `dx-game-frame-socket`
- 与 `dx-game-frame-cmd` 保持解耦，避免命令层直接绑死默认业务实现

## 为什么重要

- 当 `dx-game-texas` 出现“默认逻辑”和“游戏特化逻辑”交错时，这个模块是区分责任边界的起点
- Review 变更时，要先判断改动应该落在默认骨架还是业务仓覆写层

## 阅读顺序

1. 先看 `dx-game-frame-socket`
2. 再看 `dx-game-frame-service-core`
3. 最后回到 `dx-game-texas` 找具体重写点

## 来源

- `/Users/mac/IdeaProjects/dx-game-frame/dx-game-frame-service-core/README.md`
- `/Users/mac/IdeaProjects/dx-game-frame/dx-game-frame-socket/README.md`
