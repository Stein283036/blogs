# Maven

## 概述

Apache Maven是一个用于项目管理和构建的强大工具。它能够帮助开发者自动化项目的构建过程，包括编译源代码、运行测试、打包和部署等。Maven提供了一种标准化的项目结构和构建流程，使得开发者能够更容易地管理和构建项目。

Maven项目通过一个XML文件（POM文件）来描述，该文件定义了项目的基本信息、依赖关系、插件配置等。

Maven提供了一致的项目结构和构建流程，这有助于降低项目的复杂性，使团队成员更容易理解和协作。

## 生命周期

Maven的生命周期是一系列阶段的集合，这些阶段按照一定的顺序依次执行，用于构建和部署项目。Maven定义了三套相互独立的生命周期：

1. **Clean生命周期：**
   - `clean`生命周期用于清理项目，删除target目录。
   - 命令：`mvn clean`
2. **Default生命周期：**
   - `default`生命周期是最主要的生命周期，它包括了项目的整个构建过程，从编译到测试再到打包和部署。
   - 命令：`mvn compile`、`mvn test`、`mvn package`、`mvn install`
3. **Site生命周期：**
   - `site`生命周期用于生成项目的站点文档。
   - 命令：`mvn site`

每个生命周期包含一系列的阶段（Phase），阶段是生命周期的一个步骤。例如，在`default`生命周期中的一些常见阶段包括：

- `validate`: 验证项目是否正确
- `compile`: 编译项目的源代码
- `test`: 使用合适的测试框架运行测试
- `package`: 将编译的代码打包成可分发的格式，如JAR或WAR
- `install`: 将包安装到本地仓库，以供其他项目使用
- `deploy`: 将包复制到远程仓库，以供其他开发者或项目使用

## 配置文件

Maven主要依赖于一个名为`pom.xml`的配置文件，它包含了项目的各种配置信息。以下是`pom.xml`文件中一些常见的配置信息：

1. **项目信息配置：**
   - `groupId`: 定义项目的组织或公司。
   - `artifactId`: 定义项目的唯一标识符。
   - `version`: 定义项目的版本号。
   - `packaging`：定义项目的打包方式，默认为jar
   - `name`：定义项目的名称
   - `description`：定义项目的描述信息
   - `url`：定义项目的访问路径
   - `developers`：定义项目的开发者信息
   - `organization`：定义项目的组织信息
   - `licenses`：定义项目的许可证信息
   - `issueManagement`：定义项目的 issue 管理信息

   ```xml
   <groupId>com.example</groupId>
   <artifactId>my-project</artifactId>
   <version>1.0.0</version>
   <packaging>jar</packaging>
   <name>druid</name>
   <description>An JDBC datasource implementation.</description>
   <url>https://github.com/alibaba/druid</url>
   ```

2. **依赖配置：**
   - `dependencies`元素用于声明项目的依赖库。
   - `dependenciesManagement`元素用于集中管理项目中所有模块的依赖版本。
   - `<properties>` 元素来定义版本号，然后在需要的地方引用该属性

   ```xml
   <properties>
   	<spring.version>4.2.5.RELEASE</spring.version>
   	<junit.version>4.12</junit.version>
   	<gpg.skip>false</gpg.skip>
   	<javadoc.skip>false</javadoc.skip>	
       <project.build.sourceEncoding>UTF8</project.build.sourceEncoding>
   	<jdk.version>1.6</jdk.version>
   </properties>
   <dependencies>
       <dependency>
           <groupId>com.example</groupId>
           <artifactId>my-library</artifactId>
           <version>1.0.0</version>
       </dependency>
   </dependencies>
   ```

3. **插件配置：**
   - `plugins`元素用于配置Maven插件，扩展和定制构建过程。

   ```xml
   <build>
       <plugins>
           <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-compiler-plugin</artifactId>
               <version>3.8.1</version>
               <configuration>
                   <source>1.8</source>
                   <target>1.8</target>
               </configuration>
           </plugin>
       </plugins>
   </build>
   ```

4. **资源配置：**
   - `resources`元素用于指定项目的资源文件。

   ```xml
   <build>
       <resources>
           <resource>
               <directory>src/main/resources</directory>
               <includes>
                   <include>**/*.properties</include>
               </includes>
           </resource>
       </resources>
   </build>
   ```

5. **插件仓库配置：**
   - `repositories`元素用于配置项目的插件仓库。

   ```xml
   <repositories>
       <repository>
           <id>central</id>
           <url>https://repo.maven.apache.org/maven2</url>
       </repository>
   </repositories>
   ```

## 依赖管理

### 依赖坐标

Maven 的依赖坐标指的是描述一个 Maven 项目或模块的唯一标识信息，主要包括三个元素：`groupId`（组织或公司的唯一标识符）、`artifactId`（项目的唯一标识符）、`version`（项目的版本号）。

Maven 依赖坐标的基本结构如下：

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>my-library</artifactId>
    <version>1.0.0</version>
