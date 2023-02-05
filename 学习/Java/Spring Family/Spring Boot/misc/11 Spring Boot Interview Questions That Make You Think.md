# [11 Spring Boot Interview Questions That Make You Think](https://www.marcobehler.com/guides/spring-boot-interview-questions)

Most lists of Spring Boot Interview questions make you memorize random details from the Spring Boot documentation. But memorization is a poor substitute for truly understanding and feeling confident about Spring Boot.

So today, we’re going to take a different approach. Rather than listing 50 questions on Spring Boot minutiae, we’re going to focus on 11 that make you think and thus learn a lot along the way.

Here they are, in random order.

## 1. Is the following statement true or false: "Every Spring Boot application is a web application running within an embedded Apache Tomcat". Give reasons for your answer.

The statement is false.

When it comes to web applications, Spring Boot works with a variety of servlet containers. The default one is [Apache Tomcat](http://tomcat.apache.org/), but you can also use it with [Jetty](https://www.eclipse.org/jetty/), [Undertow](https://undertow.io/), or without an embedded servlet container at all.

What’s more, Spring Boot isn’t tied to just web applications, though one might get that impression by using the spring-boot-starter-web dependency and thus Spring Boot’s web [autoconfiguration](https://www.marcobehler.com/guides/spring-boot). You can write all kinds of services with it, from batch jobs and command-line services, over to messaging backends and reactive web applications.

## 2. What is the difference between Spring Boot and Spring MVC? Or between Spring Boot and Spring Framework? Can you use them together in the same project?

Spring Boot builds *on top* of [Spring Framework](https://spring.io/projects/spring-framework) and Spring MVC.

Example: Spring Framework offers you the ability to read in .properties files from a variety of places, e.g. with the help of @PropertySource annotations. It also offers you the ability to write JSON REST controllers with the help of its Web MVC framework.

The issue is, you have to tell Spring from where to read in your properties and properly configure its web framework for e.g. JSON support. Spring Boot, on the other hand, takes these individual pieces and pre-configures them for you. Example:

- *It always and automatically* looks for application.properties files in various predefined places and reads them in.
- *It always boots up an embedded Tomcat* so you can immediately see the results of writing your @RestControllers and start writing web applications
- *It automatically* configures everything for you to send/receive JSON, without needing to worry a ton about specific Maven/Gradle dependencies. All, by running the main method in a Java class, which is annotated with the @SpringBootApplication annotation.
  If this explanation still leaves you with questions, have a look at [this extensive guide I wrote](https://www.marcobehler.com/guides/spring-framework), covering the topic in more detail.

## 3. Name two ways to create a new Spring Boot project from scratch? Also, how do you know what spring-boot-starters your project needs?

You can create new Spring Boot projects through the [Spring Initializr](https://start.spring.io/) web application or the [Spring Boot CLI](https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started-installing-the-cli). Interestingly enough, Spring Initializr is not just a website where you can generate project skeleton .zip files. It is also an API, that you can programmatically call. All major IDEs (Spring Tool Suite, IntelliJ IDEA Ultimate, Netbeans and VSCode) directly integrate with it, so that you can create new Spring Boot projects right out of your IDE.

As for starters, you need to read [the documentation](https://docs.spring.io/spring-boot/docs/2.3.3.RELEASE/reference/htmlsingle/#using-boot-starter) and have a bit of experience. If working with a web application, you will start with *spring-boot-starter-web* and then add the appropriate starter from the documentation, once you want to include a certain technology. After a while, you will get a good feel for what starters you need for which technologies.

## 4. Why do you not need to specify dependency versions in your pom.xml file when including 3rd party libraries? Does that hold true for all 3rd party libraries or only some? How can you find out what libraries Spring Boot supports?

This is because Spring Boot does *some* dependency management for you.

On a high-level, Spring Boot starters pull-in a parent pom.xml file (or a build.gradle file) which has all the dependencies and respective versions defined that a specific Spring Boot version supports - **a so-called bill of materials**. You can then simply use those pre-defined versions, or override the version numbers in your own build scripts.

You can find the list of all currently supported 3rd party libraries and versions in the [spring-boot-dependencies](https://github.com/spring-projects/spring-boot/blob/master/spring-boot-project/spring-boot-dependencies/build.gradle) project.

## 5. You want to make your application configurable, say specify a different database connection for development and production environments. What are your options?

By default, Spring Boot pulls in properties [from almost 20 locations](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config), from environment variables and command-line arguments to configuration files (application.properties).
These locations are also ordered, so that the locations lower in the list, override earlier ones. You can, for example, put a default application.properties inside your deployable .jar file, whereas your ops colleagues only override some of them by supplying their own application.properties file on the deployment machine.

It is essential to understand these locations and the default behavior, as to not re-implement Spring Boot’s properties functionality with a custom PropertySourceProvider or use more heavyweight options like spring-cloud configuration server.

You also need to make sure to understand Spring’s [relaxed properties binding concept](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config-relaxed-binding-from-environment-variables), in that you can bind properties from those locations to configuration bean properties, without an explicit name match.

## 6. Is the following statement true or false: "Every Spring Boot project must use Thymeleaf as an HTML templating engine". What are your options when it comes to rendering HTML?

The statement is false.

Spring Boot works with a variety of HTML template engines, and while [Thymeleaf](https://www.thymeleaf.org/) is a popular choice and fully integrated with Spring, you can also use many others, like [Freemarker](https://freemarker.apache.org/), [Velocity](https://velocity.apache.org/) or even [JSP](https://docs.oracle.com/javaee/5/tutorial/doc/bnagy.html) (though not strictly a templating engine).

It is usually recommended to go with the option you are most comfortable with / that is being used in your company as the default.

## 7. How can you implement relational database access with Spring Boot? What are your options?

Spring Boot integrates with plenty of Java database access libraries ([see a comprehensive list here](https://www.marcobehler.com/guides/java-databases)). The majority of users will probably go with [spring-boot-starter-jpa](https://spring.io/guides/gs/accessing-data-jpa/), [spring-boot-starter-jdbc](https://spring.io/guides/gs/relational-data-access/) or one of the corresponding [spring-data projects](https://spring.io/projects/spring-data).

There are also more lightweight alternatives, such as [jOOQ](https://www.jooq.org/) or [myBatis](https://mybatis.org/mybatis-3/). Finally, you can always go with NoSQL options, such as [MongoDB](https://spring.io/guides/gs/accessing-data-mongodb/) etc.

## 8. You need to configure logging in your application but you want to differentiate between the log levels on your machine and the log levels on different environments (qa, test, prod). What options do you have?

First off, it is always a good idea to properly understand the [Java logging ecosystem](https://www.marcobehler.com/guides/a-guide-to-logging-in-java) and then read the corresponding Spring Boot [chapter on logging](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-logging).

There are various options when it comes to configuring your output:

- Directly in an application.properties file (that can and should of course differ in DEV and PRD environments).
- Depending on the used logging framework, specifying a custom configuration file (such as logback-spring.xml).
- Or even through JMX at runtime.

The two popular, modern logging libraries, Logback and Log4j2, also support hot reloading of the logging configuration, without having to bounce your application

## 9. What is the easiest way to deploy a Spring Boot application in production? What other options are there?

The simplest way to deploy your Spring Boot application is as a .jar file with an embedded servlet container, to any server or platform that has a JRE installed.
For organizational and historical reasons, you can also deploy your Spring Boot application as a .war file, into an existing servlet container or application server.

Last but not least, you can, of course, also put your .jar file into a Docker image and even deploy those with Kubernetes.

## 10. You’ve been told to enable "Spring Security" on your application. What happens when you add the Spring Security starter to your application?

This is a bit of a trick question. Adding the Spring Security Starter to your app, will suddenly prompt you with a login every time you try to access your application. Also, form submissions/REST endpoints will work differently or are outright blocked.

The gist is, that you "do not simply enable" security on a Spring Boot application, you need a solid understanding of what you are doing.

Luckily, I wrote a comprehensive [guide on Spring Security](https://www.marcobehler.com/guides/spring-security), that explains all the gory aspects of security in the easiest way possible.

## 11. How would you find out which auto-configurations Spring Boot applied on startup and which conditions it evaluated?

[Spring Boot Actuato](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html)r can provide that information, through HTTP or JMX endpoints. Alternatively, you can start-up your Spring Boot application with the "--debug" flag.

Do note, that the information on evaluated conditions is a bit "raw" and not easily digested. For that, [read this guide](https://www.marcobehler.com/guides/spring-boot) to make sure you understand how Spring Boot’s auto-configurations work.

## Fin

There is obviously no guarantee that you will meet these questions in your own Spring Boot interview, though knowing (and understanding) the answers to them should prove as a solid foundation for any interview.

If you want to get a deeper understanding of the entire Spring ecosystem, you might also want to check out the other Spring articles [on my blog](https://www.marcobehler.com/guides) and the [Confident Spring Developer](https://www.marcobehler.com/courses/spring-professional) course.

Do you have any other questions you think might be useful for interviews? Let me know in the comment section.

Enjoy!