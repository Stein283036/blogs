# JSP

## 概述

JSP（JavaServer Pages）是一种用于开发动态Web页面的Java技术。它允许开发者将Java代码嵌入到HTML页面中，以实现在Web页面上生成动态内容的目的。JSP文件以`.jsp`为扩展名，其中包含静态HTML代码和嵌入的Java代码。

JSP的主要优势是将Java代码与HTML页面分离，提高了代码的可维护性。它还提供了标签库和内置对象，简化了开发过程。

## 原理

JSP实际上会被转化为Servlet并在Servlet容器中执行。JSP和Servlet可以一起使用，JSP用于处理页面的呈现，而Servlet用于处理业务逻辑。

## 内置对象

JSP（JavaServer Pages）中有一些内置对象，它们是由Servlet容器提供的，可以在JSP页面中直接使用。这些内置对象提供了访问与请求、响应、会话等相关的信息，以及执行一些常见任务的功能。以下是JSP中一些常用的内置对象：

1. **request：**
   - `request`对象代表了客户端的HTTP请求，通过这个对象可以获取请求参数、请求头、请求方法等信息。

   ```jsp
   <%= request.getParameter("parameterName") %>
   ```

2. **response：**
   - `response`对象代表了服务器对客户端的HTTP响应，通过这个对象可以设置响应的状态码、头部信息等。

   ```jsp
   <%= response.getStatus() %>
   ```

3. **out：**
   - `out`对象是一个`JspWriter`实例，用于向客户端输出内容。可以使用`out.print()`或者直接在JSP页面中使用表达式输出内容。

   ```jsp
   <% out.print("Hello, World!"); %>
   <%= "Hello, World!" %>
   ```

4. **session：**
   - `session`对象代表了用户的会话，可以用于在多个请求之间共享数据。

   ```jsp
   <%= session.getAttribute("attributeName") %>
   ```

5. **application：**
   - `application`对象代表了整个Web应用程序的上下文，可以用于在应用程序范围内共享数据。

   ```jsp
   <%= application.getAttribute("attributeName") %>
   ```

6. **config：**
   - `config`对象包含了JSP页面的配置信息，可以通过它获取初始化参数等。

   ```jsp
   <%= config.getInitParameter("parameterName") %>
   ```

7. **pageContext：**
   - `pageContext`对象是一个JSP页面的上下文对象，它封装了对其他内置对象的访问，并提供了一些额外的功能。

   ```jsp
   <%= pageContext.getServletContext().getRealPath("/") %>
   ```

8. **page：**
   - `page`对象表示当前JSP页面的实例，可以在页面中直接调用其方法。

   ```jsp
   <%= page.getClass().getName() %>
   ```

9. **exception：**
   - `exception`对象包含有关在页面中发生的异常的信息。在发生异常时，可以使用这个对象访问异常信息。

   ```jsp
   <%@ page errorPage="/errorPage.jsp" %>
   ```

这些内置对象使得在JSP页面中能够方便地访问与请求、响应、会话等相关的信息，并执行一些常见任务。在JSP页面中，这些内置对象可以直接使用，无需额外的声明或初始化。

## JSP脚本

JSP（JavaServer Pages）中的脚本允许在HTML页面中嵌入Java代码。有三种主要类型的脚本在JSP页面中使用，它们分别是声明、表达式和脚本块。

1. **声明脚本（Declaration）：**
   - 声明脚本用于在JSP页面中定义变量和方法。它们位于`<%! ... %>`标签之间，不会产生输出到客户端。声明脚本通常用于定义成员变量或方法，这些成员可以在整个JSP页面中使用。

   ```jsp
   <%!
       int counter = 0;
       void incrementCounter() {
           counter++;
       }
   %>
   ```

2. **表达式脚本（Expression）：**
   - 表达式脚本用于在JSP页面中输出结果到客户端。它们位于`<%= ... %>`标签之间，将表达式的结果直接作为out.print()方法的参数输出到页面上。表达式脚本通常用于显示变量或执行一些简单的运算。

   ```jsp
   <%= "Hello, World!" %>
   ```

   表达式脚本也可以用于输出变量的值：

   ```jsp
   <%= counter %>
   ```

3. **脚本块脚本（Scriptlet）：**
   
   - 脚本块脚本用于在JSP页面中插入任意的Java代码。它们位于`<% ... %>`标签之间，可以包含任意的Java语句、控制流结构等。脚本块中的代码会被执行，生成的输出将被包含在生成的Servlet的`_jspService()`方法中。
   
   ```jsp
   <%
       for (int i = 0; i < 5; i++) {
           out.print("Iteration: " + i + "<br>");
       }
   %>
   ```

