## 1、Spring

### 1.1、简介

- 2002年，首次推出了Spring框架的雏形：interface21框架
- Spring框架即以interface21框架为基础，经过重新设计，并不断丰富其内涵，于2004年3月24日，发布了1.0正式版
- **Rod Johnson**，Spring Framework创始人，著名作者。很难想象Rod Johnson 的学历，真的让很多人大吃一惊，他是悉尼大学的博士，然而他的专业不是计算机，而是音乐学。
- Spring理念：使现有的技术更加容易使用，本身是一个大杂烩，整合了现有的技术框架
- SSH：Strurs2 + Spring + Hibernate
- SSM：SpringMVC + Spring + Mybatis

官网地址：[https://spring.io/projects/spring-framework#overview](https://spring.io/projects/spring-framework#overview)

官方下载地址：[http://repo.spring.io/release/org/springframework/spring](http://repo.spring.io/release/org/springframework/spring)

GitHub：[https://github.com/spring-projects/spring-framework](https://github.com/spring-projects/spring-framework)

Maven：

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
	<groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.0.RELEASE</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
	<groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.0.RELEASE</version>
</dependency>
```

### 1.2、优点

- Spring是一个开源的免费的框架（容器）
- Spring是一个轻量级的、非入侵式的框架
- 控制反转（IOC），面向切面编程（AOP）
- 支持事务的处理，对框架整合的支持

总结：Spring就是一个轻量级的控制反转（IOC）和面向切面编程（AOP）的框架

### 1.3、组成

![](https://img2018.cnblogs.com/blog/1010726/201909/1010726-20190908042152777-1895820426.png)

- Spring Core：核心容器
- Spring AOP：AOP模块
- Spring ORM：对象/关系映射集成模块
- Spring DAO：JDBC抽象和DAO模块
- Spring Web：Spring的Web模块
- Spring Context：应用上下文（Context）模块
- Spring MVC：Spring的MVC框架

### 1.4、拓展

在Spring的官网有这个介绍：现代化的Java开发！说白了就是基于Spring的开发！

![](https://i.loli.net/2021/02/09/Kpw2nrFWvIeCTdg.png)

- Spring Boot
  - 一个快速开发的脚手架
  - 基于SpringBoot可以快速的开发单个微服务
  - 约定大于配置
- Spring Cloud
  - SpringCloud是基于SpringBoot实现的

因为现在大多数公司都在使用SpringBoot进行快速开发，学习SpringBoot的前提，需要完全掌握Spring及SpringMVC



**弊端：发展了太久之后，违背了原来的理念。配置十分繁琐，人称：“配置地狱”**

## 2、IOC理论推导

1. UserDao 接口
2. UserDaoImpl 实现类
3. UserService 业务接口
4. UserServiceImpl 业务实现类

在我们之前的业务中，用户的需求可能会影响我们原来的代码，我们需要根据用户的需求去修改源码！如果程序代码量十分大，修改一次的成本代价是十分昂贵的

我们使用一个Set接口实现，已经发生了革命性的变化

```java
private UserDao userDao;

//  利用set进行动态实现值的注入
public void setUserDao(UserDao userDao){
    this.userDao = userDao;
}
```

- 之前，程序是主动创建对象！控制权在程序员手上
- 使用了set注入后，程序不再具有主动性，而是变成了被动的接受对象

这种思想，从本质上解决了问题，我们程序员不用再去管理对象的创建了。系统的耦合性大大降低，可以更加专注的在业务的实现上！这是IOC的原型！

### IOC本质

**控制反转Ioc（Inversion of Control），是一种设计思想，DI（依赖注入）是实现IoC的一种方法**，也有人认为DI只是IoC的另一种说法。没有IoC的程序中，我们使用面向对象编程，对象的创建于对象间的依赖关系完全硬编码在程序中，对象的创建由程序自己控制，控制反转后将对象的创建转移给第三方，个人认为所谓控制反转就是：**获得依赖对象的方式反转了**。

采用xml方式配置Bean的时候，Bean的定义信息是和实现分离的，而采用注解的方式可以把两者合为一体，Bean的定义信息直接以注解的形式定义在实现类中，从而达到了零配置的目的。

**控制反转是一种通过描述（xml或注解）并通过第三方去生产或获取特定对象的方式，在Spring中实现控制反转的是IoC容器，其实现方法是依赖注入（Dependency Injection,DI）。**	

## 3、Hello Spring

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- 使用Spring来创建对象，在Spring这些都称为Bean

    类型 变量名 = new 类型();
    Hello hello = new Hello();

    id = 变量名
    class = new 的对象;
    property 相当于给对象中的属性设置一个值


    -->
    <bean id="hello" class="com.zc.pojo.Hello">
        <property name="name" value="Spring" />
    </bean>
</beans>
```

```java
public static void main(String[] args) {
    //  获取Spring的上下文对象
    ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");
    //  我们的对象现在都在Spring中的管理了，我们要使用，直接去里面取出来就好了
    Hello hello =(Hello) context.getBean("hello");
    System.out.println(hello.toString());
}
```

### 思考问题

- Hello对象是谁创建的？

  hello对象是由Spring创建的

- Hello对象的属性是怎么设置的？

  hello对象的属性是由Spring容器设置的

控制：谁来控制对象的创建，传统应用程序的对象是由程序本身控制创建的，使用Spring后，对象是由Spring来创建的。

反转：程序本身不创建对象，而变成被动的接收对象

依赖注入：就是利用set方法来进行注入的

IOC是一种编程思想，由主动的编程编程被动的接收

可以通过 `newClassPathXmlApplicationContext`去浏览一下底层源码

**OK，到了现在，我们彻底不用在程序中改动了，要实现不同的操作，只需要在xml配置文件中进行修改，所谓的IoC，一句话搞定：对象由Spring来创建，管理，装配！**

## 4、IOC创建对象的方式

1. 使用无参构造创建对象，默认！

2. 假设我们要使用有残构造创建对象。

   1. 下标赋值

      ```xml
      <!-- 第一种，下标赋值 -->
      <bean id="user" class="com.zc.pojo.user">
      	<constructor-arg index="0" value="tom" />
      </bean>
      ```

   2. 类型

      ```xml
      <!-- 第二种，通过类型创建，不建议使用 -->
      <bean id="user" class="com.zc.pojo.user">
      	<constructor-arg type="java.lang.String" value="tom" />
      </bean>
      ```

   3. 参数名

      ```xml
      <!-- 第三种，直接通过参数名来设置 -->
      <bean id="user" class="com.zc.pojo.user">
      	<constructor-arg name="name" value="tom" />
      </bean>
      ```

   总结：在配置文件加载的时候，容器中管理的对象就已经初始化了！

## 5、Spring配置

### 5.1、别名

```xml
<!-- 别名，如果添加了别名，我们也可以使用别名获取到这个对象 -->
<alias name="user" alias="userNew" />
```

### 5.2、Bean的配置

```xml
<!--
    id： bean 的唯一标识符，也就是相当于我们学的对象名
    class： bean 对象所对应的权限定名： 包名 + 类名
    name： 也是别名，而且name 可以同时取多个别名
    -->
    <bean id="userT" class="com.zc.pojo.User" name="userTT">
        <property name="name" value="aaa" />
    </bean>
```

### 5.3、import

一般用于团队开发使用，他可以将多个配置文件，导入合并为一个

假设，现在项目中有多个人开发，他们负责不同类的开发，不同的类需要注册在不同的Bean中，我们可以利用 import 将所有人的beans.xml合并为一个

使用的时候，直接使用合并后总的配置就可以了

## 6、依赖注入

### 6.1、构造器注入

### 6.2、Set方式注入【重点】

- 依赖注入：Set注入
  - 依赖：bean对象的创建依赖于容器
  - 注入：bean对象中的所有属性，由容器来注入

【环境搭建】

1. 复杂类型

   ```java
   @Data
   public class Address {
       private String address;
   }
   ```

2. 真实测试对象

   ```java
   public class Student {
   
       private String name;
       private Address address;
       private String[] books;
       private List<String> hobbys;
       private Map<String,String> card;
       private Set<String> games;
       private String wife;
       private Properties info;
   }
   ```

3. beans.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <bean id="student" class="com.zc.pojo.Student">
           <property name="name" value="张三" />
       </bean>
   
   </beans>
   ```

4. 测试类

   ```java
   public static void main(String[] args) {
       ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
       Student student =(Student) context.getBean("student");
       System.out.println(student.getName());
   }
   ```

完善注入信息

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="address" class="com.zc.pojo.Address" >
        <property name="address" value="吉林" />
    </bean>

    <bean id="student" class="com.zc.pojo.Student">
        <!-- 第一种，普通值注入 value -->
        <property name="name" value="张三" />
        <!-- 第二种，Bean注入 ref -->
        <property name="address" ref="address" />

        <!-- 数组注入 ref -->
        <property name="books">
            <array>
                <value>Java</value>
                <value>Spring</value>
                <value>Mybatis</value>
            </array>
        </property>

        <!-- List -->
        <property name="hobbys">
            <list>
                <value>唱</value>
                <value>跳</value>
                <value>rap</value>
                <value>篮球</value>
            </list>
        </property>

        <!-- Map -->
        <property name="card">
            <map>
                <entry key="身份证" value="11111222223333344" />
                <entry key="银行卡" value="789456123321654987" />
            </map>
        </property>

        <!-- Set -->
        <property name="games">
            <set>
                <value>英雄联盟</value>
                <value>地下城与勇士</value>
                <value>穿越火线</value>
            </set>
        </property>

        <!-- null -->
        <property name="wife">
            <null />
        </property>

        <!-- Properties -->
        <property name="info">
            <props>
                <prop key="学号">20210209</prop>
                <prop key="性别">男</prop>
            </props>
        </property>
    </bean>

</beans>
```



### 6.3、拓展方式注入

我们可以使用 p命令空间 和 c命令空间 进行注入

![](https://i.loli.net/2021/02/09/dtpn9lHNUVB6QRk.png)

使用

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <!-- p命名空间注入，可以直接注入属性的值：property -->
    <bean id="user" class="com.zc.pojo.User" p:name="张三" p:age="18" />
    
    <!-- c命名空间注入，通过构造器注入：construct-args -->
    <bean id="user2" class="com.zc.pojo.User" c:age="18" c:name="李四" />
</beans>
```

测试

```java
@Test
public void test() {
    ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
    User user = context.getBean("user2", User.class);
    System.out.println(user);
}
```

注意点：p命名和c命名空间不能直接使用，需要导入xml约束

```xml
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"
```

### 6.4、Bean的作用域

![](https://i.loli.net/2021/02/09/mfrpGkIRj2KDZMB.png)

1. 单例模式（Spring默认机制）

   ```xml
   <bean id="user2" class="com.zc.pojo.User" c:age="18" c:name="李四" scope="singleton"/>
   ```

2. 原型模式：每次从容器中get的时候都会产生一个新的对象

   ```xml
   <bean id="user2" class="com.zc.pojo.User" c:age="18" c:name="李四" scope="prototype"/>
   ```

3. 其余的 request、session、application，这些只能在 web 开发中使用

## 7、Bean的自动装配

- 自动装配是Spring满足Bean依赖的一种方式
- Spring会在上下文中自动寻找，并自动给Bean装配属性

在Spring中有三种装配的方式

1. 在xml中显示的配置
2. 在java中显示配置
3. 隐式的自动装配

### 7.1、自动装配

1. 环境搭建
   1. 一个人有两个宠物

### 7.2、ByName自动装配

```xml
<!--
    byName：会自动在容器上下文中查找，和自己对象set方法后面的值对应的beanid
    -->
<bean id="people" class="com.zc.pojo.People" autowire="byName">
    <property name="name" value="张三" />
</bean>
```

### 7.3、ByType自动装配

```xml
<!--
    byType：会自动在容器上下文中查找，和自己对象属性类型相同的Bean
    -->
<bean id="people" class="com.zc.pojo.People" autowire="byType">
    <property name="name" value="张三" />
</bean>
```

小结：

- byName的时候，需要保证所有bean的id唯一，且这个bean需要和自动注入的属性的set方法的值一致
- byType的时候，需要保证所有bean的class唯一，且这个bean需要和自动注入的属性的类型一致

### 7.4、使用注解实现自动装配

jdk1.5支持的注解，Spring2.5支持的注解

The introduction of annotation-based configuration raised the question of whether this approach is "better" than XML.

要使用注解须知：

1. 导入约束：context约束

2. 配置注解的支持：`<context:annotation-config/>`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/context
                              https://www.springframework.org/schema/context/spring-context.xsd">
   
       <context:annotation-config/>
   
   </beans>
   ```

**@Autowired**

直接在属性上使用即可！也可以在set方式上使用

使用@Autowired 我们可以不用编写set方法了，前提是你这个自动装配的属性在IOC（Spring）容器中存在且符合名字byName

科普：

```java
@Nullable	//	字段标记了这个注解，说明这个字段可以为null
```

```java
public @interface Autowired{
    boolean required() default true;
}
```



测试代码

```java
@Data
public class People {

    //	如果显示定义了 @Autowired 的 required 属性为false，说明这个对象可以为null，否则不允许为空
    @Autowired(required = false)
    private Cat cat;
    @Autowired
    private Dog dog;
    private String name;
}
```

如果 @Autowired 自动装配的环境比较复杂，自动装配无法通过一个注解【@Autowired】完成的时候，我们可以使用 @Qualifier(value="xxx")去配置 @Autowired 的使用，指定一个唯一的bean对象注入

```java
@Data
public class People {
    @Autowired
    @Qualifier(value = "cat111")
    private Cat cat;
    @Autowired
    @Qualifier(value = "dog222")
    private Dog dog;
    private String name;
}
```

**@Resource注解**

```java
@Data
public class People {
    
    @Resource(name = "cat111")
    private Cat cat;
   	
    @Resource
    private Dog dog;
}
```

小结：

**@Resource 和 @Autowired 的区别**

- 都是用来自动装配的，都可以放在属性字段上
- @Autowired 通过byType的方式实现，而且必须要求这个对象存在！【常用】
- @Resource 默认通过byName的方式实现，如果找不到名字，则通过byType实现！如果两个都找不到的情况下，就会报错【常用】
- 执行顺序不同：@Autowired 通过byType的方式实现，@Resource 默认通过byName的方式实现

## 8、使用注解开发

在Spring4之后，要使用注解开发，必须要保证 aop 的包导入了

![](https://i.loli.net/2021/02/09/v8gQdaKGWo7UzEt.png)

使用注解需要导入 context 约束，增加注解的支持

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

</beans>
```

1. bean

   

2. 属性如何注入

   ```java
   //  等价于<bean id="user" class="com.zc.pojo.User"/>
   //  @Component 组件
   @Component
   @Data
   public class User {
   
       public String name;
   
       //  相当于<property name="name" value="张三" />
       @Value("张三")
       public void setName(String name) {
           this.name = name;
       }
   }
   ```

3. 衍生的注解

   @Component 有几个衍生注解，我们在web开发中，会按照mvc三层架构分层

   - dao 【@Repository】

   - service 【@Service】 

   - controller 【@Controller】

     这四个注解功能都是一样的，都是代表将某个类注册到Spring中，装配Bean

4. 自动装配

   - @Autowired：自动装配通过类型。名字

     ​	如果Autowired不能唯一自动装配上属性，则需要通过@Qualifier(value = "xxx")

   - @Nullable：字段标记了这个注解，说明这个字段可以为null

   - @Resource：自动装配通过名字。类型

5. 作用域

   ```java
   @Component
   //	singleton：单例模式
   //	prototype：原型模式
   @Scope("prototype")
   public class User {
   
       public String name;
   
       //  相当于<property name="name" value="张三" />
       @Value("张三")
       public void setName(String name) {
           this.name = name;
       }
   }
   ```

6. 小结

   xml与注解：

   - xml更加万能，适用于任何场合！维护简单方便
   - 注解 不是自己的类使用不了，维护相对复杂

   xml与注解最佳实践：

   - xml用来管理bean

   - 注解只负责完成属性的注入

   - 我们在使用的过程中，只需要注意一个问题：必须让注解生效，就需要开启注解的支持

     ```xml
     <!-- 指定要扫描的包，这个包下的注解就会生效 -->
     <context:component-scan base-package="com.zc.pojo" />
     <context:annotation-config/>
     ```

## 9、使用Java的方式配置Spring

我现在要完全不使用Spring的xml配置了，全权交给Java来做！

JavaConfig是Spring的一个子项目，在Spring4之后，他成为了一个核心功能

![](https://i.loli.net/2021/02/09/mBDCHJ8qcvlI72R.png)

实体类

```java
@Data
//  这里这个注解的意思，就是说明这个类被Spring接管了，注册到了容器中
@Component
public class User {

    @Value("张三")
    private String name;
}
```

配置文件

```java
//  这个也会被Spring容器托管，注册到容器中，因为他本来就是一个@Component。
//  @Component代表这是一个配置类，就和我们之前看的beans.xml是一样的
@Configuration
@ComponentScan("com.zc.pojo")
@Import(MyConfig2.class)
public class MyConfig {

    //  注册一个bean，就相当于我们之前写的一个bean标签，
    //  这个方法的名字就相当于bean标签中的id属性
    //  这个方法的返回值，就相当于bean标签中的class属性
    @Bean
    public User getUser() {
        return new User();  //就是返回要注入到bean的对象
    }
}
```

测试类

```java
public class MyTest {

    public static void main(String[] args) {
        //  如果完全使用了配置类方式去做，我们就只能通过AnnotationConfig 上下文来获取容器，通过配置类的class对象加载
        ApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);
        User user = context.getBean("getUser", User.class);
        System.out.println(user.getName());
    }
}
```

这种纯Java的配置方式，在SpringBoot中随处可见

## 10、代理模式

**为什么要学习代理模式？**

因为这就是SpringAOP的底层

代理模式的分类：

- 静态代理
- 动态代理

### 10.1、静态代理

角色分析

- 抽象角色：一般会使用接口或抽象类来解决
- 真实角色：被代理的角色
- 代理角色：代理真实角色，代理真实角色后，我们一般会做一些附属操作
- 客户：访问代理对象的人

代码步骤：

1. 接口

   ```java
   //  租房
   public interface Rent {
   
       public void rent();
   }
   ```

2. 真实角色

   ```java
   package com.zc.demo01;
   
   public class Host implements Rent {
       public void rent() {
           System.out.println("房东要出租房子");
       }
   }
   ```

3. 代理角色

   ```java
   @Data
   @AllArgsConstructor
   @NoArgsConstructor
   public class Proxy implements Rent{
   
       private Host host;
   
       public void rent() {
           seeHouse();
           host.rent();
           hetong();
           fare();
       }
   
       //  看房
       public void seeHouse() {
           System.out.println("中介带你看房");
       }
   
       //  收中介费
       public void fare() {
           System.out.println("收中介费");
       }
   
       //  签租赁合同
       public void hetong() {
           System.out.println("签租赁合同");
       }
   }
   ```

4. 客户端访问代理角色

   ```java
   public class Client {
       public static void main(String[] args) {
           Host host = new Host();
           //  代理，中介帮房东租房子。但是代理角色一般会有一些附属操作
           Proxy proxy = new Proxy(host);
   
           //  不用面对房东，直接在中介租房即可
           proxy.rent();
       }
   }
   ```

代理模式好处：

- 可以使真实角色的操作更加纯粹！不用去关注一些公共的业务
- 公共业务也就交给了代理角色！实现了业务的分工
- 公共业务发生扩展的时候，方便集中管理

缺点：

- 一个真实角色就会产生一个代理角色；代码量会翻倍，开发效率会变低

### 10.2 、加深理解

1. 接口

   ```java
   public interface UserService {
       public void add();
       public void delete();
       public void update();
       public void query();
   }
   ```

2. 真实角色

   ```java
   public class UserServiceImpl implements UserService {
       public void add() {
           System.out.println("添加了一个用户");
       }
   
       public void delete() {
           System.out.println("删除了一个用户");
       }
   
       public void update() {
           System.out.println("修改了一个用户");
       }
   
       public void query() {
           System.out.println("查询了一些用户");
       }
   }
   ```

3. 代理角色

   ```java
   @Data
   public class UserServiceProxy implements UserService {
   
       UserServiceImpl userService;
   
       public void add() {
           log("add");
           userService.add();
       }
   
       public void delete() {
           log("delete");
           userService.delete();
       }
   
       public void update() {
           log("update");
           userService.update();
       }
   
       public void query() {
           log("query");
           userService.query();
       }
   
       //  日志方法
       public void log(String message) {
           System.out.println("[DeBug]使用了" + message + "方法");
       }
   }
   ```

4. 客户端访问代理角色

   ```java
   public class Client {
       public static void main(String[] args) {
           UserServiceImpl userService = new UserServiceImpl();
   
           UserServiceProxy userServiceProxy = new UserServiceProxy();
           userServiceProxy.setUserService(userService);
   
           userServiceProxy.add();
       }
   }
   ```

![](https://i.loli.net/2021/02/09/FWsYV56CBOHontb.png)

### 10.3、动态代理

- 动态代理和静态代理角色一样

- 动态代理的代理类是动态生成的，不是我们直接写好的

- 动态代理分为两大类：基于接口的动态代理，基于类的动态代理

  - 基于接口：JDK 动态代理

  - 基于类：cglib
  - java字节码实现：javasist

需要了解两个类：Proxy：代理，InvocationHandler：调用处理程序

动态代理的好处：

- 可以使真实角色的操作更加纯粹！不用去关注一些公共的业务
- 公共业务也就交给了代理角色！实现了业务的分工
- 公共业务发生扩展的时候，方便集中管理
- 一个动态代理类代理的是一个接口，一般就是对应的一类业务
- 一个动态代理类可以代理多个类，只要是实现了同一个接口即可

```java
package com.zc.demo03;

import lombok.Data;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

@Data
//  我们会用这个类自动生成代理类
public class ProxyInvocationHandler implements InvocationHandler {

    //  被代理的接口
    private Object target;

    public void setTarget(Object target) {
        this.target = target;
    }

    //  生成得到代理对象
    public Object getProxy() {
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),target.getClass().getInterfaces(),this);
    }

    //  处理代理实例，并返回结果
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

        log(method.getName());
        //  动态代理的本质就是使用反射机制实现！
        Object invoke = method.invoke(target, args);
        return invoke;
    }

    //  增加打印日志功能
    public void log(String message) {
        System.out.println("[DeBug]执行了" + message + "方法");
    }
}
```

## 11、AOP

### 11.1、什么是AOP

AOP(Aspect Oriented Programming) 意味：面向切面编程，通过预编译方式和运行期动态代理实现程序功能的统一维护维护的一种技术。AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范性。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

![](https://i.loli.net/2021/02/09/WHbr1UEqPueYIKR.png)

### 11.2、AOP在Spring中的作用

提供声明式事务；允许用户自定义切面

- 横切关注点：跨越应用程序多个模块的方法或功能。即是，与我们业务逻辑无关的，但是我们需要关注的部分，就是横切关注点。如日志，安全，缓存，事务等等
- 切面（ASPECT）：横切关注点 被模块化 的特殊对象。即，它是一个类
- 通知（Advice）：切面必须要完成的工作。即，它是类中的一个方法
- 目标（Target）：被通知对象
- 代理（Proxy）：向目标对象应用通知之后创建的对象
- 切入点（PointCut）：切面通知 执行的“地点”的定义
- 连接点（JointPoint）：与切入点匹配的执行点

![](https://i.loli.net/2021/02/09/e8EKVAHgYJmizPj.png)

SpringAOP中，通过Advice定义横切逻辑，Spring中支持5种类型的Advice：

![](https://i.loli.net/2021/02/09/q2CTp9Ib7DkGrhl.png)

即AOP在不改变原有代码的情况下，去增加新的功能

### 11.3、使用Spring实现AOP

【重点】使用AOP植入，需要导入一个依赖包

```xml
<!-- AOP -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.4</version>
</dependency>
```

**方式一：使用Spring的API接口【主要是Spring API接口实现】**

1. 接口

   ```java
   public class UserServiceImpl implements UserService {
       public void add() {
           System.out.println("增加了一个用户");
       }
   
       public void delete() {
           System.out.println("删除了一个用户");
       }
   
       public void update() {
           System.out.println("修改了一个用户");
       }
   
       public void query() {
           System.out.println("查询了一个用户");
       }
   }
   ```

2. 实现类

   ```java
   public interface UserService {
       public void add();
       public void delete();
       public void update();
       public void query();
   }
   ```

3. 日志文件1

   ```java
   public class Log implements MethodBeforeAdvice {
   
       //method：要执行的目标对象的方法
       //object：参数
       //target：目标对象
       public void before(Method method, Object[] objects, Object target) throws Throwable {
           System.out.println(target.getClass().getName() + "的" + method.getName() + "被执行了");
       }
   }
   ```

4. 日志文件2

   ```java
   public class AfterLog implements AfterReturningAdvice {
   
       //returnValue：返回值
       public void afterReturning(Object returnValue, Method method, Object[] objects, Object o1) throws Throwable {
           System.out.println("执行了" + method.getName() + "返回结果为：" + returnValue);
       }
   }
   ```

5. applicationContext.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/aop
                              https://www.springframework.org/schema/aop/spring-aop.xsd">
   
       <!-- 注册bean -->
       <bean id="userService" class="com.zc.service.UserServiceImpl" />
       <bean id="log" class="com.zc.log.Log" />
       <bean id="afterLog" class="com.zc.log.AfterLog" />
   
       <!-- 方式一：使用原声Spring API接口 -->
       <!-- 配置AOP：需要导入AOP的约束 -->
       <aop:config>
           <!-- 切入点：expression：表达式，execution(要执行的位置！* * * * *) -->
           <aop:pointcut id="pointcut" expression="execution(* com.zc.service.UserServiceImpl.*(..))" />
   
           <!-- 执行环绕增加！-->
           <aop:advisor advice-ref="log" pointcut-ref="pointcut" />
           <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut" />
       </aop:config>
   
   
   </beans>
   ```

6. 测试类

   ```java
   public static void main(String[] args) {
       ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
       //  动态代理，代理的是接口
       UserService userService = context.getBean("userService", UserService.class);
   
       userService.add();
   }
   ```

注意点：由于在xml中注册的是接口类型的bean，在测试类中通过`getBean`方法获得的实例必须是接口类型

**方式二：自定义来实现AOP【主要是切面定义】**

1. 接口

   ```java
   public interface UserService {
       public void add();
       public void delete();
       public void update();
       public void query();
   }
   ```

2. 实现类

   ```java
   public class UserServiceImpl implements UserService {
       public void add() {
           System.out.println("增加了一个用户");
       }
   
       public void delete() {
           System.out.println("删除了一个用户");
       }
   
       public void update() {
           System.out.println("修改了一个用户");
       }
   
       public void query() {
           System.out.println("查询了一个用户");
       }
   }
   ```

3. 日志文件

   ```java
   public class DiyPointCut {
   
       public void before() {
           System.out.println("方法执行前");
       }
   
       public void after() {
           System.out.println("方法执行后");
       }
   }
   ```

4. applicationContext.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/aop
                              https://www.springframework.org/schema/aop/spring-aop.xsd">
   
       <!-- 注册bean -->
       <bean id="userService" class="com.zc.service.UserServiceImpl" />
       <bean id="log" class="com.zc.log.Log" />
       <bean id="afterLog" class="com.zc.log.AfterLog" />
   
       <!-- 方式二：自定义类 -->
       <bean id="diy" class="com.zc.diy.DiyPointCut"/>
       <aop:config>
           <!-- 自定义切面，ref需要引用的类 -->
           <aop:aspect ref="diy">
               <!-- 切入点 -->
               <aop:pointcut id="point" expression="execution(* com.zc.service.UserServiceImpl.*(..))"/>
               <!-- 通知 -->
               <aop:before method="before" pointcut-ref="point" />
               <aop:after method="after" pointcut-ref="point" />
           </aop:aspect>
       </aop:config>
   
   
   </beans>
   ```

5. 测试类

```java
public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        //  动态代理，代理的是接口
        UserService userService = context.getBean("userService", UserService.class);

        userService.add();
    }
