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

## 请求

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
@RestController表示这是一个控制类，包括收取发送的请求+将处理结果返回，@RequestMapping表示“IP+端口号+/user/login”的post与get请求会被login()处理。

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

3. 如果前端发送的是日期，则可以用@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss")

```java
public String dateParam(@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss") LocalDateTime updateTime){
    System.out.println(updateTime);
    return "ok";
}
```

4. 如果前端发送的是Json格式，则可以用@RequestBody将json格式的数组转换为实体类

```java
public String jsonParam(@RequestBody User user){
    System.out.println(user);
    return "嘻嘻";
}
```

5. 如果请求中的path含有参数，如“IP+端口号+/pathParam/id/name”，则可以用@PathVariable获取参数

```java
public String pathParam(@PathVariable String id,@PathVariable String name){
    System.out.println(id+" "+name);
    return "不嘻嘻";
}
```
