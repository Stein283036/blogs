# Spring Boot 自动配置原理

条件注解并不是 Spring Boot 所独有，而是在 Spring3.1 版本时，为了满足不同环境注册不同的 Bean ，引入了 [`@Profile`](https://github.com/spring-projects/spring-framework/blob/master/spring-context/src/main/java/org/springframework/context/annotation/Profile.java) 注解。示例代码如下：

```java
@Configurationpublic class DataSourceConfiguration {    @Bean    @Profile("DEV")    public DataSource devDataSource() {        // ... 单机 MySQL    }    @Bean    @Profile("PROD")    public DataSource prodDataSource() {        // ... 集群 MySQL    }    }
```

在 Spring4 版本时，提供了 [`@Conditional`](https://github.com/spring-projects/spring-framework/blob/master/spring-context/src/main/java/org/springframework/context/annotation/Conditional.java) 注解，用于声明在配置类或者创建 Bean 的方法上，表示需要满足指定条件才能生效。示例代码如下：

```java
@Configurationpublic class TestConfiguration {    
    @Bean    
    @Conditional(XXXCondition.class)    
    public Object xxxObject() {        return new Object();    }    }
```

显然，Spring4 提交的 `@Conditional` 注解非常不方便，需要我们自己去拓展。因此，Spring Boot 进一步增强，提供了常用的条件注解：

- `@ConditionalOnBean`：当容器里有指定 Bean 的条件下
- `@ConditionalOnMissingBean`：当容器里没有指定 Bean 的情况下
- `@ConditionalOnSingleCandidate`：当指定 Bean 在容器中只有一个，或者虽然有多个但是指定首选 Bean
- `@ConditionalOnClass`：当类路径下有指定类的条件下
- `@ConditionalOnMissingClass`：当类路径下没有指定类的条件下
- `@ConditionalOnProperty`：指定的属性是否有指定的值
- `@ConditionalOnResource`：类路径是否有指定的值
- `@ConditionalOnExpression`：基于 SpEL 表达式作为判断条件
- `@ConditionalOnJava`：基于 Java 版本作为判断条件
- `@ConditionalOnJndi`：在 JNDI 存在的条件下差在指定的位置
- `@ConditionalOnNotWebApplication`：当前项目不是 Web 项目的条件下
- `@ConditionalOnWebApplication`：当前项目是 Web项 目的条件下

## 参考文章

- [芋道 Spring Boot 自动配置原理](https://www.iocoder.cn/Spring-Boot/autoconfigure/)