```

**方式三：使用注解**

1. 接口

   ```java
   public interface UserService {
       public void add();
       public void delete();
       public void update();
       public void query();
   }
   ```

2. 实现类

   ```java
   public class UserServiceImpl implements UserService {
       public void add() {
           System.out.println("增加了一个用户");
       }
   
       public void delete() {
           System.out.println("删除了一个用户");
       }
   
       public void update() {
           System.out.println("修改了一个用户");
       }
   
       public void query() {
           System.out.println("查询了一个用户");
       }
   }
   ```

3. 日志类

   ```java
   @Aspect //  标注这个类是一个切面
   public class AnnotationPointCut {
   
       @Before(value = "execution(* com.zc.service.UserServiceImpl.*(..))")
       public void before() {
           System.out.println("方法执行前");
       }
   
       @After(value = "execution(* com.zc.service.UserServiceImpl.*(..))")
       public void after() {
           System.out.println("方法执行后");
       }
   
       //  在环绕增强中，我们可以给定一个参数，代表我们要获取处理切入的点
       @Around(value = "execution(* com.zc.service.UserServiceImpl.*(..))")
       public void around(ProceedingJoinPoint point) throws Throwable {
           System.out.println("环绕前");
   
           Signature signature = point.getSignature();//获得签名
           System.out.println("signature = " + signature);
   
           //  执行方法
           Object proceed = point.proceed();
   
   
           System.out.println("环绕后");
       }
   }
   
   ```

4. applicationContext.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/aop
                              https://www.springframework.org/schema/aop/spring-aop.xsd">
   
       <!-- 注册bean -->
       <bean id="userService" class="com.zc.service.UserServiceImpl" />
       
       <bean id="annotationPointCut" class="com.zc.diy.AnnotationPointCut" />
       <aop:aspectj-autoproxy />
   
   </beans>
   ```

