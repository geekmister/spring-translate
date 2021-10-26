# 构建一个RESTful Web服务

这份指南将带着你完成使用Spring创建一个"Hello World"的RESTful web服务的整个过程。

## 译者说

因我个人工作需求，所以在查阅官方资料时，顺便将官方资料翻译成中文。因本人非专业翻译，所以难免在语义上会略有错误，但是在逻辑上是没有问题的，因为我也是程序员，如果有需要阅读官方资料，还请移步官方[Building a RESTful Web Service](https://spring.io/guides/gs/rest-service/)。

如需帮忙，或者请想参与一起翻译，可以发邮件联系我，geekmister.mg@gmail.com

## 你将构建的是什么？

你将要构建一个可以处理http://localhost:8080/greeting请求的服务。

greeting这个接口将会返回一个JSON格式的响应，如下表所示：

```
{"id":1,"content":"Hello, World!"}
```

在查询字符串中你可以用一个可选参数```name```定制greeting这个接口，如下表所示：

```
http://localhost:8080/greeting?name=User
```

这个```name```参数值会覆盖默认值```World```，并且会在响应中反射回来，如下表所示:

```
{"id":1,"content":"Hello, User!"}
```

## 你需要做什么？

- 大概15分钟时间
- 一个你喜欢的文本编辑器或者IDE
- [JDK 1.8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or later
- [Gradle 4+](http://www.gradle.org/downloads) or [Maven 3.2+](https://maven.apache.org/download.cgi)
- 你可以直接将代码导入进你的IDE:
  - [Spring Tool Suite (STS)](https://spring.io/guides/gs/sts)
  - [IntelliJ IDEA](https://spring.io/guides/gs/intellij-idea/)

## 该怎样完成这篇指南

类似其他Spring开始指南，你可以从头开始一步一步完成或者绕过你已经熟悉的步骤。无论哪种方法，你最终可以将这些代码应用到到你工作中。

从头开始，请移步到[Starting with Spring Initializr](https://spring.io/guides)

跳过基础步骤，按照如下操作：

- [下载](https://github.com/spring-guides/gs-rest-service/archive/main.zip)本指南的资源仓库，或者使用[git](https://spring.io/understanding/Git)克隆它:
```
git clone https://github.com/spring-guides/gs-rest-service.git
```

- 打开```gs-rest-service/initial```

- 创建一个实体类

当你完成上述操作时，你可以在```gs-rest-service/complete```中检查你的结果代码。

## 使用Spring Initializr开始

// TODO

## 创建一个实体类

// TODO

## 创建一个资源控制器

在Spring构建RESRful Web Service的方法中，Http请求是被Controller处理的。这些Controller使用```@RestController```注解进行标记，```GreetingController```详情如下(所在位置:```src/main/java/com/example/restservice/GreetingController.java```)```/greeting```处理```get```请求，处理完成后返回一个```Greeting```的实例:

```
package com.example.restservice;

import java.util.concurrent.atomic.AtomicLong;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

	private static final String template = "Hello, %s!";
	private final AtomicLong counter = new AtomicLong();

	@GetMapping("/greeting")
	public Greeting greeting(@RequestParam(value = "name", defaultValue = "World") String name) {
		return new Greeting(counter.incrementAndGet(), String.format(template, name));
	}
}
```

这个Controller比较简洁且只是一个样例，在这个模板下还有很多事情要做，我们接下来一步一步攻克。

```@GetMapping```注解标记了当用户发起```/greeting```的Get http请求时将被映射到```greeting()```方法进行处理。

标记http请求处理方法的其他注解还有，例如```@PostMapping```是用来标记处理post http请求方法的注解，你也可以换一种写法，```@RequestMapping```，但是你需要声明http 请求的方式，这样写```@RequestMapping(method=GET)```

@RequestParam绑定的值是查询参数name，这个参数name作为greeting()的参数name传入，如果查询参数不存在name，设置的defaultValue=world将被作为默认值传入。
