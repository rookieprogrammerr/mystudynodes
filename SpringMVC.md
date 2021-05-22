# SpringMVC

SSM：mybatis + Spring + SpringMVC  **MVC三层架构**

### 什么是MVC

- MVC是模型（Model）、视图（View）、控制器（Controller）的简写，是一种软件设计规范

- 是将业务逻辑、数据、显示分离的方法来组织代码

- MVC主要作用是降低了视图与业务逻辑间的双向耦合

- MVC不是一种设计模式，MVC是一种架构模式。当然不同的MVC存在差异

  **Model（模型）**：数据模型，提供要展示的数据，因此包含数据和行为，可以认为是领域模式或JavaBean组件（包含数据和行为），不过现在一般都分离开来：Value Object（数据Dao）和服务层（行为Service）。也就是模型提供了模型数据查询和模型数据的状态更新等功能，包含数据和业务。

  **View（视图）**：负责进行模型的展示，一般就是我们见到的用户界面，客户想看到的东西。

  **Controller（控制器）**：接收用户请求，委托给模型进行处理（状态改变），处理完毕后把返回的模型数据返回给视图，由视图负责展示。也就是说控制器做了个调度员的工作。

##### Model1时代

- 在web早期的开发中，通常采用的都是Model1.
- Model中，主要分为两层，视图层和模型层

