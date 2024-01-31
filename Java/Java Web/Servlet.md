# Servlet

## 概述

Java Servlet是Java编写的服务器端程序，主要用于处理HTTP请求和生成HTTP响应。它是Java EE（Java Platform, Enterprise Edition）规范的一部分，用于构建Web应用程序。

## Servlet组件

- Servlet 接口

- GenericServlet抽象类

- HttpServlet抽象类

  定义了针对HTTP协议的方法，如`doGet()`、`doPost()`、`doHead()`等，简化了HTTP请求的处理。

- Servlet容器

  Servlet容器是Web服务器或应用服务器的一部分，负责管理和执行Servlet的生命周期、处理Servlet的初始化和销毁，并调用Servlet的`service()`方法来处理客户端请求。

- ServletConfig接口

  用于封装Servlet的配置信息。

  在Servlet初始化时，Servlet容器会将ServletConfig传递给Servlet，以提供Servlet的配置参数。

- ServletContext接口

  代表Servlet的上下文，提供了在整个Web应用程序中共享信息的机制。

  允许Servlet访问应用程序范围内的资源，如初始化参数、共享属性等。

## Servlet接口方法

1. **init(ServletConfig config):**
   - 该方法在Servlet被初始化时被调用。
   - 在Servlet的生命周期内，该方法只会被调用一次。
   - 用于执行一次性的初始化任务，例如加载配置信息。
2. **service(ServletRequest request, ServletResponse response):**
   - 该方法用于处理客户端请求并生成响应。
   - 在每次请求时都会被调用。
   - Servlet容器调用此方法来处理HTTP请求，其中ServletRequest包含客户端的请求信息，而ServletResponse用于生成响应。
3. **destroy():**
   - 该方法在Servlet被销毁时被调用。
   - 在Servlet的生命周期内，该方法只会被调用一次。
   - 用于执行清理操作，释放资源，如关闭数据库连接等。
4. **getServletConfig():**
   - 该方法返回Servlet的配置信息，通常在初始化时由Servlet容器设置。
   - ServletConfig对象包含了Servlet的初始化参数等信息。
5. **getServletInfo():**
   - 该方法返回Servlet的信息，通常由开发者提供。
   - 用于描述Servlet的一般信息，例如版本号、作者等。

## Servlet容器

Servlet需要在Servlet容器中运行，常见的Servlet容器有Apache Tomcat、Jetty等。这些容器负责加载、实例化和运行Servlet，并提供Servlet所需的运行环境。

## Servlet生命周期

Servlet生命周期是指一个Servlet从创建到销毁的整个过程，它包括以下几个阶段：

1. **加载和实例化：** 当Servlet容器启动时，会加载并实例化在`web.xml`文件或通过注解配置的Servlet类。这个过程发生在第一次请求到达该Servlet时。

2. **初始化：** Servlet容器调用Servlet的`init()`方法进行初始化。可以通过注解或web.xml配置文件修改参数loadOnStartup参数（正数是容器启动时加载，默认-1是第一次请求时加载）来改变Servlet的加载时机。在这个阶段，Servlet可以执行一些初始化操作，例如读取配置文件、建立数据库连接等。`init()`方法只在Servlet的生命周期中调用一次。

3. **请求处理：** 一旦Servlet被初始化，它可以处理客户端的请求。处理请求的逻辑通常写在`doGet()`和/或`doPost()`等方法中，这取决于请求的类型。每次有请求到达时，容器会创建一个新的线程或从线程池中取出线程，然后调用Servlet的`service()`方法来处理请求。

4. **服务：** 在`service()`方法中，Servlet容器会调用与请求类型对应的方法，例如`doGet()`或`doPost()`，以处理具体的请求。这是Servlet的主要工作阶段。

5. **销毁：** 当Servlet容器关闭或Web应用被卸载时，容器会调用Servlet的`destroy()`方法进行销毁。在这个阶段，Servlet可以执行一些清理工作，例如关闭数据库连接、释放资源等。

在整个生命周期中，Servlet实例可能会被创建和销毁多次。每次有新的请求到达时，容器可能会使用现有的Servlet实例，也可能会创建一个新的实例来处理请求。容器的决定通常基于负载均衡、Servlet配置、线程池策略等因素。

## HttpServletRequest和HttpServletResponse

`HttpServletRequest` 继承自 `ServletRequest`，实现类是 `RequestFacade`，由Tomcat解析HTTP请求信息并创建对象。

`HTTPServletResponse`继承自`ServletResponse`，实现类是`ResponseFacade`，由Tomcat完成响应对象的创建并返回。