</dependency>
```

- **`groupId`（组织或公司的唯一标识符）：** 通常使用组织或公司的域名倒序表示，确保唯一性。例如，`com.example`。

- **`artifactId`（项目的唯一标识符）：** 项目的名称或标识符，通常是小写字母和连接符。例如，`my-library`。

- **`version`（项目的版本号）：** 项目的版本号，遵循语义化版本规则。例如，`1.0.0`。

这些元素一起构成了一个唯一的依赖坐标，用于标识 Maven 项目或模块。

### 依赖范围

Maven 的依赖范围（Scope）定义了依赖项在不同阶段的使用范围。每个依赖都可以指定一个特定的范围，以指示 Maven 在构建、测试、运行等不同的阶段是否应该包括这个依赖。以下是 Maven 中常见的依赖范围：

1. **compile（默认）：** 在所有阶段都有效，包括编译、测试和运行。这是默认的依赖范围，如果不指定范围，就会使用 compile。

    ```xml
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>my-library</artifactId>
        <version>1.0.0</version>
    </dependency>
    ```

2. **provided：** 在编译和测试阶段有效，但在运行阶段由 JDK 或容器提供。这通常用于 Servlet API、JSP API 等在运行时由容器提供的依赖。

    ```xml
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
    </dependency>
    ```

3. **runtime：** 在运行和测试阶段有效，但不会参与编译。这是指定在运行时需要，但在编译时不需要的依赖的范围。

    ```xml
    <dependency>
        <groupId>com.oracle</groupId>
        <artifactId>ojdbc6</artifactId>
        <version>11.2.0.3</version>
        <scope>runtime</scope>
    </dependency>
    ```

4. **test：** 仅在测试阶段有效，不会参与编译和运行。这通常用于测试框架和工具。

    ```xml
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
    ```

5. **system：** 类似于 provided 范围，但需要显式提供文件路径。这不推荐使用，因为它打破了 Maven 的依赖管理机制。

    ```xml
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>my-library</artifactId>
        <version>1.0.0</version>
        <scope>system</scope>
        <systemPath>${basedir}/lib/my-library.jar</systemPath>
    </dependency>
    ```

6. **import（仅用于 `<dependencyManagement>` 中）：** 用于声明由其它 Maven 项目提供的依赖。在项目中并不直接引入依赖，但可以在 `<dependencyManagement>` 中声明。

    ```xml
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>com.example</groupId>
                <artifactId>my-library</artifactId>
                <version>1.0.0</version>
                <scope>import</scope>
                <type>pom</type>
            </dependency>
        </dependencies>
    </dependencyManagement>
    ```

### 依赖传递

在 A 依赖 B，B 依赖 C 的前提下，C 是否能够传递到 A，取决于 B 依赖 C 时使用的依赖范围以及配置

- B 依赖 C 时使用 compile 范围，可以传递

- B 依赖 C 时使用 test 或 provided 范围，不能传递，所以需要这样的 jar 包时，就必须在需要的地方明确配置依赖才可以

- B 依赖 C 时，若配置了以下标签，则不能传递

  ```xml
  <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.2.15</version>
      <optional>true</optional>
  </dependency>
  ```

### 依赖排除

依赖排除（exclusions）和包含（includes）是 Maven 中用于控制项目依赖关系的机制，它们可以帮助你更精确地管理项目的依赖项。

在 Maven 的 `<dependency>` 元素中，可以使用 `<exclusions>` 和 `<includes>` 元素进行相应的配置。这些元素可以包含一个或多个 `<exclusion>` 或 `<include>` 元素，每个元素表示一个依赖项的排除或包含规则。

### 依赖排除（Exclusions）：

当你引用一个库时，这个库可能本身依赖于其他一些库。有时你可能希望排除这些传递性的依赖，即阻止 Maven 引入这些依赖。这时就可以使用依赖排除。

示例：

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>my-library</artifactId>
    <version>1.0.0</version>
    <exclusions>
        <exclusion>
            <groupId>org.unwanted</groupId>
            <artifactId>unwanted-library</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

上述例子中，`my-library` 依赖被引入，但其中的 `unwanted-library` 依赖会被排除，不会纳入到当前项目的依赖中。

### 依赖包含（Includes）：

相反，如果你想要明确地引入一个传递性依赖，即使它不是直接被你的项目依赖所需要，你可以使用 `<includes>` 元素。

示例：

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>my-library</artifactId>
    <version>1.0.0</version>
    <includes>
        <include>
            <groupId>org.desired</groupId>
            <artifactId>desired-library</artifactId>
        </include>
    </includes>
</dependency>
```

在这个例子中，`desired-library` 依赖明确地被包含，即使它可能是 `my-library` 的传递性依赖。

## 仓库

Maven 仓库是用来存储 Maven 构件（JAR、WAR、POM 等文件）的地方，它是 Maven 项目中依赖管理的核心。Maven 仓库主要分为两种类型：本地仓库、远程仓库和中央仓库。

### 1. 本地仓库（Local Repository）：

