# Java CLI

Java 提供了一系列命令行工具，用于编译、运行、调试、监测和分析 Java 程序。以下是一些常用的 Java 命令行工具：

## 1. **javac - Java 编译器：**
   - 用于将 Java 源代码文件编译成 Java 字节码文件（.class 文件）。
   - 示例：`javac YourProgram.java`

## 2. **java - Java 运行时环境：**
   - 用于运行 Java 程序。
   - 示例：`java YourProgram`

## 3. **jar - Java 归档工具：**
   - 用于创建和操作 JAR 文件，将多个类文件打包成一个 JAR 文件。
   - 示例：`jar cf YourArchive.jar YourClass.class`

## 4. **javadoc - Java 文档生成工具：**
   - 用于从 Java 源代码中生成 API 文档。
   - 示例：`javadoc YourClass.java`

## 5. **javap - Java 类文件反汇编工具：**
   - 用于反汇编 Java 字节码文件，查看类的结构和成员。
   - 示例：`javap -c YourClass`

## 6. **jdb - Java 调试器：**
   - 用于在命令行中调试 Java 程序，支持断点设置、变量查看等调试功能。
   - 示例：`jdb YourProgram`

## 7. **jps - Java 进程状态工具：**
   - 用于显示 Java 虚拟机（JVM）中运行的 Java 进程的信息。
   - 示例：`jps`

## 8. **jstack - Java 堆栈跟踪工具：**
   - 用于生成 Java 进程中每个线程的堆栈跟踪。
   - 示例：`jstack YourPID`

## 9. **jmap - Java 内存映像工具：**
   - 用于生成 Java 进程的堆转储快照，查看内存使用情况。
   - 示例：`jmap -dump:format=b,file=heapdump.hprof YourPID`

## 10. **jstat - Java 虚拟机统计监视工具：**
   - 用于监视虚拟机各种状态，如垃圾回收、类装载、JIT 编译等。
   - 示例：`jstat -gcutil YourPID`

## 11. **jvisualvm - Java VisualVM：**
   - 用于监视、分析和调试本地或远程的 Java 应用程序。
   - 示例：运行 `jvisualvm` 命令启动可视化工具。

这些命令行工具为 Java 开发者提供了丰富的功能，可以用于开发、调试和性能分析。在实际开发中，根据需求和场景选择合适的工具进行使用。