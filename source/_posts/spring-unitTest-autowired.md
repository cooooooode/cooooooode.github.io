---
title: spring autowired为null问题解决
date: 2022-08-10 15:21:53
tags:
 - spring
 - autowired
---

### Spring Autowired无法自动装载问题

如下代码在使用了`Component`和`Autowired`注解后仍然不能自动装载, 具体代码如下

![](/images/2022-08-10-asyncComponent.png)

![](/images/2022-08-10-junit.png)

解决方法如下: 加上`@SpringBootTest`注解

![](/images/2022-08-10-autowired-null.png)

```java
package com.baeldung.async;

import com.baeldung.async.config.SpringAsyncConfig;
import org.junit.jupiter.api.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Configurable;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.test.context.support.AnnotationConfigContextLoader;

import java.util.concurrent.ExecutionException;
import java.util.concurrent.Future;

@RunWith(SpringJUnit4ClassRunner.class)
@SpringBootTest
@ContextConfiguration(classes = {SpringAsyncConfig.class}, loader = AnnotationConfigContextLoader.class)
public class AsyncAnnotationExampleIntegrationTest {

    @Autowired
    private AsyncComponent asyncAnnotationExample;

    // tests

    @Test
    public void testAsyncAnnotationForMethodsWithVoidReturnType() {
        System.out.println("Start - invoking an asynchronous method. " + Thread.currentThread().getName());
        asyncAnnotationExample.asyncMethodWithVoidReturnType();
        System.out.println("End - invoking an asynchronous method. ");
    }

    @Test
    public void testAsyncAnnotationForMethodsWithReturnType() throws InterruptedException, ExecutionException {
        System.out.println("Start - invoking an asynchronous method. " + Thread.currentThread().getName());
        final Future<String> future = asyncAnnotationExample.asyncMethodWithReturnType();

        while (true) {
            if (future.isDone()) {
                System.out.println("Result from asynchronous process - " + future.get());
                break;
            }
            System.out.println("Continue doing something else. ");
            Thread.sleep(1000);
        }
    }

    @Test
    public void testAsyncAnnotationForMethodsWithConfiguredExecutor() {
        System.out.println("Start - invoking an asynchronous method . ");
        asyncAnnotationExample.asyncMethodWithConfiguredExecutor();
        System.out.println("End - invoking an asynchronous method. ");
    }

    @Test
    public void testAsyncAnnotationForMethodsWithException() throws Exception {
        System.out.println("Start - invoking an asynchronous method. ");
        asyncAnnotationExample.asyncMethodWithExceptions();
        System.out.println("End - invoking an asynchronous method. ");
    }
}

```

### 参考

[https://stackoverflow.com/questions/19896870/why-is-my-spring-autowired-field-null](https://stackoverflow.com/questions/19896870/why-is-my-spring-autowired-field-null)



