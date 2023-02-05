# Maven

构建定义：把动态的Web工程经过编译得到的编译结果部署到服务器上的整个过程。jar包、war包就是构建之后的结果。

如果项目非常庞大，就不适合使用package来划分模块，最好是每一个模块对应一个工程，利于分工协作。借助于maven就可以将一个项目拆分成多个工程。Project包含Module，各个Module之间可能会相互依赖，Module由包组成。

maven是一款服务于java平台的自动化构建工具。

部署：最终在sevlet容器中部署的不是动态web工程，而是编译后的工程，jar包或者war包。因为JVM只能加载执行.class文件。

*scope就是依赖的范围*

**1、compile，**默认值，适用于所有阶段（开发、测试、部署、运行），本jar会一直存在所有阶段。

**2、provided，**只在开发、测试阶段使用，目的是不让Servlet容器和你本地仓库的jar包冲突 。如servlet.jar。

**3、runtime，**只在运行时使用，如JDBC驱动，适用运行和测试阶段。

**4、test，**只在测试时使用，用于编译和运行测试代码。不会随项目发布。

[maven官网](https://maven.apache.org/)

Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.

