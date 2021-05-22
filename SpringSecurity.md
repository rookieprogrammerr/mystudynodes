# 安全框架

## SpringSecurity（安全）

在web开发中，安全第一位！

**安全应该在什么时候考虑**

- 漏洞，隐私泄露
- 架构一旦确定
- 设计之初

### 什么是SpringSecurity

Spring Security是针对Spring项目的安全框架，也是SpringBoot底层安全模块默认的技术选型，它可以实现强大的Web安全控制，对于安全控制，我们仅需要引入spring-boot-starter-security模块，进行少量的配置，即可实现强大的安全管理

记住几个类

- WebSecurityConfigurerAdapter：自定义Security策略
- AuthenticationManagerBuilder：自定义认证策略
- @EnableWebSecurity：开启WebSecurity模式

Spring Security的两个主要目标是“认证”和“授权”（访问控制）

“认证”（Authentication）

“授权”（Authorization）

这个概念是通用的，而不是只在Spring Security中存在

参考官网：https://spring.io/projects/spring-security，查找到我们自己项目中的版本，找到对应的帮助文档：

https://docs.spring.io/spring-security/site/docs/5.2.0.RELEASE/reference/htmlsingle

### 第一个SpringSecurity测试项目 

创建一个springboot项目，`springboot-06-springsecurity`，并导入相关依赖

