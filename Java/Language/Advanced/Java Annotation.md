# Java Annotation

## 概述

*Annotations*, a form of metadata, provide data about a program that is not part of the program itself. Annotations have no direct effect on the operation of the code they annotate.

注解以 `@` 符号开始，不能使用关键字extends来继承某个@interface，但注解在编译后，编译器会自动继承java.lang.annotation.Annotation接口

注解中可以包含元素，如果注解一个名称为value的元素，那么名称可以省略。

```java
@SuppressWarnings(value = "unchecked")
void myMethod() { ... }

@SuppressWarnings("unchecked")
void myMethod() { ... }
```

如果注解没有任何元素，那么()可以省略。

```java
@Override
void mySuperMethod() { ... }
```

同一个Java程序元素上（类、接口、构造器等）可以声明多个注解。

```java
@Author(name = "Jane Doe")
@EBook
class MyClass { ... }
```

## 注解的作用

- **Information for the compiler** — Annotations can be used by the compiler to detect errors or suppress warnings.

- **Compile-time and deployment-time processing** — Software tools can process annotation information to generate code, XML files, and so forth.
- **Runtime processing** — Some annotations are available to be examined at runtime.

## Meta Annotations

在Java中，元注解是用于注解其他注解的注解。元注解提供了对注解进行更精细控制的能力，可以用于自定义注解的行为。元注解定义在 `java.lang.annotation` 包下。

在JDK 1.5中提供了4个标准的元注解：`@Target`，`@Retention`，`@Documented`，`@Inherited`, 在JDK 1.8中提供了两个元注解 `@Repeatable`和`@Native`。

### @Documented

用于指定注解是否包含在JavaDoc中。如果一个注解使用了`@Documented`，则它会出现在生成的文档中。

### @Target

用于指定注解的作用目标，可以是类、方法、字段等。常用的值包括：

- `ElementType.TYPE`：类、接口、注解、枚举。
- `ElementType.METHOD`：方法。
- `ElementType.FIELD`：字段或属性。
- `ElementType.PARAMETER`：形参。
- `ElementType.CONSTRUCTOR`：构造器。
- `ElementType.ANNOTATION_TYPE`：注解。
- `ElementType.PACKAGE`：包。

### @Retention

用于指定注解的保留策略，有三个值可选：

- `RetentionPolicy.SOURCE`：注解仅在源代码中存在，编译时会被丢弃，比如 `@Override`。
- `RetentionPolicy.CLASS`：注解在编译时被保留在字节码文件中，但在运行时被JVM忽视而不可见（默认值）。
- `RetentionPolicy.RUNTIME`：注解在运行时可见。

编译器并没有记录下 sourcePolicy() 方法的注解信息；

编译器分别使用了 `RuntimeInvisibleAnnotations` 和 `RuntimeVisibleAnnotations` 属性去记录了`classPolicy()`方法 和 `runtimePolicy()`方法 的注解信息。

### @Inherited

用于指定注解是否可继承。如果一个父类被注解，且该注解使用了`@Inherited`，则子类默认也被该注解。此注解仅适用于类声明。

### @Native

使用 @Native 注解修饰成员变量，则表示这个变量可以被本地代码引用，常常被代码生成工具使用。

### @Repeatable

`@Repeatable` 注解是 Java 8 引入的元注解，用于支持重复注解。通过 `@Repeatable`，一个注解类型可以在同一程序元素上多次使用，而不需要嵌套在容器注解中。

在之前的Java版本中，同一元素上不能多次使用相同类型的注解，而使用了`@Repeatable`注解之后，可以让同一元素上多次使用相同类型的注解。

出于兼容性原因，重复注解存储在 Java 编译器自动生成的容器注解中。

容器注解类型必须具有数组类型的 `value` 元素。数组类型的元素类型必须是可重复的注解类型。