这三种类型的脚本允许在JSP页面中嵌入Java代码，实现动态内容的生成。然而，为了提高可维护性和降低耦合度，推荐在JSP页面中尽可能减少直接的Java代码，而使用标签库、EL表达式等更高层次的抽象。这有助于分离业务逻辑和页面呈现的关注点。

## EL表达式

EL（Expression Language）是JSP（JavaServer Pages）中的一种表达式语言，用于在JSP页面中访问和操作数据。EL提供了一种简化和更直观的方式来获取JavaBean中的属性、调用方法、访问集合等操作，从而减少在JSP页面中嵌入Java代码的需求。

### 基本语法

EL表达式的基本语法为`${expression}`，其中`expression`可以是变量、属性、方法调用等。EL表达式可以嵌套使用，可以访问作用域中的变量、JavaBean中的属性等。

注意，为了使用JavaBean，还需要在页面中使用`<jsp:useBean>`标签进行声明。在使用EL表达式的时候推荐加上作用域前缀。

```jsp
<!-- 访问作用域中的变量 -->
${requestScope.variableName}

<!-- 访问JavaBean中的属性 -->
${user.name}

<!-- 调用JavaBean中的方法 -->
${userManager.getUserCount()}

<!-- 访问集合中的元素 -->
${myList[0]}

<!-- 访问Map中的值 -->
${myMap.keyName}
```

### JSP中使用EL

```java
@WebServlet("/jsp-el")
public class JSPServlet extends HttpServlet {
    private static final BrandService brandService = new BrandService();

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        List<Brand> brands = brandService.list();
        req.setAttribute("brands", brands);
        req.getRequestDispatcher("/jsp-request.jsp").forward(req, resp);
    }
}
```

```jsp
<%@ page contentType="text/html;charset=UTF-8" %>
<%@ page isELIgnored="false" %>
<html>
<head>
    <title>jsp-request</title>
</head>
<body>
<jsp:useBean id="brands" type="java.util.List" scope="request"/>
${brands}
</body>
</html>
```

## JSTL标签

JSTL（JavaServer Pages Standard Tag Library）是一组在JSP页面中使用的标签库，用于简化和增强JSP页面的功能。JSTL提供了一些核心标签和许多其他功能性标签，包括条件判断、循环、格式化输出、国际化等。JSTL的使用可以减少在JSP页面中使用Java代码的需求，使页面更加清晰、简洁。

### 核心标签：

JSTL的核心标签主要包括以下几个：

1. **`<c:if>`：** 用于执行条件判断。
2. **`<c:choose>`：** 类似于Java中的`switch`语句，用于多条件判断。
3. **`<c:forEach>`：** 用于迭代集合或数组。
4. **`<c:forTokens>`：** 用于迭代分隔符分割的字符串。
5. **`<c:set>`：** 用于设置变量。
6. **`<c:remove>`：** 用于移除变量。
7. **`<c:out>`：** 用于输出表达式的值。
8. **`<c:url>`：** 用于生成URL。

### 使用JSTL：

1. **引入Maven依赖：**

   ```xml
   <dependency>
       <groupId>jstl</groupId>
       <artifactId>jstl</artifactId>
       <version>1.2</version>
   </dependency>
   
   <dependency>
       <groupId>taglibs</groupId>
       <artifactId>standard</artifactId>
       <version>1.1.2</version>
   </dependency>
   ```

2. **引入JSTL库：** 在JSP页面中使用JSTL前，需要在页面的头部引入JSTL库。以下是引入JSTL库的示例：

   ```jsp
   <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
   ```

上述代码将JSTL的核心标签库定义为一个自定义前缀（这里是`c`）。`uri`是标签库的命名空间。

3. **使用JSTL标签：** 一旦引入了JSTL库，就可以在页面中使用JSTL标签了。以下是一个简单的示例，展示了如何使用`<c:if>`和`<c:forEach>`：

   ```jsp
   <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
   
   <html>
   <head>
       <title>JSTL Example</title>
   </head>
   <body>
   
       <c:if test="${condition}">
           <p>This is displayed if condition is true.</p>
       </c:if>
   
       <c:forEach var="item" items="${items}">
           <p>${item}</p>
       </c:forEach>
   
   </body>
   </html>
   ```

在上述示例中，`${condition}`是一个EL表达式，用于定义`<c:if>`的条件。`${items}`是一个集合，用于在`<c:forEach>`中迭代。