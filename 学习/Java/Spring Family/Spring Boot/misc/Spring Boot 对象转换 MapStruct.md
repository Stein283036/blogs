# Spring Boot 对象转换 MapStruct

为了让应用的代码更易维护，我们往往会将项目进行分层。在《阿里巴巴 Java 开发手册》中，推荐分层如下图：

![应用分层](https://static.iocoder.cn/ef0d24cfaecdbe703ad646e09e697454)

分层之后，每一层都有自己的领域模型，即不同类型的 Bean：

- **DO**（Data Object）：与数据库表结构一一对应，通过DAO层向上传输数据源对象。
- **DTO**（Data Transfer Object）：数据传输对象，Service或Manager向外传输的对象。
- **BO**（Business Object）：业务对象。由Service层输出的封装业务逻辑的对象。
- 等

通过创建一个 MapStruct **Mapper** 接口，并定义一个转换接口方法，后续交给 MapStruct 自动生成对象转换的代码即可。

MapStruct 是用于生成类型安全的 Bean 映射类的 Java 注解处理器。

你所要做的就是定义一个映射器接口，声明任何需要映射的方法。在编译过程中，MapStruct 将生成该接口的实现。此实现使用**纯 Java 的方法调用源对象和目标对象之间进行映射，并非 Java 反射机制**。

在对象转换时，我们可能会存在属性不是完全映射的情况，例如说**属性名**不同。此时，我们可以使用 MapStruct 提供的 [`@Mapping`](https://github.com/mapstruct/mapstruct/blob/master/core/src/main/java/org/mapstruct/Mapping.java) 注解，配置相应的映射关系。示例如下图：

![ 映射](https://static.iocoder.cn/images/Spring-Boot/2019-02-07/31.png)

## 参考文章

- [芋道 Spring Boot 对象转换 MapStruct 入门](https://www.iocoder.cn/Spring-Boot/MapStruct/)