5. 测试类

   ```java
   public static void main(String[] args) {
       ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
       //  动态代理，代理的是接口
       UserService userService = context.getBean("userService", UserService.class);
   
       userService.add();
   }
   ```

## 12、整合Mybatis

步骤：

1. 导入相关jar包

   - junit
   - mybatis
   - mysql数据库
   - spring相关的
   - aop织入
   - mybatis-spring【new】

   ```xml
   <dependencies>
           <!-- junit -->
           <dependency>
               <groupId>junit</groupId>
               <artifactId>junit</artifactId>
               <version>4.12</version>
           </dependency>
           <!-- mysql -->
           <dependency>
               <groupId>mysql</groupId>
               <artifactId>mysql-connector-java</artifactId>
               <version>5.1.47</version>
           </dependency>
           <!-- mybatis -->
           <dependency>
               <groupId>org.mybatis</groupId>
               <artifactId>mybatis</artifactId>
               <version>3.5.2</version>
           </dependency>
           <!-- spring -->
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-webmvc</artifactId>
               <version>5.1.9.RELEASE</version>
           </dependency>
           <!-- Spring 操作数据库的话，还需要一个spring-jdbc -->
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-jdbc</artifactId>
               <version>5.1.9.RELEASE</version>
           </dependency>
           <!-- AOP -->
           <dependency>
               <groupId>org.aspectj</groupId>
               <artifactId>aspectjweaver</artifactId>
               <version>1.8.13</version>
           </dependency>
           <!-- spring整合mybatis -->
           <dependency>
               <groupId>org.mybatis</groupId>
               <artifactId>mybatis-spring</artifactId>
               <version>2.0.2</version>
           </dependency>
       </dependencies>
   ```

