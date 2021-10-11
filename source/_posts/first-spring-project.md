---
title: "Hello Spring"
date: 2021-10-03 16:42
banner:
tags:
  - Java
  - Spring
---

### Spring网站下载压缩包

进入[https://start.spring.io/](https://start.spring.io/)网站，选择相关的配置, 然后下载就可以直接使用了。
注意如果需要web开发，需要选择web插件，否则不会包含相应类库。

如图所示

![](/images/2021-10-03-spring001.png)

用IDEA打开解压缩后的文件，即可自动下载相关类库。

可在application.properties文件中修改相关配置，如修改端口号

![](/images/2021-10-03-spring002.png)

### 通过IDEA来创建Spring Project

![](/images/2021-10-03-spring003.png)

![](/images/2021-10-03-spring004.png)

选择Spring Web即可。

### 实现第一个Restful Hello World

```java
package com.xuboso.demo3;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class Demo3Application {

    public static void main(String[] args) {
        SpringApplication.run(Demo3Application.class, args);
    }

    @GetMapping("/hello")
    public String hello(@RequestParam(value = "name", defaultValue = "kitty") String name) {
        return String.format("Hello %s", name);
    }

}

```

