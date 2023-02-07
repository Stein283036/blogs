# 03-Spring Boot Web开发

## Lombok

[Lombok](https://github.com/rzwitserloot/lombok) 是一个 Java 工具，通过使用其定义的注解，自动生成常见的冗余代码，提升开发效率。简化POJO的定义，比如简化setter和getter方法，简化构造方法，简化equals和hashCode方法，简化toString方法。

Lombok 的实现原理，基于 [JSR269(Pluggable Annotation Processing API)](https://jcp.org/en/jsr/detail?id=269) 规范，自定义编译器注解处理器，用于在 Javac 编译阶段时，扫描使用到 Lombok 定义的注解的类，进行自定义的代码生成。

[`@Slf4j`](https://github.com/rzwitserloot/lombok/blob/master/src/core/lombok/Slf4j.java) 注解，添加在**类**上，给该类创建 Slf4j Logger **静态**属性。

![@Slf4j 示例](https://static.iocoder.cn/images/Spring-Boot/2019-02-04/21.png)

Lombok 还提供了 [`@CommonsLog`](https://github.com/rzwitserloot/lombok/blob/master/src/core/lombok/extern/apachecommons/CommonsLog.java)、[`@Flogger`](https://github.com/rzwitserloot/lombok/blob/master/src/core/lombok/extern/flogger/Flogger.java)、[`@Log`](https://github.com/rzwitserloot/lombok/blob/master/src/core/lombok/extern/java/Log.java)、[`@JBossLog`](https://github.com/rzwitserloot/lombok/blob/master/src/core/lombok/extern/jbosslog/JBossLog.java)、[@Log4j](https://github.com/rzwitserloot/lombok/blob/master/src/core/lombok/extern/log4j/Log4j.java)、[@Log4j2](https://github.com/rzwitserloot/lombok/blob/master/src/core/lombok/extern/log4j/Log4j2.java)、[@Slf4jX](https://github.com/rzwitserloot/lombok/blob/master/src/core/lombok/Slf4jX.java) 注解，支持持不同的 Logger 组件。因为 Spring Boot 使用 Slf4j 日志门面框架，所以绝大多数情况下，我们都是使用 `@Slf4j` 注解。

[`@NonNull`](https://github.com/rzwitserloot/lombok/blob/master/src/core/lombok/NonNull.java) 注解，添加在**方法参数**、**类属性**上，用于自动生成 `null` 参数检查。若确实是 `null` 时，抛出 NullPointerException 异常。

![@Slf4j 示例](https://static.iocoder.cn/images/Spring-Boot/2019-02-04/41.png)

## 数据校验

## 参考文章

- [芋道 Spring Boot SpringMVC 入门](https://www.iocoder.cn/Spring-Boot/SpringMVC/)
- [芋道 Spring Boot 消除冗余代码 Lombok 入门](https://www.iocoder.cn/Spring-Boot/Lombok/)
- 