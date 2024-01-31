# Cookie && Session

## Cookie

Cookie是存储在用户计算机上的小型文本文件，由服务器发送到用户浏览器，然后浏览器将其保存在本地。Cookie包含一些关键-值对和一些其他属性，用于标识和跟踪用户。Cookie不能直接存储中文信息，需要在存储前进行URL编码，以及获取前进行URL解码。

## Session

Session是一种服务器端的机制，用于在服务器上存储和维护用户的状态信息。每个用户会话都有一个唯一的标识符，通常是通过Cookie或URL重写传递给客户端。

在一次会话中第一个发送的请求对象如果使用到了session，那么服务端就会为这次会话设置一个唯一的sessionId，添加到浏览器的Cookies中(例如JSESSIONID=EBEAEAE1C0D9FC77B73C4F61B2C7F9CC)。之后当前会话的每个请求都会携带所有的Cookies数据， 其中包含了sessionId， 当服务端接收到请求后， 发现请求中含有sessionId的Cookie信息， 就会查找与这个id相同的session对象，这样就实现了服务端的会话跟踪技术，因此Session是基于Cookie的。

session的钝化：在服务器正常关闭后，Tomcat会自动将Session数据写入硬盘的文件中，钝化的数据路径为：项目目录\target\tomcat\work\Tomcat\localhost\项目名称\SESSIONS.ser。

session的活化：再次启动服务器后，从文件中加载数据到内存Session中数据加载到Session中后，路径中的SESSIONS.ser文件会被删除掉。

session的声明周期：session数据默认在30分钟后自动销毁，可以通过在项目的web.xml文件中配置session-config和session-timeout，如果没有配置，默认是30分钟，默认值是在Tomcat的web.xml配置文件配置的。

session的销毁：invalidate()，一般在用户退出时，需要将session销毁掉。

## Cookie和Session的区别

- **存储位置：** Cookie存储在用户浏览器端，Session存储在服务器端。
- **数据存储：** Cookie可以存储少量的文本数据，而Session通常用于存储更大量的数据。
- **过期时间：** Cookie可以设置过期时间，可以是会话级别或持久性的，而Session也有一个过期时间，可以是会话级别或通过配置的时间。
- **隐私：** 由于Cookie存储在用户本地，可能涉及一些隐私问题；而Session相对更安全，数据存储在服务器上。
- **跨域：** Cookie可以被跨域访问，但有安全策略限制；Session是与用户在同一域下的应用程序相关的。

## 前后端会话

前后端的会话是指在一个Web应用中，前端（通常是浏览器端）和后端（服务器端）之间建立的一种交互状态。这种交互状态允许服务器在多个请求之间保持对用户的特定信息的跟踪，从而实现用户的状态管理、认证、授权等功能。会话是在用户与应用之间建立的一种持久性连接，通过这种连接，应用可以跟踪用户的状态和行为。

在Web开发中，会话通常包括以下关键概念：

1. **会话的建立：** 会话的建立通常涉及到用户的登录。当用户成功登录时，服务器会为该用户创建一个会话，并生成一个唯一的会话标识，通常是一个会话ID。

2. **会话的保持：** 一旦建立了会话，服务器会在后续的请求中保持与该用户的连接。这可以通过不同的机制来实现，例如Cookie、Session等。

3. **会话的终止：** 会话可以在用户注销、超时或其他特定条件下终止。在终止时，服务器可能会清除与会话相关的数据，释放资源。

4. **会话的数据存储：** 会话允许存储特定于用户的数据，这些数据可以在用户的多个请求之间传递。这些数据可以包括用户的身份信息、用户的配置设置、购物车内容等。

5. **会话的安全性：** 会话通常需要考虑安全性，以防止会话劫持（Session Hijacking）等攻击。使用安全的通信协议（如HTTPS）和采用安全的会话管理机制可以增强会话的安全性。

两种常见的前后端会话管理方式是：

- **基于Cookie的会话管理：** 服务器在响应中设置一个包含会话标识的Cookie，浏览器在后续的请求中将该Cookie发送给服务器，以维持会话状态。

- **基于Session的会话管理：**服务器可以在服务器端创建和维护会话（Session），将会话ID传递给客户端，客户端在后续的请求中通过该会话ID与服务器的会话相关联。

会话的管理对于许多Web应用都是至关重要的，它使得应用能够实现用户认证、用户状态跟踪、个性化设置等功能。

## Cookie会话管理

Cookie是一种用于在客户端和服务器之间传递信息的机制，常被用于实现会话跟踪。在Web开发中，Cookie通常被用来存储少量的文本数据，其中包括会话标识符（Session ID），以便在用户的多个请求之间保持会话状态。以下是使用Cookie实现会话跟踪的一般步骤：

