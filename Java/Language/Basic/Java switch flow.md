# Java switch flow

switch 比较时进行类型转换。

String 类型先比较 hashCode，在比较 equals 方法。

**其实 switch flow 只支持一种数据类型，那就是整型，其他数据类型都是转换成整型之后再使用 switch 的。**

枚举……。

从 Java 7 开始，我们可以在 switch case 中使用字符串，但这仅仅是一个语法糖。内部实现在 switch 中使用字符串的 hash code。

枚举比较的是 ordinal 方法的值。