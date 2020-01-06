[toc]

# Spring Boot Admin

​		第三方文档: [Spring Boot Admin](https://www.cnblogs.com/forezp/p/10242004.html)

​		**用于管理和监控SpringBoot服务应用，显示如运行状态、内存使用、进程和线程情况的运行细节，以及应用配置、Bean列表等应用内部细节，整体上偏向于对于服务应用单体的详细监控。**

---

## Admin Server

1. 加入依赖

   ​		*不同于文档，此处使用的是2.2.0版本，加入了对于中文的支持，并且对Spring Boot 和Spring Cloud已经进行了统一版本依赖管理*

```xml
<!--        Spring Boot Starter-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>
<!--        Spring Boot Admin Server-->
        <dependency>
            <groupId>de.codecentric</groupId>
            <artifactId>spring-boot-admin-starter-server</artifactId>
            <version>${spring-boot-admin.version}</version>
        </dependency>
<!--        Spring Boot Web-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
```

2. 配置文件中指定端口名和应用名
3. 主配置类上添加注解`@EnableAdminServer`

---

## Admin Client

1. 加入依赖

```xml
<!--        Spring Boot Starter-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>
<!--        Spring Boot Admin Client-->
        <dependency>
            <groupId>de.codecentric</groupId>
            <artifactId>spring-boot-admin-starter-client</artifactId>
            <version>${spring-boot-admin.version}</version>
        </dependency>
<!--        Spring Boot Web-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
<!--        Spring Boot Actuator-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
```

2. 配置文件中指定Admin Server地址，以及暴露监控端点

```yml
spring:
  application:
    name: AdminClient
  boot:
    admin:
      client:
        url: http://localhost:8888
 
management:
  endpoints:
    web:
      exposure:
        include: '*'
  endpoint:
    health:
      show-details: ALWAYS
```

3. 运行后在Admin Server上应用选项查看应用列表以及URL、运行时间，应用墙中点击对应应用可以查看应用详细信息。

---

## 配合微服务注册中心

​		Admin Server还可以配合微服务注册中心进行使用，例如Eureka和Nacos等，只需在注册在这些注册中心的应用中添加以上依赖与配置，即可通过Spring Boot Admin配合注册中心对服务进行综合监控与管理。详细实现的示例可查看Demo项目。


