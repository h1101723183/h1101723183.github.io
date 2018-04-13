---
layout: post
title: "Spring boot项目部署war包"
description: 
headline: 
modified: 2017-11-27
category: java
tags: [blog, work, spring boot, java]
imagefeature: 
mathjax: 
featured: true
---


# Spring boot项目部署war包

参考：https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#howto-create-a-deployable-war-file

### 1、修改pom.xml
1、修改packaging为war
2、增加spring-boot-starter-tomcat,并设置scope为provided

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <!-- ... -->
    <packaging>war</packaging>
    <!-- ... -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
        <!-- ... -->
    </dependencies>
</project>
```

### 2、创建SpringBootServletInitializer的子类


修改RecruitmentApplication文件

```
@SpringBootApplication
public class RecruitmentApplication extends SpringBootServletInitializer {

	@Override
	protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
		return builder.sources(RecruitmentApplication.class);
	}

	public static void main(String[] args) {
		SpringApplication.run(RecruitmentApplication.class, args);
	}
}
```

