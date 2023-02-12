# 常用类（API）

## Number && Math

## Collections

## Arrays

- fill 填充数组
- sort 排序
- binarySearch 二分查找
- equals 比较数组的元素值是否相等
- copyOf 复制数组并返回一个新容量的数组

## 日期类

### Date

常用方法

|  1   | **boolean after(Date date)** 若当调用此方法的Date对象在指定日期之后返回true,否则返回false。 |
| :--: | :----------------------------------------------------------: |
|  2   | **boolean before(Date date)** 若当调用此方法的Date对象在指定日期之前返回true,否则返回false。 |
|  3   |            **Object clone( )** 返回此对象的副本。            |
|  4   | **int compareTo(Date date)** 比较当调用此方法的Date对象和指定日期。两者相等时候返回0。调用对象在指定日期之前则返回负数。调用对象在指定日期之后则返回正数。 |
|  5   | **int compareTo(Object obj)** 若obj是Date类型则操作等同于compareTo(Date) 。否则它抛出ClassCastException。 |
|  6   | **boolean equals(Object date)** 当调用此方法的Date对象和指定日期相等时候返回true,否则返回false。 |
|  7   | **long getTime( )** 返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。 |
|  8   |         **int hashCode( )**  返回此对象的哈希码值。          |
|  9   | **void setTime(long time)**   用自1970年1月1日00:00:00 GMT以后time毫秒数设置时间和日期。 |
|  10  | **String toString( )** 把此 Date 对象转换为以下形式的 String： dow mon dd hh:mm:ss zzz yyyy 其中： dow 是一周中的某一天 (Sun, Mon, Tue, Wed, Thu, Fri, Sat)。 |

**日期比较**

- 使用 getTime() 方法获取两个日期（自1970年1月1日经历的毫秒数值），然后比较这两个值。
- 使用方法 before()，after() 和 equals()。例如，一个月的12号比18号早，则 new Date(99, 2, 12).before(new Date (99, 2, 18)) 返回true。
- 使用 compareTo() 方法，它是由 Comparable 接口定义的，Date 类实现了这个接口。

**使用 SimpleDateFormat 格式化日期**

SimpleDateFormat 是一个以语言环境敏感的方式来格式化和分析日期的类。SimpleDateFormat 允许你选择任何用户自定义日期时间格式来运行。具体的日期格式化查看类文档就行。

### Calendar

设置和获取日期数据的特定部分呢，比如说小时，日，或者分钟? 我们又如何在日期的这些部分加上或者减去值呢? 答案是使用Calendar 类。

Calendar类的功能要比Date类强大很多，而且在实现方式上也比Date类要复杂一些。

Calendar类是一个抽象类，在实际使用时实现特定的子类的对象，创建对象的过程对程序员来说是透明的，只需要使用getInstance方法创建即可。

**Calendar类对象字段类型**

|         常量          |              描述              |
| :-------------------: | :----------------------------: |
|     Calendar.YEAR     |              年份              |
|    Calendar.MONTH     |              月份              |
|     Calendar.DATE     |              日期              |
| Calendar.DAY_OF_MONTH | 日期，和上面的字段意义完全相同 |
|     Calendar.HOUR     |         12小时制的小时         |
| Calendar.HOUR_OF_DAY  |         24小时制的小时         |
|    Calendar.MINUTE    |              分钟              |
|    Calendar.SECOND    |               秒               |
| Calendar.DAY_OF_WEEK  |             星期几             |

## BigInteger

在Java中，由CPU原生提供的整型最大范围是64位`long`型整数。使用`long`型整数可以直接通过CPU指令进行计算，速度非常快。

如果我们使用的整数范围超过了`long`型怎么办？这个时候，就只能用软件来模拟一个大整数。`java.math.BigInteger`就是用来表示任意大小的整数。`BigInteger`内部用一个`int[]`数组来模拟一个非常大的整数。

对`BigInteger`做运算的时候，只能使用实例方法。

和`long`型整数运算比，`BigInteger`不会有范围限制，但缺点是速度比较慢。

## BigDecimal

`BigDecimal`可以表示一个任意大小且精度完全准确的浮点数。

`BigDecimal`用`scale()`表示小数位数。

通过`BigDecimal`的`stripTrailingZeros()`方法，可以将一个`BigDecimal`格式化为一个相等的，但去掉了末尾0的`BigDecimal`。

对`BigDecimal`做加、减、乘时，精度不会丢失，但是做除法时，存在无法除尽的情况，这时就必须指定精度以及如何进行截断。

比较两个`BigDecimal`的值是否相等时，要特别注意，使用`equals()`方法不但要求两个`BigDecimal`的值相等，还要求它们的`scale()`相等。

必须使用`compareTo()`方法来比较，它根据两个值的大小分别返回负数、正数和`0`，分别表示小于、大于和等于。