2. 编写配置文件

3. 测试

### 12.1、回忆Mybatis

1. 编写实体类

   ```java
   @Data
   public class User {
       private int id;
       private String name;
       private String password;
   }
   ```

2. 编写核心配置文件

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE configuration
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-config.dtd">
   <!-- 核心配置文件 -->
   <configuration>
   
       <typeAliases>
           <package name="com.zc.pojo"/>
       </typeAliases>
   
       <environments default="development">
           <environment id="development">
               <transactionManager type="JDBC"/>
               <dataSource type="POOLED">
                   <property name="driver" value="com.mysql.jdbc.Driver"/>
                   <property name="url" value="jdbc:mysql://47.98.47.51:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                   <property name="username" value="root"/>
                   <property name="password" value="root3306"/>
               </dataSource>
           </environment>
       </environments>
       <mappers>
           <mapper class="com.zc.mapper.UserMapper" />
       </mappers>
   </configuration>
   ```

3. 编写接口

   ```java
   public interface UserMapper {
       public List<User> selectUser();
   }
   ```

4. 编写Mapper.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.zc.mapper.UserMapper">
   
       <select id="selectUser" resultType="User">
           select * from mybatis.user
       </select>
   
   </mapper>
   ```

5. 测试

   ```java
   public class MyTest {
   
       @Test
       public void test() throws IOException {
           String reources = "mybatis-config.xml";
           InputStream inputStream = Resources.getResourceAsStream(reources);
   
           SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
           SqlSession sqlSession = sqlSessionFactory.openSession(true);
   
           UserMapper mapper = sqlSession.getMapper(UserMapper.class);
           List<User> userList = mapper.selectUser();
           for (User user : userList) {
               System.out.println(user);
           }
       }
   }
   ```