`HttpServletRequest` 和 `HttpServletResponse` 是 Servlet API 中用于处理HTTP请求和响应的两个重要接口。它们提供了访问客户端请求和生成服务器响应的方法。

1. **HttpServletRequest（HTTP 请求）：**
   - `javax.servlet.http.HttpServletRequest` 接口代表客户端的HTTP请求。
   - 提供了访问客户端请求的方法，如获取请求参数、请求头信息、会话（Session）等。
   - 一些常用的方法包括：
     - **`getParameter(String name)`: 获取请求参数的值。**
     - **`getParameterMap`：获取所有参数的键值对集合。**
     - `getParameterValues(String name)`：根据参数名称获取多个值（前端的多选框）。
     - `getHeader(String name)`: 获取指定请求头的值。
     - `getMethod()`: 获取HTTP请求的方法，如GET、POST等。
     - `getSession()`: 获取与请求关联的会话对象。
     - `getInputStream`：获取请求的输入流，用于读取请求体（文本）的内容。
     - `getReader`：获取请求的字符输入流，用于读取请求体（图片、音视频）的内容。
     - `getHeader(String name)`: 获取指定名称的请求头的值。
     - `getMethod()`: 获取HTTP请求的方法，如GET、POST等。
     - `getRequestURI()`: 获取请求的URI（统一资源标识符）。
     - `getRequestURL()`: 获取请求的URL（统一资源定位符）。
2. **HttpServletResponse（HTTP 响应）：**
   - `javax.servlet.http.HttpServletResponse` 接口代表服务器对客户端的HTTP响应。
   - 提供了生成响应的方法，如设置响应头、写入响应内容等。
   - 一些常用的方法包括：
     - `setStatus(int sc)`: 设置HTTP响应的状态码。
     - `setHeader(String name, String value)`: 设置响应头信息。
     - `getWriter()`: 获取用于写入字符文本的 PrintWriter 对象。
     - `getOutputStream()`: 获取用于写入原始字节数据的 OutputStream 对象。
     - `sendRedirect(String location)`: 重定向客户端到指定的URL。

这两个接口在Servlet的 `service()` 方法中被传递，开发者通过这些接口可以读取客户端的请求信息，并生成相应的响应。例如，在 `doGet()` 和 `doPost()` 方法中，这两个接口经常被使用来处理GET请求和POST请求。

总的来说，`HttpServletRequest` 提供了获取客户端请求信息的方法，而 `HttpServletResponse` 提供了生成服务器响应的方法，这两者共同协作，使得开发者能够灵活处理和响应客户端的HTTP请求。

## Servlet urlPatterns 匹配方式

- 扩展名匹配：`*.extension`，匹配指定扩展名的URL，不能加前缀`/`
- 精确匹配：`/user/login`
- 任意匹配：`/*`，不要使用
- 路径参数匹配：`/users/*`，`/users/123`和`/users/john`都会匹配。

## Servlet编程

1. **创建Servlet类：** 编写一个Java类，继承自`javax.servlet.http.HttpServlet`。重写`doGet`和/或`doPost`方法，处理HTTP请求。

   ```java
   import java.io.IOException;
   import javax.servlet.ServletException;
   import javax.servlet.http.HttpServlet;
   import javax.servlet.http.HttpServletRequest;
   import javax.servlet.http.HttpServletResponse;
   
   public class MyServlet extends HttpServlet {
       protected void doGet(HttpServletRequest request, HttpServletResponse response)
               throws ServletException, IOException {
           // 处理GET请求的逻辑
           response.getWriter().println("Hello, this is a servlet!");
       }
   }
   ```

2. **配置Servlet：** 

   **在`web.xml`文件中配置Servlet的映射。**

   ```xml
   <web-app>
       <servlet>
           <servlet-name>MyServlet</servlet-name>
           <servlet-class>com.example.MyServlet</servlet-class>
       </servlet>
       <servlet-mapping>
           <servlet-name>MyServlet</servlet-name>
           <url-pattern>/myservlet</url-pattern>
       </servlet-mapping>
   </web-app>
   ```

   **注解配置**

   ```java
   import java.io.IOException;
   import javax.servlet.annotation.WebServlet;
   import javax.servlet.http.HttpServlet;
   import javax.servlet.http.HttpServletRequest;
   import javax.servlet.http.HttpServletResponse;
   
   @WebServlet("/myservlet")
   public class MyServlet extends HttpServlet {
       protected void doGet(HttpServletRequest request, HttpServletResponse response)
               throws IOException {
           // 处理GET请求的逻辑
           response.getWriter().println("Hello, this is a servlet!");
       }
   }
   ```

