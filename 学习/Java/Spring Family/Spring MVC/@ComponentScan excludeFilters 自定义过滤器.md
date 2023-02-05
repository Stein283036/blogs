# @ComponentScan excludeFilters 自定义过滤器

@ComponentScan 用来扫描应用程序中的组件即Bean，当一个组件使用@Component或者@Component的复合注解，它就是一个候选Bean，如果有@Condition注解的话，那么还需要在满足条件的情况下，才能成为待注册的Bean。

## 过滤指定的注解

```java
@SpringBootApplication
@ComponentScan(basePackages = "com.guhe.springbootdemo", excludeFilters = {@ComponentScan.Filter(type = FilterType.ANNOTATION, classes = {Service.class, Controller.class})})
public class SpringBootDemoApplication {

	public static void main(String[] args) {
		ConfigurableApplicationContext ctx = SpringApplication.run(SpringBootDemoApplication.class, args);
		String[] beanDefinitionNames = ctx.getBeanDefinitionNames();
		boolean myService = Arrays.asList(beanDefinitionNames).contains("myService");
		boolean myController = Arrays.asList(beanDefinitionNames).contains("myController");
		System.out.println("myService = " + myService);
		System.out.println("myController = " + myController);
	}

}

@Service
class MyService {

}

@Controller
class MyController {

}
```

## 过滤指定的类

```java
@ComponentScan(basePackages = "com.guhe.springbootdemo", excludeFilters = {@ComponentScan.Filter(type = FilterType.ASSIGNABLE_TYPE, classes = {MyService.class})})
```

## 自定义过滤

通过将 type 设置为 FilterType.CUSTOM，来实现自定义过滤，自定义的 classes 指定的类要实现**TypeFilter**接口。

```java
package com.guhe.springbootdemo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.FilterType;
import org.springframework.core.io.Resource;
import org.springframework.core.type.AnnotationMetadata;
import org.springframework.core.type.ClassMetadata;
import org.springframework.core.type.classreading.MetadataReader;
import org.springframework.core.type.classreading.MetadataReaderFactory;
import org.springframework.core.type.filter.TypeFilter;
import org.springframework.stereotype.Controller;
import org.springframework.stereotype.Service;

import java.io.IOException;
import java.util.Arrays;

@SpringBootApplication
@ComponentScan(basePackages = "com.guhe.springbootdemo", excludeFilters = {@ComponentScan.Filter(type = FilterType.CUSTOM, classes = {MyTypeFilter.class})})
public class SpringBootDemoApplication {

	public static void main(String[] args) {
		ConfigurableApplicationContext ctx = SpringApplication.run(SpringBootDemoApplication.class, args);
		String[] beanDefinitionNames = ctx.getBeanDefinitionNames();
		boolean myService = Arrays.asList(beanDefinitionNames).contains("myService");
		boolean myController = Arrays.asList(beanDefinitionNames).contains("myController");
		System.out.println("myService = " + myService);
		System.out.println("myController = " + myController);
	}

}

class MyTypeFilter implements TypeFilter {

	@Override
	public boolean match(MetadataReader metadataReader, MetadataReaderFactory metadataReaderFactory) throws IOException {
		AnnotationMetadata annotationMetadata = metadataReader.getAnnotationMetadata();
		Resource resource = metadataReader.getResource();
		ClassMetadata classMetadata = metadataReader.getClassMetadata();
		System.out.println(classMetadata.getClassName());
		if (classMetadata.getClassName().contains("MyService")) {
			return true;
		}
		return false;
	}
}

@Service
class MyService {

}

@Controller
class MyController {

}
```

