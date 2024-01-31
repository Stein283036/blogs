# JDBC

## 概述

JDBC（Java Database Connectivity）是Java语言访问关系型数据库的一种标准接口。它提供了一组用于连接、查询、更新和管理数据库的API。通过JDBC，Java程序可以与各种关系型数据库（如MySQL、Oracle、SQL Server等）进行交互，执行SQL语句，获取查询结果等。

## Statement

### 步骤：

1. **加载数据库驱动：**
   
   - 使用`Class.forName`加载数据库驱动，这个驱动是数据库厂商提供的，用于让JDBC连接到特定的数据库。
   
    ```java
    Class.forName("com.mysql.cj.jdbc.Driver"); // MySQL 8 的加载驱动
    // com.mysql.jdbc.Driver MySQL 5 的加载驱动
    ```
   
2. **建立数据库连接：**
   - 使用`DriverManager.getConnection`方法建立与数据库的连接，需要提供数据库的URL、用户名和密码。

    ```java
    String url = "jdbc:mysql://localhost:3306/your_database";
    // 如果是本地连接 //localhost:3306 可以简化成//
    String username = "your_username";
    String password = "your_password";
    Connection connection = DriverManager.getConnection(url, username, password);
    ```
   
3. **创建Statement对象：**
   - 使用`connection.createStatement`创建`Statement`对象，用于执行SQL语句。

    ```java
    Statement statement = connection.createStatement();
    ```

4. **执行SQL语句：**
   - 使用`Statement`的`executeQuery`方法执行查询语句，`executeUpdate`执行更新语句（如INSERT、UPDATE、DELETE等）。

    ```java
    String sqlQuery = "SELECT * FROM your_table";
    ResultSet resultSet = statement.executeQuery(sqlQuery);
   
    // 或者执行更新语句
    String sqlUpdate = "UPDATE your_table SET column1 = value1 WHERE column2 = value2";
    int rowsAffected = statement.executeUpdate(sqlUpdate);
    ```

5. **处理查询结果：**
   - 如果执行的是查询语句，可以使用`ResultSet`对象获取查询结果。

    ```java
    while (resultSet.next()) {
        // 处理每一行的数据
        String columnValue = resultSet.getString("column_name");
        // 其他处理...
    }
    ```

6. **关闭资源：**
   - 使用完JDBC资源后，需要手动关闭，包括`ResultSet`、`Statement`和`Connection`。

    ```java
    resultSet.close();
    statement.close();
    connection.close();
    ```

### JDBC代码示例：

以下是一个简单的JDBC代码示例，演示了连接到MySQL数据库并执行查询的过程：

```java
import java.sql.*;

public class JdbcExample {
    public static void main(String[] args) {
        try {
            // 加载数据库驱动
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 建立数据库连接
            String url = "jdbc:mysql://localhost:3306/your_database";
            String username = "your_username";
            String password = "your_password";
            Connection connection = DriverManager.getConnection(url, username, password);

            // 创建Statement对象
            Statement statement = connection.createStatement();

            // 执行查询语句
            String sqlQuery = "SELECT * FROM your_table";
            ResultSet resultSet = statement.executeQuery(sqlQuery);

            // 处理查询结果
            while (resultSet.next()) {
                String columnValue = resultSet.getString("column_name");
                System.out.println(columnValue);
                // 其他处理...
            }

            // 关闭资源
            resultSet.close();
            statement.close();
            connection.close();

        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        }
    }
}
```

请注意，以上代码中的数据库连接信息、SQL语句等都需要根据实际情况修改。此外，为了防止SQL注入攻击，建议使用`PreparedStatement`替代`Statement`执行SQL语句。

### SQL 注入

SQL注入是一种恶意利用应用程序对用户输入的不当处理，从而在执行SQL查询时插入或注入恶意的SQL代码的攻击。这种攻击的根本原因是应用程序在构建SQL查询时，未能正确地验证、转义或过滤用户提供的输入，导致恶意用户能够操纵数据库查询，执行未经授权的操作。

**拼接字符串的方式构建SQL查询：**

```mysql
javaCopy code
String query = "SELECT * FROM users WHERE username='" + userInput + "' AND password='" + passwordInput + "'";
```

如果用户输入包含恶意SQL代码，例如 `' OR '1'='1' --`，整个查询就会变成：

```mysql
sqlCopy code
SELECT * FROM users WHERE username='' OR '1'='1' --' AND password='';
```

为了防范SQL注入，应采取以下措施：

- **使用参数化查询：** 使用 `PreparedStatement` 或其他支持参数化的数据库访问方式，避免手动拼接SQL字符串。
- **输入验证和过滤：** 对用户输入进行验证和过滤，确保只有合法的字符被允许。
- **最小权限原则：** 给予数据库用户最小的权限，仅允许执行必要的操作，降低攻击面。

## PreparedStatement

使用 `PreparedStatement` 可以更安全和高效地执行 SQL 语句，尤其是在处理用户输入时。以下是一个使用 `PreparedStatement` 访问并操作数据库的示例，包括插入、更新和查询操作：

```java
import java.sql.*;

public class PreparedStatementExample {
    public static void main(String[] args) {
        // JDBC连接的URL，注意如果是MySQL的话，需要加上时区的设置
        String url = "jdbc:mysql://localhost:3306/your_database?serverTimezone=UTC";
        String username = "your_username";
        String password = "your_password";

        try (Connection connection = DriverManager.getConnection(url, username, password)) {
            // 插入数据
            insertData(connection, "John Doe", 25);

            // 更新数据
            updateData(connection, 1, "Jane Doe");

            // 查询数据
            queryData(connection);

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    // 插入数据
    private static void insertData(Connection connection, String name, int age) throws SQLException {
        String insertSql = "INSERT INTO your_table (name, age) VALUES (?, ?)";

        try (PreparedStatement preparedStatement = connection.prepareStatement(insertSql)) {
            preparedStatement.setString(1, name);
            preparedStatement.setInt(2, age);

            int rowsAffected = preparedStatement.executeUpdate();
            System.out.println(rowsAffected + " row(s) inserted.");
        }
    }

    // 更新数据
    private static void updateData(Connection connection, int id, String newName) throws SQLException {
        String updateSql = "UPDATE your_table SET name = ? WHERE id = ?";

        try (PreparedStatement preparedStatement = connection.prepareStatement(updateSql)) {
            preparedStatement.setString(1, newName);
            preparedStatement.setInt(2, id);

            int rowsAffected = preparedStatement.executeUpdate();
            System.out.println(rowsAffected + " row(s) updated.");
        }
    }

    // 查询数据
    private static void queryData(Connection connection) throws SQLException {
        String querySql = "SELECT * FROM your_table";

        try (PreparedStatement preparedStatement = connection.prepareStatement(querySql);
             ResultSet resultSet = preparedStatement.executeQuery()) {

            while (resultSet.next()) {
                int id = resultSet.getInt("id");
                String name = resultSet.getString("name");
                int age = resultSet.getInt("age");

                System.out.println("ID: " + id + ", Name: " + name + ", Age: " + age);
            }
        }
    }
}
```
