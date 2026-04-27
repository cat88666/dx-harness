# 仓库-dx-game-core

## 定位

`dx-game-core` 是一个偏示例化的运行时骨架仓，核心在于线程分发、事件调度、延迟任务和任务队列模型。它更像底层机制的可读样板，而不是完整业务实现。

## 关键结构

- `src/main/java/com/example/core/frame/thread/`：线程池、线程管理、命名线程工厂
- `src/main/java/com/example/core/frame/event/`：事件管理入口
- `src/main/java/com/example/core/frame/delay/`：延迟事件与触发器
- `src/main/java/com/example/core/frame/queue/`：按分组串行执行的任务队列
- `src/main/java/com/example/core/frame/task/`：命令任务与事件任务样例

## 工作价值

- 适合作为理解 `dx-game-frame` 生产版线程模型的简化镜像
- 适合先读这个仓，再回到 `dx-game-frame` 看增强实现
- 适合沉淀“串行分组执行”和“延迟事件驱动”这两个基础概念

## 关注点

- `TaskQueueManager.submit()` 只入队，不主动触发首任务执行，阅读时要连带看调用链
- `ThreadPoolManager` 使用固定前缀 `TEST-` 的线程池配置，仅适合作为骨架参考

## 来源

- `/Users/mac/IdeaProjects/dx-game-core/src/main/java/com/example/core/frame/thread/ThreadManager.java`
- `/Users/mac/IdeaProjects/dx-game-core/src/main/java/com/example/core/frame/event/EventManager.java`
- `/Users/mac/IdeaProjects/dx-game-core/src/main/java/com/example/core/frame/queue/TaskQueueManager.java`
