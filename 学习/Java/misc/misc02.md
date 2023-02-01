# misc02

对于 Java 的平台无关性的支持是分布在整个 Java 体系结构中的。其中扮演着重要角色的有 Java 语言规范、Class 文件、Java 虚拟机等。

- Java 语言规范
  - 通过规定 Java 语言中基本数据类型的取值范围和行为
- Class 文件
  - 所有 Java 文件要编译成统一的 Class 文件
- Java 虚拟机
  - 通过 Java 虚拟机将 Class 文件转成对应平台的二进制文件等

Java 的平台无关性是建立在 Java 虚拟机的平台有关性基础之上的，是因为 Java 虚拟机屏蔽了底层操作系统和硬件的差异。

**传值调用是指在调用函数时将实际参数`复制`一份传递到函数中，传引用调用是指在调用函数时将实际参数的引用`直接`传递到函数中。**

![pass-by-reference-vs-pass-by-value-animation](http://www.hollischuang.com/wp-content/uploads/2020/04/pass-by-reference-vs-pass-by-value-animation.gif)

这里我们来举一个形象的例子。再来深入理解一下传值调用和传引用调用：

你有一把钥匙，当你的朋友想要去你家的时候，如果你`直接`把你的钥匙给他了，这就是引用传递。

这种情况下，如果他对这把钥匙做了什么事情，比如他在钥匙上刻下了自己名字，那么这把钥匙还给你的时候，你自己的钥匙上也会多出他刻的名字。

你有一把钥匙，当你的朋友想要去你家的时候，你`复刻`了一把新钥匙给他，自己的还在自己手里，这就是值传递。

这种情况下，他对这把钥匙做什么都不会影响你手里的这把钥匙。

**参数传递**

传值调用（值传递）
在传值调用中，实际参数先被求值，然后其值通过复制，被传递给被调函数的形式参数。因为形式参数拿到的只是一个"局部拷贝"，所以如果在被调函数中改变了形式参数的值，并不会改变实际参数的值。
传引用调用（引用传递）
在传引用调用中，传递给函数的是它的实际参数的隐式引用而不是实参的拷贝。因为传递的是引用，所以，如果在被调函数中改变了形式参数的值，改变对于调用者来说是可见的。
传共享对象调用（共享对象传递）
传共享对象调用中，先获取到实际参数的地址，然后将其复制，并把该地址的拷贝传递给被调函数的形式参数。因为参数的地址都指向同一个对象，所以我们称也之为"传共享对象"，所以，如果在被调函数中改变了形式参数的值，调用者是可以看到这种变化的。

很多人说 Java 中的基本数据类型是值传递的，这个基本没有什么可以讨论的，普遍都是这样认为的。

但是，有很多人却误认为 Java 中的对象传递是引用传递。之所以会有这个误区，主要是因为 Java 中的变量和对象之间是有引用关系的。Java 语言中是通过对象的引用来操纵对象的。所以，很多人会认为对象的传递是引用的传递。

很多人通过代码示例的现象说明 Java 对象是引用传递，那么我们就从现象入手，先来反驳下这个观点。

我们前面说过，无论是值传递，还是引用传递，只不过是求值策略的一种，那求值策略还有很多，比如前面提到的共享对象传递的现象和引用传递也是一样的。那凭什么就说 Java 中的参数传递就一定是引用传递而不是共享对象传递呢？

那么，Java 中的对象传递，到底是哪种形式呢？其实，还真的就是共享对象传递。

其实在 《The Java™ Tutorials》中，是有关于这部分内容的说明的。首先是关于基本类型描述如下：

> Primitive arguments, such as an int or a double, are passed into methods by value. This means that any changes to the values of the parameters exist only within the scope of the method. When the method returns, the parameters are gone and any changes to them are lost.

**即，原始参数通过值传递给方法。这意味着对参数值的任何更改都只存在于方法的范围内。当方法返回时，参数将消失，对它们的任何更改都将丢失。**

关于对象传递的描述如下：

> Reference data type parameters, such as objects, are also passed into methods by value. This means that when the method returns, the passed-in reference still references the same object as before. However, the values of the object’s fields can be changed in the method, if they have the proper access level.

**也就是说，引用数据类型参数(如对象)也按值传递给方法。这意味着，当方法返回时，传入的引用仍然引用与以前相同的对象。但是，如果对象字段具有适当的访问级别，则可以在方法中更改这些字段的值。**

这一点官方文档已经很明确的指出了，Java 就是值传递，只不过是把对象的引用当做值传递给方法。

**其实 Java 中使用的求值策略就是传共享对象调用，也就是说，Java 会将对象的地址的拷贝传递给被调函数的形式参数。**只不过"传共享对象调用"这个词并不常用，所以 Java 社区的人通常说"Java 是传值调用"，这么说也没错，因为传共享对象调用其实是传值调用的一个特例。

十进制小数转换成二进制小数，又该如何计算呢？

十进制小数转换成二进制小数采用"乘 2 取整，顺序排列"法。

具体做法是：

- 用 2 乘十进制小数，可以得到积
- 将积的整数部分取出，再用 2 乘余下的小数部分，又得到一个积
- 再将积的整数部分取出，如此进行，直到积中的小数部分为零，此时 0 或 1 为二进制的最后一位。或者达到所要求的精度为止。

如尝试将 0.625 转成二进制：

![-w624](https://www.hollischuang.com/wp-content/uploads/2020/10/16024172361526.jpg)

但是 0.625 是一个特列，用同样的算法，请计算下 0.1 对应的二进制是多少：

![-w624](https://www.hollischuang.com/wp-content/uploads/2020/10/16024175486626.jpg)

我们发现，0.1 的二进制表示中出现了无限循环的情况，也就是(0.1)10 = (0.000110011001100…)2

这种情况，计算机就没办法用二进制精确的表示 0.1 了。

所以，为了解决部分小数无法使用二进制精确表示的问题，于是就有了 IEEE 754 规范。

IEEE 二进制浮点数算术标准（IEEE 754）是 20 世纪 80 年代以来最广泛使用的浮点数运算标准，为许多 CPU 与浮点运算器所采用。

> 浮点数和小数并不是完全一样的，计算机中小数的表示法，其实有定点和浮点两种。因为在位数相同的情况下，定点数的表示范围要比浮点数小。所以在计算机科学中，使用浮点数来表示实数的近似值。

IEEE 754 规定了四种表示浮点数值的方式：单精确度（32 位）、双精确度（64 位）、延伸单精确度（43 比特以上，很少使用）与延伸双精确度（79 比特以上，通常以 80 位实现）。

其中最常用的就是 32 位单精度浮点数和 64 位双精度浮点数。

IEEE 并没有解决小数无法精确表示的问题，只是提出了一种使用近似值表示小数的方式，并且引入了精度的概念。

一个浮点数 a 由两个数 m 和 e 来表示：a = m × b^e。

自动装箱都是通过包装类的 valueOf() 方法来实现的.自动拆箱都是通过包装类对象的 xxxValue() 来实现的。

**哪些地方会自动拆装箱**

1. 将基本数据类型添加进集合中

2. 和基本数据类型进行比较时

3. 包装类型的运算

4. 三目运算符的使用

   ```java
   boolean flag = true;
       Integer i = 0;
       int j = 1;
       int k = flag ? i : j;复制ErrorOK!
   ```

   很多人不知道，其实在 `int k = flag ? i : j;` 这一行，会发生自动拆箱（ JDK1.8 之前，详见：[《阿里巴巴 Java 开发手册-泰山版》提到的三目运算符的空指针问题到底是个怎么回事？](https://www.hollischuang.com/archives/4749) ）。

   反编译后代码如下：

   ```java
       boolean flag = true;
       Integer i = Integer.valueOf(0);
       int j = 1;
       int k = flag ? i.intValue() : j;
       System.out.println(k);复制ErrorOK!
   ```

   这其实是三目运算符的语法规范。当第二，第三位操作数分别为基本类型和对象时，其中的对象就会拆箱为基本类型进行操作。

   因为例子中，`flag ? i : j;` 片段中，第二段的 i 是一个包装类型的对象，而第三段的 j 是一个基本类型，所以会对包装类进行自动拆箱。如果这个时候 i 的值为 `null`，那么就会发生 NPE。

5. 函数参数与返回值

   ```java
     //自动拆箱
       public int getNum1(Integer num) {
        return num;
       }
       //自动装箱
       public Integer getNum2(int num) {
        return num;
       }
   ```

当需要进行自动装箱时，如果数字在 -128 至 127 之间时，会直接使用缓存中的对象，而不是重新创建一个对象。

在 Boxing Conversion 部分的 Java 语言规范(JLS)规定如下：

如果一个变量 p 的值是：

- -128 至 127 之间的整数 (§3.10.1)
- true 和 false 的布尔值 (§3.10.3)
- `\u0000` 至 `\u007f` 之间的字符 (§3.10.4)

范围内的时，将 p 包装成 a 和 b 两个对象时，可以直接使用 a == b 判断 a 和 b 的值是否相等。

Byte, Short, Long 有固定范围: -128 到 127。对于 Character, 范围是 0 到 127。除了 Integer 以外，这个范围都不能改变。

内存泄露：在计算机科学中，内存泄漏指由于疏忽或错误造成程序未能释放已经不再使用的内存。 内存泄漏并非指内存在物理上的消失，而是应用程序分配某段内存后，由于设计错误，导致在释放该段内存之前就失去了对该段内存的控制，从而造成了内存的浪费。

运算符重载：在计算机程序设计中，运算符重载（英语：operator overloading）是多态的一种。运算符重载，就是对已有的运算符重新进行定义，赋予其另一种功能，以适应不同的数据类型。

语法糖：语法糖（Syntactic sugar），也译为糖衣语法，是由英国计算机科学家彼得·兰丁发明的一个术语，指计算机语言中添加的某种语法，这种语法对语言的功能没有影响，但是更方便程序员使用。语法糖让程序更加简洁，有更高的可读性。

使用+拼接字符串，其实只是 Java 提供的一个语法糖， 那么，我们就来解一解这个语法糖，看看他的内部原理到底是如何实现的。

还是这样一段代码。我们把他生成的字节码进行反编译，看看结果。

```markup
String wechat = "Hollis";
String introduce = "每日更新Java相关技术文章";
String hollis = wechat + "," + introduce;复制ErrorOK!
```

反编译后的内容如下，反编译工具为 jad。

```markup
String wechat = "Hollis";
String introduce = "\u6BCF\u65E5\u66F4\u65B0Java\u76F8\u5173\u6280\u672F\u6587\u7AE0";//每日更新Java相关技术文章
String hollis = (new StringBuilder()).append(wechat).append(",").append(introduce).toString();复制ErrorOK!
```

通过查看反编译以后的代码，我们可以发现，原来字符串常量在拼接过程中，是将 String 转成了 StringBuilder 后，使用其 append 方法进行处理的。

那么也就是说，Java 中的+对字符串的拼接，其实现原理是使用 StringBuilder.append。

但是，String 的使用+字符串拼接也不全都是基于 StringBuilder.append，还有种特殊情况，那就是如果是两个固定的字面量拼接，如：

```markup
String s = "a" + "b"复制ErrorOK!
```

编译器会进行常量折叠(因为两个都是编译期常量，编译期可知)，直接变成 String s = "ab"。

scope=compile 的情况（默认 scope),也就是说这个项目在编译，测试，运行阶段都需要这个 artifact(模块)对应的 jar 包在 classpath 中。

对于 scope=provided 的情况，则可以认为这个 provided 是目标容器已经 provide 这个 artifact。换句话说，它只影响到编译，测试阶段。在编译测试阶段，我们需要这个 artifact 对应的 jar 包在 classpath 中。

snapshot 快照，alpha 内部测试，beta 公测，release 稳定，GA 正式发布。

方法区是**逻辑概念**，而永久代、元空间都是方法区的实现。JDK1.8 中取消了永久代，区而代之使用了元空间来实现方法区。

在 JDK1.8 中，把 JDK 7 中永久代还剩余的内容（主要是类型信息）全部移到元空间中。注意这里的剩余内容：即字符串常量池，静态常量，在 JDK1.8 中，并不属于元空间。
在 JDK1.8 中，使用元空间代替永久代来实现方法区，但是方法区并没有改变，变动的只是方法区中内容的物理存放位置。正如上面所说，类型信息（元数据信息）等其他信息被移动到了元空间中；但是运行时常量池和字符串常量池被移动到了堆中。

Key Features of Stack Memory
Some other features of stack memory include:

It grows and shrinks as new methods are called and returned, respectively.
Variables inside the stack exist only as long as the method that created them is running.
It's automatically allocated and deallocated when the method finishes execution.
If this memory is full, Java throws java.lang.StackOverFlowError.
Access to this memory is fast when compared to heap memory.
This memory is threadsafe, as each thread operates in its own stack.

Heap space is used for the dynamic memory allocation of Java objects and JRE classes at runtime. New objects are always created in heap space, and the references to these objects are stored in stack memory.

These objects have global access and we can access them from anywhere in the application.

We can break this memory model down into smaller parts, called generations, which are:

Young Generation – this is where all new objects are allocated and aged. A minor Garbage collection occurs when this fills up.
Old or Tenured Generation – this is where long surviving objects are stored. When objects are stored in the Young Generation, a threshold for the object's age is set, and when that threshold is reached, the object is moved to the old generation.
Permanent Generation – this consists of JVM metadata for the runtime classes and application methods.

Key Features of Java Heap Memory
Some other features of heap space include:

It's accessed via complex memory management techniques that include the Young Generation, Old or Tenured Generation, and Permanent Generation.
If heap space is full, Java throws java.lang.OutOfMemoryError.
Access to this memory is comparatively slower than stack memory
This memory, in contrast to stack, isn't automatically deallocated. It needs Garbage Collector to free up unused objects so as to keep the efficiency of the memory usage.
Unlike stack, a heap isn't threadsafe and needs to be guarded by properly synchronizing the code.

intern()版本区别
jdk1.6 中，将这个字符串对象尝试放入串池。

如果串池中有，则并不会放入。返回已有的串池中的对象的地址
如果没有，会把此对象复制一份，放入串池，并返回串池中的对象地址

Jdk1.7 起，将这个字符串对象尝试放入串池。

如果串池中有，则并不会放入。返回已有的串池中的对象的地址
如果没有，则会把堆中对象的引用地址复制一份，放入串池，并返回串池中的引用地址

new String("a") + new String("b") 创建几个对象？

StringBuilder.toString()也是通过 new String(value, 0, count)创建 String 对象，toString()字节码如下：

new String(value, 0, count)和 new String("a")字节码指令是不同的。new String(value, 0, count)里的 value 为变量，不会在字符串常量池放一份字符串对象，而 new String("a")是显式的‘a’参数传入的，是字符串常量，会在常量池中放一份“a”（为什么是放值而不是引用？：因为“a”的字节码命令是在调用构造器之前的，相当于 new 之前就有字面量“a”了）

对象 1：new StringBuilder()
对象 2： new String("a")
对象 3： 常量池中的"a"
对象 4： new String("b")
对象 5： 常量池中的"b"
对象 6 ：new String("ab") （深入剖析： StringBuilder 的 toString()相当于： 变量=“ab” ;new String(变量)，在字符串常量池中，没有生成"ab"）

//new String("ab") 执行完以后，字符串常量池中并没有"ab"
String s = new String("a") + new String("b");

            //jdk6中：在串池中创建一个字符串"ab"
            //jdk8中：字符串池中没有创建字符串"ab",而是创建一个引用，指向new String("ab")，将此引用返回
            String s2 = s.intern();

            System.out.println(s2 == "ab");//jdk6:true  jdk8:true
            System.out.println(s == "ab");//jdk6:false  jdk8:true
            System.out.println(s == s2);//jdk8:true

JVM 总是动态加载 class，可以在运行期根据条件来控制加载 class。

setAccessible(true)可能会失败。如果 JVM 运行期存在 SecurityManager，那么它会根据规则进行检查，有可能阻止 setAccessible(true)。例如，某个 SecurityManager 可能不允许对 java 和 javax 开头的 package 的类调用 setAccessible(true)，这样可以保证 JVM 核心库的安全。