```java
// 定义重复注解的容器注解
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface MyRepeatedAnnotations {
    MyAnnotation[] value();
}

// 定义可重复注解
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@Repeatable(MyRepeatedAnnotations.class)
public @interface MyAnnotation {
    String value();
}

// 使用重复注解
@MyAnnotation("First")
@MyAnnotation("Second")
public class MyClass {
    // class body
}

// 获取重复注解的值
public class Main {
    public static void main(String[] args) {
        // 通过注解容器获取可重复注解
        MyAnnotations myAnnotations = MyClass.class.getAnnotation(MyAnnotations.class);
        
        // 直接获取可重复注解
        MyAnnotation[] annotations = MyClass.class.getAnnotationsByType(MyAnnotation.class);

        for (MyAnnotation annotation : annotations) {
            System.out.println(annotation.value());
        }
    }
}
```

## Built-in Annotations

### @SuppressWarnings

每个编译器警告都属于一个类别。 Java 语言规范列出了两个类别：`deprecation` and `unchecked`。当与泛型出现之前编写的遗留代码交互时，可能会出现未经检查的警告。

`@SuppressWarnings`注解用于抑制编译器产生的警告信息，可以应用于类、方法、字段等元素。在某些情况下，编译器可能会发出一些警告，但开发者知道这些警告是安全的或者是故意的，因此可以使用`@SuppressWarnings`来告诉编译器忽略这些警告。

`@SuppressWarnings`注解的使用方式如下：

```java
@SuppressWarnings("warning_type")
```

其中，`"warning_type"`是一个字符串参数，表示要抑制的警告类型。以下是一些常见的`@SuppressWarnings`参数值：

1. **"all"：**
   - 抑制所有警告，不推荐使用，因为可能会掩盖真正的问题。

   ```java
   @SuppressWarnings("all")
   ```

2. **"unchecked"：**
   - 抑制使用泛型时的未检查警告。

   ```java
   @SuppressWarnings("unchecked")
   ```

3. **"deprecation"：**
   - 抑制使用已过时的方法或类的警告。

   ```java
   @SuppressWarnings("deprecation")
   ```

4. **"rawtypes"：**
   - 抑制使用原始类型（raw types）的警告。

   ```java
   @SuppressWarnings("rawtypes")
   ```

5. **"serial"：**
   - 抑制没有声明序列化UID的类实现Serializable接口的警告。

   ```java
   @SuppressWarnings("serial")
   ```

6. **"unused"：**
   - 抑制未使用的元素的警告，例如未使用的变量、方法、字段等。

   ```java
   @SuppressWarnings("unused")
   ```

7. **"resource"：**
   
   - 抑制有关资源关闭的警告，例如未关闭的`AutoCloseable`对象。
   
   ```java
   @SuppressWarnings("resource")
   ```

### @FunctionalInterface

`@FunctionalInterface`是Java 8引入的标记注解，用于标识一个接口是函数式接口。函数式接口是一个只包含一个抽象方法的接口，它可以被Lambda表达式或方法引用所使用。`@FunctionalInterface`注解是可选的，但它会帮助编译器检查该接口是否符合函数式接口的规定。

一个函数式接口必须满足以下条件：

1. 仅包含一个抽象方法（可以有默认方法和静态方法）。
2. 用`@FunctionalInterface`注解标识。

```java
@FunctionalInterface
public interface MyFunctionalInterface {
    void myMethod();
}
```

### @Override

通知编译器该元素将覆盖超类中声明的元素。

虽然重写方法时不需要使用此注释，但它有助于防止错误。如果标有 @Override 的方法无法正确重写其超类之一中的方法，则编译器会生成错误。

### @Deprecated

表明标记的元素已被弃用，不应再使用。每当程序使用带有 @Deprecated 注解的方法、类或字段时，编译器都会生成警告。

### @SafeVarargs

当应用于方法或构造函数时，保证代码不会对其 varargs 参数执行潜在的不安全操作。使用此注解类型时，将抑制与可变参数使用相关的未经检查的警告。

## Custom Annotations

在Java中，自定义注解是通过使用`@interface`关键字来创建的。

1. 使用 `@interface` 关键字定义注解，并指定注解的元素。

2. 在注解中定义元素，元素类似于接口的方法，可以有默认值。

3. 在需要使用注解的地方通过反射读取注解信息。

