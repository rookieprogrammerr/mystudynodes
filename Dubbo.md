# 分布式

## 任务

- 异步任务

  通常我们在实现多线程时，会出现等待情况。这对于Web来讲是非常致命的问题。我们可以通过Spring中的异步来处理该问题

  AsyncService

  ```java
  package com.zc.service;
  
  import org.springframework.scheduling.annotation.Async;
  import org.springframework.stereotype.Service;
  
  @Service
  public class AsyncService {
  
      //  告诉Spring这是一个异步的方法
      @Async
      public void hello() {
  
          try {
              Thread.sleep(3000);
          } catch (InterruptedException e) {
              e.printStackTrace();
          }
  
          System.out.println("數據正在處理...");
      }
  
  }
  ```

  HelloController

  ```java
  package com.zc.controller;
  
  import com.zc.service.AsyncService;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  public class HelloController {
  
      @Autowired
      AsyncService asyncService;
  
      @GetMapping("/hello")
      public String hello() {
          asyncService.hello();
          return "hello";
      }
  
  }
  ```

  **要在Springboot的启动类中加入开启异步注解功能**

  ```java
  //  开启异步注解功能
  @EnableAsync
  ```

  实现效果：页面瞬间加载

  ![](http://zhaocan.fym233.cn/5qyri62k3i)

  3秒后控制台输出内容

  ![](http://zhaocan.fym233.cn/i8rdgl714g)

- 邮件发送

  在qq或任意邮箱中开启SMTP服务，并配置application.yml

  ```yml
  spring:
    mail:
      username: xxxxxxxx@qq.com
      password: xxxxxxxxxxxxxxx
      host: smtp.qq.com
      # 开启加密授权验证
      properties:
        mail:
          smtp:
            ssl:
              enable: true
  ```

  进入测试类进行测试

  ```java
  @SpringBootTest
  class Springboot09TestApplicationTests {
  
      @Autowired
      JavaMailSenderImpl mailSender;
  
      @Test
      void contextLoads() {
  
          //  一个简单的邮件
          SimpleMailMessage mailMessage = new SimpleMailMessage();
  
          mailMessage.setSubject("你好赵灿");
          mailMessage.setText("正文：您好赵灿");
          mailMessage.setTo("zc1872751113@gmail.com");
          mailMessage.setFrom("1872751113@qq.com");
  
          mailSender.send(mailMessage);
      }
  
  
      @Test
      void contextLoads2() throws MessagingException {
  
          //  一个复杂的邮件
          //MimeMessage mimeMessage = new MimeMessage();
  
          MimeMessage mimeMessage = mailSender.createMimeMessage();
          MimeMessageHelper helper = new MimeMessageHelper(mimeMessage, true);
  
          helper.setSubject("你好赵灿-plus");
          helper.setText("<h1 style='color: red'>正文：您好赵灿</h1>", true);
  
          //  附件
          helper.addAttachment("1.jps", new File("F:\\project\\springboot-09-test\\src\\main\\resources\\static\\welcome-cover.jpg"));
  
          helper.setTo("zc1872751113@gmail.com");
          helper.setFrom("1872751113@qq.com");
  
          mailSender.send(mimeMessage);
      }
  }
  ```

  可以将所有功能封装成一个工具类

  ```java
  package com.zc.utils;
  
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.mail.SimpleMailMessage;
  import org.springframework.mail.javamail.JavaMailSenderImpl;
  import org.springframework.mail.javamail.MimeMessageHelper;
  import org.springframework.stereotype.Component;
  
  import javax.mail.MessagingException;
  import javax.mail.internet.MimeMessage;
  import java.io.File;
  
  @Component
  public class SendMailUtils {
  
      @Autowired
      JavaMailSenderImpl mailSender;
  
      /**
       *
       * @param subject：邮件标题
       * @param text：邮件正文
       * @param setTo：发送至邮箱
       */
      public void EasyMail(String subject, String text, String setTo) {
  
          //  一个简单的邮件
          SimpleMailMessage mailMessage = new SimpleMailMessage();
  
          mailMessage.setSubject(subject);
          mailMessage.setText(text);
          mailMessage.setTo(setTo);
          mailMessage.setFrom("1872751113@qq.com");
  
          mailSender.send(mailMessage);
      }
  
      /**
       *
       * @param html：邮件内容是否以html标签格式输出
       * @param subject：邮件标题
       * @param text：邮件正文
       * @param setTo：邮件发送至邮箱
       * @throws MessagingException
       */
      public void SendMail(boolean html, String subject, String text, String setTo) throws MessagingException {
  
          //  一个复杂的邮件
          //MimeMessage mimeMessage = new MimeMessage();
  
          MimeMessage mimeMessage = mailSender.createMimeMessage();
          MimeMessageHelper helper = new MimeMessageHelper(mimeMessage, true);
  
          helper.setSubject(subject);
          helper.setText(text, html);
          helper.setTo(setTo);
          helper.setFrom("1872751113@qq.com");
  
          mailSender.send(mimeMessage);
      }
  
      /**
       *
       * @param html：邮件内容是否以html标签格式输出
       * @param subject：邮件标题
       * @param text：邮件正文
       * @param setTo：邮件发送至邮箱
       * @param filename：附件名称
       * @param filepath：附件路径
       * @throws MessagingException
       */
      public void SendMailByFile(boolean html, String subject, String text, String setTo, String filename, String filepath) throws MessagingException {
  
          //  一个复杂的邮件
          //MimeMessage mimeMessage = new MimeMessage();
  
          MimeMessage mimeMessage = mailSender.createMimeMessage();
          MimeMessageHelper helper = new MimeMessageHelper(mimeMessage, true);
  
          helper.setSubject(subject);
          helper.setText(text, html);
  
          //  附件
          helper.addAttachment(filename, new File(filepath));
  
          helper.setTo(setTo);
          helper.setFrom("1872751113@qq.com");
  
          mailSender.send(mimeMessage);
      }
  }
  ```

- 定时任务 

  ```java
  TaskScheduler	//任务调度这
  TaskExecutor	//任务执行者
  
  @EnableScheduling	//开启定时功能的注解
  @Scheduled			//什么时候执行	
  
  cron表达式    
  ```

  ScheduledService

  ```java
  package com.zc.service;
  
  import org.springframework.scheduling.annotation.Scheduled;
  import org.springframework.stereotype.Service;
  
  @Service
  public class ScheduledService {
  
      //  在一个特定的时间执行这个方法
  
      //cron表达式
      //秒 分 时 日 月 周几
      @Scheduled(cron = "0 * * * * 0-7")
      public void hello() {
          System.out.println("hello，你被执行了");
      }
  }
  ```

  在SpringBoot启动类上加入注解

  ```java
  @EnableScheduling   //开启定时功
  ```

## Dobbo+Zookeeper+Springboot

### 什么是分布式

分布式系统是由一组通过网络进行通信、为了完成共同的任务而协调工作的计算机节点组成的系统。分布式系统的出现是为了用廉价的、普通的机器完成单个计算机无法完成的计算、存储任务。其目的是**利用更多的机器，处理更多的数据**。

分布式系统（**distributed system**）是建立在网络之上的软件系统

首先需要明确的是，只有当单个节点的处理能力无法满足日益增长的计算、存储任务的时候，且硬件的提升（加内存、加磁盘、使用更好的CPU）高昂到得不尝试的时候。应用程序也不能进一步优化的时候，我们才需要考虑分布式系统。因为，分布式系统要解决的问题本身就是和单机系统一样的，而由于分布式系统多节点、通过网络通信的拓扑结构，会引入很多单机系统没有的问题，为了解决这些问题又会引入更多的机制、协议，带来更多的问题。

### Dubbo文档

随着互联网的发展，网站应用的规模不断扩大，常规的垂直应用架构已无法应对，分布式服务架构以及流动计算架构势在必行，急需一个治理系统确保架构有条不紊的演进

![](http://zhaocan.fym233.cn/v0ogjkcutd)

**单一应用架构**

当网站流量很小时，只需一个应用，将所有功能都部署在一起，以减少部署节点和成本。此时，用于简化增删改查工作量的数据访问框架（ORM）是关键

![](http://zhaocan.fym233.cn/it7nttsc9s)

适用于小型网站，小型管理系统，将所有功能都部署到一个功能里，简单易用。

缺点：

1. 性能扩展比较难
2. 协同开发问题
3. 不利于升级维护

**垂直应用架构**

当访问量逐渐增大，单一应用增加机器带来的加速度越来越小，将应用拆成互不相干的几个应用，以提升效率。此时，用于加速前端页面开发的Web框架（MVC）是关键。

![](http://zhaocan.fym233.cn/fkt92epo3e)

通过切分业务来实现各个模块独立部署，降低了维护和部署的难度，团队各司其职更易管理，性能扩展也更方便；更有针对性

缺点：共用模块无法重复利用，开发性的浪费

**分布式服务架构**

当垂直应用越来越多，应用之间交互不可避免，将核心业务抽取出来，作为独立的服务，逐渐形成稳定的服务中心，使前端应用能更快速的响应多变的市场需求。此时，用于提高业务复用及整合的**分布式服务框架（RPC）才是关键**。

![](http://zhaocan.fym233.cn/b2gnxhbz58)

**流动计算架构**

当服务越来越多，容量的评估，小服务资源的浪费等问题逐渐显现，此时需增加一个调度中心基于访问压力实时管理集群容量，提高集群利用率。此时，用于**提高机器利用率的资源调度和治理中心（SOA）[ Service Oriented Architecture ]是关键**。

![](http://zhaocan.fym233.cn/mvf0fh0jm6)

### RPC

什么是RPC

RPC【Remote Procedure Call】是指远程过程调用，是一种进程间通信方式，他是一种技术的思想，而不是规范。它允许程序调用另一个地址空间（通常是共享网络的另一台机器上）的过程或函数，而不用程序员显示编码这个远程调用的细节。即程序员无论是调用本地的还是远程的函数，本质上编写的调用代码基本相同。

也就是说两台服务器 A，B。一个应用部署在A服务器上，想要调用B服务器上应用提供的函数/方法，由于不在一个内存空间，不能直接调用，需要通过网络来表达调用的语义和传达调用的数据。为什么要用RPC呢？就是无法在一个进程内，甚至一个计算机内通过本地调用的方式完成的需求，比如不同的系统间的通讯，甚至不同的组织间的通讯，由于计算能力需要横向扩展，需要在多态机器组成的集群上部署应用。RPC就是要像调用本地的函数一样去调远程函数。

**RPC基本原理**

![](http://zhaocan.fym233.cn/ojdvng1iv8)

**步骤解析：**

![](http://zhaocan.fym233.cn/58dkpr90su)

RPC两个核心模块：通讯，序列化

## Dubbo

### 什么是Dubbo

Apache Dubbo 是一款高性能、轻量级的开源Java RPC框架，它提供了三大核心能力：

- 面向接口的远程方法调用
- 只能容错和负载均衡
- 服务自动注册和发现

[dubbo官网](https://dubbo.apache.org/zh/)

1. 了解Dubbo的特性
2. 查看官方文档

**dubbo基本概念**

![](http://zhaocan.fym233.cn/2u51k0tr5k)

- 服务提供者（Provider）：暴露服务的服务提供方，服务提供者在启动时，向注册中心注册自己提供的服务
- 服务消费者（Consumer）：调用远程服务的服务消费方，服务消费者在启动时，向注册中心订阅自己所需的服务，服务消费者，从提供者地址列表中，基于软负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用。
- 注册中心（Registry）：注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者
- 监控中心（Monitor）：服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心

**调用关系说明**

- 服务容器负责启动，加载，运行服务提供者
- 服务提供者在启动时，向注册中心注册自己提供的服务
- 服务消费者在启动时，向注册中心订阅自己所需的服务
- 注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者
- 服务消费者，从提供者地址列表中，基于软负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用
- 服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心

### Dubbo环境搭建

[Zookeeper注册中心](https://dubbo.apache.org/zh/docs/v2.7/user/references/registry/zookeeper/)

[Zookeeper官方文档](https://zookeeper.apache.org/)

> window下安装zookeeper

1. 下载zookeeper：[下载地址](https://www.apache.org/dyn/closer.lua/zookeeper/zookeeper-3.6.2/apache-zookeeper-3.6.2-bin.tar.gz)

2. 运行`/bin/zkServer.cmd`，初次运行会报错，没有zoo,cfg配置文件；可能遇到问题：闪退

   解决方案：编辑zkServer.cmd文件末尾添加pause，这样运行出错就不会退出，会提示错误信息，方便找到原因

   ![](http://zhaocan.fym233.cn/r7ywj1hp5)

3. 修改zoo.cfg配置文件

   将conf文件夹下面的zoo_sample.cof复制一份改名为zoo.cfg即可

   注意及格重要位置：

   - dataDir=./	临时数据存储的目录（可写相对路径）
   - clientPort=2181   zookeeper的端口号

   修改完成后再次启动zookeeper

   ![](http://zhaocan.fym233.cn/qddyyouk4a)

4. 使用zkCli.cmd测试

   `ls /`：列出zookeeper根下保存的所有节点

   ```shell
   [zk: localhost:2181(CONNECTED) 0] ls /
   [zookeeper]
   ```

   `create -e /zhaocan 123`：创建一个zhaocan节点，值为123

   ![](http://zhaocan.fym233.cn/e65ulqghuw)

   `get /zhaocan`：获取/zhaocan节点的值

   ![](http://zhaocan.fym233.cn/5c3p7qivob)

### windows下安装dubbo-admin

dubbo本身并不是一个服务软件。它其实就是一个jar包，能够帮你的java程序连接到zookeeper，并利用zookeeper消费、提供服务。

但是为了让用户更好的管理监控众多的dubbo服务，官方提供了一个可视化的监控程序dubbo-admin，不过这个监控即使不装也不影响使用

1. 下载dubbo-admin

   地址：https://github.com/apache/dubbo-admin/tree/master

2. 解压进入目录

   修改 dubbo-admin\src\main\resources\application.properties 指定 zookeeper地址

   ```properties
   server.port=7001
   spring.velocity.cache=false
   spring.velocity.charset=UTF-8
   spring.velocity.layout-url=/templates/default.vm
   spring.messages.fallback-to-system-locale=false
   spring.messages.basename=i18n/message
   spring.root.password=root
   spring.guest.password=guest
   # 注册中心的地址
   dubbo.registry.address=zookeeper://127.0.0.1:2181
   ```

3. 在项目目录下打包dubbo-admin

   ```shell
   mvn clean package -Dmaven.test.skip=true
   ```

   ![](http://zhaocan.fym233.cn/e241rwjlfc)

4. 执行 dubbo-admin\target 下的 dubbo-admin-0.0.1-SNAPSHOT.jar

   ```shell
   java -jar dubbo-admin-0.0.1-SNAPSHOT.jar
   ```

总结：

- zookeeper：注册中心
- dubbo-admin：是一个监控管理后台，查看我们注册了哪些服务，哪些服务被消费了
- dubbo：jar包

## 第一个微服务架构项目

- zookeeper
- dubbo
- SpringBoot
- JDK
- Maven

**创建2个项目，分别为提供者与消费者**

提供者：provider-services

1. 导入相关依赖

   ```xml
   <!-- Dubbo + zookeeper -->
   <!-- https://mvnrepository.com/artifact/org.apache.dubbo/dubbo-spring-boot-starter -->
   <dependency>
       <groupId>org.apache.dubbo</groupId>
       <artifactId>dubbo-spring-boot-starter</artifactId>
       <version>2.7.3</version>
   </dependency>
   
   <!-- zkClient -->
   <!-- https://mvnrepository.com/artifact/com.101tec/zkclient -->
   <dependency>
       <groupId>com.101tec</groupId>
       <artifactId>zkclient</artifactId>
       <version>0.11</version>
   </dependency>
   
   <!-- 日志会冲突 -->
   <!-- 引入zookeeper -->
   <!-- https://mvnrepository.com/artifact/org.apache.curator/curator-framework -->
   <dependency>
       <groupId>org.apache.curator</groupId>
       <artifactId>curator-framework</artifactId>
       <version>2.12.0</version>
   </dependency>
   <!-- https://mvnrepository.com/artifact/org.apache.curator/curator-recipes -->
   <dependency>
       <groupId>org.apache.curator</groupId>
       <artifactId>curator-recipes</artifactId>
       <version>2.12.0</version>
   </dependency>
   
   <dependency>
       <groupId>org.apache.zookeeper</groupId>
       <artifactId>zookeeper</artifactId>
       <version>3.4.14</version>
       <!-- 排除这个slf4j-log4j12-->
       <exclusions>
           <exclusion>
               <groupId>org.slf4j</groupId>
               <artifactId>slf4j-log4j12</artifactId>
           </exclusion>
       </exclusions>
   </dependency>
   ```

2. 编写业务相关的Service层

   com.zc.service.TicketService

   ```java
   package com.zc.service;
   
   public interface TicketService {
   
       public String getTicket();
   
   }
   ```

   com.zc.service.TicketServiceImpl

   ```java
   package com.zc.service;
   
   import org.apache.dubbo.config.annotation.Service;
   import org.springframework.stereotype.Component;
   
   @Service    //可以被扫描到，在项目一启动就注册到注册中心  dubbo下的@Service
   @Component  //使用了Dubbo后尽量不要用@Service
   public class TicketServiceImpl implements TicketService{
   
       @Override
       public String getTicket() {
           return "学习微服务";
       }
   }
   ```

   注意点：

   1. @Service是Dubbo下的@Service，用于项目启动时注册到注册中心
   2. 尽量不要用Spring下的@Service，使用原生的@Component

3. 编写application.yml配置文件

   ```yaml
   server:
     port: 8001
   # 服务应用名字
   dubbo:
     application:
       name: provider-servers
   # 注册中心地址
     registry:
       address: zookeeper://127.0.0.1:2181
   # 哪些服务要被注册
     scan:
       base-packages: com.zc.service
   ```

4. 测试结果

   通过官方文档提供的dubbo-admin来测试

   ```shell
   java -jar dubbo-admin-0.0.1-SNAPSHOT.jar
   ```

   ![](http://zhaocan.fym233.cn/yowrwbnj38)

消费者：consumer-servers

1. 引入依赖

   ```xml
   <!-- Dubbo + zookeeper -->
   <!-- https://mvnrepository.com/artifact/org.apache.dubbo/dubbo-spring-boot-starter -->
   <dependency>
       <groupId>org.apache.dubbo</groupId>
       <artifactId>dubbo-spring-boot-starter</artifactId>
       <version>2.7.3</version>
   </dependency>
   
   <!-- zkClient -->
   <!-- https://mvnrepository.com/artifact/com.101tec/zkclient -->
   <dependency>
       <groupId>com.101tec</groupId>
       <artifactId>zkclient</artifactId>
       <version>0.11</version>
   </dependency>
   
   <!-- 日志会冲突 -->
   <!-- 引入zookeeper -->
   <!-- https://mvnrepository.com/artifact/org.apache.curator/curator-framework -->
   <dependency>
       <groupId>org.apache.curator</groupId>
       <artifactId>curator-framework</artifactId>
       <version>2.12.0</version>
   </dependency>
   <!-- https://mvnrepository.com/artifact/org.apache.curator/curator-recipes -->
   <dependency>
       <groupId>org.apache.curator</groupId>
       <artifactId>curator-recipes</artifactId>
       <version>2.12.0</version>
   </dependency>
   
   <dependency>
       <groupId>org.apache.zookeeper</groupId>
       <artifactId>zookeeper</artifactId>
       <version>3.4.14</version>
       <!-- 排除这个slf4j-log4j12-->
       <exclusions>
           <exclusion>
               <groupId>org.slf4j</groupId>
               <artifactId>slf4j-log4j12</artifactId>
           </exclusion>
       </exclusions>
   </dependency>
   ```

2. 编写业务相关的Service层

   com.zc.UserService

   ```java
   package com.zc.service;
   
   public interface UserService {
   
       public void buyTicket();
   }
   ```

   com.zc.UserServiceImpl

   ```java
   package com.zc.service;
   
   import org.apache.dubbo.config.annotation.Reference;
   import org.springframework.stereotype.Service;
   
   @Service    //Spring的@Service，放到容器中
   public class UserServiceImpl implements UserService{
   
       //拿到provider-servers提供的票，要去注册中心拿到服务
       //引用：
       //1.Pom坐标，可以定义路径相同的接口名
       @Reference
       TicketService ticketService;
   
       public void buyTicket() {
           String ticket = ticketService.getTicket();
           System.out.println("在注册中心拿到=>"+ticket);
       }
   
   }
   ```

   com.zc.TicketService

   ```java
   package com.zc.service;
   
   public interface TicketService {
   
       public String getTicket();
   
   }
   ```

   **注意：**

   1. @Service是Spring中的@Service，将该类放入到容器中
   2. @Reference是从注册中心中拿到该类型的实体注入，而不是使用@Autowired
   3. 想要使用提供者提供服务的方法，需要在同样的路径下建立一个同样的接口

3. 编写application.yml配置文件

   ```yaml
   server:
     port: 8002
   # 消费者去哪里拿服务需要暴露自己的名字
   dubbo:
     application:
       name: consumer-servers
   # 注册中心的地址，可以在任何电脑上
     registry:
       address: zookeeper://127.0.0.1:2181
   ```

4. 测试结果

   ![](http://zhaocan.fym233.cn/y4py5t0luq)

   ![](http://zhaocan.fym233.cn/fr5e25kvcg)

步骤分析：

**前提：zookeeper服务已开启！！！**

1. 提供者提供服务
   1. 导入依赖
   2. 配置注册中心的地址，以及服务发现名，和要扫描的包
   3. 在想要被注册的服务上面，增加一个注解`@Service`（Dubbo的）
2. 消费者如何消费
   1. 导入依赖
   2. 配置注册中心地址，配置自己的服务名
   3. 从远程注入服务