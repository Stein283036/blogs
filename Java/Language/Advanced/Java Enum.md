# Java Enum

## 概述

枚举是 Java 语言的一种特殊的类，使用关键字 `enum` 定义一个枚举类，枚举类表示确定的有限个的常量对象集合，枚举类隐式继承 `Enum` 类，因此不能继承其它类，构造方法默认私有，字段默认使用 `public static final` 修饰。

在加载枚举类的时候虚拟机会自动调用 `Enum` 类的构造方法创建枚举常量对象。

枚举通常被用于 switch 选择分支中用于比较的流程控制。

枚举类的常量成员必须定义在类的开始处，优先于任何其它方法、构造器等，多个常量成员之间使用 `,` 分隔。

反编译出的 `Color.class` ：

```java
public final class com.stein.enumeration.Color extends java.lang.Enum<com.stein.enumeration.Color> {
  public static final com.stein.enumeration.Color RED;                                              
  public static final com.stein.enumeration.Color GREEN;                                            
  public static final com.stein.enumeration.Color BLUE;                                             
  public static com.stein.enumeration.Color[] values();                                             
  public static com.stein.enumeration.Color valueOf(java.lang.String);                              
  public void colorInfo();                                                                          
  static {};
}
```

## 枚举的相关方法

这些方法都是定义在 Enum 类中的，values() 和 valueOf() 是静态方法

**values()，ordinal()，name() 和 valueOf() 方法**

`enum` 定义的枚举类默认继承了 `java.lang.Enum` 类，并实现了 `java.lang.Serializable` 和 `java.lang.Comparable` 两个接口。

`values()` 、`ordinal()` 和 `valueOf()` 方法声明在 `java.lang.Enum` 类中：

- values() 返回枚举类中所有的常量。
- ordinal() 方法可以找到每个枚举常量的索引，就像数组索引一样。
- name() 方法返回枚举常量的名称
- valueOf() 方法返回指定字符串值的枚举常量。

## 枚举类成员

枚举跟普通类一样可以定义自己的变量、代码块、方法和构造函数，构造函数只能使用 private 访问修饰符，所以外部无法调用。枚举常量使用`private static final`修饰。

枚举既可以包含具体方法，也可以包含抽象方法。 如果枚举类具有抽象方法，则枚举类的每个实例都必须实现它。

## 枚举在Switch分支中的原理

在Java中，枚举类型在使用`switch`语句时，其原理是基于整数的索引值。每个枚举常量都被分配一个整数值，从0开始递增。当`switch`语句中使用枚举类型时，实际上是在比较整数索引值，而非枚举常量本身。

以下是使用枚举类型的`switch`语句的原理：

1. **为枚举常量分配整数值：**
   - 编译器会为每个枚举常量分配一个整数值，从0开始递增。这个整数值称为枚举的序数（ordinal）。第一个枚举常量的序数为0，第二个为1，以此类推。

2. **生成类似于整数的`switch`代码：**
   - 在生成字节码时，编译器会将`switch`语句转化为类似于整数`switch`的代码。这是因为Java中的`switch`语句只支持整数类型（`byte`, `short`, `char`, `int`以及它们的包装类、`enum`和`String`）。

3. **比较整数索引值：**
   - 在运行时，`switch`语句会比较枚举变量的整数索引值。根据匹配的索引值执行相应的代码块。

示例代码：

```java
enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
}

public class EnumSwitchExample {
    public static void main(String[] args) {
        Day day = Day.MONDAY;

        switch (day) {
            case SUNDAY:
                System.out.println("It's Sunday!");
                break;
            case MONDAY:
                System.out.println("It's Monday!");
                break;
            // ... other cases ...
            default:
                System.out.println("It's another day.");
        }
    }
}
```

在上面的例子中，每个枚举常量被赋予一个整数值，而`switch`语句比较的是这些整数值。这样的设计使得在使用枚举时，`switch`语句更具可读性，而且能够保持与原始的枚举顺序一致。

## 高级使用