3. **部署到Servlet容器：** 将编写的Servlet类和`web.xml`文件打包成WAR（Web Application Archive）文件，然后部署到Servlet容器中。

4. **访问Servlet：** 启动Servlet容器后，在浏览器中访问配置的URL（例如：`http://localhost:8080/yourwebapp/myservlet`），即可触发Servlet处理请求。

在上述例子中，`@WebServlet`注解指定了Servlet的映射路径，替代了`web.xml`中的配置。

实际应用中，Servlet通常结合JavaServer Pages（JSP）等技术一起使用，以更方便地生成动态内容。

## Request

### GET请求和POST请求参数乱码

#### 乱码原因

乱码问题的原因主要有两点：

- 浏览器和服务器之间使用的字符编码不一致。
- Servlet默认使用ISO-8859-1编码来解析请求参数，可能导致中文等字符乱码。

#### GET请求参数乱码

GET请求参数是通过查询字符串读取的是字符，而不是字节输入流，所以不能通过设置字符编码的方式来解决。浏览器会对中文字符进行UTF-8字符集URL编码，而Tomcat使用ISO-8859-1进行URL解码。GET请求的参数通常附加在URL中，因此需要确保浏览器和服务器之间使用相同的URL字符编码。Tomcat8之后以解决GET请求的乱码问题。

#### POST请求参数乱码

POST请求的参数包含在请求体中，需要确保正确解析请求体中的参数。POST的请求参数是通过request的getReader()来获取流中的数据。

1. 在Servlet的 `doPost()` 方法中，使用 `request.setCharacterEncoding("UTF-8")` 设置请求对象的字符编码。这样可以确保解析请求体参数时使用UTF-8编码。

   ```java
   protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
       request.setCharacterEncoding("UTF-8");
       // 处理POST请求逻辑
   }
   ```

2. **配置过滤器（Filter）：**

   可以配置过滤器来统一设置请求和响应的字符编码。通过过滤器，可以确保在所有的Servlet执行之前进行字符编码的设置。

   ```
   javaCopy codepublic class EncodingFilter implements Filter {
       public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
               throws IOException, ServletException {
           request.setCharacterEncoding("UTF-8");
           response.setCharacterEncoding("UTF-8");
           chain.doFilter(request, response);
       }
   }
   ```

   在 `web.xml` 文件中配置过滤器：

   ```
   xmlCopy code<filter>
       <filter-name>EncodingFilter</filter-name>
       <filter-class>com.example.EncodingFilter</filter-class>
   </filter>
   <filter-mapping>
       <filter-name>EncodingFilter</filter-name>
       <url-pattern>/*</url-pattern>
   </filter-mapping>
   ```

### Request Forward

在Servlet中，请求转发（Request Forwarding）是一种机制，允许一个Servlet将其处理过程中的请求传递给另一个Servlet进行处理。这在构建Web应用程序时非常有用，可以将请求传递给其他资源，实现模块化和重用性。

#### 请求转发的步骤：

1. **获取请求转发器对象：**
   - 使用`getRequestDispatcher(String path)`方法获取`RequestDispatcher`对象，其中`path`是要转发的资源的路径。路径可以是相对于当前Servlet上下文的路径，也可以是绝对路径。

   ```java
   RequestDispatcher dispatcher = request.getRequestDispatcher("/path/to/destination");
   ```

2. **进行请求转发：**
   - 使用`forward()`方法进行请求转发。这将把请求传递给指定路径的资源，并由该资源进行处理。

   ```java
   dispatcher.forward(request, response);
   ```

3. **在目标资源中处理请求：**
   - 控制权转移到目标资源（转发到的资源），目标资源将接收请求和响应对象，并执行相应的逻辑。


#### 示例代码：

假设有两个Servlet，`SourceServlet`负责处理初始请求，而`DestinationServlet`是目标资源，用于接收并处理转发的请求。

```java
// SourceServlet.java
@WebServlet("/source")
public class SourceServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 获取请求转发器对象
        RequestDispatcher dispatcher = request.getRequestDispatcher("/destination");

        // 设置一些属性，如果需要在目标资源中使用
        request.setAttribute("message", "Hello from SourceServlet!");

        // 进行请求转发
        dispatcher.forward(request, response);
    }
}
```

```java
// DestinationServlet.java
@WebServlet("/destination")
public class DestinationServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 从请求中获取设置的属性
        String message = (String) request.getAttribute("message");

        // 在目标资源中处理请求
        response.getWriter().write("Message from SourceServlet: " + message);
    }
}
```

