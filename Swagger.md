# Swagger

## 前后端分离

后端时代：前端只用管理静态页面，html==>后端

**前后端分离时代**

- 后端：后端控制层，服务层，数据访问层
- 前端：前端控制层，视图层
  - 伪造后端数据，json。即不需要后端，前端工程依旧可以正常使用

**前后端如何交互**

通过一个API

**前后端分离的好处**

- 前后端相对独立，松耦合
- 前后端甚至可以部署在不同的服务器上

**缺点**

- 前后都安集成联调，前端人员和后端人员无法做到及时协商，最终导致问题集中爆发

**解决方案**

- 首先制定一个schema [计划的提纲]，实时更新最新API，降低集成的 
- 制定word计划文档
- 前后端分离：
  - 前端测试后端接口：postman
  - 后端提供接口，需要实时更新最新的消息及改动

## Swagger

- 号称世界上最流行的API框架
- RestFul API 文档在线自动生成 ==> **API文档与Api定义同步更新**
- 直接运行，可以在线测试API接口
- 支持多种语言

官网：[https://swagger.io/](https://swagger.io/)

在项目中使用Swagger需要 springbox

- swagger2
- ui

## SpringBoot 集成Swagger

1. 新建一个SpringBoot项目

2. 导入相关依赖

   ```xml
   <dependency>
   	<groupId>io.springfox</groupId>
       <artifactId>springfox-swagger2</artifactId>
       <version>2.9.2</version>
   </dependency>
   <dependency>
   	<groupId>io.springfox</groupId>
       <artifactId>springfox-swagger-ui</artifactId>
       <version>2.9.2</version>
   </dependency>
   ```

3. 编写一个Hello工程

4. 配置Swagger ==> Config

   ```java
   package com.zc.swagger.config;
   
   import org.springframework.context.annotation.Configuration;
   import springfox.documentation.swagger2.annotations.EnableSwagger2;
   
   @Configuration
   //  开启Swagger2
   @EnableSwagger2
   public class SwaggerConfig {
       
   }
   ```

5. 测试运行

![](http://zhaocan.fym233.cn/ji18x00d5c)

##### 配置Swagger

Swagger的bean实例 Docket；

```java
package com.zc.swagger.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.service.Contact;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

import java.util.ArrayList;

@Configuration
//  开启Swagger2
@EnableSwagger2
public class SwaggerConfig {

    //  配置了Swagger的Docket的bean实例
    @Bean
    public Docket docket() {
        return new Docket(DocumentationType.SWAGGER_2)
            .apiInfo(apiInfo());
    }

    //  配置Swagger信息 ==> apiInfo
    private ApiInfo apiInfo() {
        Contact contact = new Contact("赵灿", "http://fym233.cn/zcblog", "zc1872751113@gmail.com");
        return new ApiInfo(
            "赵灿的SwaggerAPI文档",
            "没有描述",
            "z1.0",
            "http://fym233.cn/zcblog",
            contact,
            "Apache 2.0",
            "http://www.apache.org/licenses/LICENSE-2.0",
            new ArrayList());

    }
}
```

##### Swagger配置扫描接口

Docket.select（）

```java
//  配置了Swagger的Docket的bean实例
@Bean
public Docket docket() {
    return new Docket(DocumentationType.SWAGGER_2)
        .apiInfo(apiInfo())
        .select()
        //RequestHandlerSelectors：配置要扫描接口的方式
        //basePackage：指定要扫描的包
        //any()：扫描全部
        //none()：不扫描
        //withClassAnnotation()：扫描类上的注解，参数是一个注解的反射对象
        //withMethodAnnotation()：扫描方法上的注解
        .apis(RequestHandlerSelectors.basePackage("com.zc.swagger.controller"))
        //.paths()：过滤路径
        .build();
}
```

配置是否启动Swagger

```java
//  配置了Swagger的Docket的bean实例

@Bean
public Docket docket() {
    return new Docket(DocumentationType.SWAGGER_2)
        .apiInfo(apiInfo())
        //  enable是否启动swagger，如果为false，则swagger不能在浏览器中访问。默认为true
        .enable(false)
        .select()
        .build();
}
```

配置API分组

```java
new Docket(DocumentationType.SWAGGER_2)
    .apiInfo(apiInfo())
    .groupName("赵灿")
```

如何配置多个分组

- 创建多个Docket实例

  ```java
  @Bean
  public Docket docket1() {
      return new Docket(DocumentationType.SWAGGER_2)
          .groupName("docket1");
  }
  
  @Bean
  public Docket docket2() {
      return new Docket(DocumentationType.SWAGGER_2)
          .groupName("docket2");
  }
  
  @Bean
  public Docket docket3() {
      return new Docket(DocumentationType.SWAGGER_2)
          .groupName("docket3");
  }
  
  @Bean
  public Docket docket4() {
      return new Docket(DocumentationType.SWAGGER_2)
          .groupName("docket4");
  }
  
  ....
  ```

实体类配置

```java
package com.zc.swagger.pojo;

import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;

@ApiModel("用户实体类")
@Data
public class User {

    @ApiModelProperty("用户名")
    public String username;
    @ApiModelProperty("密码")
    public String password;

}
```

Controller

```java
package com.zc.swagger.controller;

import com.zc.swagger.pojo.User;
import io.swagger.annotations.ApiOperation;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RestController;


@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "hello";
    }

    //  只要我们的接口中，返回值中存在实体类，他就会被扫描到Swagger中
    @PostMapping("/user")
    public User user() {
        return new User();
    }
    
    //Operation接口，不是放在类上的，是方法
    @ApiOperation("Hello控制类")
    @GetMapping("/hello2")
    public String hello2(@ApiParam("用户名") String name) {
        return "hello"+username;
    }
    
    @ApiOperation("Post测试类")
    @PostMapping("/postt")
    public User postt(@ApiParam("用户") User user) {
        int i = 5/0;
        return user;
    }
}
```



总结：

1. 我们可以通过Swagger给一些比较难理解的属性或者接口，增加注释信息
2. 接口文档实时更新
3. 可以在线测试

注意点：

- 出于安全考虑，在正式发布的时候，关闭Swagger！！
- 节省内存