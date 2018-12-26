---
title: SpringBoot添加jsp支持
date: 2017-08-13 20:45:29
categories: 
 - 技术研究
tags:
 - springboot
---

> SpringBoot官方是推荐使用Thymeleaf，而不建议使用jsp作为页面的，但是，这总难不倒我们，不推荐并不代表不能使用。

1. 第一种方法，那就是建立一个常规web项目，然后添加springBoot的各种依赖，以及启动文件，但是，这并不是我们最想要的，所以，在此推荐第二种方法。

2. 首先，是添加支持编译jsp的Maven依赖

   ```java
   <!--用于编译jsp-->
   <dependency>
       <groupId>org.apache.tomcat.embed</groupId>
       <artifactId>tomcat-embed-jasper</artifactId>
       <scope>provided</scope>
   </dependency>
   ```

   如果使用的是IDEA开发，scope需要更改为其他类型，如compile，项目启动后，才能找到跳转页面。

   其次，在application.properties配置中，添加以下配置

   ```java
   spring.mvc.view.prefix: /WEB-INF/jsp/
   spring.mvc.view.suffix: .jsp
   ```

   在此，特别强调，/WEB-INF/jsp需要在resources下新建如下文件夹，META-INF/resources/,也就是，spring.mvc.view.prefix的起始根目录是resources/META-INF/resources，这是唯一不爽的地方，路径太长，但是，也能忍受了，比起使用熟悉的jsp开发，这一点不算什么大问题。