```xml
<!-- springsecurity -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<!-- web -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<!-- thymeleaf -->
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-spring5</artifactId>
</dependency>
<dependency>
    <groupId>org.thymeleaf.extras</groupId>
    <artifactId>thymeleaf-extras-java8time</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

1. 编写首页及登录页面，并加入需授权访问页面

   templates.index.html

   ```html
   <!DOCTYPE html>
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
       <title>首页</title>
       <!--semantic-ui-->
       <link href="https://cdn.bootcss.com/semantic-ui/2.4.1/semantic.min.css" rel="stylesheet">
       <link th:href="@{/qinjiang/css/qinstyle.css}" rel="stylesheet">
   </head>
   <body>
   
   <!--主容器-->
   <div class="ui container">
   
       <div class="ui segment" id="index-header-nav" th:fragment="nav-menu">
           <div class="ui secondary menu">
               <a class="item"  th:href="@{/index}">首页</a>
   
               <!--登录注销-->
               <div class="right menu">
                   <!--未登录-->
                   <a class="item" th:href="@{/toLogin}">
                       <i class="address card icon"></i> 登录
                   </a>
                   <!--已登录
                   <a th:href="@{/usr/toUserCenter}">
                       <i class="address card icon"></i> admin
                   </a>
                   -->
               </div>
           </div>
       </div>
   
       <div class="ui segment" style="text-align: center">
           <h3>Spring Security Study by 秦疆</h3>
       </div>
   
       <div>
           <br>
           <div class="ui three column stackable grid">
               <div class="column">
                   <div class="ui raised segment">
                       <div class="ui">
                           <div class="content">
                               <h5 class="content">Level 1</h5>
                               <hr>
                               <div><a th:href="@{/level1/1}"><i class="bullhorn icon"></i> Level-1-1</a></div>
                               <div><a th:href="@{/level1/2}"><i class="bullhorn icon"></i> Level-1-2</a></div>
                               <div><a th:href="@{/level1/3}"><i class="bullhorn icon"></i> Level-1-3</a></div>
                           </div>
                       </div>
                   </div>
               </div>
   
               <div class="column">
                   <div class="ui raised segment">
                       <div class="ui">
                           <div class="content">
                               <h5 class="content">Level 2</h5>
                               <hr>
                               <div><a th:href="@{/level2/1}"><i class="bullhorn icon"></i> Level-2-1</a></div>
                               <div><a th:href="@{/level2/2}"><i class="bullhorn icon"></i> Level-2-2</a></div>
                               <div><a th:href="@{/level2/3}"><i class="bullhorn icon"></i> Level-2-3</a></div>
                           </div>
                       </div>
                   </div>
               </div>
   
               <div class="column">
                   <div class="ui raised segment">
                       <div class="ui">
                           <div class="content">
                               <h5 class="content">Level 3</h5>
                               <hr>
                               <div><a th:href="@{/level3/1}"><i class="bullhorn icon"></i> Level-3-1</a></div>
                               <div><a th:href="@{/level3/2}"><i class="bullhorn icon"></i> Level-3-2</a></div>
                               <div><a th:href="@{/level3/3}"><i class="bullhorn icon"></i> Level-3-3</a></div>
                           </div>
                       </div>
                   </div>
               </div>
           </div>
       </div>
   </div>
   <script th:src="@{/qinjiang/js/jquery-3.1.1.min.js}"></script>
   <script th:src="@{/qinjiang/js/semantic.min.js}"></script>
   </body>
   </html>
   ```

   templates.views.login.html

   ```html
   <!DOCTYPE html>
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
       <title>登录</title>
       <!--semantic-ui-->
       <link href="https://cdn.bootcss.com/semantic-ui/2.4.1/semantic.min.css" rel="stylesheet">
   </head>
   <body>
   
   <!--主容器-->
   <div class="ui container">
   
       <div class="ui segment">
   
           <div style="text-align: center">
               <h1 class="header">登录</h1>
           </div>
   
           <div class="ui placeholder segment">
               <div class="ui column very relaxed stackable grid">
                   <div class="column">
                       <div class="ui form">
                           <form th:action="@{/usr/login}" method="post">
                               <div class="field">
                                   <label>Username</label>
                                   <div class="ui left icon input">
                                       <input type="text" placeholder="Username" name="username">
                                       <i class="user icon"></i>
                                   </div>
                               </div>
                               <div class="field">
                                   <label>Password</label>
                                   <div class="ui left icon input">
                                       <input type="password" name="password">
                                       <i class="lock icon"></i>
                                   </div>
                               </div>
                               <input type="submit" class="ui blue submit button"/>
                           </form>
                       </div>
                   </div>
               </div>
           </div>
   
           <div style="text-align: center">
               <div class="ui label">
                   </i>注册
               </div>
               <br><br>
               <small>blog.kuangstudy.com</small>
           </div>
           <div class="ui segment" style="text-align: center">
               <h3>Spring Security Study by 秦疆</h3>
           </div>
       </div>
   </div>
   <script th:src="@{/qinjiang/js/jquery-3.1.1.min.js}"></script>
   <script th:src="@{/qinjiang/js/semantic.min.js}"></script>
   </body>
   </html>
   ```

   在views下建立level1、level2、level3级别目录，并写入页面

2. 编写Controller

   ```java
   package com.zc.controller;
   
   import org.springframework.stereotype.Controller;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.PathVariable;
   
   @Controller
   public class RouterController {
   
       @GetMapping("/")
       public String index() {
           return "index";
       }
   
       @GetMapping("/toLogin")
       public String toLogin() {
           return "view/login";
       }
   
       @GetMapping("/level1/{id}")
       public String level1(@PathVariable("id")int id) {
           return "view/level1/"+id;
       }
   
       @GetMapping("/level2/{id}")
       public String level2(@PathVariable("id")int id) {
           return "view/level1/"+id;
       }
   
       @GetMapping("/level3/{id}")
       public String level3(@PathVariable("id")int id) {
           return "view/level1/"+id;
       }
   }
   ```

3. 编写SecurityConfig配置类

   ```java
   package com.zc.config;
   
   import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
   import org.springframework.security.config.annotation.web.builders.HttpSecurity;
   import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
   import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
   
   @EnableWebSecurity
   public class SecurityConfig extends WebSecurityConfigurerAdapter {
   
       //  授权
       //  链式编程
       @Override
       protected void configure(HttpSecurity http) throws Exception {
           //  首页所有人可以访问，功能页只有对应有权限的人才能访问
           //  请求授权的规则
           http.authorizeRequests()
                   .antMatchers("/").permitAll()
                   .antMatchers("/level1/**").hasRole("vip1")
                   .antMatchers("/level2/**").hasRole("vip2")
                   .antMatchers("/level3/**").hasRole("vip3");
   
           //  没有权限默认会到登录页面，需要开启登录的页面
           http.formLogin();
   
       }
   
       //  认证
       @Override
       protected void configure(AuthenticationManagerBuilder auth) throws Exception {
   
           //  这些数据正常应该从数据库中读取
   
           auth.inMemoryAuthentication()
                   .withUser("zc").password("123456").roles("vip2","vip3")
                   .and()
                   .withUser("root").password("123456").roles("vip1","vip2","vip3")
                   .and()
                   .withUser("guest").password("123456").roles("vip1");
       }
   }
   ```

4. 测试发现出现`There is no PasswordEncoder mapped for the id "null"`的问题

   - springboot 2.1.x可以直接使用

   - 密码编码：PasswordEncoder

   - 在SpringSecurity5.0+中，新增了很多的加密方式.

   - 需要将密码进行加密处理

     ```java
     package com.zc.config;
     
     import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
     import org.springframework.security.config.annotation.web.builders.HttpSecurity;
     import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
     import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
     import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
     
     @EnableWebSecurity
     public class SecurityConfig extends WebSecurityConfigurerAdapter {
     
         //  授权
         //  链式编程
         @Override
         protected void configure(HttpSecurity http) throws Exception {
             //  首页所有人可以访问，功能页只有对应有权限的人才能访问
             //  请求授权的规则
             http.authorizeRequests()
                     .antMatchers("/").permitAll()
                     .antMatchers("/level1/**").hasRole("vip1")
                     .antMatchers("/level2/**").hasRole("vip2")
                     .antMatchers("/level3/**").hasRole("vip3");
     
             //  没有权限默认会到登录页面，需要开启登录的页面
             http.formLogin();
     
         }
     
         //  认证
         @Override
         protected void configure(AuthenticationManagerBuilder auth) throws Exception {
     
             //  这些数据正常应该从数据库中读取
     
             auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())
                     .withUser("zc").password(new BCryptPasswordEncoder().encode("123456")).roles("vip2","vip3")
                     .and()
                     .withUser("root").password(new BCryptPasswordEncoder().encode("123456")).roles("vip1","vip2","vip3")
                     .and()
                     .withUser("guest").password(new BCryptPasswordEncoder().encode("123456")).roles("vip1");
         }
     }
     ```

5. 测试OK

### Thymeleaf整合SpringSecurity

用户的权限认证不仅在后台进行验证，在前台我们需要认证该用户的权限并动态的显示所拥有的权限

1. 添加注销功能

   在SecurityConfig中加入注销功能

   ```java
   //  注销，开启注销功能
   http.logout().logoutSuccessUrl("/");
   ```

   参数说明

   - logout()：开启注销功能
   - logoutSuccessUrl("/")：注销成功后指定返回的页面

2. 在html中进行判断，如果未登录显示登录按钮；如果登录了则显示注销按钮及用户名

   ```html
   <!--登录注销-->
   <div class="right menu">
       
   	<!--如果未登录-->
       <div sec:authorize="!isAuthenticated()">
           
           <a class="item" th:href="@{/toLogin}">
               <i class="address card icon"></i> 登录
           </a>
       </div>
       
   	<!-- 如果已登录，显示用户名和注销 -->
       <div sec:authorize="isAuthenticated()">
           <a class="item">
               用户名：<span sec:authentication="name"></span>
           </a>
       </div>
   
       <div sec:authorize="isAuthenticated()">
           <a class="item" th:href="@{/logout}">
               <i class="sign-out icon"></i> 注销
           </a>
       </div>
   </div>
   ```

   下面也需要判断登录用户的角色，并动态的显示用户所拥有的权限

   ```html
   <div class="ui three column stackable grid">
   
       <!-- 根据用户的角色动态实现 -->
       <!-- 权限认证：只有vip1的角色才能显示并访问 -->
       <div class="column" sec:authorize="hasRole('vip1')">
           <div class="ui raised segment">
               <div class="ui">
                   <div class="content">
                       <h5 class="content">Level 1</h5>
                       <hr>
                       <div><a th:href="@{/level1/1}"><i class="bullhorn icon"></i> Level-1-1</a></div>
                       <div><a th:href="@{/level1/2}"><i class="bullhorn icon"></i> Level-1-2</a></div>
                       <div><a th:href="@{/level1/3}"><i class="bullhorn icon"></i> Level-1-3</a></div>
                   </div>
               </div>
           </div>
       </div>
   
       <div class="column" sec:authorize="hasRole('vip2')">
           <div class="ui raised segment">
               <div class="ui">
                   <div class="content">
                       <h5 class="content">Level 2</h5>
                       <hr>
                       <div><a th:href="@{/level2/1}"><i class="bullhorn icon"></i> Level-2-1</a></div>
                       <div><a th:href="@{/level2/2}"><i class="bullhorn icon"></i> Level-2-2</a></div>
                       <div><a th:href="@{/level2/3}"><i class="bullhorn icon"></i> Level-2-3</a></div>
                   </div>
               </div>
           </div>
       </div>
   
       <div class="column" sec:authorize="hasRole('vip3')">
           <div class="ui raised segment">
               <div class="ui">
                   <div class="content">
                       <h5 class="content">Level 3</h5>
                       <hr>
                       <div><a th:href="@{/level3/1}"><i class="bullhorn icon"></i> Level-3-1</a></div>
                       <div><a th:href="@{/level3/2}"><i class="bullhorn icon"></i> Level-3-2</a></div>
                       <div><a th:href="@{/level3/3}"><i class="bullhorn icon"></i> Level-3-3</a></div>
                   </div>
               </div>
           </div>
       </div>
   
   </div>
   ```

3. 测试后发现：注销功能出现问题

   - 因为springboot中自带防止csrf攻击的属性，设置该属性即可

     ```java
     //  关闭csrf功能
     http.csrf().disable();
     ```

   - CSRF（Cross-siterequestforgery，跨站请求伪造），也被称为one-click attack或者session riding，是一种挟制用户在当前已登录的[Web应用程序](https://baike.sogou.com/lemma/ShowInnerLink.htm?lemmaId=159605&ss_c=ssc.citiao.link)上执行非本意的操作的攻击方法。

     它通过伪装来自受信任用户的请求来利用受信任的网站。与[XSS攻击](https://baike.sogou.com/lemma/ShowInnerLink.htm?lemmaId=66173755&ss_c=ssc.citiao.link)相比，CSRF攻击往往不大流行和难以防范，所以被认为比XSS更具危险性。

注意点：

- 关闭csrf

- 导入springsecurity命名空间

  ```html
  <html lang="en" xmlns:th="http://www.thymeleaf.org"
        xmlns:sec="http://www.thymeleaf.org/extras/spring-security">
  ```

### 记住我及首页定制

1. 在SecurityConfig中加入记住我功能

   ```java
   //  开启记住我功能，默认保存2周
   http.rememberMe().rememberMeParameter("remember");
   ```

   参数说明

   - rememberMe()：开启记住我
   - .rememberMeparameter("remember")：接收表单对象name为remember传递的参数

2. 在html中加入记住我功能

   ```html
   <div class="field">
       <input type="checkbox" name="remember"> 记住我
   </div>
   ```

3. 定制login登录页

   ```java
   //  定制登录页
   http.formLogin().loginPage("/toLogin").usernameParameter("username").passwordParameter("password").loginProcessingUrl("/login");
   
   ```

   参数说明

   - formLogin()：无权限默认跳转至登录页面
   - usernameParameter("username")：接收表单对象name为username传递的参数
   - passwordParameter("password")：接收表单对象name为password传递的参数
   - loginProcessingUrl("/login")：登录验证

4. 修改页面中的表单信息

   templates.views.login.html

   ```html
   <form th:action="@{/login}" method="post">
   ```

   templates.index.html

   ```html
   <a class="item" th:href="@{/toLogin}">
   ```