### 12.2、Mybatis-spring

| MyBatis-Spring | MyBatis | Spring框架 | Spring Batch |  Java  |
| :------------: | :-----: | :--------: | :----------: | :----: |
|      2.0       |  3.5+   |    5.0+    |     4.0+     | Java8+ |
|      1.3       |  3.4+   |   3.2.2+   |     2.1+     | Java6+ |

1. 编写数据源配置

   ```xml
   <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
       <property name="driverClassName" value="com.mysql.jdbc.Driver" />
       <property name="url" value="jdbc:mysql://47.98.47.51:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8" />
       <property name="username" value="root" />
       <property name="password" value="root3306" />
   </bean>
   ```

2. sqlSessionFactory

   ```xml
   <!-- sqlSessionFactory -->
   <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
       <property name="dataSource" ref="dataSource" />
       <!-- 绑定Mybatis配置文件 -->
       <property name="configLocation" value="classpath:mybatis-config.xml" />
       <property name="mapperLocations" value="classpath:com/zc/mapper/*.xml" />
   </bean>
   ```

3. sqlSessionTemplate

   ```xml
   <!-- SqlSessionTemplate：就是我们使用的sqlSession -->
   <bean id="SqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
       <!-- 只能使用构造器注入sqlSessionFactory，因为它没有set方法 -->
       <constructor-arg index="0" ref="sqlSessionFactory" />
   </bean>
   ```

