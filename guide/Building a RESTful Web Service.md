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
