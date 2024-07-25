---
layout: post
title: "SSM学习记录"
date:   24-07-24
tags: [java]
comments: false
author: takagi
---

磨刀不误砍柴功

# SpringBootWeb

SpringBootWeb被用作服务端处理客户端/浏览器发送的请求。其中Controller层接受页面过来的参数，传给Service处理，接到返回值，再传给页面。

1. @RestController与RequestMapping针对不同的url有不同的处理方法。 

```java
@RestController
public class UserController {
    @RequestMapping("/user/login")  
    public String login() {
        return "user login";
    }
}
```
@RestController表示这是一个控制类，@RequestMapping表示“IP+端口号+/user/login”的post与get请求会被login()处理。

2. 对于含有参数的请求，有两种解决办法。第一种是直接在函数中声明参数，如login可能需要用户名与密码，则采用如下代码。注意的是前端参数与后端参数名需一致。

```java
@RestController
public class UserController {
    @RequestMapping("/user/login")  
    public String login(String name,String password) {
        System.out.println(user);
        return "user login";
    }
}
```

第二种方式是新定义一个类型，比如user类。

```java
@Data
public class User {
    private String name;
    private Integer age;
}

@RestController
public class UserController {
    @RequestMapping("/user/login")  
    public String login(User user) {
        System.out.println(user);
        return "user login";
    }
}
```

