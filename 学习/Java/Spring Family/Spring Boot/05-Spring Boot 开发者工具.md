# 05-Spring Boot 开发者工具

## 热部署

在日常开发中，我们需要经常修改 Java 代码，手动重启项目，查看修改后的效果。如果在项目小时，重启速度比较快，等待的时间是较短的。但是随着项目逐渐变大，重启的速度变慢，等待时间 1-2 min 是比较常见的。

[`spring-boot-devtools`](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-project/spring-boot-devtools) 是 Spring Boot 提供的开发者工具，它会监控当前应用所在的 classpath 下的文件发生变化，进行**自动重启**。

Spring Boot 通过使用两个类加载器来提供了重启技术。

- 不改变的类（例如，第三方 jar）被加载到 **base** 类加载器中。
- 经常处于开发状态的类被加载到 **restart** 类加载器中。

当应用重启时，**restart** 类加载器将被丢弃，并重新创建一个新的。这种方式意味着应用重启比**冷启动**要快得多，因为省去 **base** 类加载器的处理步骤，并且可以直接使用。

## 参考文章

- [芋道 Spring Boot 热部署入门](https://www.iocoder.cn/Spring-Boot/hot-swap/)