# 02-Spring Boot 配置文件

**配置基于Spring应用的三种方式**

JavaConfig：就是基于Java语言进行配置，而不是XML配置，区分开来，通常使用@Configuration和@Bean在Java文件中进行配置，基于Spring的配置是利用能将Bean表示为Spring容器管理的注解来标识，比如@Component、@Controller等。、



**默认配置和自动配置**

在使用 Spring Boot 时，我们仅需在 `pom.xml` 文件中，引入需要**组件**的 `*-starter`场景启动器 依赖，并在 `application.yaml` 等配置文件中添加该组件定义的**配置项**，最终 Spring Boot 在自动化配置时，会基于该组件的配置项 + **配置类**，自动创建该组件的 Bean 们（这个场景需要的所有Bean）。对于大多数的场景启动器来说，SpringBoot都做了默认的配置，如jdbc和web-mvc、redis等。



**Spring Boot的配置文件格式**

Spring Boot 支持 [Properties](https://zh.wikipedia.org/zh-cn/.properties)、[YAML](https://zh.wikipedia.org/zh/YAML)、JSON 三种格式的配置文件。目前主流的采用的是 Properties 或是 YAML 格式。

YAML是"YAML Ain't a Markup Language"（YAML不是一种[标记语言](https://zh.wikipedia.org/wiki/标记语言)）的[递归缩写](https://zh.wikipedia.org/wiki/遞迴縮寫)。在开发的这种语言时，YAML的意思其实是："Yet Another Markup Language"（仍是一种标记语言）但为了强调这种语言以数据为中心，而不是以标记语言为重点，而用反向缩略语重命名。

**注意，配置文件的配置项单词之间，Spring Boot 推荐使用 - 中划线间隔。**



**自定义配置**

引入 [`spring-boot-configuration-processor`](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-project/spring-boot-tools/spring-boot-configuration-processor) 依赖的原因是，编译项目时，会扫描 `@ConfigurationProperties` 注解，生成 `spring-configuration-metadata.json` 配置元数据文件给 IDEA。这样在 IDEA 中，可以带来两个好处：

- 在 `application.yaml` 配置文件，添加配置项时，IDEA 会给出提示。
- 点击配置项时，可以跳转到对应的 `@ConfigurationProperties` 注解的配置类。



**读取配置文件中的配置项**

在类上，添加 `@ConfigurationProperties` 注解，并设置 `prefix = "order"` 属性，这样它就可以读取**前缀**为 `order` 配置项，设置到配置类对应的属性上。而可以不用@Value注解读取配置文件的配置项了。前提是配置文件的配置项和配置类的属性名称一致。

**`@Value` 注解是 Spring 所提供，`@ConfigurationProperties` 注解是 Spring Boot 所提供。**

CommandLineRunner接口定义了一个Bean包含在一个Spring应用中在应用启动时应该运行run方法。

`@Value`注解加载属性值的时候可以支持两种表达式来进行配置：

- 一种是PlaceHolder方式，格式为 `${...}`，大括号内为PlaceHolder
- 另外还可以使用SpEL表达式（Spring Expression Language）， 格式为 `#{...}`，大括号内为SpEL表达式



**多环境配置**

通过命令行连续的两个中划线 `--`，后面接 `配置项=配置值` 的方式，修改配置文件中对应的**配置项**为对应的**配置值**。例如说，`--配置项=配置值`。如果希望修改多个配置项，则使用多组 `--` 即可，中间使用空格分开。例如说，`--配置项1=配置值1 --配置项2=配置值2`。

命令行配置使用的还是**非常多**的。例如说，通过 `--spring.profiles.active=prod` 命令行参数，设置生效的 Profile 为 `prod` 生产环境。

如果只使用**一份**配置文件，每次部署到不同的环境，就需要重复去修改，显然非常麻烦且容易出错。所以针对多环境场景下，我们会给每个环境创建一个配置文件 `application-${profile}.yaml`。其中，`${profile}` 为**环境名**，对应到 Spring Boot 项目**生效的 Profile**。

例如说：`application-dev.yaml` 配置文件，对应 dev 开发环境。这样，我们在**生产**环境的服务器上，**使用 `java -jar xxx.jar --spring.profiles.active=prod` 命令**，就可以加载 `application-prod.yaml` 配置文件，从而连接上配置文件配置的**生产**环境的 MySQL、Redis 等等服务。

另外，我们会创建 application.yaml 配置文件，放不同环境的相同配置。例如说，spring.application.name 配置项，肯定是相同的啦。

Spring Boot 默认读取文件名为 `application` 的配置文件。例如说，`application.yaml` 配置文件。同时，Spring Boot 可以通过 `spring.config.name` 配置项，设置自定义配置文件名。

YAML还可以在一个单个文件中通过使用`spring.profiles`属性来定义多个不同的环境配置。

![image-20230108011431397](C:\Users\BellaCiao\AppData\Roaming\Typora\typora-user-images\image-20230108011431397.png)

YAML目前还有一些不足，它无法通过@PropertySource注解来加载配置，不过影响不大，通常使用@ConfigurationProperties注解配合prefix属性读取配置文件中的配置项。



**参数引用**

在`application.properties`中的各个参数之间，我们也可以直接通过使用PlaceHolder的方式来进行引用，就像下面的设置：

```properties
book.name=SpringCloud
book.author=ZhaiYongchao
book.desc=${book.author}  is writing《${book.name}》
```









## 参考文章

- [芋道 Spring Boot 配置文件入门](https://www.iocoder.cn/Spring-Boot/config-file/)
- [Spring Boot 2.x基础教程：加密配置中的敏感信息](https://blog.didispace.com/spring-boot-learning-2-1-5/)
- 