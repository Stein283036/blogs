# 06-Spring Boot 数据源

## 数据库连接池

在我们的项目中，数据库连接池基本是必不可少的组件。在目前数据库连接池的选型中，主要是

- [Druid](https://github.com/alibaba/druid) ，为**监控**而生的数据库连接池。
- [HikariCP](https://github.com/brettwooldridge/HikariCP) ，号称**性能**最好的数据库连接池。
- Spring Boot 2.X 版本，默认采用 HikariCP 。
- 阿里大规模采用 Druid 。

## 多数据源（读写分离）

在项目中，我们可能会碰到需要多数据源的场景。例如说：

- 读写分离：数据库主节点压力比较大，需要增加从节点提供读操作，以减少压力。
- 多数据源：一个复杂的单体项目，需要连接**多个业务**的数据源。

本质上，读写分离，仅仅是多数据源的一个场景，从节点是只提供读操作的数据源。所以只要实现了多数据源的功能，也就能够提供读写分离。

## 参考文章

- [芋道 Spring Boot 数据库连接池入门](https://www.iocoder.cn/Spring-Boot/datasource-pool/)
- [芋道 Spring Boot 多数据源（读写分离）入门](https://www.iocoder.cn/Spring-Boot/dynamic-datasource/?github)