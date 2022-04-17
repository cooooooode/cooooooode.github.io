---
title: property-can-not-found错误
date: 2022-04-17 11:42:31
tags:
  - java
  - spring
  - problems
---

### java Properties  could not be found错误

跟着spring tutorial学习的过程中，在学到上传文件 `https://spring.io/guides/gs/uploading-files/` 的时候按照原文代码编译报错了，错误如下

```bash
Parameter 0 of constructor in com.example.uploadingfiles.storage.FileSystemStorageService required a bean of type 'com.example.uploadingfiles.storage.StorageProperties' that could not be found.
```

![](/images/2020-04-17-property-problem.png)

大意是说定义的property没有找到，但是在入口不是使用了@SpringApplication注解吗，怎么会扫描不到呢，后来Google一番，发现说是被覆盖掉了，经过一番折腾终于解决了。

解决办法就是需要在你的property添加`@Component`注解，这样就能被发现了。

![](/images/2022-04-17-component.png)


最开始的时候还遇到了这个报错 

```bash
@ConfigurationProperties Spring Boot Configuration Annotation Processor not found in classpath

@ConfigurationProperties Spring Boot Configuration Annotation Processor not configured
```

解决办法是安装依赖 `spring-boot-configuration-processor` 更新pom.xml

![](/images/2022-04-17-processor.png)


### 参考

[https://stackoverflow.com/questions/42839126/configurationproperties-spring-boot-configuration-annotation-processor-not-foun](https://stackoverflow.com/questions/42839126/configurationproperties-spring-boot-configuration-annotation-processor-not-foun)

[https://www.roseindia.net/answers/viewqa/Spring/265507-consider-defining-a-bean-of-type-in-your-configuration-spring-boot.html](https://www.roseindia.net/answers/viewqa/Spring/265507-consider-defining-a-bean-of-type-in-your-configuration-spring-boot.html)

[https://github.com/spring-projects/spring-boot/issues/19603](https://github.com/spring-projects/spring-boot/issues/19603)