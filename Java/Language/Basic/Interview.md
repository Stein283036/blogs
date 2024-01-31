# Java Language Interview

## 创建 Java 对象的方式有哪些

- `new` 关键字
- 反射，`Class.forName()`
- `clone()` 方法，对象实现 `Cloneable` 接口并重写 `clone()` 方法，可以通过对象的 `clone()` 方法创建对象的一个副本。
- 反序列化，对象实现 `Serializable` 接口，可以通过反序列化的方式创建对象。
- 工厂方法模式

## hashcode() 和 equals 的区别

## == 和 equals 的区别

## Java 中的 Math. round(-1. 5) 等于多少

-1

## 对象克隆的方式有哪些

## **怎样将 GB2312 编码的字符串转换为 ISO-8859-1 编码的字符串**

String s1 = "你好";

String s2 = newString(s1.getBytes("GB2312"), "ISO-8859-1");

