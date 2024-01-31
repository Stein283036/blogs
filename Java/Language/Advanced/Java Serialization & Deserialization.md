# Java Serialization & Deserialization

## 概述

**序列化（Serialization）** 指的是将对象在程序中保存的状态通过持久化技术如IO、网络传输、数据库存储等将内存中临时的数据转换成字节流写入到长期存储的媒介中，以此来保存对象的状态并为以后需要时恢复。

反序列化就是相当于序列化而言，将字节流转换为对象的过程。

类 ObjectInputStream 和 ObjectOutputStream 是高层次的数据流，它们包含反序列化和序列化对象的方法。

Serializable 是 Java 提供的一个标记接口，用来表示一个类是否具备序列化的能力，如果一个类想要具备序列化的能力，那么必须实现该接口，否则在运行期 JVM 会检测出错误并抛出 NotSerializableException 异常。

对于引用类型需要被序列化的话那么也需要实现序列化接口，否则序列化和反序列时都会抛出异常，导致序列化过程失败。

## 作用

1. **对象的持久化：** 将对象转换为字节流后，可以将这些字节保存到文件、数据库或者通过网络传输。这使得对象的状态能够被永久性地保存下来。
2. **远程通信：** 在分布式系统中，可以通过序列化和反序列化在网络上传递对象，实现远程通信。
3. **对象的克隆：** 通过序列化和反序列化，可以实现对象的深拷贝，而不是简单的引用拷贝。

## transient

transient 修饰的成员变量不会参与序列化过程，在反序列化的时候会被赋予该类型的默认值。

**一个静态变量不管是否被 transient 修饰，均不能被序列化。**

## ObjectInputStream 和 ObjectOutputStream

ObjectInputStream 的 readObject() 方法用来从输入流中读取保存的对象状态，以此来恢复对象，即是反序列化的过程。

ObjectOutputStream 的 writeObject() 方法用来将对象的状态写入到输出流中，是序列化的过程。

writeObject0的方法实现

```java
private void writeObject0(Object obj, boolean unshared) throws IOException {
      ...
    if (obj instanceof String) { 
        writeString((String) obj, unshared);
    } else if (cl.isArray()) { 
        writeArray(obj, desc, unshared);
    } else if (obj instanceof Enum) {
        writeEnum((Enum) obj, desc, unshared);
    } else if (obj instanceof Serializable) {
        writeOrdinaryObject(obj, desc, unshared);
    } else {
        if (extendedDebugInfo) {
            throw new NotSerializableException(cl.getName() + "\n"
                    + debugInfoStack.toString());
        } else {
            throw new NotSerializableException(cl.getName());
        }
    }
    ...
} 
```

从上述代码可知，如果被写对象的类型是 String，或数组，或 Enum，或 Serializable，那么就可以对该对象进行序列化，否则将抛出 NotSerializableException。

## serialVersionUID

如果可序列化类未显式声明 serialVersionUID，则序列化运行时将基于该类的各个方面计算该类的默认 serialVersionUID 值。原因是计算默认的 serialVersionUID 对类的详细信息具有较高的敏感性，根据编译器实现的不同可能千差万别，这样在反序列化过程中可能会导致意外的 InvalidClassException。

如果缺少 serialVersionUID ，那么编译器在序列化和反序列化的时候每次都会根据类的结构信息计算新的 serialVersionUID 值，即如果在序列化一个对象后给该对象的类添加了一个新的字段且没有指定 serialVersionUID 值的话，那么在反序列化的时候则会抛出 InvalidClassException，并指出反序列化的 serialVersionUID 和本地的 serialVersionUID 不一致，如果指定了 serialVersionUID，那么就不会出现这种错误，恢复的状态也是和序列化时的状态一致。

## ArrayList 中的使用

查看 ArrayList 的序列化和反序列化方法

transient Object[] elementData; 保存元素的数组使用了 transient 修饰，因为这样在序列化和反序列化的时候就可以自定义需要保存和元素个数和需要恢复的元素个数，因为有可能数组的容量有剩余，即没有存储元素。

**ArrayList 的反序列化方法**

```java
private void readObject(java.io.ObjectInputStream s)
    throws java.io.IOException, ClassNotFoundException {
    elementData = EMPTY_ELEMENTDATA;

    // Read in size, and any hidden stuff
    s.defaultReadObject();

    // Read in capacity
    s.readInt(); // ignored

    if (size > 0) {
        // be like clone(), allocate array based upon size not capacity
        int capacity = calculateCapacity(elementData, size);
        SharedSecrets.getJavaOISAccess().checkArray(s, Object[].class, capacity);
        ensureCapacityInternal(size);

        Object[] a = elementData;
        // Read in all elements in the proper order.
        for (int i=0; i<size; i++) {
            a[i] = s.readObject();
        }
    }
}
```

**ArrayList 的序列化方法**

```java
private void writeObject(java.io.ObjectOutputStream s)
    throws java.io.IOException{
    // Write out element count, and any hidden stuff
    int expectedModCount = modCount;
    s.defaultWriteObject();

    // Write out size as capacity for behavioural compatibility with clone()
    s.writeInt(size);

    // Write out all elements in the proper order.
    for (int i=0; i<size; i++) {
        s.writeObject(elementData[i]);
    }

    if (modCount != expectedModCount) {
        throw new ConcurrentModificationException();
    }
}
```

