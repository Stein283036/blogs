# Java classpath 和 jar

## classpath

`classpath` 就是一组类文件目录的路径集合，它设置的搜索路径与操作系统相关。在 Windows 系统上，用 `;` 分隔，带空格的目录用`""`括起来，例如：

```
C:\work\project1\bin;C:\shared;"D:\My Documents\project1\bin"
```

在 Linux 系统上，用 `:` 分隔，例如：

```
/usr/shared:/usr/local/bin:/home/liaoxuefeng/bin
```

现在我们假设 `classpath` 是`.;C:\work\project1\bin;C:\shared`，当 JVM 在加载`abc.xyz.Hello` 这个类时，会依次查找：

- <当前目录>\abc\xyz\Hello.class
- C:\work\project1\bin\abc\xyz\Hello.class
- C:\shared\abc\xyz\Hello.class

注意到 `.` 代表当前目录。如果 JVM 在某个路径下找到了对应的 `class` 文件，就不再往后继续搜索。如果所有路径下都没有找到，就会抛出 `ClassNotFoundException`。

`classpath` 的设定方法有两种：

在系统环境变量中设置 `classpath` 环境变量，不推荐；

在启动 JVM 时设置 `classpath` 变量，推荐。

强烈**不推荐**在系统环境变量中设置 `classpath` ，那样会污染整个系统环境。在启动 JVM 时设置 `classpath` 才是推荐的做法。实际上就是给 `java` 命令传入 `-classpath` 或 `-cp` 参数：

```
java -classpath .;C:\work\project1\bin;C:\shared abc.xyz.Hello
```

或者使用 `-cp` 的简写：

```
java -cp .;C:\work\project1\bin;C:\shared abc.xyz.Hello
```

如果没有设置系统环境变量，也没有传入`-cp` 参数，那么 JVM 默认的 `classpath` 为 `.`，即当前目录：

```
java abc.xyz.Hello
```

上述命令告诉 JVM 只在当前目录搜索 `/abc/xyz/Hello.class`。

在 IDE 中运行 Java 程序，IDE 默认的 `-cp` 参数是当前工程的 `bin `目录和引入的 jar 包。

## jar

如果有很多 `.class` 文件，散落在各层目录中，肯定不便于管理。如果能把目录打一个包，变成一个文件，就方便多了。

jar 包就是用来干这个事的，它可以把 `package` 组织的目录层级，以及各个目录下的所有文件（包括 `.class` 文件和其它文件）都打成一个 jar 文件，这样一来，无论是备份，还是发给其它用户，就简单多了。

jar 包实际上就是一个 zip 格式的压缩文件，如果我们要执行一个 jar 包的 `class`，就可以把 jar 包放到 `classpath` 中：

```
java -cp ./hello.jar abc.xyz.Hello
```

这样 JVM 会自动在 `hello.jar` 文件里去搜索某个类。

jar 包还可以包含一个特殊的 `/META-INF/MANIFEST.MF` 文件，`MANIFEST.MF` 是纯文本，可以指定 `Main-Class` 和其它信息。JVM 会自动读取这个 `MANIFEST.MF` 文件，如果存在 `Main-Class`，我们就不必在命令行指定启动的类名，而是用更方便的命令：

```
java -jar hello.jar
```

jar 包还可以包含其它 jar 包，这个时候，就需要在 `MANIFEST.MF` 文件里配置 `classpath` 了（参考Spring Boot 项目的 jar 包）。

在大型项目中，不需要手动编写 `MANIFEST.MF` 文件和创建 jar 包。Java 社区提供了大量的开源构建工具，例如 Maven，可以非常方便地创建 jar 包。

