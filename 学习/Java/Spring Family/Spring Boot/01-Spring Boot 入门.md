# 01-Spring Boot 入门



## 为什么需要Spring Boot

### 基于SSM开发的痛点

**大量的配置**

回想基于SSM开发Web应用的时候，总是需要对库做大量的配置，既包括Spring内置的也包括第三方的，比如：

- 配置数据源
- 配置事务管理器
- 配置MyBatis
- 配置Spring
- 配置WebMvc
- 配置基于Spring的应用
- 配置Redis
- 等等

其次，还需要将应用打成war包，需要额外配置一个servlet容器，比如Tomcat。

**依赖管理**

此外，还需要手动导入大量的jar包，比如开发web应用，那么基本的jsp、servlet、jackson、webmvc等依赖是至少必须导入的，还有随着应用功能增多，导入的jar包也越来越多，因此这些jar包间很有可能会出现依赖冲突，需要我们手动去解决，而且这些jar包的版本也需要我们进行管理，非常耗时，降低了开发人员的生产力。

**打包部署**

使用基于SSM开发的应用需要打包成war部署到Tomcat中运行，增加了部署维护成本。



## 什么是Spring Boot

Spring Boot是一个构建在Spring其它项目基础上的一个非常流行的Spring项目，简单的说，它简化了各种Spring项目的使用，从而使开发者可以更加方便地基于Spring开发各种各样的应用。

Spring Boot可以帮助我们创建一个单体的、生产级别的、基于Spring并且可以直接运行的应用。

Spring Boot帮助我们进行依赖管理的仲裁，采用约定大于配置的设计理念，对大多数库进行自动配置，大多数Boot应用只需要非常少的Spring配置。

Spring Boot为开发者提供更好的体验，简化Spring应用的开发。

开箱即用，提供各种默认配置来简化应用配置，基于约定大于配置的理念。

内嵌Servlet容器，默认为Tomcat，可以通过java -jar命令行的方式直接运行，简化web应用的部署。

没有冗余代码的生成，也绝不要求XML配置。

Spring Boot提供了各种应用场景的starter启动器，通过引入一个个starter，Spring Boot就会通过maven依赖的传递性，自动引入该场景所需要的所有jar包，从而应用程序便有了针对此场景开发的依赖，并且在不同场景的starter产生jar包冲突时，Spring Boot会自动解决。

Spring Boot提供了生产级别的特性，可以监控应用的各种指标、进行健康状态检查、端点检测等。

Spring Boot支持外部化配置，可以将本地开发的配置与生产部署的配置进行分离，从而提高应用的安全性。



## 参考文章

|               标题                |                          来源                           |
| :-------------------------------: | :-----------------------------------------------------: |
| Spring Boot 2.x基础教程：快速入门 | https://blog.didispace.com/spring-boot-learning-21-1-1/ |
|                                   |                                                         |
|                                   |                                                         |
|                                   |                                                         |