1. **创建会话ID：**
   - 当用户首次访问网站时，服务器会为该用户生成一个唯一的会话标识符（Session ID）。这个标识符通常是一个随机生成的字符串。

2. **将会话ID存储在Cookie中：**

   - 服务器将生成的会话ID存储在一个名为"sessionID"（或其他自定义名称）的Cookie中，并将该Cookie发送到用户的浏览器。这可以通过`Set-Cookie` HTTP头部来实现。

   ```http
   Set-Cookie: sessionID=abc123; Path=/; HttpOnly
   ```

   上述示例中，`sessionID`是Cookie的名称，`abc123`是会话ID的值。`Path=/`表示该Cookie在整个网站都有效，而`HttpOnly`标志表示该Cookie不能通过JavaScript访问，提高安全性。

3. **浏览器发送Cookie：**
   - 在用户的后续请求中，浏览器会自动将存储在Cookie中的会话ID发送给服务器。这样，服务器就能够识别请求的用户。

4. **服务器识别会话ID：**
   - 服务器在接收到用户请求时，从请求中获取Cookie中的会话ID，并使用它来识别该用户的会话。通过会话ID，服务器可以检索与该会话相关联的用户状态信息。

   ```java
   String sessionID = request.getCookies()[0].getValue();
   ```

   上述Java代码示例中，通过`request.getCookies()`获取所有的Cookie，然后通过索引获取到名为`sessionID`的Cookie的值。

5. **维护会话状态：**
   - 服务器使用会话ID来维护用户的会话状态。可以在会话中存储用户的身份认证信息、用户配置、购物车内容等。

6. **过期和更新：**
   - Cookie可以设置过期时间，通常是会话级别的或持久性的。如果会话ID过期或失效，用户可能需要重新登录，服务器会为其生成新的会话ID。

```java
// 设置Cookie
@WebServlet("/cookie01")
public class CookieServlet01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) {
        Cookie cookie = new Cookie("username", "stein");
        // 正数: 将 Cookie 写入浏览器所在电脑的硬盘，持久化存储。到时间自动删除
        // 负数: 默认值，Cookie 在当前浏览器内存中，当浏览器关闭，则 Cookie 被销毁
        // 零：立即删除 Cookie
        cookie.setMaxAge(60 * 60 * 24 * 7); // 设置Cookie的有效时间: 一周, 这样关闭浏览器后Cookie在一周之内依然有效，默认是-1
        cookie.setHttpOnly(true);
        cookie.setPath("/");
        resp.addCookie(cookie);
    }
}

// 接收Cookie
@WebServlet("/cookie02")
public class CookieServlet02 extends HttpServlet {
	protected void doGet(HttpServletRequest request, HttpServletResponse response) {
		// 读取浏览器中的所有Cookie对象
		Cookie[] cookies = request.getCookies();
		for (Cookie cookie : cookies) {
			String name = cookie.getName();
			String value = cookie.getValue();
			System.out.println(name + ": " + value);
		}
	}
}
```

## Session会话管理

基于Session的会话管理是一种在Web应用中维护用户状态的机制。会话（Session）是服务器端的一种状态管理方式，用于跟踪用户在应用中的活动状态。通过会话管理，服务器可以在多个请求之间保持用户的状态信息，实现用户认证、状态跟踪等功能。以下是基于Session的会话管理的实现步骤：

1. **会话的创建：**
   - 当用户第一次访问应用时，服务器会为该用户创建一个新的会话。会话通常由服务器生成一个唯一的标识符，称为会话ID。这个ID用于唯一标识该用户的会话。

2. **会话的存储：**
   - 服务器会将会话ID与用户的状态信息关联，并存储在服务器端。这些状态信息可以包括用户的身份认证信息、用户的配置设置等。存储方式可以包括内存、数据库等。

3. **会话ID的传递：**
   - 服务器将生成的会话ID发送给客户端，通常通过Cookie的方式。Cookie中包含了会话ID，客户端在后续的请求中会将这个Cookie发送给服务器。

4. **会话的维护：**
   - 在用户的后续请求中，服务器通过解析请求中的会话ID来识别用户的会话。通过会话ID，服务器可以检索到与该会话关联的用户状态信息。

5. **会话的更新：**
   - 用户的每次请求都可能导致会话状态的变化，例如用户登录、注销、修改配置等操作。服务器会根据这些操作来更新与会话关联的状态信息。

6. **会话的失效：**
   - 会话通常有一个过期时间，如果用户在一段时间内没有活动，会话可能会自动失效。失效后，用户需要重新登录或重新建立会话。

