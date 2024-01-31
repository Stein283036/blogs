# Interview

## 框架概述

## 框架的功能

- 轻量
- IOC
- AOP
- 事务控制
- 异常处理
- 其它框架

## 模块组成以及它们的功能

Spring大约18个基本模块，大致分为4类；分别是核心模块、AOP、数据访问、Web模块、测试模块。

核心模块包括：core、beans、context、context-support、expression共5个模块；

AOP模块包括：aop、aspects、instrument共3个模块；

数据访问模块包括：jdbc、tx、orm、oxm共4个模块；

Web模块包括：web、webmvc、websocket、webflux共4个模块；

集成测试模块：test模块。

## IOC 以及 AOP

## BeanFactory 和 ApplicationContext

## DI 的注入方式有哪些

## **Spring 容器配置的方式**

- XML 配置文件
- 注解配置
- Java 代码配置

## Bean 的作用域

singleton、prototype、request、session、global-session

## Bean 的声明周期

## Bean 线程安全

默认线程的作用域是 singleton 单例的，如果是无状态的 bean 则是线程安全的，有状态的 bean 需要修改 bean 的作用域 为 prototype。

## Bean 自动装配的方式有哪些

## 事务管理

- 声明式
- 编程式

## @**Required** 注解

## @Qualifier 注解

## Spring 事务的隔离级别

## Spring 框架中都用到了哪些设计模式

## FileSystemResource 和 ClassPathResource 的区别

