# Tomcat 请求参数乱码

## POST 请求参数乱码

设置 POST 请求报文的编码方式。

```java
req.setCharacterEncoding("UTF-8");
```

## GET 请求参数乱码

GET 请求参数特殊符号是 URL 编码，修改 Tomcat 的 server.xml 配置文件项 Connector。

```xml
<Connector URIEncoding="UTF-8" port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443"
           maxParameterCount="1000"
/>
```