```java
import java.lang.annotation.*;

// 定义自定义注解
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyAnnotation {
    String value() default "Default Value";
    int count() default 0;
}

// 使用自定义注解
public class MyClass {

    @MyAnnotation(value = "Hello Annotation", count = 42)
    public void myMethod() {
        // Method body
    }

    public static void main(String[] args) {
        // 获取注解信息
        MyClass obj = new MyClass();
        try {
            // 获取方法上的注解
            MyAnnotation annotation = obj.getClass()
                    .getMethod("myMethod")
                    .getAnnotation(MyAnnotation.class);

            // 输出注解元素的值
            System.out.println("Value: " + annotation.value());
            System.out.println("Count: " + annotation.count());
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        }
    }
}
```

在上面的例子中，首先通过`@interface`定义了一个名为`MyAnnotation`的自定义注解，并在注解中定义了两个元素：`value`和`count`。然后，在`MyClass`类的`myMethod`方法上使用了`@MyAnnotation`注解。

在`main`方法中，通过反射获取了`myMethod`方法上的注解，并输出了注解元素的值。自定义注解可以用于标记和配置代码，充分发挥了元数据的作用。

## Annotation Processor

### AnnotatedElement

AnnotatedElement 接口是所有程序元素（Class、Method和Constructor）的父接口，在Java中，`AnnotatedElement` 接口是一个用于表示具有注解的程序元素（如类、方法、字段等）的通用接口。`AnnotatedElement` 接口提供了一系列用于获取注解信息的方法。以下是 `AnnotatedElement` 接口的主要方法：

1. **getAnnotation(Class<T> annotationClass)：**获取指定类型的注解。如果指定类型的注解不存在，则返回 `null`。
   
   ```java
   <T extends Annotation> T getAnnotation(Class<T> annotationClass);
   ```
   
2. **getAnnotations()：**获取所有注解的数组。返回一个包含所有注解的 `Annotation[]` 数组。
   
   ```java
   Annotation[] getAnnotations();
   ```
   
3. **getDeclaredAnnotation(Class<T> annotationClass)：**获取指定类型的注解，仅包括直接声明在此元素上的注解（不包括继承的注解）。
   
   ```java
   <T extends Annotation> T getDeclaredAnnotation(Class<T> annotationClass);
   ```
   
4. **getDeclaredAnnotations()：**获取所有直接声明在此元素上的注解的数组，不包括继承的注解。
   
   ```java
   Annotation[] getDeclaredAnnotations();
   ```
   
5. **isAnnotationPresent(Class<? extends Annotation> annotationClass)：**判断是否存在指定类型的注解。
   
   ```java
   boolean isAnnotationPresent(Class<? extends Annotation> annotationClass);
   ```

通过使用 `AnnotatedElement` 接口提供的这些方法，可以在运行时检查程序元素上的注解，并获取相应的注解信息。这对于实现自定义注解处理器或者实现某些框架功能时非常有用。这些方法的使用通常涉及到 Java 的反射机制。

## 注解中的元素数据类型

在Java中，注解（Annotation）本身不能直接定义数据类型。注解是一种用于提供元数据的结构，它们通常用于向Java代码中添加关于程序结构、行为或其他相关信息的额外信息。

注解中可以定义的元素（成员）的数据类型是有限的，Java语言规范中规定了几种基本的数据类型，以及这些数据类型的数组形式。

1. **所有基本数据类型：**`int`, `short`, `long`, `float`, `double`, `byte`, `char`, `boolean`
   
2. **字符串（String）：**`String`
   
3. **枚举（Enum）：**可以使用枚举类型作为注解元素的数据类型。
   
   ```java
   public @interface MyAnnotation {
       MyEnumType value();
   }
   ```
   
4. **Class 类型：**`Class` 类型，表示一个Java类。
   
   ```java
   public @interface MyAnnotation {
       Class<?> clazz();
   }
   ```
   
5. **数组：**以上任何一种类型都可以声明为数组。
   
   ```java
   public @interface MyAnnotation {
       int[] values();
       String[] names();
   }
   ```

注意：在注解中，元素的类型受到一些限制，例如不能使用包装类型，只能使用基本数据类型；也不能使用 `void` 类型等。同时，元素的值必须是常量表达式，不能是运行时计算得到的值。
