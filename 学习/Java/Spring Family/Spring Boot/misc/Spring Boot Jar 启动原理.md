# Spring Boot Jar 启动原理

**Spring Boot 提供了 Maven 插件 [`spring-boot-maven-plugin`](https://docs.spring.io/spring-boot/docs/current/reference/html/build-tool-plugins.html#build-tool-plugins-maven-plugin)，可以方便的将 Spring Boot 项目打成 `jar` 包或者 `war` 包。**

考虑到部署的便利性，我们绝大多数 99.99% 的场景下，我们会选择打成 `jar` 包。这样，我们就无需在部署项目的服务器，配置相应的 Tomcat、Jetty 等 Servlet 容器。只需要有JRE环境运行Java程序即可。

## 参考文章

- [芋道 Spring Boot Jar 启动原理](https://www.iocoder.cn/Spring-Boot/jar/)