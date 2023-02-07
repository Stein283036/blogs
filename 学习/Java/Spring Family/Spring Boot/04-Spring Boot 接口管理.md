# 04-Spring Boot 接口管理

## Swagger

## Spring Boot API 接口调试 IDEA HTTP Client

IDEA HTTP Client 是 IDEA 提供的 HTTP API **测试**插件，默认**内置**，直接开启即可使用。

![IDEA HTTP Client 示例](https://static.iocoder.cn/images/Spring-Boot/2019-12-01/12.gif)

3 种**常见** HTTP API 的示例：

- GET 请求

- POST 请求 + Form

  ```http
  ### 测试 /user/login：登陆成功POST http://127.0.0.1:8080/user/loginContent-Type: application/x-www-form-urlencodedusername=yudaoyuanma&password=123456
  ```

- POST 请求 + JSON

  ```http
  ### 测试 /user/update：更新成功POST http://127.0.0.1:8080/user/updateContent-Type: application/json{  "nickname": "我是昵称",  "gender": 1}
  ```

在 Spring Boot 项目中，我们通过 **Profile** 机制，实现不同环境，不同配置文件。在 IDEA HTTP Client 插件中，提供类似的机制，可以定义配置文件，抽取出不同环境的**变量**。

- 通过创建 `http-client.env.json` 配置文件，定义**通用**变量。例如说，url 地址、port 端口等等。
- 通过创建 `http-client.private.env.json` 配置文件，定义**敏感**变量。例如说，username/password 账号密码、token 访问令牌等等。

## 参考文章

- [芋道 Spring Boot API 接口文档 Swagger 入门](https://www.iocoder.cn/Spring-Boot/Swagger/)
- [芋道 Spring Boot API 接口调试 IDEA HTTP Client](https://www.iocoder.cn/Spring-Boot/IDEA-HTTP-Client/)