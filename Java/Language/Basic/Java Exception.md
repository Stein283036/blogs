# Java Exception

## 概述

在 Java 中，异常（Exception）是指在程序运行过程中发生的不正常情况，分为 `Error` 和 `Exception` 两大类，都继承自 `Throwable`，Throwable 包含了其线程创建时线程执行堆栈的快照，它提供了 printStackTrace() 等接口用于获取堆栈跟踪数据等信息。而 Exception 又分为编译期异常和运行时异常。这些不正常情况可能导致程序中断、崩溃。异常是 Java 中处理错误的一种机制，它有助于提高程序的稳定性和可靠性。异常在编译和运行过程中都会出现，对于**检查异常（Checked Exception）**， 继承自 `Exception` 类的异常，是在编译时检查的异常，程序必须显式地处理或抛出；对于**运行时异常（Unchecked Exception）**，继承自 `RuntimeException` 的异常，是在运行时才会发生的异常，编译器不会进行检查。

导致异常的可能原因比如：

- 程序内部错误
  - 内存溢出
  - 程序算法设计缺陷
- 程序外部错误
  - 用户输入
  - 文件读取失败
  - （MySQL、Redis）网络连接失败

## 异常的层次体系

![exception.drawio](D:\2024年\blogs\Java\Basic\assets\exception.drawio-170479526851413.png)

## 异常的分类

`Throwable` 是 Java 中所有异常类的父类。

- Exception
  - RuntimeException(Unchecked Exception)
    - NullPointerException
    - ClassCastException
    - ArrayIndexOutOfBoundsException
  - Checked Exception
    - IOException
    - SQLException
- Error
  - OutOfMemoryError
  - StackOverflowError

## 常见的异常

- 空指针异常（NullPointerException）
- 数组越界异常（ArrayIndexOutOfBoundsException）
- 文件操作异常 （IOException）
- 类型转换异常（ClassCastException）
- 算数异常（ArithmeticException），除零
- 数据库异常（SQLException）
- 并发修改异常（ConcurrentModificationException）
- 自定义异常

## 异常的处理机制

### try-catch-finally

使用 `try-catch-finally` 语句。

将可能出现异常的代码写在 try 语句块中，可能抛出的异常使用 catch 捕获，可以捕获多个可能抛出的异常，但是父类异常必须声明在子类异常之后。finally 语句块的代码一般情况下都会执行，除非程序在执行 finally 代码块前编写了强制退出等终止程序的代码，通常用来释放系统资源、网络连接、IO流等。

try 语句后必须有 catch 或 finally 其中一个语句。

在 Java 7 之后，可以使用多异常捕获和**异常链**来更灵活地处理异常。

```java
try {
    // 代码可能抛出异常的部分
} catch (IOException | SQLException e) {
    // 处理多个异常
    throw new MyException("Something went wrong", e);
}
```

### try-with-resources

Java7 的 `try-with-resources` 语句（打开的资源必须实现 `AutoClosable` 接口）。使用这种方式抛出异常，则会被抑制，抛出的仍然为原始异常。被抑制的异常会由 addSusppressed 方法添加到原来的异常，如果想要获取被抑制的异常列表，可以调用 getSuppressed 方法来获取。

### throw 和 throws

throw 表示显示地使用 Java 关键字 throw 抛出一个异常（通常都是运行期异常），这个异常可以是 JDK 自带的异常，当然在不满足需求下，应当自定义运行期异常（继承 RuntimeException）来抛出，这样抛出的异常更加明确。

throws 出现在方法的签名处，表示该方法可能抛出的所有异常，异常之间使用 , 分开，这样做意味着在当前方法调用栈中不会处理这些可能会抛出的异常，因此将异常的处理委托给了方法的调用栈处理，如果调用栈也不处理该异常，那么次方法的签名处也需要显示地抛出无法处理的异常，依次类推，最顶层的处理程序是 JVM。

### thorws抛出异常的规则

- 如果是不可查异常（unchecked exception），即Error、RuntimeException或它们的子类，那么可以不使用throws关键字来声明要抛出的异常，编译仍能顺利通过，但在运行时会被系统抛出。
- 必须声明方法可抛出的任何可查异常（checked exception）。即如果一个方法可能出现受可查异常，要么用try-catch语句捕获，要么用throws子句声明将它抛出，否则会导致编译错误
- 仅当抛出了异常，该方法的调用者才必须处理或者重新抛出该异常。当方法的调用者无力处理该异常的时候，应该继续抛出。
- 若覆盖一个方法，则不能声明与覆盖方法不同的异常。声明的任何异常必须是被覆盖方法所声明异常的同类或子类。

## 断言

断言（Assertion）是一种调试程序的方式。在 Java 中，使用 `assert` 关键字来实现断言。

简单的断言例子：

```java
public static void main(String[] args) {
    double x = Math.abs(-123.45);
    assert x >= 0;
    System.out.println(x);
}
```

语句`assert x >= 0;`即为断言，断言条件`x >= 0`预期为`true`。如果计算结果为`false`，则断言失败，抛出`AssertionError`。

使用`assert`语句时，还可以添加一个可选的断言消息：

```
assert x >= 0 : "x must >= 0";
```

这样，断言失败的时候，`AssertionError`会带上消息`x must >= 0`，更加便于调试。

Java断言的特点是：断言失败时会抛出`AssertionError`，导致程序结束退出。因此，断言不能用于可恢复的程序错误，只应该用于开发和测试阶段。

**实际开发中，很少使用断言。更好的方法是编写单元测试。**

## 自定义异常

习惯上，定义一个异常类应包含两个构造函数，一个无参构造函数和一个带有详细描述信息的构造函数（Throwable 的 toString 方法会打印这些详细信息，调试时很有用）。

```java
public class MyException extends RuntimeException {
    public MyException() {}
    public MyException(String message) {
        super(message);
    }
}
```

## finally 不会执行的情况

在 Java 中，`finally` 块中的代码通常被设计用于无论是否发生异常都必须执行的情况。然而，有一些特殊情况下 `finally` 块中的代码可能不会执行，主要包括以下几种情况：

1. **System.exit() 被调用：**
   
   - 当调用 `System.exit()` 方法时，Java 虚拟机将立即退出，导致 `finally` 块中的代码不会执行。
   
   ```java
   try {
       // 一些代码
   } finally {
       System.exit(0);
       System.out.println("This will not be executed.");
   }
   ```
   
2. **无限循环或死锁：**
   - 如果在 `try` 块中发生了无限循环或死锁，导致程序无法正常执行，那么 `finally` 块中的代码也不会执行。

   ```java
   try {
       while (true) {
           // 无限循环
       }
   } finally {
       System.out.println("This will not be executed.");
   }
   ```

3. **在 `finally` 块中抛出异常：**
   - 如果 `finally` 块中抛出了异常，并且这个异常没有被捕获，那么 `finally` 块中的代码执行过程中将被中断。

   ```java
   try {
       // 一些代码
   } finally {
       throw new RuntimeException("Exception in finally block");
   }
   ```

## 异常底层原理

Exception Table
