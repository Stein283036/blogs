# 08-Spring Boot 缓存



## Spring Boot Redis

<img src="https://static.iocoder.cn/images/Redis/2019_09_28/01.png" alt="Spring Data Redis 调用" style="zoom:50%;" />

- 对于下层，Spring Data Redis 提供了统一的操作模板（后文中，我们会看到是 RedisTemplate 类，模板方法模式），封装了 Jedis、Lettuce 的 API 操作，访问 Redis 数据。所以，**实际上，Spring Data Redis 内置真正访问的实际是 Jedis、Lettuce 等 API 操作**。
- 对于上层，开发者学习如何使用 Spring Data Redis 即可，而无需关心 Jedis、Lettuce 的 API 操作。甚至，未来如果我们想将 Redis 访问从 Jedis 迁移成 Lettuce 来，无需做任何的变动。😈 相信很多胖友，在选择 Java Redis 工具库，也是有过烦恼的。
- 目前，Spring Data Redis 暂时只支持 Jedis、Lettuce 的内部封装，而 Redisson 是由 [redisson-spring-data](https://github.com/redisson/redisson/tree/master/redisson-spring-data) 来提供。

在 `spring-boot-starter-data-redis` 项目 2.X 中，默认使用 Lettuce 作为 Java Redis 工具库。

考虑到自己项目中，使用 Jedis 为主，并且问了几个朋友，都是使用 Jedis ，并且有吐槽 Lettuce 坑多多，所以个人推荐的话，生产中还是使用 Jedis ，稳定第一。也因此，本节我们是 Spring Data Redis + Jedis 的组合。



## 参考文章

- [芋道 Spring Boot Redis 入门](https://www.iocoder.cn/Spring-Boot/Redis/?github)