4. 需要给接口加实现类

   ```java
   @Data
   public class UserMapperImpl implements UserMapper {
   
       //  在原来我们的所有操作都是用sqlSession来执行，现在都是用sqlSessionTemplate；
       private SqlSessionTemplate sqlSessionTemplate;
   
       public List<User> selectUser() {
           UserMapper mapper = sqlSessionTemplate.getMapper(UserMapper.class);
           return mapper.selectUser();
       }
   }
   ```

5. 将自己写的实现类注入到Spring中

   ```xml
   <bean id="userMapper" class="com.zc.mapper.UserMapperImpl">
           <property name="sqlSessionTemplate" ref="SqlSessionTemplate" />
       </bean>
   ```

   

   ```java
   @Data
   public class UserMapperImpl implements UserMapper {
   
       //  在原来我们的所有操作都是用sqlSession来执行，现在都是用sqlSessionTemplate；
       private SqlSessionTemplate sqlSessionTemplate;
   
       public List<User> selectUser() {
           UserMapper mapper = sqlSessionTemplate.getMapper(UserMapper.class);
           return mapper.selectUser();
       }
   }
   ```

6. 测试

```java
@Test
public void test() throws IOException {
    ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
    UserMapper userMapper = applicationContext.getBean("userMapper", UserMapper.class);
    List<User> userList = userMapper.selectUser();
    for (User user : userList) {
        System.out.println(user);
    }
}
```

