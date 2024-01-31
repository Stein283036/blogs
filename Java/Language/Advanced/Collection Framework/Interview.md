# Collection Framework Interview

## Java集合的遍历的方式有哪些？

**Iterator遍历**:

- 使用Iterator接口的实现类，可以遍历集合中的元素。这是最传统、最通用的遍历方式。

**For-Each循环**:

- For-Each循环是一种简洁的语法糖，用于遍历数组和实现Iterable接口的集合。

**Lambda表达式**:

- 使用Java 8引入的Lambda表达式，可以更简洁地遍历集合。

**Stream API**:

- 使用Java 8引入的Stream API，可以进行更灵活的集合处理操作。

**parallelStream方法**:

- Java 8引入的`parallelStream`方法允许集合并行处理，适用于大数据量的情况。

## jdk1.7到jdk1.8 Map发生了什么变化(底层)?

1.8之后hashMap的数据结构发生了变化，从之前的单纯的数组+链表结构变成数组+链表+红黑树。也就是说在JVM存储hashMap的K-V时仅仅通过key来决定每一个entry的存储槽位（Node[]中的index）。并且Value以链表的形式挂在到对应槽位上（1.8以后如果value长度大于8则转为红黑树）。

但是hashmap1.7跟1.8 中都没有任何同步操作，容易出现并发问题，甚至出现死循环导致系统不可用。解决方案是jdk的ConcurrentHashMap，位于java.util.concurrent下，专门解决并发问题。

## ConcurrentHashMap

## ArrayList 和 LinkedList 的区别

## HashMap 和 HashTable 的区别

- HashTable 不允许 key 或 value 为 null，HashMap 允许
- HashTable 是线程安全的，HashMap 不是
- HashTable 是一个遗留类，不建议使用
- HashMap 是 fail-fast 的，HashTable 不是

## Collections 集合工具类

## HashSet 的底层原理

基于 HashMap 实现的。

## 如何实现数组和 List 之间的互换

## Iterator 的 fail-fast 机制

## Iterator 和 ListIterator 有什么区别

- Iterator 可以遍历 List 和 Set 集合，而 ListIterator 只能遍历 List 集合
- Iterator 只能单向遍历，而 ListIterator 可以双向遍历
- ListIterator 从 Iterator 接口继承，具有额外的其它功能

## 怎么确保一个集合不能被修改

可以使用 Collections.unmodifiable() 方法获取一个不可以修改的集合，任何修改集合的操作都会导致 `UnsupportedOperationException` 异常。

