# MyBatis Config File

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!-- 引入properties文件，此时就可以${属性名}的方式访问属性值 -->
    <properties resource="jdbc.properties"/>
    
    <settings>
        <!-- 将表中字段的下划线自动转换为驼峰 -->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
        <!-- 开启延迟加载 -->
        <setting name="lazyLoadingEnabled" value="true"/>
    </settings>
    
    <!-- typeAliases标签: 给指定类设置别名 -->
    <typeAliases>
        <!--        <typeAlias type="org.stein.mybatis3.pojo.User" alias="User"/>-->
        <!-- 包扫描的方式给指定包下得所有类设置别名 -->
        <package name="org.stein.mybatis3.pojo"/>
    </typeAliases>
    
    <!-- environments标签: 数据库的环境 -->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <!-- 数据库连接信息 -->
                <property name="driver" value="${jdbc.driver}"/>
                <property name="url" value="${jdbc.url}"/>
                <property name="username" value="${jdbc.user}"/>
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>
    
    <!-- mappers标签: 加载Mapper接口对应的映射文件 -->
    <mappers>
        <!--加载sql映射文件 -->
        <!--        <mapper resource="UserMapper.xml"/>-->
        <!-- 包扫描: 将包下的所有Mapper映射文件全部导入, 前提: Mapper接口和Mapper映射文件必须在相同的包下 -->
        <package name="org.stein.mybatis3.mapper"/>
    </mappers>
</configuration>
```