整合xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop
                           https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- DataSource：使用Spring的数据源替换Mybatis的配置
    这里使用Spring提供的JDBC
    -->

    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver" />
        <property name="url" value="jdbc:mysql://47.98.47.51:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8" />
        <property name="username" value="root" />
        <property name="password" value="root3306" />
    </bean>

    <!-- sqlSessionFactory -->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <!-- 绑定Mybatis配置文件 -->
        <property name="configLocation" value="classpath:mybatis-config.xml" />
        <property name="mapperLocations" value="classpath:com/zc/mapper/*.xml" />
    </bean>

    <!-- SqlSessionTemplate：就是我们使用的sqlSession -->
    <bean id="SqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
        <!-- 只能使用构造器注入sqlSessionFactory，因为它没有set方法 -->
        <constructor-arg index="0" ref="sqlSessionFactory" />
    </bean>

    <bean id="userMapper" class="com.zc.mapper.UserMapperImpl">
        <property name="sqlSessionTemplate" ref="SqlSessionTemplate" />
    </bean>
</beans>
```

方式二：与方式一不同的是，实现类继承了`SqlSessionDaoSupport`，可以从父类直接获取到sqlSession对象，并进行使用

```java
public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper{
    public List<User> selectUser() {
        SqlSession sqlSession = getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        return userMapper.selectUser();
    }
}
```

在xml中也可省略对SqlSessionTemplate的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop
                           https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- DataSource：使用Spring的数据源替换Mybatis的配置
    这里使用Spring提供的JDBC
    -->

    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver" />
        <property name="url" value="jdbc:mysql://47.98.47.51:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8" />
        <property name="username" value="root" />
        <property name="password" value="root3306" />
    </bean>

    <!-- sqlSessionFactory -->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <!-- 绑定Mybatis配置文件 -->
        <property name="configLocation" value="classpath:mybatis-config.xml" />
        <property name="mapperLocations" value="classpath:com/zc/mapper/*.xml" />
    </bean>

    <bean id="userMapper2" class="com.zc.mapper.UserMapperImpl2">
        <property name="sqlSessionFactory" ref="sqlSessionFactory" />
    </bean>

</beans>
```

