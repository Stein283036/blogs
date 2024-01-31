# Java SE & Java EE

Java SE（Standard Edition）和 Java EE（Enterprise Edition）是 Java 平台的两个主要版本，它们面向不同的应用场景，拥有不同的特性和组件。

## Java SE（Standard Edition）：

Java SE 是 Java 平台的标准版，它提供了一套用于开发桌面和嵌入式应用的核心API。Java SE 包含了 Java 编程语言的基础类库、虚拟机（JVM）、开发工具和其他基本组件。

主要特性和组件：

1. **核心类库：** 提供了基本的数据结构、文件操作、网络通信、多线程、日期时间、数学运算、工具类等基本功能的类库。

2. **图形用户界面（GUI）：** 提供了用于构建桌面应用程序的 Swing 和 AWT 等图形库。

3. **输入输出（I/O）：** 提供了处理输入输出操作的类和接口。

4. **多线程：** 提供了多线程支持，使得开发者能够更好地处理并发问题。

5. **网络编程：** 提供了用于网络通信的类和接口。

6. **安全性：** 包括了用于安全编程的类库，支持数字签名、加密解密等安全操作。

## Java EE（Enterprise Edition）：

Java EE 是 Java 平台的企业版，它是建立在 Java SE 基础上的，并提供了用于开发大规模、复杂的企业级应用程序的扩展API和服务。Java EE 主要关注于分布式计算、事务管理、消息传递、Web 应用程序等企业级应用领域。

主要特性和组件：

1. **Servlet：** 用于开发基于 Java 的 Web 应用程序的 API。

2. **JSP（JavaServer Pages）：** 用于构建动态 Web 页面的技术。

3. **EJB（Enterprise JavaBeans）：** 用于开发企业级组件的 API。

4. **JPA（Java Persistence API）：** 用于简化 Java 对象和数据库之间的映射关系的 API。

5. **JMS（Java Message Service）：** 用于在分布式系统中进行异步消息传递的 API。

6. **JTA（Java Transaction API）：** 用于处理事务的 API。

7. **JCA（Java Connector Architecture）：** 用于连接企业信息系统和 EIS（Enterprise Information Systems）的 API。

8. **Web Services：** 支持创建和部署 Web 服务的相关技术。

### 区别：

1. **应用场景：**
   - Java SE 主要用于桌面应用程序、嵌入式设备、移动应用等。
   - Java EE 主要用于开发大型企业级应用，包括 Web 应用、分布式应用等。

2. **功能和组件：**
   - Java SE 提供了基本的核心类库和用于桌面应用的图形库。
   - Java EE 在 Java SE 的基础上提供了更多的企业级组件，例如 Servlet、EJB、JSP 等。

3. **开发复杂度：**
   - Java SE 更适用于相对简单的应用开发。
   - Java EE 更适用于复杂的企业级应用开发，涉及分布式计算、事务处理等。

4. **依赖关系：**
   - Java EE 依赖于 Java SE。Java EE 包含了 Java SE 的所有功能，并在其基础上提供了额外的功能和组件。

总体而言，Java SE 和 Java EE 是 Java 平台的两个重要版本，提供了不同层次和领域的功能，开发者根据应用的规模和需求选择适当的版本。在实践中，许多 Java EE 应用也会使用 Java SE 的功能。