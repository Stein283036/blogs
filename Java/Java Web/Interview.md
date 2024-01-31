# Java Web Interview

## JSP 有哪些内置对象，作用分别是什么

- request：封装客户端的请求，其中包含来自 get 或 post 请求的参数

- response：封装服务器对客户端的响应

- pageContext：通过该对象可以获取其他对象

- session：封装用户会话的对象

- application：封装服务器运行环境的对象

- out：服务器响应的输出流对象

- config：Web 应用的配置对象

- page：JSP 页面本身

- exception：封装页面抛出异常的对象

## JSP 的四种作用域

- page
- request
- session
- application

## session 和 cookie 的区别

- session 存储在服务器，cookie 存储在客户端浏览器
- cookie 安全性差，容易被劫持篡改
- cookie 有大小限制

## session 的工作原理

## 如何避免 SQL 注入

- 使用 PreparedStatement 预编译 SQL 语句
- 检查用户输入，使用正则表达式过滤特殊字符

## 什么是 XSS 攻击，如何避免

## 什么是 CSRF 攻击，如何避免

## http 响应码 301 和 302 代表的是什么，有什么区别

## forward 和 redirect 的区别

## 跨域解决方案







