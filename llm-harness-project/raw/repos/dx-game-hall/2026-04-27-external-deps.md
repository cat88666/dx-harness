# dx-game-hall External Dependencies

来源：`/Users/mac/IdeaProjects/dx-game-hall/pom.xml`

## 直接共享依赖

- `com.dx:dx-game-frame-proto`
- `com.dx:dx-game-frame-rpc-provider`
- `com.dx:dx-game-frame-repository`
- `com.dx:dx-common-facades`

## 业务共享依赖

- `com.dz:dz-game-biz`
- `com.dz:dz-game-core`
- `com.dz:dz-game-common`
- `com.dz:dz-common-api`

## 基础设施依赖

- `com.alibaba.cloud:spring-cloud-starter-alibaba-nacos-config`
- `com.alibaba.cloud:spring-cloud-starter-alibaba-nacos-discovery`
- `org.apache.dubbo:dubbo-spring-boot-starter`
- `org.apache.dubbo:dubbo-nacos-spring-boot-starter`
- `org.apache.dubbo:dubbo-metadata-report-nacos`
- `org.redisson:redisson-spring-boot-starter`
- `com.dz:dz-redis-shield`
- `com.dz:dz-rocketmq-shield`
- `org.apache.rocketmq:rocketmq-spring-boot-starter`
- `com.lmax:disruptor`

## 观察

仓库强依赖共享框架和基础设施封装，明显不是孤立服务。