本地仓库是存储 Maven 构件的本地文件系统路径。当你第一次构建 Maven 项目时，Maven 会将下载的构件存储在本地仓库，以后的构建就可以直接从本地仓库中获取，避免了重复下载。

本地仓库的路径通常是用户主目录下的 `.m2/repository` 目录，但你可以在 Maven 的 `settings.xml` 文件中配置本地仓库的路径。以下是 `settings.xml` 中配置本地仓库的示例：

```xml
<settings>
  <localRepository>/path/to/your/local/repo</localRepository>
</settings>
```

### 2. 远程仓库（Remote Repository）：

远程仓库是 Maven 构件存储在网络上的服务器，供开发者和团队共享。当 Maven 构建项目时，它会首先查找本地仓库，如果本地仓库中没有相应的构件，它会从配置的远程仓库中下载。

### 3. 镜像仓库（Mirror Repository）：

镜像仓库是一种特殊的远程仓库，它用于代理另一个远程仓库。配置镜像仓库有助于提高构建速度，特别是在国内访问国外的 Maven 中央仓库时。你可以在 Maven 的 `settings.xml` 文件中配置镜像仓库。以下是配置阿里云 Maven 镜像的示例：

```xml
<settings>
  ...
  <mirrors>
    <mirror>
      <id>aliyun</id>
      <name>Aliyun Maven Mirror</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public</url>
      <mirrorOf>central</mirrorOf>
    </mirror>
  </mirrors>
  ...
</settings>
```

## 插件

Maven 插件是用于扩展 Maven 构建过程的工具，它们提供了额外的功能，使开发者能够执行各种任务和目标。插件可以用于编译代码、运行测试、创建文档、打包构建产物等多种任务。

### Maven 插件的作用：

1. **扩展构建生命周期：** Maven 插件可以将新的目标（goals）添加到 Maven 的构建生命周期中。通过插件，你可以在编译、测试、打包等各个构建阶段执行自定义的任务。

2. **提供额外的功能：** 插件可以提供一些 Maven 本身不提供的功能，例如代码生成、静态分析、部署到服务器等。

3. **自定义构建行为：** 插件允许你定制 Maven 构建的行为，以满足项目的特定需求。这可以包括定制编译过程、添加资源、生成文档等。

### Maven 插件的使用：

Maven 插件的使用主要涉及两个方面：配置插件和绑定插件目标到构建生命周期。

#### 配置插件：

在 Maven 项目的 `pom.xml` 文件中，你可以通过 `<build>` 元素配置插件。以下是一个简单的例子，展示了如何配置 Maven Compiler 插件：

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.8.1</version>
      <configuration>
        <source>1.8</source>
        <target>1.8</target>
      </configuration>
    </plugin>
  </plugins>
</build>
```

在上述例子中，`maven-compiler-plugin` 插件被配置为使用 Java 1.8 版本进行编译。

#### 绑定插件目标：

插件的目标（goals）是插件的具体任务。你可以通过 `<executions>` 元素将插件目标绑定到 Maven 构建的生命周期阶段。以下是一个将插件目标绑定到构建生命周期的示例：

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.8.1</version>
      <executions>
        <execution>
          <goals>
            <goal>compile</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

上述例子将 `maven-compiler-plugin` 的 `compile` 目标绑定到 Maven 构建的默认生命周期中。

总体来说，Maven 插件是通过配置和绑定来扩展 Maven 构建过程的工具。你可以根据项目的需求选择合适的插件，并根据需要配置它们。Maven 提供了丰富的插件生态系统，包括编译、测试、部署、静态分析等各种插件，可以大大简化和增强项目的构建和管理。

## 源码下载失败

`mvn dependency:resolve -Dclassifier=sources`

## BOM

https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html

## Nexus 私服

参考链接：https://www.bilibili.com/video/BV1JN411G7gX?p=46，尚硅谷2023Maven

进入 D:\softwares\nexus\nexus-3.30.1-01\bin 目录，运行 `nexus.exe /run` 命令启动 nexus 服务，浏览器地址栏输入 `http://localhost:8081/` 访问服务，用户名 `admin`，密码 `njl283036`。

修改 Maven 配置文件 `D:\dev_tools\Java\apache-maven-3.8.4\conf\settings-nexus.xml`。

修改 nexus 的远程仓库地址。

![image-20240122214819915](D:\2024年\blogs\Java\Maven\assets\image-20240122214819915.png)

### jar 包部署到 nexus 私服

```xml
<distributionManagement>
    <snapshotRepository>
        <id>nexus-local</id>
        <name>nexus-local</name>
        <url>http://localhost:8081/repository/maven-snapshots/</url>
    </snapshotRepository>
</distributionManagement>
```

### 引用 nexus 私服 jar 包

 ```xml
 <repositories>
     <repository>
         <id>nexus-local</id>
         <name>nexus-local</name>
         <url>http://localhost:8081/repository/maven-snapshots/</url>
         <snapshots>
             <enabled>true</enabled>
         </snapshots>
         <releases>
             <enabled>true</enabled>
         </releases>
     </repository>
 </repositories>
 ```