## Serializable 和 Externalizable 的区别

`Serializable` 和 `Externalizable` 是 Java 中用于实现对象序列化和反序列化的两种接口。它们之间有一些重要的区别，主要涉及序列化的控制、灵活性、性能和使用方式。

### Serializable 接口：

1. **自动序列化和反序列化：**
   - `Serializable` 接口是一个标记接口，不包含任何方法。类实现了 `Serializable` 接口后，对象的序列化和反序列化过程将由 Java 运行时自动处理。

   ```java
   import java.io.Serializable;
   
   public class MyClass implements Serializable {
       // 类的成员和方法
   }
   ```

2. **默认序列化：**
   - 默认情况下，所有非`transient`修饰的成员变量都会被序列化。子类中如果有父类实现了 `Serializable` 接口，也会被自动序列化。

   ```java
   private int age;
   private String name;
   ```

3. **版本控制：**
   
   - 可以通过 `serialVersionUID` 显式声明版本号，确保序列化和反序列化的兼容性。
   
   ```java
   private static final long serialVersionUID = 1L;
   ```

### Externalizable 接口：

1. **手动实现序列化和反序列化逻辑：**
   - `Externalizable` 接口继承了 `Serializable` 接口，但是要求实现 `writeExternal` 和 `readExternal` 方法，程序员需要手动指定序列化和反序列化的逻辑。

   ```java
   import java.io.Externalizable;
   import java.io.IOException;
   import java.io.ObjectInput;
   import java.io.ObjectOutput;
   
   public class MyClass implements Externalizable {
       // 实现 Externalizable 接口的方法
       @Override
       public void writeExternal(ObjectOutput out) throws IOException {
           // 序列化逻辑
       }
   
       @Override
       public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
           // 反序列化逻辑
       }
   }
   ```

2. **自定义序列化：**
   
   - `Externalizable` 接口提供更高度的自定义序列化和反序列化，可以选择性地保存对象的哪些成员变量，或者在序列化时执行一些特殊的逻辑。
   
3. **性能优化：**
   - `Externalizable` 提供了更大的灵活性，允许程序员进行一些性能优化，例如只序列化对象的一部分数据，或者采用紧凑的二进制格式。
   
4. 在选择使用 `Serializable` 还是 `Externalizable` 时，通常情况下，大多数情况下 `Serializable` 提供的默认行为就够用了。但在需要更精细的控制和更高性能的场景下，`Externalizable` 提供了更大的灵活性。

## 案例

```java
package com.stein.serialization;

import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * @author njl
 * @date 2023/1/29
 */
public class SerializationApp {
    public static void main(String[] args) {
//    serialization1();
        serialization2();
    }

    /**
     * 使用 ObjectInputStream 反序列化对象
     */
    public static void serialization2() {
        try (ObjectInputStream ois = new ObjectInputStream(Files.newInputStream(Paths.get("D:\\java-learning\\01-JavaBasic\\java-programming-learning\\java-language-base\\src\\main\\java\\com\\stein\\serialization\\employee.ser")))) {
            Employee employee = (Employee) ois.readObject();
            System.out.println("employee = " + employee);
            employee.mailCheck();
        } catch (IOException | ClassNotFoundException e) {
            throw new RuntimeException(e);
        }
    }

    /**
     * 使用 ObjectOutputStream 序列化对象
     */
    public static void serialization1() {
        try (ObjectOutputStream oos = new ObjectOutputStream(Files.newOutputStream(Paths.get("D:\\java-learning\\01-JavaBasic\\java-programming-learning\\java-language-base\\src\\main\\java\\com\\stein\\serialization\\employee.ser")))) {
            Address address = new Address();
            address.province = "江苏省";
            address.detail = "雨花台区";

            Employee employee = new Employee();
            employee.setName("倪京龙");
            employee.setSSN(283036);
            employee.setNumber("17710450421");
            employee.setAddress(address);

            oos.writeObject(employee);
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}

class Employee implements java.io.Serializable {
    private static final long serialVersionUID = 1L;

    private String name;
    private transient int SSN; // transient 修饰的字段不会参与序列化过程，在反序列化的时候会被赋予该类型的默认值。
    private String number;
    private Address address; // 对于引用类型需要被序列化的话那么也需要实现序列化接口，否则序列化和反序列时都会抛出异常，导致序列化过程失败。

    public void mailCheck() {
        System.out.println("Mailing a check to " + name + " " + address);
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getSSN() {
        return SSN;
    }

    public void setSSN(int SSN) {
        this.SSN = SSN;
    }

    public String getNumber() {
        return number;
    }

    public void setNumber(String number) {
        this.number = number;
    }

    public Address getAddress() {
        return address;
    }

    public void setAddress(Address address) {
        this.address = address;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "name='" + name + '\'' +
                ", SSN=" + SSN +
                ", number='" + number + '\'' +
                ", address=" + address +
                '}';
    }
}

class Address implements Serializable {
    public String province;
    public String detail;

    @Override
    public String toString() {
        return "Address{" +
                "province='" + province + '\'' +
                ", detail='" + detail + '\'' +
                '}';
    }
}
```
