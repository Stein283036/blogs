# misc01

浮点数运算和整数运算相比，只能进行加减乘除这些数值计算，不能做位运算和移位运算。

Java的浮点数完全遵循[IEEE-754](https://web.archive.org/web/20070505021348/http://babbage.cs.qc.edu/courses/cs341/IEEE-754references.html)标准，这也是绝大多数计算机平台都支持的浮点数标准表示方法。

Java在内存中总是使用Unicode表示字符，所以，一个英文字符和一个中文字符都可以用一个`char`类型表示，它们都占用两个字节。要显示一个字符的Unicode编码，只需将`char`类型直接赋值给`int`类型即可。

switch 的实现机制：对于基本类型的整数而言，比较的就是值相等，而对于字符串的比较是先比较字符串的 hashCode 是否相等，再hashcode 相等的情况下然后再比较 equals 方法是否也相同，如果相等则进入对应的分支。

实例对象能访问静态字段只是因为编译器可以根据实例类型自动转换为`类名.静态字段`来访问静态对象。

静态方法经常用于工具类。例如：

- Arrays.XXX
- Math.XXX
- Collections.XXX

静态方法也经常用于辅助方法。注意到 Java 程序的入口`main()`也是静态方法。

Java EE是企业版，它只是在Java SE的基础上加上了大量的API和库，以便方便开发Web应用（Servlet）、数据库、消息服务（JMS）等。
为了保证Java语言的规范性，SUN公司搞了一个JSR规范，凡是想给Java平台加一个功能，比如说访问数据库的功能，大家要先创建一个JSR规范，定义好接口，这样，各个数据库厂商都按照规范写出Java驱动程序，开发者就不用担心自己写的数据库代码在MySQL上能跑，却不能跑在PostgreSQL上。
Java规定，某个类定义的public static void main(String[] args)是Java程序的固定入口方法，因此，Java程序总是从main方法开始执行。

基本数据类型是CPU可以直接进行运算的类型。

int i5 = 0b1000000000; // 二进制表示的512。

Java语言对布尔类型的存储并没有做规定，因为理论上存储布尔类型只需要1 bit，但是通常JVM内部会把boolean表示为4字节整数。

Java的char类型除了可表示标准的ASCII外，还可以表示一个Unicode字符。

引用类型的变量类似于C语言的指针，它内部存储一个“地址”，指向某个对象在内存的位置。
整数2147483640和15换成二进制做加法：

0111 1111 1111 1111 1111 1111 1111 1000

0000 0000 0000 0000 0000 0000 0000 1111

1000 0000 0000 0000 0000 0000 0000 0111 这是二进制补码形式，要计算**真值**需要先转换为原码，由于最高位计算结果为1，因此，加法结果变成了一个负数。对byte和short类型进行移位时，会首先转换为int再进行位移。

运算符记不住也没关系，只需要**加括号**就可以保证运算的优先级正确。

Java的`String`和`char`在内存中总是以Unicode编码表示。

英文字符的`Unicode`编码就是简单地在前面添加一个`00`字节。

因为英文字符的`Unicode`编码高字节总是`00`，包含大量英文的文本会浪费空间，所以，出现了`UTF-8`编码，它是一种**可变长编码**，用来把固定长度的`Unicode`编码变成1～4字节的变长编码。通过`UTF-8`编码，英文字符`'A'`的`UTF-8`编码变为`0x41`，正好和`ASCII`码一致，而中文`'中'`的`UTF-8`编码为3字节`0xe4b8ad`。

`UTF-8`编码的另一个好处是容错能力强。如果传输过程中某些字符出错，不会影响后续字符，因为`UTF-8`编码依靠高字节位来确定一个字符究竟是几个字节，它经常用来作为传输编码。

在Java中，`char`类型实际上就是两个字节的`Unicode`编码。如果我们要手动把字符串转换成其他编码，可以这样做：

```java
byte[] b1 = "Hello".getBytes(); // 按系统默认编码转换，不推荐
byte[] b2 = "Hello".getBytes("UTF-8"); // 按UTF-8编码转换
byte[] b2 = "Hello".getBytes("GBK"); // 按GBK编码转换
byte[] b3 = "Hello".getBytes(StandardCharsets.UTF_8); // 按UTF-8编码转换
```

Java规定：

- 必须捕获的异常，包括`Exception`及其子类，但不包括`RuntimeException`及其子类，这种类型的异常称为Checked Exception。
- 不需要捕获的异常，包括`Error`及其子类，`RuntimeException`及其子类。

输出日志，而不是用`System.out.println()`，有以下几个好处：

1. 可以设置输出样式，避免自己每次都写`"ERROR: " + var`；
2. 可以设置输出级别，禁止某些级别输出。例如，只输出错误日志；
3. 可以被重定向到文件，这样可以在程序运行结束后查看日志；
4. 可以按包名控制日志级别，只输出某些包打的日志；

Java标准库内置的 Logging 使用并不是非常广泛。

数据库隔离级别

dirty read

A transaction reads data written by a concurrent uncommitted transaction.

nonrepeatable read

A transaction re-reads data it has previously read and finds that data has been modified by another transaction (that committed since the initial read).

phantom read

A transaction re-executes a query returning a set of rows that satisfy a search condition and finds that the set of rows satisfying the condition has changed due to another recently-committed transaction.

serialization anomaly

The result of successfully committing a group of transactions is inconsistent with all possible orderings of running those transactions one at a time.

| Isolation Level  | Dirty Read             | Nonrepeatable Read | Phantom Read           | Serialization Anomaly |
| ---------------- | ---------------------- | ------------------ | ---------------------- | --------------------- |
| Read uncommitted | Allowed, but not in PG | Possible           | Possible               | Possible              |
| Read committed   | Not possible           | Possible           | Possible               | Possible              |
| Repeatable read  | Not possible           | Not possible       | Allowed, but not in PG | Possible              |
| Serializable     | Not possible           | Not possible       | Not possible           | Not possible          |

 JPA是一种规范，Hibernate 实现了 JPA 规范，即 Hibernate 为 JPA 的一种实现；而 Spring Data JPA 是对 JPA 进行更高级的封装，让其 DAO 编码变得更简单。

Java 持久层框架访问数据库的方式大致分为两种。一种以 SQL 核心，封装一定程度的 JDBC 操作，比如： MyBatis。另一种是以 Java 实体类为核心，将实体类的和数据库表之间建立映射关系，也就是我们说的ORM框架，如：Hibernate、Spring Data JPA。

Spring Data JPA是在实现了JPA规范的基础上封装的一套 JPA 应用框架，虽然ORM框架都实现了JPA规范，但是在不同的ORM框架之间切换仍然需要编写不同的代码，而使用Spring Data JPA能够方便大家在不同的ORM框架之间（Hibernate、其它的 ORM 框架）进行切换而不需要更改代码。Spring Data JPA旨在通过将统一ORM框架的访问持久层的操作，来提高开发人的效率。

![img](https://pic4.zhimg.com/80/v2-9cd85ea00d3fbdc8d5c07839839c3777_720w.webp)

Hibernate其实是 JPA 的一种实现，而 Spring Data JPA 是一个 JPA 数据访问抽象。也就是说 Spring Data JPA 不是一个实现或JPA提供的程序，它只是一个抽象层，主要用于减少为各种持久层存储实现数据访问层所需的样板代码量。但是它还是需要JPA提供实现程序，其实Spring Data JPA 底层就是使用的 Hibernate实现。

**组合与继承的区别和联系**

在`继承`结构中，父类的内部细节对于子类是可见的。所以我们通常也可以说通过继承的代码复用是一种`白盒式代码复用`。（如果基类的实现发生改变，那么派生类的实现也将随之改变。这样就导致了子类行为的不可预知性；）

`组合`是通过对现有的对象进行拼装（组合）产生新的、更复杂的功能。因为在对象之间，各自的内部细节是不可见的，所以我们也说这种方式的代码复用是`黑盒式代码复用`。（因为组合中一般都定义一个类型，所以在编译期根本不知道具体会调用哪个实现类的方法）

`继承`，在写代码的时候就要指名具体继承哪个类，所以，在`编译期`就确定了关系。从基类继承来的实现是无法在运行期动态改变的，因此降低了应用的灵活性。

`组合`，在写代码的时候可以采用面向接口编程。所以，类的组合关系一般在`运行期`确定。

继承要慎用，其使用场合仅限于你确信使用该技术有效的情况。一个判断方法是，问一问自己是否需要从新类向基类进行向上转型。如果是必须的，则继承是必要的。反之则应该好好考虑是否需要继承。

只有当子类真正是超类的子类型时，才适合用继承。换句话说，对于两个类A和B，只有当两者之间确实存在[`is-a`](https://zh.wikipedia.org/wiki/Is-a)关系的时候，类B才应该继承类A。

平台指的是 OS + 计算机硬件。

对于不同的硬件和操作系统，最主要的区别就是指令不同。比如同样执行 `a + b`，A 操作系统对应的二进制指令可能是 10001000，而 B操作系统对应的指令可能是 11101110。那么，想要做到跨平台，最重要的就是可以根据对应的硬件和操作系统生成对应的二进制指令。

![img](https://www.hollischuang.com/wp-content/uploads/2021/06/Jietu20210627-141259-2.jpg)