在上述示例中，`SourceServlet`接收GET请求，设置了一个属性，并将请求转发给`DestinationServlet`。`DestinationServlet`接收请求，从请求中获取属性并进行处理，然后向客户端返回响应。

注意：请求转发是在服务器内部完成的，客户端浏览器不会察觉到转发的存在，因为浏览器仍然认为它在与初始请求的Servlet通信。这使得请求转发是一种在Web应用程序内部实现模块化和分层的强大方式。

#### 请求转发之间共享资源

在Servlet中，通过请求转发进行资源共享是通过HttpServletRequest对象的setAttribute方法设置属性，然后在目标资源中通过HttpServletRequest对象的getAttribute方法获取属性来实现的。这样可以在不同的Servlet之间传递数据，实现资源共享。

#### 请求转发特点

- 浏览器URL不会发生变化
- 只能转发到服务器内部Servlet进行处理
- 一次请求转发中可以共享request域中的资源

## Response

### Response Redirect

在Servlet中，使用`HttpServletResponse`对象的`sendRedirect()`方法可以实现重定向。重定向是一种机制，用于告知浏览器跳转到另一个URL。这可以用于在客户端浏览器中触发一个新的HTTP请求。

以下是通过`sendRedirect()`方法实现重定向的简单示例：

```java
@WebServlet("/redirect-source")
public class RedirectSourceServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 构造重定向URL，需要加上虚拟目录前缀
        String redirectURL = "/redirect-destination?message=Hello+from+RedirectSourceServlet";

        // 发送重定向响应
        response.sendRedirect(redirectURL);
    }
}
```

在这个例子中，`RedirectSourceServlet`接收GET请求，然后使用`response.sendRedirect(redirectURL)`将浏览器重定向到`/redirect-destination`，并携带了一个参数`message`。

在目标资源 `RedirectDestinationServlet` 中，可以获取这个参数并进行相应的处理：

```java
@WebServlet("/redirect-destination")
public class RedirectDestinationServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 获取重定向携带的参数
        String message = request.getParameter("message");

        // 处理重定向后的逻辑
        response.getWriter().write("Message from RedirectSourceServlet: " + message);
    }
}
```

这样，通过`sendRedirect()`方法，浏览器将会向`/redirect-destination`发起新的HTTP请求，然后`RedirectDestinationServlet`中的逻辑会处理这个新请求，并向客户端返回响应。

总体来说，`sendRedirect()`方法是一种在Servlet中进行重定向的常用方式，适用于需要跳转到其他URL的场景。

### Response重定向的特点

- 因为是重定向转发，浏览器地址栏会发生跳转，发送新的请求
- 可以重定向到服务器外部的资源
- 不能共享request域中的资源，因为是两次请求

### Response响应字符数据编码

```java
// 设置响应头的字符编码
response.setHeader("Content-Type", "text/html; charset=UTF-8");

// 设置响应对象的字符编码
response.setCharacterEncoding("UTF-8");
```

### Response响应字符和字节数据

在Servlet中，`HttpServletResponse`对象允许开发者向客户端发送字符数据或字节数据。这通常取决于响应内容的类型，例如，如果是HTML文档，则发送字符数据更合适，而对于图片或文件等二进制数据，发送字节数据更为适用。

#### 发送字符数据：

1. **设置响应头：**
   - 设置`Content-Type`响应头，指定内容类型和字符编码。

   ```java
   response.setContentType("text/html; charset=UTF-8");
   ```

2. **获取`PrintWriter`对象：**
   - 使用`getWriter()`方法获取`PrintWriter`对象，用于向客户端发送字符数据。

   ```java
   PrintWriter writer = response.getWriter();
   ```

3. **向客户端发送字符数据：**
   - 使用`PrintWriter`的`write()`方法向客户端发送字符数据。

   ```java
   writer.write("Response Data: Hello, World!");
   ```

#### 发送字节数据：

1. **设置响应头：**
   - 设置`Content-Type`响应头，指定内容类型。

   ```java
   response.setContentType("application/octet-stream");
   ```

   这里使用了`application/octet-stream`表示二进制流，适用于发送字节数据。

2. **获取`OutputStream`对象：**
   - 使用`getOutputStream()`方法获取`OutputStream`对象，用于向客户端发送字节数据。

   ```java
   OutputStream outputStream = response.getOutputStream();
   ```

3. **向客户端发送字节数据：**
   - 使用`OutputStream`的`write()`方法向客户端发送字节数据。

   ```java
   byte[] byteData = { /* 字节数据 */ };
   outputStream.write(byteData);
   ```
