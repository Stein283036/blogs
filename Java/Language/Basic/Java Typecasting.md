# Java Typecasting

## **隐式类型转换（向上类型转换）**

因为 Java 默认的数值类型是 int，因此在将 char、byte、short 和 int 一起运算时，会进行隐式地类型转换，将运算结果转换为 int 型。

```java
byte n1 = 1;
byte n2 = n1 + 1; // wrong
byte n1 = 1;
n1 += 2; // 隐式类型转换 (int) ((byte)1 + (int)2)
```

总之，表达式的结果是参与表达式计算的最大值的类型。

**三元表达式的类型转换**



## 强制类型转换（向下类型转换）