![](https://i.loli.net/2021/02/10/mNeGUFgxapw56rl.png)

Model1 优点：架构简单，比较适合小型项目开发

Model1 缺点：JSP职责不单一，指责过重，不适于维护

##### Model2时代

Model2 把一个项目分层三部分，包括**视图、控制、模型。**

![](https://i.loli.net/2021/02/10/CgFOD8Ycqba1eBp.png)

1. 用户发送请求

2. Servlet接收请求数据，并调用对应的业务逻辑方法

3. 业务处理完毕，返回更新后的数据给servlet

4. servlet转向到JSP，由JSP来渲染页面

5. 响应给前端更新后的页面

   **职责分析：**

   **Controller：控制器**

   1. 取得表单数据
   2. 调用业务逻辑
   3. 转向指定的页面

   **Model：模型**

   1. 业务逻辑
   2. 保存数据的状态

   **View：视图**

   1. 显示页面

Model2 这样不仅提高了代码的复用率与项目的拓展性，且大大降低了项目的维护成本。Model1 模式的实现比较简单，适用于快速开发小规模项目，Model1 中JSP页面身兼View和Controller两种角色，将控制逻辑和表现逻辑混杂在一起，从而导致代码的重用性非常低，增加了应用的扩展性和维护的难度。Model2 消除了Model1 的缺点。

##### 回顾Servlet

1. 新建一个Maven工程当做父工程，并导入pom依赖

   ```xml
   <!-- 导入依赖 -->
   <dependencies>
       <!-- junit -->
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.12</version>
       </dependency>
       <!-- web mvc -->
       <dependency>
           <groupId>org.springframework</groupId>
           <artifactId>spring-webmvc</artifactId>
           <version>5.1.9.RELEASE</version>
       </dependency>
       <!-- servlet -->
       <dependency>
           <groupId>javax.servlet</groupId>
           <artifactId>servlet-api</artifactId>
           <version>2.5</version>
       </dependency>
       <!-- jsp -->
       <dependency>
           <groupId>javax.servlet.jsp</groupId>
           <artifactId>jsp-api</artifactId>
           <version>2.2</version>
       </dependency>
       <!-- EL表达式 -->
       <dependency>
           <groupId>javax.servlet</groupId>
           <artifactId>jstl</artifactId>
           <version>1.2</version>
       </dependency>
   </dependencies>
   ```

   

2. 建立一个Moudle：SpringMVC-01-Servlet，添加Web app的支持

   ![](https://i.loli.net/2021/02/10/JlF6cZpEUSIixMD.png)

3. 导入Servlet 和 jsp 的jar依赖

   ```xml
   <dependencies>
       <dependency>
           <groupId>javax.servlet</groupId>
           <artifactId>servlet-api</artifactId>
           <version>2.5</version>
       </dependency>
       <dependency>
           <groupId>javax.servlet.jsp</groupId>
           <artifactId>jsp-api</artifactId>
           <version>2.2</version>
       </dependency>
   </dependencies>
   ```

4. 编写一个Servlet类，用来处理用户的请求

   ```java
   public class HelloServlet extends HttpServlet {
   
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           //  1.获取前端参数
           String method = req.getParameter("method");
           if(method.equals("add")) {
               req.getSession().setAttribute("msg","执行了add方法");
           }
           if(method.equals("delete")) {
               req.getSession().setAttribute("msg","执行了delete方法");
           }
           //  2.调用业务层
           //  3.视图转发或者重定向
   
           req.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(req, resp);
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           super.doPost(req, resp);
       }
   }
   
   ```

5. 创建jsp页面

   ```jsp
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head>
       <title>Title</title>
   </head>
   <body>
   
   ${msg}
   
   
   </body>
   </html>
   
   ```

6. 配置web.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">
   
       <servlet>
           <servlet-name>hello</servlet-name>
           <servlet-class>com.zc.servlet.HelloServlet</servlet-class>
       </servlet>
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello</url-pattern>
       </servlet-mapping>
   
       <session-config>
           <session-timeout>15</session-timeout>
       </session-config>
   
   </web-app>
   ```

7. 配置Tomcat，并启动测试

   - localhost:8080/hello?method=add
   - localhost:8080/hello?method=delete

MVC框架要做哪些事情

1. 将url映射到java类或java类的方法
2. 封装用户提交的数据
3. 处理请求--调用相关的业务处理--封装响应数据
4. 将相应的数据进行渲染 .jsp/.html 等表示层数据

说明：

​	常见的服务器端MVC框架有：Struts、SpringMVC、ASP.NET MVC、Zend Framework、JSF；

​	常见的前端MVC框架有：Vue、AngularJS、React、Backbone；

​	由MVC演化出了另外一些模式如：MVP、MVVM等等

##### SpringMVC的特点

1. 轻量级，简单易学

2. 搞笑，基于请求响应的MVC框架

3. 与Spring兼容性好，无缝结合

4. 约定由于配置

5. 功能强大：RESTful、数据验证、格式化、本地化、主题等

6. 简洁灵活

   Spring的web框架围绕**DispatcherServlet** [ 调度Servlet ]设计

   DispatcherServlet的作用是将请求分发到不同的处理器。从Spring2.5开始，使用Java5或者以上版本的用户可以采用基于注解形式进行开发，十分简洁。

   正因为SpringMVC好，简单，便捷，易学，天生和Spring无缝集成（使用SpringIoC和SpringAOP），使用约定优于配置，能够进行简单的junit测试，支持RESTful风格，异常处理，本地化，国际化，数据验证，类型转换，拦截器等等。 

### HelloSpringMVC

##### 配置版

1. 新建一个Moudle，添加web的支持

2. 确定导入了SpringMVC的依赖

3. 配置web.xml，注册DispatcherServlet

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">
   
       <!-- 1、注册DispatcherServlet -->
       <servlet>
           <servlet-name>springmvc</servlet-name>
           <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
           <!-- 关联一个springmvc的配置文件：【servlet-name】-servlet.xml -->
           <init-param>
               <param-name>contextConfigLocation</param-name>
               <param-value>classpath:springmvc-servlet.xml</param-value>
           </init-param>
           <!-- 启动级别-1 -->
           <load-on-startup>1</load-on-startup>
       </servlet>
   
       <!-- /  匹配所有的请求：（不包括.jsp）-->
       <!-- /* 匹配所有的请求：（包括jsp） -->
       <servlet-mapping>
           <servlet-name>springmvc</servlet-name>
           <url-pattern>/</url-pattern>
       </servlet-mapping>
   </web-app>
   ```

4. 编写SpringMVC 的配置文件！名称：springmvc-servlet.xml：[servletname]-servlet.xml

   说明：这里的名称要求是按照官方来的

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd">
   
   </beans>
   ```

5. 添加处理器映射器

   ```xml
   <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping" />
   ```

6. 添加处理器适配器

   ```xml
   <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter" />
   ```

7. 添加视图解析器

   ```xml
   <!-- 视图解析器：DispatcherServlet给他的ModelAndView -->
   <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="internalResourceViewResolver">
       <!-- 前缀 -->
       <property name="prefix" value="/WEB-INF/jsp/" />
       <!-- 后缀 -->
       <property name="suffix" value=".jsp" />
   </bean>
   ```

8. 编写我们要操作业务Controller，要么实现Controller接口，要么增加注解；需要返回一个ModelAndView，装书局，封视图；

   ```java
   //  注意：这里我们先导入Controller接口
   public class HelloController implements Controller {
       public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
           //   ModelAndView 模型和视图
           ModelAndView modelAndView = new ModelAndView();
   
           //  封装对象，放在ModelAndView中。
           modelAndView.addObject("msg","HelloSpringMVC!");
           //  封装要跳转的视图，放在ModelAndView中
           modelAndView.setViewName("hello");  //  ：/WEB-INF/jsp/hello.jsp
           return modelAndView;
       }
   }
   ```

9. 把自己的类交给SpringIOC容器，注册bean

   ```xml
   <!-- Handler -->
   <bean id="/hello" class="com.zc.controller.HelloController" />
   ```

10. 写要跳转的jsp页面，现实ModelAndView存放的数据，以及我们的正常页面

    ```jsp
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
    </head>
    <body>
    
    ${msg}
    
    
    </body>
    </html>
    ```

11. 配置tomcat 启动测试



可能遇到的问题：访问出现404，排查步骤：

1. 查看控制台输出，看一下是不是缺少了什么jar包
2. 如果jar包存在，显示无法输出，就在IDEA的项目发布中，添加lib依赖
3. 重启Tomcat即可解决

### SpringMVC执行流程

1. DispatcherServlet表示前置控制器，是整个SpringMVC的控制中心，用户发出请求，DispatcherServlet接收请求并拦截请求。
   - 我们假设请求的url为：http://localhost:8080/SpringMVC/hello
   - 如上url拆分成三部分
   - httpL//localhost:8080 服务器域名
   - SpringMVC部署在服务器上的web站点
   - hello表示控制器
   - 通过分析，如上url表示为：请求位于服务器 localhost:8080 上的的SpringMVC站点的hello控制器
2. HandlerMapping为处理器映射，DispatcherServlet调用HandlerMapping，HandlerMapping根据请求url查找Handler
3. HandlerExecution表示具体的Handler，其主要作用是根据url查找控制器，如上url被查找控制器为：hello
4. HandlerExecution将解析后的信息传递给DispatcherServlet，如解析控制器映射等
5. HandlerAdapter表示处理器适配器，其按照特定的规则去执行Handler
6. Handler让具体的Controller执行
7. Controller将具体的执行信息返回给HandlerAdapter，如ModelAndView
8. HandlerAdapter将视图逻辑名或模型传递给DispatcherServlet
9. DispatcherServlet调用视图解析器（ViewResolver）来解析HandlerAdapter传递的逻辑视图名
10. 视图解析器将解析的逻辑视图名传给DispatcherServlet
11. DispatcherServlet根据视图解析器解析的视图结果，调用具体的视图
12. 最终视图呈现给用户

![](https://i.loli.net/2021/02/11/8WucqRA9kLEHv2D.png)

##### 注解版

1. 新建一个Moudle，添加web支持！建立包结构（com.zc.controller）

2. 由于Maven可能存在资源过滤的问题，我们将配置完善

   ```xml
   <build>
       <resources>
           <resource>
               <directory>src/main/java</directory>
               <includes>
                   <include>**/*.properties</include>
                   <include>**/*.xml</include>
               </includes>
               <filtering>false</filtering>
           </resource>
           <resource>
               <directory>src/main/sources</directory>
               <includes>
                   <include>**/*.properties</include>
                   <include>**/*.xml</include>
               </includes>
               <filtering>false</filtering>
           </resource>
       </resources>
   </build>
   ```

3. 在pom.xml文件引入相关的依赖

   ```xml
   <!-- 导入依赖 -->
   <dependencies>
       <!-- junit -->
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.12</version>
       </dependency>
       <!-- web mvc -->
       <dependency>
           <groupId>org.springframework</groupId>
           <artifactId>spring-webmvc</artifactId>
           <version>5.1.9.RELEASE</version>
       </dependency>
       <!-- servlet -->
       <dependency>
           <groupId>javax.servlet</groupId>
           <artifactId>servlet-api</artifactId>
           <version>2.5</version>
       </dependency>
       <!-- jsp -->
       <dependency>
           <groupId>javax.servlet.jsp</groupId>
           <artifactId>jsp-api</artifactId>
           <version>2.2</version>
       </dependency>
       <!-- EL表达式 -->
       <dependency>
           <groupId>javax.servlet</groupId>
           <artifactId>jstl</artifactId>
           <version>1.2</version>
       </dependency>
   </dependencies>
   ```

4. 配置web.xml

   注意点：

   - 注意web.xml版本问题，要最新版
   - 注册DispatcherServlet
   - 关联SpringMVC的配置文件
   - 启动级别为1
   - 映射路径为`/`【不要用`/*`,会404】

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">
   
       <!-- 1、注册Servlet -->
       <servlet>
           <servlet-name>springmvc</servlet-name>
           <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
           <!-- 通过初始化参数指定SpringMVC配置文件的位置，进行关联 -->
           <init-param>
               <param-name>contextConfigLocation</param-name>
               <param-value>classpath:springmvc-servlet.xml</param-value>
           </init-param>
           <!-- 启动顺序，数字越小，启动越早 -->
           <load-on-startup>1</load-on-startup>
       </servlet>
       
       <!-- 所有请求都会被springmvc拦截 -->
       <servlet-mapping>
           <servlet-name>springmvc</servlet-name>
           <url-pattern>/</url-pattern>
       </servlet-mapping>
   </web-app>
   ```

   ```html
   **/ 和 /\* 的区别：**
   <url-pattern> / </url-pattern> 不会匹配到.jsp，只针对我们编写的请求，即：.jsp 不会进入spring的 DispatcherServlet类。
   <url-pattern> /* </url-pattern> 会匹配 *.jsp，会出现返回 jsp 视图时再次进入 spring 的DispatcherServlet 类，导致找不到对应的controller
   ```

5. 添加SpringMVC配置文件

   1. 让IOC的注解生效

   2. 静态资源过滤：HTML，JS，CSS，图片，视频等

   3. MVC的注解驱动

   4. 配置视图解析器

      在resource目录下添加springmvc-servlet.xml配置文件，配置的形式与Spring容器配置基本类似，为了支持基于注解的IOC，设置了自动扫描包的功能，具体配置信息如下：

      ```xml
      <?xml version="1.0" encoding="UTF-8" ?>
      <beans xmlns="http://www.springframework.org/schema/beans"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xmlns:context="http://www.springframework.org/schema/context"
             xmlns:mvc="http://www.springframework.org/schema/mvc"
             xsi:schemaLocation="http://www.springframework.org/schema/beans
                                 http://www.springframework.org/schema/beans/spring-beans.xsd
                                 http://www.springframework.org/schema/context
                                 http://www.springframework.org/schema/context/spring-context.xsd
                                 http://www.springframework.org/schema/mvc
                                 http://www.springframework.org/schema/mvc/spring-mvc.xsd">
      
          <!-- 自动扫描包，让指定包下的注解生效，由IOC容器统一管理 -->
          <context:component-scan base-package="com.zc.controller" />
          <!-- 让SpringMVC不处理静态资源 -->
          <mvc:default-servlet-handler />
          <!--
          支持mvc注解驱动
              在Spring中一般采用@ReuqestMapping注解来完成映射关系
              要想使@RequestMapping注解生效
              必须向上下文中注册DefaultAnnotationHandlerMapping
              和一个AnnotationMethodHandlerAdapter实例
              这两个实例分别在类级别和方法级别处理。
              而annotation-driven配置帮助我们自动完成上述两个实例的注入
          -->
          <mvc:annotation-driven />
      
          <!-- 视图解析器 -->
          <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
                id="internalResourceViewResolver">
              <!-- 前缀 -->
              <property name="prefix" value="/WEB-INF/jsp/"/>
              <!-- 后缀 -->
              <property name="suffix" value=".jsp"/>
          </bean>
      </beans>
      ```

   在视图解析器中我们把所有的视图都存放在/WEB-INF/目录下，这样可以保证视图安全，因为这个目录下的文件，客户端不能直接访问。

6. 创建Controller

   编写一个Java控制类：com.zc.controller.HelloController，注意编码规范

   ```java
   package com.zc.controller;
   
   import org.springframework.stereotype.Controller;
   import org.springframework.ui.Model;
   import org.springframework.web.bind.annotation.RequestMapping;
   
   @Controller
   @RequestMapping(value = "/HelloController")
   public class HelloController {
   
       @RequestMapping(value = "/hello")
       public String hello(Model model) {
           //  封装数据
           model.addAttribute("msg","Hello，SrpingMVCAnnotation");
           return "hello";     //会被视图解析器处理
       }
   }
   
   ```

   - @Controller是为了让Spring IOC容器初始化时扫描到
   - @RequestMapping是为了映射请求路径，这里因为类与方法上都有映射所以访问时应该是 `/HelloController/hello`
   - 方法中声明Model类型的参数是为了把Action中的数据带到视图中
   - 方法返回的结果是视图的名称hello，加上配置文件中的前后缀编程`WEB-INF/jsp/hello.jsp`

7. 创建视图层

   在WEB-INF/jsp 目录中创建hello.jsp，视图可以直接取出并展示从Controller带回的信息；

   可以通过EL表达式 取出Model中存放的值，或者对象

   ```jsp
   <%--
     Created by IntelliJ IDEA.
     User: Administrator
     Date: 2021/2/11
     Time: 14:24
     To change this template use File | Settings | File Templates.
   --%>
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head>
       <title>Title</title>
   </head>
   <body>
   
       ${msg}
   
   </body>
   </html>
   ```

8. 配置Tomcat运行

   配置Tomcat，开启服务器，访问对应的请求路径！

   ![](https://i.loli.net/2021/02/11/j9xLYu14aGIVFht.png)

   **OK，运行成功**

小结：实现步骤其实非常的简单

1. 新建一个web项目

2. 导入相关jar包

3. 编写web.xml，注册DispatcherServlet

4. 编写springmvc配置文件

5. 接下来就是去创建对应的控制类：controller

6. 最后完善前端视图和controller之间的对应

7. 测试运行调试

   使用SpringMVC必须配置的三大件：

   **处理器映射（DispatcherServlet），处理器适配器（HandlerAdapter），视图解析器（ViewResolver）**

   通常，我们只需要手动配置视图解析器，而处理器映射器和处理器适配器只需要开启注解驱动即可，而省去了大段的xml配置

### Controller 及 RestFul风格

##### 控制器Controller

- 控制器负责提供访问应用程序的行为，通常通过接口定义或注解定义两种方法实现
- 控制器负责解析用户的请求并将其转换为一个模板
- 在SpringMVC中一个控制器类可以包含多个方法
- 在SpringMVC中，对于Controller的配置方式有很多

##### 实现Controller接口

Controller是一个接口，在`org.springframework.web,servlet,mvc`包下，接口中只有一个方法：

```java
//	实现该接口的类获得控制器功能
public interface Controller{
    //	处理请求且返回一个模型与视图对象
    ModelAndview handleRequest(HttpServletRequest var1, HttpServletResponse var2) throws Exception; 
}
```

**测试**

1. 新建一个Module，springmvc-04-controller，将刚才的03拷贝一份，我们进行操作！

   - 删掉HelloController
   - mvc的配置文件只留下 视图解析器！

2. 编写一个Controller类，ControllerTest1！

   ```java
   //  只要实现了Controller接口的类，说明这就是一个控制器了
   //	注意点：不要导错包，实现Controller接口，重写方法：
   public class ControllerTest1 implements Controller {
       public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
           ModelAndView modelAndView = new ModelAndView();
           modelAndView.addObject("msg","ControllerTest1");
           modelAndView.setViewName("test");
           return modelAndView;
       }
   }
   
   ```

3. 编写完毕后，去Spring配置文件中注册请求的bean；name对应请求路径，class对应处理请求的类

   ```xml
   <bean name="/t1" class="com.zc.controller.ControllerTest1"/>
   ```

4. 编写前端test.jsp，注意在WEB-INF/jsp 目录下编写，对应我们的视图解析器

   ```jsp
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head>
       <title>Title</title>
   </head>
   <body>
   
   ${msg}
   
   </body>
   </html>
   ```

5. 配置Tomcat运行测试，我这里没有项目发布名配置的就是一个`/`，所以请求不用加项目名，OK！

   ![](https://i.loli.net/2021/02/11/adJmQrTtLujUebW.png)

   说明：

   - 实现接口Controller定义控制器是较老的办法
   - 缺点是：一个控制器只有一个方法，如果要多个方法则需要定义多个Controller；定义的方式比较麻烦

##### 使用注解@Controller

- @Controller注解类型用于声明Spring类的实例是一个控制器

- Spring可以使用扫描机制来找到应用程序中所有基于注解的控制器类，为了保证Spring能找到你的控制器，需要在配置文件中声明组件扫描

  ```xml
  <!-- 自动扫描指定的包，下面所有注解类交给IOC容器管理 -->
  <context:component-scan base-package="com.zc.controller"/>
  ```

- 增加一个ControllerTest2类，使用注解实现

  ```java
  //  代表这个类会被Spring接管
  //  被这个注解的类中的所有方法，如果返回值是String，并且有具体页面可以跳转，那么就会被视图解析器解析
  @Controller
  public class ControllerTest2 {
  
      @RequestMapping(value = "/t2")
      public String test1(Model model) {
          model.addAttribute("msg","ControllerTest2");
  
          return "test";
      }
  }
  ```

- 运行tomcat测试

  ![](http://zhaocan.fym233.cn/QQ%E6%88%AA%E5%9B%BE20210211175348.png)

### RequestMapping

- @RequestMapping注解用于映射url到控制器类或一个特定的处理程序方法。可用于类或方法上。用于类上，表示类中的所有响应请求的方法都是以该地址作为父路径
- 为了测试结论更加准确，我们可以加上一个项目名测试 myweb
- 只注解在方法上面

### RestFul风格

Restful就是一个资源定位及资源操作的风格。不是标准也不是协议，只是一种风格。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存等机制

**功能**

- 资源：互联网所有的事物都可以被抽象为资源
- 资源操作：使用POST、DELETE、PUT、GET，使用不同方法对资源进行操作
- 分别对应 添加、删除、修改、查询

**传统方式操作资源**

- http://127.0.0.1/item/queryItem.action?id=1	查询，GET
- http://127.0.0.1/item/saveItem.action    新增，POST
- http://127.0.0.1/item/updateItem.action     更新，POST
- http://127.0.0.1/item/deleteItem.action?id=1    删除，GET或POST

**使用RESTful操作资源**：可以通过不同的请求方式来实现不同的效果！如下：请求地址一样，但是功能可以不同

- http://127.0.0.1/item/1    查询，GET
- http://127.0.0.1/item    新增，POST
- http://127.0.0.1/item    更新，PUT
- http://127.0.0.1/item/1    删除，DELETE

**学习测试**

1. 再新建一个类RestFulController

   ```java
   @Controller
   public class RestFulController {
   }
   ```

2. 在SpringMVC中可以使用`@PathVariable`注解，让方法参数的值对应绑定到一个URI模板变量上

   ```java
   @Controller
   public class RestFulController {
       
       //	映射访问路径
       @GetMapping(value = "/add/{a}/{b}")
       public String test1(@PathVariable int a, @PathVariable int b, Model model) {
           int sum = a + b;
   		
           //	SpringMVC会自动实例化一个Model对象用于向视图中传值
           model.addAttribute("msg","结果为"+sum);
           //	返回视图位置
           return "test";
       }
   }
   ```

3. 我们来测试请求看下

   ![](http://zhaocan.fym233.cn/QQ%E6%88%AA%E5%9B%BE20210211191427.png)

   思考：使用路径变量的好处

   - 使路径变的更加简洁
   - 获得参数更加方便，框架会自动进行类型转换
   - 通过路径变量的类型可以约束访问参数，如果类型不一样，则访问不到对应的请求方法，如这里访问的路径是`/add/1/b`，则路径与方法不匹配，而不会是参数转换失败

   ![](http://zhaocan.fym233.cn/QQ%E6%88%AA%E5%9B%BE20210211192130.png)

   ​	

4. 我们来修改下对应的参数类型，再次测试

   ```java
   @Controller
   public class RestFulController {
       
       //	映射访问路径
       @GetMapping(value = "/add/{a}/{b}")
       public String test1(@PathVariable int a, @PathVariable String b, Model model) {
           int sum = a + b;
   		
           //	SpringMVC会自动实例化一个Model对象用于向视图中传值
           model.addAttribute("msg","结果为"+sum);
           //	返回视图位置
           return "test";
       }
   }
   ```

   ![](http://zhaocan.fym233.cn/QQ%E6%88%AA%E5%9B%BE20210211192731.png)

   **使用method属性指定请求类型**

   用于约束请求的类型，可以收窄请求范围。指定请求谓词的类型如：GET，POST，PUT，DELETE，HEAD，OPTIONS，PATCH，TRACE等

   我们测试一下

   - 增加一个方法

     ```java
     //	映射访问路径，必须是POST请求
     @RequestMapping(value = "/hello", method = {RequestMethod.POST})
     public String index2(Model model) {
         model.addAttribute("msg","hello!");
         return "test";
     }
     ```

   - 我们使用浏览器地址栏进行访问默认是Get请求，会报错405！

     ![](http://zhaocan.fym233.cn/QQ%E6%88%AA%E5%9B%BE20210211192148.png)

   - 如果将POST修改为GET则正常了

     ```java
     //	映射访问路径，必须是POST请求
     @RequestMapping(value = "/hello", method = {RequestMethod.GET})
     public String index2(Model model) {
         model.addAttribute("msg","hello!");
         return "test";
     }
     ```

     ![](http://zhaocan.fym233.cn/QQ%E6%88%AA%E5%9B%BE20210211193753.png)

小结：

SpringMVC的`@RequestMapping`注解能够处理HTTP请求的方法，比如GET，PUT，POST，DELETE以及PATCH

**所有的地址栏请求默认都会是HTTP GET类型的**

方法级别的注解变体有如下几个：组合注解

```java
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
@PatchMapping
```

@GetMapping是一个组合注解

它所扮演的是`@RequestMapping(method = RequestMethod.GET)`的一个快捷方式，平时使用的会比较多

### ModelAndView

​	设置ModelAndView对象，根据view的名称，和视图解析器跳到指定的页面

页面：｛视图解析器前缀｝ + viewName + ｛视图解析器后缀｝

```xml
<!-- 视图解析器 -->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
      id="internalResourceViewResolver">
    <!-- 前缀 -->
    <property name="prefix" value="/WEB-INF/jsp/"/>
    <!-- 后缀 -->
    <property name="suffix" value=".jsp"/>
</bean>
```

对应的controller类

```java
public class ControllerTest1 implements Controller {

    public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
        //	返回一个模型对象
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.addObject("msg","ControllerTest1");
        modelAndView.setViewName("test");
        return modelAndView;
    }
}
```

### ServletAPI

通过设置ServletAPI，不需要视图解析器

1. 通过HttpServletResponse进行输出
2. 通过HttpServletResponse实现重定向
3. 通过HttpServletResponse实现转发

```java
@Controller
public class ResultGo {
    
    @RequestMapping(value = "/result/t1")
    public void test1(HttpServletRequest request, HttpServletResponse response) throws IOException {
        response.getWriter().println("Hello,Spring by ServletAPI");
    } 
    
    @RequestMapping(value = "/result/t2")
    public void test2(HttpServletRequest request, HttpServletResponse response) throws IOException {
        response.sendRedirect("/index.jsp");
    } 
    
    @RequestMapping(value = "/result/t3")
    public void test1(HttpServletRequest request, HttpServletResponse response) throws Exception {
        //	转发
        request.setAttribute("msg", "/result/t3");
        request.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(request, response);
    } 
    
}
```

### 转发与重定向

通过SpringMVC来实现转发和重定向 - 无需视图解析器

测试前，需要将视图解析器注释掉

```java
@Controller
public class ModelTest1 {

    @GetMapping(value = "/m1/t1")
    public String test1(Model model) {
        //  转发
        return "/index.jsp";
    }

    @GetMapping(value = "/m1/t2")
    public String test2(Model model) {
        //  转发
        model.addAttribute("msg", "ModelTest2");
        return "forward:/WEB-INF/jsp/test.jsp";
    }

    @GetMapping(value = "/m1/t3")
    public String test3(Model model) {
        //  重定向
        model.addAttribute("msg", "ModelTest2");
        return "redirect:/index.jsp";
    }
}
```

通过SpringMVC来实现转发和重定向 - 有视图解析器

重定向，不需要视图解析器，本质就是重新请求一个新地方，所以注意路径问题。

可以重定向到另一个请求实现

```java
@GetMapping(value = "rsm/t1")
public String test4() {
    //  转发
    return "test";
}

@GetMapping(value = "rsm/t2")
public String test5() {
    //  重定向
    return "redirect:/index.jsp";
    //  return "redirect:hello.do";     //hello.do为另一个请求
}
```

### 数据处理

##### 处理提交数据

1. 提交的域名称和处理方法的参数名一致

   提交数据：http://localhost:8080/hello?name=zc

   处理方法：

   ```java
   @GetMapping(value = "/hello")
   public String hello(String name) {
       System.out.println(name);
       return "hello";
   }
   ```

   后台输出：zc

2. 提交的域名城和处理方法的参数名不一致

   提交数据：http://localhost:8080/hello?username=zc

   处理方法：

   ```java
   //RequestParam("username")	:username提交的域的名称
   @GetMapping(value = "/hello")
   public String hello(@RequestParam("username") String name) {
       System.out.println(name);
       return "hello";
   }
   ```

   后台输出：zc

3. 提交的是一个对象

   要求提交的表单域和对象的属性名一致，参数使用对象即可

   1. 实体类

      ```java
      public class User {
          private int id;
          private String name;
          private int age;
          //	构造
          //	get/set
          //	toString()
      }
      ```

   2. 提交数据：http://localhost:8080/mvc04/user?name=zc&id=1&age=18

   3. 处理方法：

      ```java
      @GetMapping(value = "/user")
      public String user(User user) {
          System.out.println(user);
          return "hello";
      }
      ```

   说明：如果使用对象的话，前端传递的参数名和对象名必须一致，否则就是 null。

##### 数据显示到前端

##### 第一种：通过ModelAndView

```java
//  只要实现了Controller接口的类，说明这就是一个控制器了
public class ControllerTest1 implements Controller {
    public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.addObject("msg","ControllerTest1");
        modelAndView.setViewName("test");
        return modelAndView;
    }
}
```

##### 第二种：通过ModelMap

```java
@RequestMapping(value = "/hello")
public String hello(@RequestParam("username") String name, ModelMap model) {
    //	封装要显示视图中的数据
    //	相当于request.setAttribute("name", name);
    model.addAttribute("name", name);
    System.out.println(name);
    return "hello";
}
```

##### 第三种：通过Model

```java
@RequestMapping(value = "/ct2/hello")
public String hello(@RequestParam("username") String name, Model model) {
    //	封装要显示视图中的数据
    //	相当于request.setAttribute("name", name);
    model.addAttribute("msg", name);
    System.out.println(name);
    return "test";
}
```

**对比**

对于新手而言简单来说使用区别就是：

```shell
Model	只有寥寥几个方法只适合用于存储数据，简化了新手对于Model对象的操作和理解
ModelMap	继承了LinkedMap，除了实现了自身的一些方法，同样的继承LinkedMap的方法和特性
ModelAndView	可以在储存数据的同时，可以进行设置返回的逻辑视图，进行控制展示层的跳转
```

当然更多的以后开发考虑的更多的是性能和优化，就不能单单仅限于此的了解。

##### 乱码问题

测试步骤：

1. 我们可以在首页编写一个提交的表单

   ```html
   <form action="/e/t1" method="post">
       <input type="text" name="name"/>
       <input type="submit"/>
   </form>
   ```

2. 后台编写对应的处理类

   ```java
   @Controller
   public class Encoding {
       @RequestMapping("/e/t")
       public String test(Model model, String name) {
           model.addAttribute("msg", name);	//获取表单提交的值
           return "test";	//跳转到test页面显示输入的值
       }
   }
   ```

   

3. 输入中文测试，发现乱码

   ![](https://i.loli.net/2021/02/12/ewdTYk3ZtIlfqrW.png)

   不得不说，乱码问题是在我们开发中十分常见的问题，也是让我们程序员比较头大的问题！

   以前乱码问题通过过滤器解决，而SpringMVC给我们提供了一个过滤器，可以在web.xml中配置，修改了xml文件需要重启服务器！

```xml
<filter>
    <filter-name>encoding</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>utf-8</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>encoding</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

有些极端情况下，这个过滤器对get的支持不好

**`/`只能处理请求，不包括jsp，`/*`会处理所有请求，包括jsp **

### JSON

**什么是JSON**

- JSON（JavaScript Object Notation，JS对象标记）是一种轻量级的数据交换格式，目前使用特别广泛

- 采用完全独立于编程语言的**文本格式**来存储和表示数据。

- 简介和清晰的层次结构使得 JSON 成为理想的数据交换语言

- 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率

  在JavaScript语言中，一切都是对象。因此，任何JavaScript支持的类型都可以通过 JSON 来表示，例如字符串、数字、对象、数组等。看看他的要求和语法格式：

- 对象表示为键值对，数据由逗号分隔

- 花括号保存对象

- 方括号保存数组

  **JSON键值对**是用来保存 JavScript 对象的一种方式，和 JavaScript 对象的写法也大同小异，键/值对组合中的键名卸载前面并用双引号`""`包裹，使用冒号`:`分隔，然后紧接着值：

```json
{"name": "George"}
{"age": "31"}
{"sex": "男"}
```

​	很多人搞不清楚 JSON 和 JavaScript 对象的关系，甚至连谁是谁都不清楚，其实，可以这么理解：

- JSON 是 JavaScript 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串

  ```javascript
  var obj = {a: 'Hello', b: 'world'};	//这是一个对象，注意键名也是可以使用引号包裹的
  var json = '{"a": "Hello", "b": "World"}';	//这是一个 JSON 字符串，本质是一个字符串
  ```

##### JSON 和 JavaScript 对象互转

- 要实现从JSON字符串转换为JavaScript 对象，使用`JSON.parse() `方法：

  ```javascript
  var obj = JSON.parse('{"a": "Hello", "b": "World"}');
  //	结果是 {a: 'Hello', b: 'World'}
  ```

- 要实现从JavaScript 对象转换为JSON字符串，使用`JSON.stringify()`方法：

  ```javascript
  var json = JSON.stringify({a: 'Hello', b: 'World'});
  //	结果是 '{"a": "Hello", "b": "World"}'
  ```

代码测试：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script type="text/javascript">

        //  编写一个JavaScript对象
        var user = {
            name: "赵灿",
            age: 22,
            sex: "男"
        };

        //  将js对象转换为JSON对象
        var json = JSON.stringify(user);

        console.log(user);
        console.log(json);

        //  将JSON转换为js对象
        var js = JSON.parse(json);
        console.log(js);

    </script>
</head>
<body>

</body>
</html>
```

​	在IDEA中使用浏览器打开，查看控制台输出

##### Controller返回JSON数据

- Jackson应该是目前比较好的json解析工具了

- 当然工具不止这一个，比如还有阿里巴巴的 fastjson 等等

- 我们这里使用Jackson，使用它需要导入它的jar包

  ```xml
  <!-- https://mvcrespository.com/artifact/com.fasterxml.jackson.core/jackson-core -->
  <dependency>
  	<groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.10.0</version>
  </dependency>
  ```

- 配置SpringMVC需要的配置

  web.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
           version="4.0">
  
      <servlet>
          <servlet-name>springmvc</servlet-name>
          <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
          <init-param>
              <param-name>contextConfigLocation</param-name>
              <param-value>classpath:springmvc-servlet.xml</param-value>
          </init-param>
          <load-on-startup>1</load-on-startup>
      </servlet>
      <servlet-mapping>
          <servlet-name>springmvc</servlet-name>
          <url-pattern>/</url-pattern>
      </servlet-mapping>
  
      <filter>
          <filter-name>encoding</filter-name>
          <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
          <init-param>
              <param-name>encoding</param-name>
              <param-value>utf-8</param-value>
          </init-param>
      </filter>
      <filter-mapping>
          <filter-name>encoding</filter-name>
          <url-pattern>/*</url-pattern>
      </filter-mapping>
  </web-app>
  ```

  springmvc-servlet.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:mvc="http://www.springframework.org/schema/mvc"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          http://www.springframework.org/schema/context/spring-context.xsd
          http://www.springframework.org/schema/mvc
          http://www.springframework.org/schema/mvc/spring-mvc.xsd">
  
      <!-- 自动扫描指定的包，下面所有注解类交给IOC容器管理 -->
      <context:component-scan base-package="com.zc.controller"/>
      <mvc:default-servlet-handler/>
      <mvc:annotation-driven/>
  
      <!-- 视图解析器 -->
      <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
            id="internalResourceViewResolver">
          <!-- 前缀 -->
          <property name="prefix" value="/WEB-INF/jsp/"/>
          <!-- 后缀 -->
          <property name="suffix" value=".jsp"/>
      </bean>
  
  </beans>
  ```

- 我们顺便编写一个User的实体类，然后我们去编写我们的测试Controller

  ```java
  @Data
  @AllArgsConstructor
  @NoArgsConstructor
  public class User implements Serializable {
  
      private String name;
      private int age;
      private String sex;
  }
  ```

- 这里我们需要两个新东西，一个是`@ResponseBody`，一个是`ObjectMapper`对象，我们看下具体的用法

  编写一个Controller

  ```java
  @Controller
  public class UserController {
  
      @RequestMapping(value = "/j1")
      @ResponseBody   //它就不会走视图解析器,会直接返回一个字符串
      public String json1() throws JsonProcessingException {
  
          //  创建一个jackson的对象映射器，用来解析数据
          ObjectMapper mapper = new ObjectMapper();
  
          //  创建一个对象
          User user = new User("赵灿",22,"男");
  		
          //	将我们的对象解析成为json格式
          String str = mapper.writeValueAsString(user);
  
          //	由于@ResponseBody注解，这里会将str转成json格式返回，十分方便
          return str;
      }
  }
  ```

- 配置Tomcat，启动测试一下！

  http://localhost:8080/j1

- 发现出现了乱码问题，我们需要设置一下他的编码格式为utf-8，以及它返回的类型

- 通过@RequestMapping的produces属性来实现，修改下代码

  ```java
  //	produces：指定响应体返回类型和编码
  @RequestMapping(value = "j1", produces = "application/json;charset=utf-8")
  ```

- 再次测试，http://localhost:8080/j1，乱码问题OK

  注意：使用json记得处理乱码问题

##### 代码优化

**乱码统一解决**

上一种方法比较麻烦，如果项目中有许多请求则每一个都要调价，可以通过Spring配置统一指定，这样就不用每次都去处理了！

我们可以在SpringMVC的配置文件上添加一段消息StringHttpMessageConverter转换配置！

```xml
<!-- JSON乱码问题配置 -->
<mvc:annotation-driven>
    <mvc:message-converters register-defaults="true">
        <bean class="org.springframework.http.converter.StringHttpMessageConverter">
            <constructor-arg value="UTF-8"/>
        </bean>
        <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
            <property name="objectMapper">
                <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
                    <property name="failOnEmptyBeans" value="false"/>
                </bean>
            </property>
        </bean>
    </mvc:message-converters>
</mvc:annotation-driven>
```

**返回json字符串统一解决**

在类上直接使用 `@RestController`，这样子，里面所有的方法都只会返回json字符串了，不用再每一个都添加`@ResponseBody`！我们在前后端分离开发中，一般都是用`@RestController`，十分便捷

```java
@RestController
public class UserController {

    @RequestMapping(value = "/j1")
    public String json1() throws JsonProcessingException {

        //  jackson，ObjectMapper
        ObjectMapper mapper = new ObjectMapper();

        //  创建一个对象
        User user = new User("赵灿",22,"男");

        String str = mapper.writeValueAsString(user);

        return str;
    }
}
```

启动tomcat测试，结果都正常输出！

##### 测试集合输出

增加一个新方法

```java
@RequestMapping(value = "/j2")
public String json2() throws JsonProcessingException {

    //  jackson，ObjectMapper
    ObjectMapper mapper = new ObjectMapper();

    //  创建一个对象
    User user1 = new User("张三",22,"男");
    User user2 = new User("李四",22,"男");
    User user3 = new User("王五",22,"男");
    User user4 = new User("赵六",22,"男");

    List list = new ArrayList();
    list.add(user1);
    list.add(user2);
    list.add(user3);
    list.add(user4);

    String str = mapper.writeValueAsString(list);

    return str;
}
```

运行结果：十分完美，没有任何问题

##### 输出时间对象

增加一个新的方法

```java
@RequestMapping(value = "/j3")
public String json3() throws JsonProcessingException {

    //  jackson，ObjectMapper
    ObjectMapper mapper = new ObjectMapper();

    //	创建一个时间对象，java.util.Date
    Date date = new Date();
    //	将我们的对象解析称为json格式
    String str = mapper.writeValueAsString(date);
    return str;
}
```

运行结果：

- 默认日期格式会变成一个数字，是1970年1月1日到当前日期的毫秒数

- Jackson默认是会把时间转成Timestamps形式

  **解决方案：取消Timestamps形式，自定义时间格式

```java
@RequestMapping(value = "/j4")
public String json4() throws JsonProcessingException {

    ObjectMapper mapper = new ObjectMapper();

    //  不使用时间戳的方式
 	mapper.configure(SerializationFeature.WRITE_DATE_KEYS_AS_TIMESTAMPS,false);
    //  自定义日期格式对象
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    //  指定日期格式
    mapper.setDateFormat(sdf);

    Date date = new Date();

    return mapper.writeValueAsString(date);
}
```

运行结果：成功的输出了时间

##### 抽取为工具类

**如果要经常使用的话，这样是比较麻烦的，我们可以将这些代码封装到一个工具类中；我们去编写下**

```java
package com.zc.utils;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;

import java.text.SimpleDateFormat;

public class JsonUtils {

    public static String getJson(Object object) {
        return getJson(object,"yyyy-MM-dd HH:mm:ss");
    }

    public static String getJson(Object object, String dateFormat) {
        ObjectMapper mapper = new ObjectMapper();

        //  不使用时间戳的方式
        mapper.configure(SerializationFeature.WRITE_DATE_KEYS_AS_TIMESTAMPS,false);
        //  自定义日期格式
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat(dateFormat);
        mapper.setDateFormat(simpleDateFormat);


        try {
            return mapper.writeValueAsString(object);
        } catch (JsonProcessingException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

### FastJson

fastjson.jar是阿里开发的一款专门用于Java开发的包，可以方便的实现json对象与JavaBean对象的转换，实现JavaBean对象与json字符串的转换，实现json对象与json字符串的转换。实现json转换方法很多，最后的实现结果都是一样的。

​	fastjson 的 pom依赖

```xml
<dependency>
	<groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.60</version>
</dependency>
```

​	fastjson 三个主要的类

- 【JSONObject代表json对象】
  - JSONObject实现了Map接口，猜想JSONObject底层操作是由Map实现的
  - JSONObject对应json对象，通过各种形式的`get()`方法可以获取json对象中的数据，也可利用诸如`size()`，`isEmpty()`等方法获取“键：值”对的个数和判断是否为空，其本质是通过实现Map接口并调用接口中的方法完成的。
- 【JSONArray代表 json 对象数组】
  - 内部是有List接口中的方法来操作的
- 【JSON 代表 JSONObject和JSONArray的转化】
  - JSON类源码分析与使用
  - 仔细观察这些方法，主要是实现json对象，json对象数组，javabean对象，json字符串之间的相互转化

**代码测试**

```java
@RequestMapping(value = "/j5")
public String json5(){

    List<User> list = new ArrayList<User>();

    User user1 = new User("张三",22,"男");
    User user2 = new User("李四",22,"男");
    User user3 = new User("王五",22,"男");
    User user4 = new User("赵六",22,"男");

    list.add(user1);
    list.add(user2);
    list.add(user3);
    list.add(user4);
    
    System.out.println(---------Java对象 转 JSON字符串---------);
    String str1 = JSON.toJSONString(list);
    System.out.println("JSON.toJSONString(list)==>"+str1);
    String str2 = JSON.toJSONString(user1);
    System.out.println("JSON.toJSONString(user1)==>"+str2);
    
    System.out.println("\n--------- JSON字符串 转 Java对象---------");
    User jp_user1 = JSON.parseObject(str2,User.class);
    System.out.println("JSON.parseObject(str2,User.class)==>"+jp_user1);
    
    System.out.println("\n--------- Java对象 转 JSON对象---------");
    JSONObject jsonObject1 = (JSONObject) JSON.toJSON(user2);
    System.out.println("(JSONObject) JSON.toJSON(user2)==>"+jsonObject1);
    
    System.out.println("\n--------- JSON对象 转 Java对象---------");
    User to_java_user = JSON.toJavaObject(jsonObject1, User.class);
    System.out.println("JSON.toJavaObject(jsonObject1, User.class)==>"+to_java_user);
    return JSON.toJSONString(list);
}
```

### 整合SSM

##### 环境要求

- IDEA

- MySQL 5.7.19

- Tomcat9

- Maven 3.6

  要求：

- 需要熟练掌握MySQL数据库，Spring，JavaWeb及MyBatis知识，简单的前端知识

##### 数据库环境

创建一个存放书籍数据的数据库表

```sql
CREATE DATABASE `ssmbuild`;

USE `ssmbuild`;

DROP TABLE IF EXISTS `books`;

CREATE TABLE `books` (
	`bookID` INT(10) NOT NULL AUTO_INCREMENT COMMENT '书id',
	`bookName` VARCHAR(100) NOT NULL COMMENT '书名',
	`bookCounts` INT(11) NOT NULL COMMENT '数量',
	`detail` VARCHAR(200) NOT NULL COMMENT '描述',
	KEY `bookID` (`bookID`)
) ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO `books` (`bookID`,`bookName`,`bookCounts`,`detail`) VALUES 
(1,'Java',1,'从入门到放弃'),
(2,'MySQL',10,'从删库到跑路'),
(3,'Linux',5,'从进门到进牢')

)
```

##### 基本环境搭建

1. 新建一个Maven项目！添加web的支持

2. 导入相关的pom依赖

   ```xml
   <!-- 依赖 -->
   <dependencies>
       <!-- Junit -->
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.12</version>
       </dependency>
       <!-- 数据库驱动 -->
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>5.1.47</version>
       </dependency>
       <!-- 数据库连接池：c3p0 -->
       <dependency>
           <groupId>com.mchange</groupId>
           <artifactId>c3p0</artifactId>
           <version>0.9.5.2</version>
       </dependency>
   
       <!-- Servlet - JSP -->
       <dependency>
           <groupId>javax.servlet</groupId>
           <artifactId>servlet-api</artifactId>
           <version>2.5</version>
       </dependency>
       <dependency>
           <groupId>javax.servlet.jsp</groupId>
           <artifactId>jsp-api</artifactId>
           <version>2.2</version>
       </dependency>
       <!-- 支持EL表达式 -->
       <dependency>
           <groupId>javax.servlet</groupId>
           <artifactId>jstl</artifactId>
           <version>1.2</version>
       </dependency>
   
       <!-- Mybatis -->
       <dependency>
           <groupId>org.mybatis</groupId>
           <artifactId>mybatis</artifactId>
           <version>3.5.2</version>
       </dependency>
       <!-- Mybatis整合Spring -->
       <dependency>
           <groupId>org.mybatis</groupId>
           <artifactId>mybatis-spring</artifactId>
           <version>2.0.2</version>
       </dependency>
   
       <!-- Spring -->
       <dependency>
           <groupId>org.springframework</groupId>
           <artifactId>spring-webmvc</artifactId>
           <version>5.1.9.RELEASE</version>
       </dependency>
       <dependency>
           <groupId>org.springframework</groupId>
           <artifactId>spring-jdbc</artifactId>
           <version>5.1.9.RELEASE</version>
       </dependency>
   
       <!-- Lombok -->
       <dependency>
           <groupId>org.projectlombok</groupId>
           <artifactId>lombok</artifactId>
           <version>1.16.10</version>
       </dependency>
   </dependencies>
   ```

3. 静态资源过滤问题处理

   ```xml
   <!-- 静态资源导出问题 -->
   <build>
       <resources>
           <resource>
               <directory>src/main/java</directory>
               <includes>
                   <include>**/*.properties</include>
                   <include>**/*.xml</include>
               </includes>
               <filtering>false</filtering>
           </resource>
           <resource>
               <directory>src/main/resources</directory>
               <includes>
                   <include>**/*.properties</include>
                   <include>**/*.xml</include>
               </includes>
               <filtering>false</filtering>
           </resource>
       </resources>
   </build>
   ```

4. 建立基本结构和配置框架

   - com.zc.pojo

   - com.zc.dao

   - com.zc.service

   - com.zc.controller

   - mybatis-config.xml

     ```xml
     <?xml version="1.0" encoding="UTF-8" ?>
     <!DOCTYPE configuration
             PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
             "http://mybatis.org/dtd/mybatis-3-config.dtd">
     <configuration>
     
     </configuration>
     ```

   - applicationContext.xml

     ```xml
     <?xml version="1.0" encoding="UTF-8" ?>
     <beans xmlns="http://www.springframework.org/schema/beans"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://www.springframework.org/schema/beans
             http://www.springframework.org/schema/beans/spring-beans.xsd">
         
     </beans>
     ```

##### Mybatis层编写

1. 数据库配置文件 database.properties

   ```properties
   jdbc.driver=com.mysql.jdbc.Driver
   # 如果使用的是MySQL8.0+，增加一个时区的配置
   jdbc.url=jdbc:mysql://localhost:3306/ssmbuild?useSSL=false&useUnicode=true&characterEncoding=utf8
   jdbc.username=root
   jdbc.password=root
   ```

2. IDEA关联数据

3. 编写MyBatis的核心配置文件

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE configuration
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-config.dtd">
   <configuration>
   
       <!-- 配置数据源，交给Spring去做 -->
       
       <typeAliases>
           <package name="com.zc.pojo"/>
       </typeAliases>
   
       <mappers>
           <mapper class="com.zc.dao.BookMapper"/>
       </mappers>
   </configuration>
   ```

4. 编写数据库对应的实体类 com.zc.pojo.Books

   使用lombok插件！

   ```java
   package com.zc.pojo;
   
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   
   @Data
   @AllArgsConstructor
   @NoArgsConstructor
   public class Books {
   
       private int bookID;
       private String bookName;
       private int bookCounts;
       private String detail;
   }
   ```

5. 编写Dao层的Mapper接口

   ```java
   package com.zc.dao;
   
   import com.zc.pojo.Books;
   import org.apache.ibatis.annotations.Param;
   
   import java.util.List;
   
   public interface BookMapper {
   
       //  增加一本书
       int addBook(Books books);
   
       //  删除一本书
       int deleteBookById(@Param("bookID") int id);
   
       //  修改一本书
       int updateBook(Books books);
   
       //  查询一本书
       Books queryBookById(@Param("bookID") int id);
   
       //  查询全部的书
       List<Books> queryAllBook();
   }
   ```

6. 编写接口对应的Mapper.xml文件。需要导入MyBatis的包

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.zc.dao.BookMapper">
   
       <insert id="addBook" parameterType="Books">
           insert into ssmbuild.books (bookName, bookCounts, detail)
           VALUES (#{bookName}, #{bookCounts}, #{detail})
       </insert>
   
       <delete id="deleteBookById" parameterType="int">
           delete from ssmbuild.books where bookID = #{bookID}
       </delete>
   
       <update id="updateBook" parameterType="Books">
           update ssmbuild.books set
           bookName = #{bookName}, bookCounts = #{bookCounts}, detail = #{detail}
           where bookID = #{bookID};
       </update>
   
       <select id="queryBookById" resultType="Books">
           select * from ssmbuild.books where bookID = #{bookID}
       </select>
   
       <select id="queryAllBook" resultType="Books">
           select * from ssmbuild.books
       </select>
   </mapper>
   ```

7. 编写Service层的接口和实现类

   接口：

   ```java
   package com.zc.service;
   
   import com.zc.pojo.Books;
   import org.apache.ibatis.annotations.Param;
   
   import java.util.List;
   
   public interface BookService {
   
       //  增加一本书
       int addBook(Books books);
   
       //  删除一本书
       int deleteBookById(int id);
   
       //  修改一本书
       int updateBook(Books books);
   
       //  查询一本书
       Books queryBookById(int id);
   
       //  查询全部的书
       List<Books> queryAllBook();
   }
   ```

   实现类：

   ```java
   package com.zc.service;
   
   import com.zc.dao.BookMapper;
   import com.zc.pojo.Books;
   
   import java.util.List;
   
   public class BookServiceImpl implements BookService {
   
       //  service 调 dao 层
       private BookMapper bookMapper;
       public void setBookMapper(BookMapper bookMapper) {
           this.bookMapper = bookMapper;
       }
   
       public int addBook(Books books) {
           return bookMapper.addBook(books);
       }
   
       public int deleteBookById(int id) {
           return bookMapper.deleteBookById(id);
       }
   
       public int updateBook(Books books) {
           return bookMapper.updateBook(books);
       }
   
       public Books queryBookById(int id) {
           return bookMapper.queryBookById(id);
       }
   
       public List<Books> queryAllBook() {
           return bookMapper.queryAllBook();
       }
   }
   ```

##### Spring层

1. 配置Spring整合MyBatis，我们这里数据源使用c3p0连接池

2. 我们去编写Spring整合Mybatis的相关配置文件：spring-dao.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context
           https://www.springframework.org/schema/context/spring-context.xsd">
   
       <!-- 1、关联数据库配置文件 -->
       <context:property-placeholder location="classpath:database.properties" />
   
       <!-- 2、连接池
           dbcp：半自动化操作
           c3p0：自动化操作，（自动化的加载配置文件，并且可以自动设置到对象中）
           druid
           hikari
       -->
       <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
           <property name="driverClass" value="${jdbc.driver}"/>
           <property name="jdbcUrl" value="${jdbc.url}"/>
           <property name="user" value="${jdbc.username}"/>
           <property name="password" value="${jdbc.password}"/>
           
           <!-- c3p0连接池的私有属性 -->
           <property name="maxPoolSize" value="30"/>
           <property name="minPoolSize" value="10"/>
           <!-- 关闭连接后不自动Commit -->
           <property name="autoCommitOnClose" value="false"/>
           <!-- 获取连接超时时间 -->
           <property name="checkoutTimeout" value="10000"/>
           <!-- 当获取连接失败重试次数 -->
           <property name="acquireRetryAttempts" value="2"/>
       </bean>
   
       <!-- 3、sqlSessionFactory -->
       <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
           <property name="dataSource" ref="dataSource"/>
           <!-- 绑定Mybatis的配置文件 -->
           <property name="configLocation" value="classpath:mybatis-config.xml"/>
       </bean>
   
       <!-- 4、配置dao接口扫描包，动态的实现了dao接口可以注入到spring容器中 -->
       <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
           <!-- 注入sqlSessionFactory -->
           <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
           <!-- 要扫描的dao包 -->
           <property name="basePackage" value="com.zc.dao"/>
       </bean>
   </beans>
   ```

3. Spring整合service层

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context
           https://www.springframework.org/schema/context/spring-context.xsd">
   
   
       <!-- 1、扫描service 下的包 -->
       <context:component-scan base-package="com.zc.service"/>
   
       <!-- 2、将我们的所有业务类，注入到spring，可以通过配置或者注解实现 -->
       <bean id="BookServiceImpl" class="com.zc.service.BookServiceImpl">
           <property name="bookMapper" ref="bookMapper"/>
       </bean>
   
       <!-- 3、声明式事务 -->
       <bean id="DataSourceTransactionManager"
             class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
           <!-- 注入数据源 -->
           <property name="dataSource" ref="dataSource"/>
       </bean>
   
       <!-- 4、AOP事务支持 -->
   
   </beans>
   ```

##### SpringMVC

1. 添加web支持

2. 将相关依赖导入lib目录下

3. 配置applicationContext.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:mvc="http://www.springframework.org/schema/mvc"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context.xsd
           http://www.springframework.org/schema/mvc
           http://www.springframework.org/schema/mvc/spring-mvc.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
   
       <import resource="classpath:spring-dao.xml"/>
       <import resource="classpath:spring-service.xml"/>
   
       <!-- 1、注解驱动 -->
       <mvc:annotation-driven/>
   
       <!-- 2、静态资源过滤 -->
       <mvc:default-servlet-handler/>
   
       <!-- 3、扫描包：controller -->
       <context:component-scan base-package="com.zc.controller"/>
   
       <!-- 4、视图解析器 -->
       <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
           <property name="prefix" value="/WEB-INF/jsp/"/>
           <property name="suffix" value=".jsp"/>
       </bean>
   </beans>
   ```

4. 在web.xml中增加前置控制器及乱码处理等配置

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">
   
       <!-- DispatcherServlet-->
       <servlet>
           <servlet-name>springmvc</servlet-name>
           <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
           <init-param>
               <param-name>contextConfigLocation</param-name>
               <param-value>classpath:applicationContext.xml</param-value>
           </init-param>
           <load-on-startup>1</load-on-startup>
       </servlet>
       <servlet-mapping>
           <servlet-name>springmvc</servlet-name>
           <url-pattern>/</url-pattern>
       </servlet-mapping>
   
       <!-- 乱码过滤 -->
       <filter>
           <filter-name>encoding</filter-name>
           <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
           <init-param>
               <param-name>encoding</param-name>
               <param-value>utf-8</param-value>
           </init-param>
       </filter>
       <filter-mapping>
           <filter-name>encoding</filter-name>
           <url-pattern>/*</url-pattern>
       </filter-mapping>
   
       <!-- Session -->
       <session-config>
           <session-timeout>15</session-timeout>
       </session-config>
   </web-app>
   ```

##### 编写功能

1. 实体类

   ```java
   package com.zc.pojo;
   
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   
   @Data
   @AllArgsConstructor
   @NoArgsConstructor
   public class Books {
   
       private int bookID;
       private String bookName;
       private int bookCounts;
       private String detail;
   }
   ```

2. Dao层接口及xml编写

   接口

   ```java
   package com.zc.dao;
   
   import com.zc.pojo.Books;
   import org.apache.ibatis.annotations.Param;
   
   import java.util.List;
   
   public interface BookMapper {
   
       //  增加一本书
       int addBook(Books books);
   
       //  删除一本书
       int deleteBookById(@Param("bookID") int id);
   
       //  修改一本书
       int updateBook(Books books);
   
       //  查询一本书
       Books queryBookById(@Param("bookID") int id);
   
       //  查询全部的书
       List<Books> queryAllBook();
   
       //  查询书籍
       List<Books> queryBookByName(@Param("bookName") String bookName);
   }
   ```

   xml

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.zc.dao.BookMapper">
   
       <insert id="addBook" parameterType="Books">
           insert into ssmbuild.books (bookName, bookCounts, detail)
           VALUES (#{bookName}, #{bookCounts}, #{detail})
       </insert>
   
       <delete id="deleteBookById" parameterType="int">
           delete from ssmbuild.books where bookID = #{bookID}
       </delete>
   
       <update id="updateBook" parameterType="Books">
           update ssmbuild.books set
           bookName = #{bookName}, bookCounts = #{bookCounts}, detail = #{detail}
           where bookID = #{bookID};
       </update>
   
       <select id="queryBookById" resultType="Books">
           select * from ssmbuild.books where bookID = #{bookID}
       </select>
   
       <select id="queryAllBook" resultType="Books">
           select * from ssmbuild.books
       </select>
   
       <select id="queryBookByName" resultType="Books">
           select * from ssmbuild.books
           <where>
               <if test="bookName != null and bookName != ''">
                   bookName like CONCAT('%', #{bookName}, '%')
               </if>
           </where>
       </select>
   </mapper>
   ```

3. Service接口及实现类

   接口

   ```java
   package com.zc.service;
   
   import com.zc.pojo.Books;
   import org.apache.ibatis.annotations.Param;
   
   import java.util.List;
   
   public interface BookService {
   
       //  增加一本书
       int addBook(Books books);
   
       //  删除一本书
       int deleteBookById(int id);
   
       //  修改一本书
       int updateBook(Books books);
   
       //  查询一本书
       Books queryBookById(int id);
   
       //  查询全部的书
       List<Books> queryAllBook();
   
       //  查询书籍
       List<Books> queryBookByName(String bookName);
   }
   ```

   实现类

   ```java
   package com.zc.service;
   
   import com.zc.dao.BookMapper;
   import com.zc.pojo.Books;
   
   import java.util.List;
   
   public class BookServiceImpl implements BookService {
   
       //  service 调 dao 层
       private BookMapper bookMapper;
       public void setBookMapper(BookMapper bookMapper) {
           this.bookMapper = bookMapper;
       }
   
       public int addBook(Books books) {
           return bookMapper.addBook(books);
       }
   
       public int deleteBookById(int id) {
           return bookMapper.deleteBookById(id);
       }
   
       public int updateBook(Books books) {
           return bookMapper.updateBook(books);
       }
   
       public Books queryBookById(int id) {
           return bookMapper.queryBookById(id);
       }
   
       public List<Books> queryAllBook() {
           return bookMapper.queryAllBook();
       }
   
       public List<Books> queryBookByName(String bookName) {
           return bookMapper.queryBookByName(bookName);
       }
   }
   ```

4. Controller

   ```java
   package com.zc.controller;
   
   import com.zc.pojo.Books;
   import com.zc.service.BookService;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.beans.factory.annotation.Qualifier;
   import org.springframework.stereotype.Controller;
   import org.springframework.ui.Model;
   import org.springframework.web.bind.annotation.*;
   
   import java.util.List;
   
   @Controller
   @RequestMapping(value = "/book")
   public class BookController {
   
       //  Controller 调 Service 层
       @Autowired
       @Qualifier("BookServiceImpl")
       private BookService bookService;
   
       //  查询全部的书籍并且返回到一个书籍展示页面
       @GetMapping(value = "/allBook")
       public String list(Model model) {
           List<Books> list = bookService.queryAllBook();
           model.addAttribute("list",list);
           return "allBook";
       }
   
       //  跳转到增加书籍页面
       @GetMapping(value = "/toAddBook")
       public String toAddPaper() {
           return "addBook";
       }
   
       //  添加书籍的请求
       @PostMapping(value = "/addBook")
       public String addBook(Books books) {
           bookService.addBook(books);
           return "redirect:/book/allBook";    //重定向到我们的@GetMapping(value = "/allBook")请求
       }
   
       //  跳转到修改页面
       @GetMapping(value = "/toUpdateBook/{id}")
       public String toUpdatePaper(@PathVariable("id") int id, Model model) {
           Books books = bookService.queryBookById(id);
           model.addAttribute("book",books);
           return "updateBook";
       }
   
       //  修改书籍
       @PostMapping(value = "/updateBook")
       public String updateBook(Books books) {
           bookService.updateBook(books);
           return "redirect:/book/allBook";
       }
   
       //  删除书籍
       @GetMapping(value = "/deleteBook/{id}")
       public String deleteBook(@PathVariable("id") int id) {
           bookService.deleteBookById(id);
           return "redirect:/book/allBook";
       }
   
       //  查询书籍
       @GetMapping(value = "/queryBook")
       public String queryBook(String queryBookName, Model model){
           List<Books> books = bookService.queryBookByName(queryBookName);
   
           if(books.size() == 0){
               model.addAttribute("error","您的搜索内容未查到");
           }
   
           model.addAttribute("list",books);
           return "allBook";
       }
   }
   ```

5. 页面

   index.jsp

   ```jsp
   <%--
     Created by IntelliJ IDEA.
     User: Administrator
     Date: 2021/2/13
     Time: 11:53
     To change this template use File | Settings | File Templates.
   --%>
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
     <head>
       <title>$Title$</title>
   
       <style>
         a{
           text-decoration: none;
           color: black;
           font-size: 18px;
         }
         h3{
           width: 180px;
           height: 38px;
           margin: 100px auto;
           text-align: center;
           line-height: 38px;
           background: deepskyblue;
           border-radius: 5px;
         }
       </style>
     </head>
     <body>
     <h3>
       <a href="${pageContext.request.contextPath}/book/allBook">进入书籍页面</a>
     </h3>
     </body>
   </html>
   ```

   allBook.jsp

   ```jsp
   <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
   <%--
     Created by IntelliJ IDEA.
     User: Administrator
     Date: 2021/2/13
     Time: 12:18
     To change this template use File | Settings | File Templates.
   --%>
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head>
       <title>书籍展示</title>
   
       <%-- Bootstrap 美化界面 --%>
       <link href="http://libs.baidu.com/bootstrap/3.0.3/css/bootstrap.css" rel="stylesheet">
   </head>
   <body>
   
   <div class="container">
   
       <div class="row clearfix">
               <div class="col-md-12 column">
                   <div class="page-header">
                       <h1>
                           <small>书籍列表 —————— 显示所有书籍</small>
                       </h1>
                   </div>
               </div>
   
           <div class="row">
               <div class="col-md-4 column">
                   <%-- toAddBook --%>
                   <a class="btn btn-primary" href="${pageContext.request.contextPath}/book/toAddBook">新增书籍</a>
                   <a class="btn btn-primary" href="${pageContext.request.contextPath}/book/allBook">显示全部书籍</a>
               </div>
               <div class="col-md-8 column">
                   <%-- 查询书籍 --%>
                   <form class="form-inline" action="${pageContext.request.contextPath}/book/queryBook" method="get" style="float: right">
                       <input type="text" class="form-control" name="queryBookName" placeholder="请输入要查询的书籍名称">
                       <input type="submit" value="查询" class="btn btn-primary">
                       <span style="color: red;font-weight: bold">${error}</span>
                   </form>
               </div>
           </div>
       </div>
   
       <div class="row clearfix">
           <div class="col-md-12 colmn">
               <table class="table table-hover table-striped">
                   <thead>
                       <tr>
                           <th>书籍编号</th>
                           <th>书籍名称</th>
                           <th>书籍数量</th>
                           <th>书籍详情</th>
                           <th>操作</th>
                       </tr>
                   </thead>
   
                   <%-- 书籍从数据库中查询出来，从这个list中遍历：forEach --%>
                   <tbody>
                       <c:forEach var="book" items="${list}">
                           <tr>
                               <td>${book.bookID}</td>
                               <td>${book.bookName}</td>
                               <td>${book.bookCounts}</td>
                               <td>${book.detail}</td>
                               <td>
                                   <a href="${pageContext.request.contextPath}/book/toUpdateBook/${book.bookID}">修改</a>
                                   &nbsp; | &nbsp;
                                   <a href="${pageContext.request.contextPath}/book/deleteBook/${book.bookID}">删除</a>
                               </td>
                           </tr>
                       </c:forEach>
                   </tbody>
               </table>
           </div>
       </div>
   
   </div>
   
   </body>
   </html>
   ```

   addBook.jsp

   ```jsp
   <%--
     Created by IntelliJ IDEA.
     User: Administrator
     Date: 2021/2/13
     Time: 14:00
     To change this template use File | Settings | File Templates.
   --%>
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head>
       <title>添加书籍</title>
   
       <%-- Bootstrap 美化界面 --%>
       <link href="http://libs.baidu.com/bootstrap/3.0.3/css/bootstrap.css" rel="stylesheet">
   </head>
   <body>
   
       <div class="container">
   
           <div class="row clearfix">
               <div class="col-md-12 column">
                   <div class="page-header">
                       <h1>
                           <small>新增书籍</small>
                       </h1>
                   </div>
               </div>
           </div>
   
           <form action="${pageContext.request.contextPath}/book/addBook" method="post">
               <div class="form-group">
                   <label>书籍名称：</label>
                   <input type="text" name="bookName" class="form-control" required>
               </div>
               <div class="form-group">
                   <label>书籍数量：</label>
                   <input type="text" name="bookCounts" class="form-control" required>
               </div>
               <div class="form-group">
                   <label>书籍详情：</label>
                   <input type="text" name="detail" class="form-control" required>
               </div>
               <div class="form-group">
                   <input type="submit" class="form-control" value="添加">
               </div>
           </form>
       </div>
   
   
   
   </body>
   </html>
   ```

   updateBook.jsp

   ```jsp
   <%--
     Created by IntelliJ IDEA.
     User: Administrator
     Date: 2021/2/13
     Time: 14:28
     To change this template use File | Settings | File Templates.
   --%>
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head>
       <title>修改书籍</title>
   
       <%-- Bootstrap 美化界面 --%>
       <link href="http://libs.baidu.com/bootstrap/3.0.3/css/bootstrap.css" rel="stylesheet">
   </head>
   <body>
   
   <div class="container">
   
       <div class="row clearfix">
           <div class="col-md-12 column">
               <div class="page-header">
                   <h1>
                       <small>修改书籍</small>
                   </h1>
               </div>
           </div>
       </div>
   
       <form action="${pageContext.request.contextPath}/book/updateBook" method="post">
           <input type="hidden" name="bookID" value="${book.bookID}">
           <div class="form-group">
               <label>书籍名称：</label>
               <input type="text" name="bookName" value="${book.bookName}" class="form-control" required>
           </div>
           <div class="form-group">
               <label>书籍数量：</label>
               <input type="text" name="bookCounts" value="${book.bookCounts}" class="form-control" required>
           </div>
           <div class="form-group">
               <label>书籍详情：</label>
               <input type="text" name="detail" class="form-control" value="${book.detail}" required>
           </div>
           <div class="form-group">
               <input type="submit" class="form-control" value="修改">
           </div>
       </form>
   </div>
   
   </body>
   </html>
   ```

6. 测试

![](https://i.loli.net/2021/02/13/WYuEcqavIALiSje.png)

![](https://i.loli.net/2021/02/13/K98TsFCYfBuXm24.png)

![](https://i.loli.net/2021/02/13/VIoDTmaCej6W8yP.png)

完美运行！

### Ajax技术

- AJAX = Asynchronous JavaScript and XML（异步的JavaScript和XML）

- AJAX是一种在无需重新加载整个页面的情况下，能够更新部分页面的技术

- Ajax不是一种新的编程语言，而是一种用于创建更好更快以及交互性更强的Web应用程序的技术

- 在2005年，Google通过其Google Suggest 使 AJAX 变得流行起来。Google Suggest能够自动帮你完成搜索单词

- Google Suggest使用AJAX创造出动态性极强的 web 界面；当你在谷歌的搜索框输入关键字时，JavaScript会把这些字符发送到服务器，然后服务器会返回一个搜索建议的列表

- 就和国内百度的搜索框一样

  ![](https://i.loli.net/2021/02/13/dD5QhTXjt9oEpOs.png)

- 传统的网页（即不用ajax技术的网页），想要更新内容或提交一个表单，都需要重新加载整合网页

- 使用ajax技术的网页，通过在后台服务器进行少量的数据交换，就可以实现异步局部更新

- 使用Ajax，用户可以创建接近本地桌面应用的直接、高可用、更丰富、更动态的Web用户界面

##### 伪造Ajax

​	我们可以使用前端的一个标签来伪造一个ajax的样子

1. 新建一个module：springmvc-06-ajax：导入web支持

2. 编写一个 ajax-frame.html 使用 iframe 测试，感受下效果

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>iframe测试体验页面无刷新</title>
   
       <script>
           //  所有的值变量，提前获取
           function go(){
               var url = document.getElementById("url").value;
               document.getElementById("iframe1").src = url;
           }
       </script>
   </head>
   <body>
   
   <div>
       <p>请输入地址：</p>
       <p>
           <input type="text" id="url">
           <input type="button" value="提交" onclick="go()"/>
       </p>
   
   </div>
   
   <div>
       <iframe id="iframe1" frameborder="0" style="width: 100%;height: 500px"></iframe>
   </div>
   
   
   </body>
   </html>
   ```

3. 利用IDEA开浏览器测试一下

   **利用AJAX可以做：**

- 注册时，输入用户名自动监测用户是否已经存在
- 登录时，提示用户名密码错误
- 删除数据行时，将行ID发送到后台，后台在数据库中删除，数据库删除成功后，在页面DOM中奖数据行也删除。
- ...等等

##### jQuery.ajax

- 直接使用jQuery提供的，方便学习和使用，避免重复造轮子。
- Ajax的核心是XMLHttpRequest对象（XHR）。XHR为向服务器发送请求和解析服务器响应提供了接口。能够以异步方式从服务器获取新数据
- jQuery提供多个与AJAX有关的方法
- 通过jQuery AJAX方法，您能够使用 HTTP Get 和 HTTP Post 从远程服务器上请求文本、HTML、XML或JSON。同时您能够把这些外部数据直接载入网页的被选元素中
- jQuery不是生产者，而是大自然搬运工
- jQuery Ajax本质就是 XMLHttpRequest，对它进行了封装，方便调用

```css
jQuery.ajax(...)
	部分参数：
		url: 请求地址
		type：请求方式，GET、POST(1.9.0之后用method)
		headers：请求头
		data：要发送的数据
		contentType：即将发送信息至服务器的内容编码类型（默认："application/x-www.form-urlencoding"）
		async：是否异步
		timeout：设置请求超时时间（毫秒）
		beforeSend：发送请求前执行的函数（全局）
		complete：完成之后执行的回调函数（全局）
		success：成功之后执行的回调函数（全局）
		error：失败之后执行的回调函数（全局）
		accepts：通过请求头发送给服务器，告诉服务器当前客户端可接受的数据类型
		dataType：将服务器端返回的数据转换成指定类型
		"xml"：将服务器端返回的内容转换成xml格式
		"text"：将服务器端返回的内容转换成普通文本格式
		"html"：将服务器端返回的内容转换成普通文本格式，在插入DOM中时，如果包含JavaScript标签会在插入DOM时执行
		"script"：返回纯文本JavaScript代码。不会自动缓存结果。除非设置了cache参数。注意在远程请求时（不在同一个域下），所有post请求都将转为get请求。
		"json"：将服务器端返回的内容转换成相应的JavaScript对象
		"jsonp"：JSONP格式。使用SONP形式调用函数时，例如myurl?callback=?，JQuery将自动替换后一个“?”为正确的函数名，以执行回调函数。
		
```

### 拦截器

SpringMVC的处理器拦截器类似于Servlet开发中的过滤器Filter，用于对处理器进行预处理和后处理。开发者可以自己定义一些拦截器来实现特定的功能

**过滤器与拦截器的区别：**拦截器是AOP思想的具体应用

**过滤器**

- servlet规范中的一部分，任何java web工程都可以使用
- 在url-pattern 中配置了 `/*`之后，可以对所有要访问的资源进行拦截

**拦截器**

- 拦截器是SpringMVC框架自己的，只有使用了SpringMVC框架的工程才能使用
- 拦截器只会拦截访问的控制器方法，如果访问的是jsp/html/css/image/js 是不会进行拦截的

##### 自定义拦截器

想要自定义拦截器，必须实现`HandlerInterceptor`接口

1. 新建一个Module，SpringMVC-07-Interceptor，添加web支持
2. 配置 web.xml 和 springmvc-servlet.xml 文件
3. 编写一个拦截器

**注：**

1. 拦截级别：SpringMVC是方法级别的拦截，而Struts2是类级别的拦截
2. 数据独立性：SpringMVC方法间独立，独享request和response
3. 拦截机制：SpringMVC用的是独立的AOP方式，Struts2有自己的interceptor机制