在Java中，Servlet技术提供了`HttpSession`接口来支持会话管理。以下是基于Session的会话管理的简单Java Servlet示例：

```java
@WebServlet("/example")
public class ExampleServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 获取或创建会话
        HttpSession session = request.getSession();

        // 在会话中存储数据
        session.setAttribute("username", "exampleUser");

        // 获取会话中的数据
        String username = (String) session.getAttribute("username");

        // 执行其他操作...

        // 处理响应
        response.getWriter().println("Hello, " + username);
    }
}
```

在这个示例中，通过`request.getSession()`获取或创建会话，通过`session.setAttribute()`存储数据，通过`session.getAttribute()`获取数据，通过`session.removeAttribute()`删除数据，`session.invalidate()`来使session会话失效。这样，会话中的数据就能够在用户的多个请求之间共享和保持。注意，这只是一个简单示例，实际应用中可能需要更复杂的会话管理和安全性考虑。

## 会话劫持

会话劫持（Session Hijacking）是指攻击者在不经过合法认证的情况下获取并控制用户的会话信息，从而冒充用户进行恶意活动。攻击者可以通过各种手段截取或获取用户的会话标识符，然后使用这些标识符来模拟合法用户，进而获取用户的权限和敏感信息。

以下情况会发生会话劫持：

1. **未加密的传输（HTTP）：** 如果用户在使用未加密的网络连接（如公共Wi-Fi）时进行登录或会话传输，攻击者可以通过网络监听等手段获取用户的会话标识符。
2. **跨站脚本攻击（XSS）：** 攻击者通过注入恶意脚本代码到网页中，获取用户的会话信息。这可能通过窃取Cookie或其他会话标识符来实现。

如何防止和解决会话劫持：

1. **使用HTTPS：** 使用HTTPS协议加密数据传输，防止在传输过程中被中间人截取。这可以有效防止通过网络监听等方式获取会话标识符。
2. **安全的Cookie：** 设置Cookie的安全标志（Secure），确保Cookie只在加密的连接中传输。同时，设置HttpOnly标志，防止通过脚本访问Cookie，减少XSS攻击的风险。
3. **实施会话管理策略：** 引入合理的会话管理策略，包括合适的会话过期时间、单点登录（SSO）等机制。
4. **防范XSS攻击：** 对输入进行严格的验证和过滤，避免恶意脚本的注入。使用安全的编码方式输出数据。
7. **双因素认证：** 引入双因素认证，增加用户身份验证的安全性。

## 其它的会话管理方法

除了Cookie和Session之外，还有一些其他的会话管理方法。这些方法可能在特定的应用场景或安全需求下更为适用。以下是一些常见的会话管理方法：

1. **Token-Based Authentication：**
   - 使用令牌（Token）进行身份验证和会话管理是一种常见的方法。用户在登录成功后，服务器生成一个令牌，并将其返回给客户端。客户端在后续的请求中通过在请求头或参数中携带令牌来进行身份验证。这种方式常用于无状态的分布式系统，例如基于JWT（JSON Web Token）的身份验证。

2. **OAuth 和 OpenID Connect：**
   - OAuth和OpenID Connect是用于授权和身份验证的开放标准。OAuth用于授权，而OpenID Connect建立在OAuth之上，提供了身份验证的功能。它们通过令牌和授权码等机制实现会话管理，适用于跨域认证和授权场景。

3. **LocalStorage 和 SessionStorage：**
   - 前端Web存储技术，LocalStorage和SessionStorage是在浏览器端存储数据的方法。它们可以用于在客户端存储一些会话信息，但相较于Cookie，它们在HTTP请求中不会自动发送到服务器。需要注意的是，这种方法不适合存储敏感信息。

4. **JSON Web Token（JWT）：**
   - JWT是一种轻量级的、跨平台的身份验证和信息传递的开放标准。它将用户的身份信息以JSON格式进行编码，并使用签名进行验证。JWT可以用于在客户端和服务器之间传递信息，实现无状态的身份验证。

5. **Single Sign-On（SSO）：**
   - SSO是一种身份验证机制，允许用户在多个应用程序中使用单一的身份认证。用户只需登录一次，就能在多个应用程序中使用相同的身份信息。常见的SSO实现包括OAuth和SAML（Security Assertion Markup Language）。

6. **Biometric Authentication：**
   - 生物识别身份验证，如指纹识别、面部识别等，可以用于建立和管理用户的会话。这种方式通常用于移动设备或需要更高安全性的应用。

每种会话管理方法都有其适用的场景和优缺点。选择合适的方法取决于应用的需求、安全性要求以及用户体验等方面的考虑。在设计会话管理机制时，还需要综合考虑数据的传输安全性、用户隐私保护等因素。
