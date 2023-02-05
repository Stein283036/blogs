# 10-Spring Boot 分布式 Session

> Session 的一致性，简单来理解，就是相同 sessionid 在多个 Web 容器下，Session 的数据要一致。

我们先以用户使用浏览器，Web 服务器为**单台** TomcatA 举例子。

- 浏览器在第一次访问 Web 服务器 TomcatA 时，TomcatA 会发现请求的 Cookie 中**不**存在 sessionid ，所以创建一个 sessionid 为 X 的 Session ，同时将该 sessionid 写回给浏览器的 Cookie 中。
- 浏览器在下一次访问 Web 服务器 TomcatA 时，TomcatA 会发现请求的 Cookie 中**已**存在 sessionid 为 X ，则直接获得 X 对应的 Session 。

友情提示，Tomcat 产生的 sessionid 为 jsessionid 。

我们再以用户使用浏览器，Web 服务器为**两台** TomcatA、TomcatB 举例子。

- 接上述例子，浏览器已经访问 TomcatA ，获得 sessionid 为 X 。同时，在多台 Tomcat 的情况下，我们需要采用 Nginx 做负载均衡。
- 浏览器又发起一次请求访问 Web 服务器，Nginx 负载均衡转发请求到 TomcatB 上。TomcatB 会发现请求的 Cookie 中**已**存在 sessionid 为 X ，则直接获得 X 对应的 Session 。结果呢，找不到 X 对应的 Session ，只好创建一个 sessionid 为 X 的 Session 。
- 此时，虽然说浏览器的 sessionid 是 X ，但是对应到两个 Tomcat 中两个 Session 。那么，如果在 TomcatA 上做的 Session 修改，TomcatB 的 Session 还是原样，这样就会出现 **Session 不一致**的问题。

## 参考文章

- [芋道 Spring Boot 分布式 Session 入门](https://www.iocoder.cn/Spring-Boot/Distributed-Session/)