### 自定义方法和字段

枚举可以包含自定义的方法和字段。每个枚举常量都可以拥有自己的方法（抽象方法）和字段。这使得枚举更加灵活，可以包含更多的业务逻辑。

```java
public enum Day {
    SUNDAY("Sun"), MONDAY("Mon"), TUESDAY("Tue"), WEDNESDAY("Wed"),
    THURSDAY("Thu"), FRIDAY("Fri"), SATURDAY("Sat");

    private final String abbreviation;

    Day(String abbreviation) {
        this.abbreviation = abbreviation;
    }

    public String getAbbreviation() {
        return abbreviation;
    }
}
```

### 实现接口

枚举可以实现接口，使得每个枚举常量都具有接口定义的方法。这为枚举提供了更多的灵活性，可以用于实现特定的接口行为。

```java
public interface Printable {
    void print();
}

public enum Day implements Printable {
    // ...
    @Override
    public void print() {
        System.out.println("Printable day: " + this.name());
    }
}
```

### 静态导入

静态导入可以用于直接导入枚举类型的常量，使得在代码中使用时更加简洁。

```java
import static com.example.Day.*;

public class EnumExample {
    public static void main(String[] args) {
        Day today = MONDAY;
        System.out.println("Today is: " + today);
    }
}
```

### 枚举集合方法

Java 8引入了一些枚举集合方法，如`values()`、`valueOf()`和`ordinal()`。这些方法提供了对枚举类型的集合和信息的操作。

```java
Day[] days = Day.values(); // 获取所有枚举常量数组
Day monday = Day.valueOf("MONDAY"); // 根据字符串获取枚举常量
int ordinal = monday.ordinal(); // 获取枚举常量的序数
```

## JDK中常用的枚举类

Java标准库（JDK）中包含许多常用的枚举类，这些枚举类用于表示各种概念，提供了便利的方式来处理特定的场景。以下是一些JDK中常用的枚举类：

1. **java.util.concurrent 包中的枚举类：**
   
   - `TimeUnit`: 表示时间单位，用于处理时间的度量。
   
   ```java
   TimeUnit.SECONDS, TimeUnit.MINUTES, TimeUnit.HOURS, ...
   ```
   
2. **java.nio.file 包中的枚举类：**
   
   - `StandardOpenOption`: 文件操作的选项，用于指定如何打开文件。
   
   ```java
   StandardOpenOption.READ, StandardOpenOption.WRITE, StandardOpenOption.CREATE, ...
   ```
   
3. **java.nio.charset 包中的枚举类：**
   
   - `StandardCharsets`: 提供了一些常见字符集的枚举常量。
   
   ```java
   StandardCharsets.UTF_8, StandardCharsets.ISO_8859_1, StandardCharsets.US_ASCII, ...
   ```
   
4. **java.time 包中的枚举类：**
   
   - `DayOfWeek`: 表示星期几。
   - `Month`: 表示月份。
   
   ```java
   DayOfWeek.MONDAY, DayOfWeek.TUESDAY, ..., Month.JANUARY, Month.FEBRUARY, ...
   ```
   
5. **java.util 包中的枚举类：**
   - `Locale`: 表示特定地理、政治或文化地区的标识。

   ```java
   Locale.US, Locale.CHINA, Locale.JAPAN, ...
   ```

6. **java.net 包中的枚举类：**
   
   - `HttpMethod`: 表示HTTP请求方法。
   
   ```java
   HttpMethod.GET, HttpMethod.POST, HttpMethod.PUT, ...
   ```
   
7. **java.sql 包中的枚举类：**
   - `JDBCType`: 表示Java数据库连接中的SQL类型。

   ```java
   JDBCType.INTEGER, JDBCType.VARCHAR, JDBCType.DATE, ...
   ```

8. **java.lang 包中的枚举类：**
   - `Thread.State`: 表示线程的状态。

   ```java
   Thread.State.NEW, Thread.State.RUNNABLE, Thread.State.BLOCKED, ...
   ```





