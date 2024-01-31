# Filter

## 概述

过滤器（Filter）是一种用于在Servlet容器中对HTTP请求和响应进行预处理和后处理的组件。过滤器提供了一种在请求到达Servlet之前以及响应离开Servlet之后对请求和响应进行操作的机制。过滤器通常用于执行一些通用的任务，如日志记录、验证、权限检查、字符编码转换等。

## 使用方法：

1. **创建过滤器类：** 实现`javax.servlet.Filter`接口，实现`doFilter`方法来定义过滤器的逻辑。

    ```java
    public class MyFilter implements Filter {
        public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
                throws IOException, ServletException {
            // 过滤器逻辑处理
            // 可以在请求前或响应后进行处理
            chain.doFilter(request, response); // 继续请求的传递
        }

        // 其他方法：init、destroy
    }
    ```

2. **配置过滤器：** 在`web.xml`文件中配置过滤器的映射和顺序或者通过注解`@WebFilter`。

    ```xml
    <filter>
        <filter-name>MyFilter</filter-name>
        <filter-class>com.example.MyFilter</filter-class>
    </filter>
    
    <filter-mapping>
        <filter-name>MyFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    ```

    上述配置表示`MyFilter`过滤器将对所有URL模式进行处理。

## 使用场景：

1. **日志记录：** 记录请求和响应的信息，用于调试和分析。

2. **权限检查：** 验证用户是否有权限访问某些资源。

3. **字符编码转换：** 对请求参数和响应内容进行字符编码的转换。

4. **防止跨站脚本攻击（XSS）：** 对请求参数进行过滤，防止恶意脚本注入。

5. **缓存控制：** 控制响应的缓存策略，如过期时间、缓存验证等。

6. **压缩响应：** 对响应内容进行压缩，减少传输数据量。

7. **性能优化：** 在请求前后执行一些性能优化的任务，如资源合并、压缩等。

## 执行流程

过滤器（Filter）在Java Web应用中的执行流程主要包括三个方法：`init()`、`doFilter()`、`destroy()`。以下是它们的执行流程：

1. **init() 方法：**
   - 当Web容器（如Tomcat）启动时，会创建过滤器实例并调用其 `init()` 方法。
   - `init()` 方法用于初始化过滤器，在整个生命周期内只会执行一次。
   - 可以在这个方法中进行一些初始化的操作，例如读取配置信息、建立数据库连接等。

2. **doFilter() 方法：**
   - 当有请求匹配到过滤器的URL模式时，容器会调用过滤器的 `doFilter()` 方法。
   - `doFilter()` 方法是过滤器中最重要的方法，它包含了过滤器的主要逻辑。
   - 在 `doFilter()` 方法内，可以对请求进行处理，也可以选择继续调用过滤器链中的下一个过滤器（通过 `chain.doFilter(request, response)` 实现）。
   - 如果没有继续调用 `chain.doFilter(request, response)`，则请求将不会传递给下一个过滤器，也不会到达Servlet。

3. **过滤器链执行：**
   - 在 `doFilter()` 方法中，如果调用了 `chain.doFilter(request, response)`，则请求会继续传递给下一个过滤器。
   - 如果没有更多的过滤器或已经执行完所有过滤器的 `doFilter()` 方法，最终请求会到达目标Servlet。
   - 过滤器链的执行顺序是根据 `web.xml` 中的配置顺序确定的。

4. **目标Servlet执行：**
   - 请求到达目标Servlet，目标Servlet的 `service()` 方法被调用，处理请求并生成响应。
   - 如果在 `doFilter()` 方法中有对请求或响应进行修改，这些修改将反映在目标Servlet的执行中。

5. **过滤器链的逆向执行：**
   - 一旦目标Servlet处理完请求并生成响应，过滤器链将以相反的顺序执行。
   - 这时 `doFilter()` 方法的逆向调用，可以进行一些后处理的操作。
   - 逆向执行直到最初调用的过滤器，然后响应被发送给客户端。

6. **destroy() 方法：**
   - 当Web容器关闭或Web应用被卸载时，过滤器的 `destroy()` 方法被调用。
   - `destroy()` 方法用于释放资源，完成一些清理工作。

总体来说，过滤器提供了对请求和响应的全局性处理机制，通过过滤器链的执行，可以在请求前、请求后以及响应前、响应后执行相应的逻辑。这使得开发人员能够方便地实现一些通用的功能，如日志记录、权限验证、字符编码转换等。

## 过滤器映射规则

过滤器映射规则主要由过滤器的 `url-pattern` 配置决定，这个配置可以使用不同的通配符来指定拦截的URL路径。以下是常见的过滤器映射规则：

1. **精确路径匹配：**
   - 使用 `/path` 表示仅匹配指定路径的请求，例如 `/example` 只匹配 "/example" 路径的请求。

2. **通配符 `*` 匹配：**
   - 使用 `/*` 表示匹配所有路径的请求，包括根路径。例如，`/*` 将匹配所有请求，包括 "/example"、"/user" 等。

3. **通配符 `/` 匹配：**
   - 使用 `/` 表示匹配所有路径的请求，但不包括根路径。例如，`/` 将匹配 "/example"、"/user" 等，但不匹配根路径 "/".

4. **后缀通配符 `*.` 匹配：**
   - 使用 `*.extension` 表示匹配指定扩展名的请求。例如，`*.jsp` 将匹配以 ".jsp" 结尾的请求路径。

5. **路径匹配规则：**
   - 使用 `/path/*` 表示匹配指定路径下的所有请求，例如 `/images/*` 将匹配 "/images/logo.png"、"/images/banner.jpg" 等。

6. **精确匹配和通配符组合：**
   - 可以将精确匹配和通配符组合使用，例如 `/app/*.html` 将匹配 "/app/index.html"、"/app/page.html" 等。

7. **多路径映射：**
   - 可以使用逗号分隔多个路径，表示一个过滤器映射到多个路径。例如，`/path1, /path2` 表示过滤器匹配 "/path1" 和 "/path2"。

这些规则可以在 `web.xml` 文件中的 `<filter-mapping>` 元素的 `url-pattern` 部分配置，或者在过滤器类上使用 `@WebFilter` 注解的 `urlPatterns` 属性中配置。根据具体需求和应用场景，选择适当的映射规则可以确保过滤器只拦截到需要处理的请求。