## 13、声明式事务

### 1、回顾事务

- 把一组业务当成一个业务来做；要么都成功，要么都失败
- 事务在项目开发中，十分的重要，涉及到数据的一致性问题
- 确保完整性和一致性

事务ACID原则：

- 原子性
- 一致性
- 隔离性
  - 多个业务可能操作同一个资源，防止数据损坏
- 持久性
  - 事务一旦提交，无论系统发生什么问题，结果都不会再被影响，被持久化的写到存储器中

### 2、Spring中的事务管理

- 声明式事务：AOP
- 编程式事务：需要在代码中，进行事务的管理

思考：

为什么需要事务？

- 如果不配置事务，可能存在数据提交不一致的情况
- 如果我们不在Spring中取配置声明式事务，我们就需要在代码中手动配置事务
- 事务在项目的开发中十分重要，涉及到数据的一致性和完整性问题

```xml
<!-- 配置声明式事务 -->


<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <constructor-arg ref="dataSource" />
</bean>

<!-- 结合AOP实现事务的织入 -->
<!-- 配置事务的类 -->
<tx:advice id="txAdvice" transaction-manager="transactionManager">
    <!-- 给哪些方法配置事务 -->
    <!-- 配置事务的传播特性：new -->
    <tx:attributes>
        <tx:method name="add" propagation="REQUIRED"/>
        <tx:method name="delete" propagation="REQUIRED"/>
        <tx:method name="update" propagation="REQUIRED"/>
        <tx:method name="query" propagation="REQUIRED"/>
        <tx:method name="*" propagation="REQUIRED"/>
    </tx:attributes>
</tx:advice>

<!-- 配置事务切入 -->
<aop:config>
    <aop:pointcut id="txPointCut" expression="execution(* com.zc.mapper.*.*(..))"/>
    <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
</aop:config>
```

