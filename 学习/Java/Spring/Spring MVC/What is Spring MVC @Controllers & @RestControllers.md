# [What is Spring MVC: @Controllers & @RestControllers](https://www.marcobehler.com/guides/spring-framework)

## Introduction

[Spring MVC](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html) is Spring’s web framework. It lets you build web sites or RESTful services (think: JSON/XML) and is nicely integrated into the Spring ecosystem, e.g. it powers the @Controllers and @RestControllers of your Spring Boot applications.

## MVC Basics: HttpServlets

When writing web applications in Java, with or without Spring (MVC/Boot), you are mostly talking about writing applications that return two different data formats:

1. **HTML** → Your web app creates HTML pages that can be viewed in a browser.
2. **JSON/XML** → Your web app provides RESTful services, that produce JSON or XML. Javascript-heavy websites or even other web services can then consume the data that these services provide.

How would you write such applications *without* any framework? Just with plain Java?

Answering this question is essential to *really* understanding Spring MVC, so do not just skip ahead because you think it has nothing to do with Spring MVC.

**Answer**

At the lowest level, every Java web application consists of one or more `*HttpServlets*`. They generate your HTML, JSON, or XML.

In fact, (almost) every single framework of the 1 million available Java web frameworks ([Spring MVC](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html), [Wicket](https://wicket.apache.org/), [Struts](https://struts.apache.org/)) is built *on top* of HttpServlets.

### How to write HTML pages with HttpServlets

Let’s have a look at a super simple HttpServlet that returns a very simple, static, HTML page.

```java
package com.marcobehler.springmvcarticle;

import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class MyServletV1 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        if (req.getRequestURI().equals("/")) {
            resp.setContentType("text/html");
            resp.getWriter().print("<html><head></head><body><h1>Welcome!</h1><p>This is a very cool page!</p></body></html>");
        }
        else {
            throw new IllegalStateException("Help, I don't know what to do with this url");
        }
    }
}
```

After writing your servlet, you would register it with a servlet container, like [Tomcat](https://tomcat.apache.org/) or [Jetty](https://www.eclipse.org/jetty/).

Remember: web sites are just HTML strings!

### How to write JSON endpoints with HttpServlets

Imagine that apart from your (pretty empty) HTML index page, you now also want to offer a REST API for your soon-to-be-developed front end. So your React or AngularJS front end would call a URL like this:

```
*/api/users/{userId}*
```

That endpoint should return data in JSON format for the user with the given userId. How could we enhance our `*MyServlet*` to do this, again, no frameworks allowed?

```java
package com.marcobehler.springmvcarticle;

import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class MyServletV2 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        if (req.getRequestURI().equals("/")) {
            resp.setContentType("text/html");
            resp.getWriter().print("<html><head></head><body><h1>Welcome!</h1><p>This is a very cool page!</p></body></html>");
        } else if (req.getRequestURI().startsWith("/api/users/")) {

            Integer prettyFragileUserId = Integer.valueOf(req.getRequestURI().lastIndexOf("/") + 1);

            resp.setContentType("application/json");

            // User user = dao.findUser(prettyFragileUserId)
            // actually: jsonLibrary.toString(user)
            resp.getWriter().print("{\n" +
                    "  \"id\":" + prettyFragileUserId + ",\n" +
                    "  \"age\": 55,\n" +
                    "  \"name\" : \"John Doe\"\n" +
                    "}");
        } else {
            throw new IllegalStateException("Help, I don't know what to do with this url");
        }
    }
}
```

## What is Spring MVC’s DispatcherServlet?

What if I told you that Spring MVC is really just one servlet, like our uber-servlet above? (And yes, that’s of course a bit of a lie)

Meet the `*DispatcherServlet*`.

Spring MVC’s DispatcherServlet handles `*every*` incoming HTTP request (that’s it is also called *front controller*). Now, what does *handle* mean, exactly?

### A sample HTTP request flow

Imagine a "register user workflow", where a user fills out a form and submits it to the server to get a nice little success HTML page back.

In that case, your DispatcherServlet needs to do the following things:

1. It needs to have a look at the incoming HTTP method request URI and any request parameters. E.g.: `*POST /register?name=john&age33*`.
2. It needs to potentially convert the incoming data (request parameters/body) to nice little Java objects and forward them to a `*@Controller*` or `*@RestController*` class that *you* wrote.
3. Your `*@Controller*` method saves a new user to the database, maybe sends out an email, etc. It would highly likely delegate that to another service class, but let’s assume for now this happens inside the controller.
4. It needs to take whatever the output from your @Controller was and convert it back to `*HTML/JSON/XML*`.

## How to write HTML with @Controllers

A controller class in Spring is simply annotated with the `*@Controller*` annotation, it does not need to implement a specific interface or extend from another class.

```
<p th:text="'Hello ' + ${user.name} + '!'"></p>
```

The question is, what is this `*th:text=*` syntax? Is that Spring-specific? Is it something else?

And the answer is that Spring MVC doesn’t really know anything about HTML templates. It needs a 3rd-party templating library to do all HTML templating work and doesn’t necessarily care what library you choose.

In the above case, you are looking at a [Thymeleaf](https://www.thymeleaf.org/) template, which is a very popular choice when working on Spring MVC projects.

### Spring MVC & Templating Libraries

There are several different templating libraries that integrate well with Spring MVC that you can choose from: [Thymeleaf](https://www.thymeleaf.org/), [Velocity](https://velocity.apache.org/), [Freemarker](https://freemarker.apache.org/), [Mustache](https://mustache.github.io/) and even [JSP](https://en.wikipedia.org/wiki/JavaServer_Pages) (even though that is not a templating library).

In fact, you *must* explicitly choose a templating library, because if you do not have such a templating library added to your project and configured correctly, then your @Controller method would not render your HTML page - because it wouldn’t know how to do it.

### What is a ViewResolver?

For a second, let’s think about where Spring will actually try and find your HTML templates that your @Controller returns.

The class that tries to *find* your template is called a `*ViewResolver*`. So whenever a request comes into your Controller, Spring will have a look at the configured ViewResolvers and ask them, in order, to find a template with the given name. If you don’t have any ViewResolvers configured, this won’t work.

Imagine you want to integrate with [Thymeleaf](https://www.thymeleaf.org/). Hence you would need a ThymeleafViewResolver.

```java
package com.marcobehler.springmvcarticle;

import org.springframework.context.annotation.Bean;
import org.thymeleaf.spring5.SpringTemplateEngine;
import org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver;
import org.thymeleaf.spring5.view.ThymeleafViewResolver;

public class ThymeleafConfig {

    @Bean
    public ThymeleafViewResolver viewResolver() {
        ThymeleafViewResolver viewResolver = new ThymeleafViewResolver();

        SpringResourceTemplateResolver templateResolver = new SpringResourceTemplateResolver();
        templateResolver.setPrefix("classpath:/templates");
        templateResolver.setSuffix(".html");
        // some other lines neglected...

        SpringTemplateEngine templateEngine = new SpringTemplateEngine();
        templateEngine.setTemplateResolver(templateResolver);
        // some other lines neglected...

        viewResolver.setTemplateEngine(templateEngine);
        return viewResolver;
    }
}
```

## How to write XML/JSON with @RestControllers

Things are a bit different when you are writing RESTFul services. Your client, be that a browser or another web service, will (usually) create JSON or XML requests. The client sends, say, a JSON request, you process it, and then the sender expects JSON back.

So, a sender might send you this piece of JSON as part of the HTTP request body.

```
POST http://localhost:8080/users

###
{"email": "angela@merkel.de"}
```

But on the Java side (in your Spring MVC program) you do not want to mess with raw JSON strings. Neither when receiving requests like above, nor when sending responses back to the client.

Instead, you’d like to just have Java objects that get converted automatically, by Spring.

```
public class UserDto {
    private String email;
    //...
}
```

This also means that you do *not* need all that model and view processing that you had to do when rendering HTML in your @Controllers. For RESTful services you don’t have a templating library reading in an HTML template and filling it with model data to generate a JSON response for you.

Instead, you want to go directly from HTTP Request → Java object and from Java Object → HTTP response.

As you might have guessed, that’s exactly what Spring MVC allows you to do, by writing `*@RestControllers*`.

### How (Response) Content Negotiation works: Accept Header

In short, content negotiation means that the *client* needs to tell your server what response format it wants to get back from your @RestController.

How? By specifying the `*Accept*` header with the HTTP request.

```
GET http://localhost:8080/transactions/{userid}
Accept: application/json
```

Spring MVC will have a look at that `*Accept*` header and know: The client wants JSON (application/json) back, so I need to convert my `*List<Transaction>*` to JSON. (Quick note: there are other ways to do [content negotiation](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-config-content-negotiation), but the Accept header is the default way.)

Let’s call this *response* content negotiation, because it is about the data format of the HTTP response that you are sending back to your client.

But content negotiation also works for incoming requests. Let’s see how.

### How Request Content Negotiation works: Content-Type Header

When building RESTful APIs, there’s an extremely high chance that you also want your clients to be able to send in JSON, or XML. Let’s pick up the example from the beginning of the chapter again, where you offer a REST endpoint to register new users:

```
POST http://localhost:8080/users

###
{"email": "angela@merkel.de"}
```

How would Spring know that the request body above contains JSON and not XML or YAML?

You might have guessed right, you’ll need to add another header, this time it’s the `*Content-Type*` header.

```
POST ...

Content-Type: application/json; charset=UTF-8

###
...
```

### How does Spring convert data formats?

There’s only one small problem: Spring knows about the Accept and Content-Type headers, but it does not know how to convert between Java Objects and JSON. Or XML. Or YAML.

It needs an appropriate 3rd-party library to do the dirty work (also called `*marshalling/unmarshalling*` or `*serialization/deserialization*`.)

And the classes that integrate between Spring MVC and these 3rd-party libaries are called `*HttpMessageConverters*`.

### What is a HttpMessageConverter?

An HttpMessageConverter is an interface with four methods (note, I simplified the interface a bit for an easier explanation, as it looks a bit more advanced in real life).

1. **canRead(MediaType)** → Can this converter read (JSON|XML|YAML|etc)? The MediaType passed in here is typically the value from the `*Content-Type*` request header.
2. **canWrite(MediaType)** → Can this converter write (JSON|XML|YAML|etc)? The MediaType passed in here is typically the value from the `*Accept*` request header.
3. **read(Object, InputStream, MediaType)** → Read my Java object from the (JSON|XML|YAML|etc.) InputStream
4. **write(Object, OutputStream, MediaType)** → Write my Java object to the OutputStream as (JSON|XML|YAML|etc.)

In short, a MessageConverter needs to know what MediaTypes it supports (think: application/json) and then needs to implement two methods to do the actual reading/writing in that data format.

### Which HttpMessageConverters are there?

Luckily, you don’t need to write these message converters yourself. Spring MVC comes with a class that automatically registers a couple of default HTTPMessageConverters for you - if you have the appropriate 3rd-party libraries on the classpath.

If you don’t know about this, it’ll sound like magic. In any case, have a look at Spring’s `*AllEncompassingFormHttpMessageConverter*` 

### Side-Note: Spring MVC, Spring Boot & RestControllers

When building Spring Boot projects, you’ll automatically use Spring MVC under the hood. But Spring Boot also pulls in Jackson by default.

*That* is the reason why you can immediately write JSON endpoints with Spring Boot, because the correct HttpMessageConverts will be added automatically for you.

## FAQ

### What kind of HTTP request input does Spring MVC understand?

Spring MVC understands basically everything that HTTP offers - with the help of third-party libraries.

That means you can throw JSON, XML, or HTTP (Multipart) Fileuploads request bodies at it, and Spring will conveniently convert that input to Java objects.

### What kind of HTTP responses can Spring MVC write?

Spring MVC can write anything that you want into an HttpServletResponse - with the help of 3rd-party libraries.

Be that HTML, JSON, XML or even WebSocket response bodies. Even better, it takes your Java objects and generates those response bodies for you.

### How to access the user’s current HttpSession?

In your Spring MVC @Controller or @RestController, you can simply specify the HttpSession as a method argument, and Spring will *automatically* inject it (creating one if it doesn’t yet exist)

You cannot do that with random @Components or @Services, but you are still able to @Autowire the HttpSession into them.

### How to access the HttpServletRequest?

In your Spring MVC @Controller or @RestController, you can simply specify the HttpServletRequest as a method argument and Spring will *automatically* inject it (creating one if it doesn’t yet exist)

You cannot do that with random @Components or @Services, but you are still able to @Autowire the HttpServletRequest into them.

### How to read HTTP Headers?

There’s a variety of ways to access the request headers, depending on whether you want just a single one or a map with all of them. In either case you need to annotate them with @RequestHeader.

```java
    @GetMapping("/headers1")
    public void singleHeader(@RequestHeader("x-forwarded-for") String xForwardedFor) {
       // ...
    }

    @GetMapping("/headers2")
    public void headersAsMap(@RequestHeader Map<String,String> headers) {  // or MultiValueMap<String,String>
        // ...
    }

    @GetMapping("/headers3")
    public void headersAsObject(HttpHeaders headers) {
        // ...
    }
```

### How to read and write cookies?

For reading cookies you can use the `*@CookieValue*` annotation in your controllers. You’ll have to write cookies directly to the HttpServletResponse.

### How can you handle file uploads in a Spring MVC application?

Given that you have the proper HTML file upload form, which reads something like this:

```
<form method="POST" enctype="multipart/form-data" action="/upload">
    File to upload:<input type="file" name="file" />
    <input type="submit" value="Upload" />
</form>
```

You simply need a @Controller with a corresponding @PostMapping and a MultiPartFile parameter, which contains your upload data and convenient methods to store the file on your disk.

```
package com.marcobehler.springmvcarticle;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.multipart.MultipartFile;


import java.io.IOException;
import java.nio.file.Path;
import java.nio.file.Paths;

@Controller
public class FileUploadController {

    @PostMapping("/upload")
    public String handleFileUpload(@RequestParam MultipartFile file) throws IOException {
        // don't generate upload files like this in a real project.
        // give them random names and save their uploaded name as metadata in a database or similar
        final Path uploadDestination = Paths.get("C:\\uploads").resolve(file.getName());

        file.transferTo(uploadDestination);
        return "redirect:/";
    }

}
```

### How to handle byte (xls, pdf, csv, jpg, zip file) downloads with Spring Controllers?

There’s a variety of ways to get this working, from writing directly to the HttpServletResponse or returning a byte[] as a result.

However, the most Spring-y and flexible version is by returning `*ResponseEntity<Resource>*`s. Depending on where you stored the file, you would use a different resource.

- On a disk → FileSystemResource
- On your project’s classpath → ClassPathResource
- Stream it from "somewhere" → InputStreamResource
- Have it available as byte[] in memory → ByteArrayResource

All that’s left to do then, is set the appropriate response HTTP headers (filename, content-type, etc).

```java
package com.marcobehler.springmvcarticle;

import org.springframework.core.io.ClassPathResource;
import org.springframework.core.io.Resource;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpStatus;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.server.ResponseStatusException;

import java.io.IOException;

@Controller
public class FileDownloadController {

    @RequestMapping(value = "/download/{jpgName}", method = RequestMethod.GET)
    public ResponseEntity<Resource> downloadJpg(
            @PathVariable String jpgName) throws IOException {

        //  Resource downloadResource = new InputStreamResource(soimeinputStream)
        //  Resource downloadResource = new ByteArrayResource(someByteArray)
        //  Resource downloadResource = new FileSystemResource(someFile)
        final ClassPathResource downloadResource = new ClassPathResource(jpgName);

        if (!downloadResource.exists()) {
            throw new ResponseStatusException(HttpStatus.BAD_REQUEST);
        }

        HttpHeaders headers = new HttpHeaders();

        // 1. set the correct content type
        headers.setContentType(MediaType.IMAGE_JPEG);

        // 2. set the correct content length, maybe stored in a db table
        headers.setContentLength(downloadResource.contentLength());

        // 3. if you want to force downloads, otherwise attachments might be displayed directly in the brwoser
        headers.setContentDispositionFormData("attachment", jpgName);

        return new ResponseEntity<>(downloadResource, headers, HttpStatus.OK);
    }
}
```

### How can I handle exceptions from my @Controllers globally?

There’s literally a gazillion ways of handling exceptions with Spring MVC, if you don’t want to handle them directly in your @Controller methods, but rather in one central place.

Create a `*@ControllerAdvice*` or `*@RestControllerAdvice*` class, in combination with the @ResponseStatus and @ExceptionHandler annotations. A couple of notes:

1. You might guess the difference between these two by understanding the difference between @Controllers and @RestControllers.
2. @ResponseStatus lets you define the HTTP Status code that should be returned to the client after handling your exception.
3. @ExceptionHandler specifies the exception that should trigger your handler method.
4. Other than that, it’s like writing a normal @Controller or @RestController.

