

## SpringBoot

### 什么是Spring

Spring是一个开源框架，2003年兴起的一个轻量级Java开发框架，作者：Rod Johnson。

**Spring是为了解决企业级应用开发的复杂性而创建的，简化开发。**

### Spring是如何简化Java开发的

为了降低Java开发的复杂性，Spring采用了以下4种关键策略：

1. 基于POJO的轻量级最小侵入性编程
2. 通过IOC，依赖注入（DI）和面向接口实现松耦合
3. 基于切面（AOP）和惯性进行声明式编程
4. 通过切面和模板减少样式代码

### 什么是SpringBoot

Springboot是一个 javaweb 的开发框架，和SpringMVC类似，对比其他 javaweb 框架的好处，官方说是简化开发，约定大于配置，you can "just run"，能迅速的开发 web 应用，几行代码开发一个 http 接口。

所有的技术框架的发展似乎都避循了一条主线规律:从一个复杂应用场象行生一种规范柜架们只需要进行各种配置而不需要自己去实现它，这时候强大的配置功能成了优点:发展到定程度之 后，人们根据实际生产应用情况，选取其中实用功能和设计精华，重购出一 些轻要 级的框架:之后为了提高开发效率，嫌弃原先的各类配置过于麻烦，于是开始提倡”约定大于配置”，进而行生出一些站式的解决方案。

是的这就是Java企业级应用->J2EE->spring-> springboot的过程。

随着Spring不断的发展，涉及的领域越来越多，项目整合开发需要配合各种各样的文件，保修变 得不那么易用简单，违背了最初的理念，甚至人称配置地狱。Spring Boot正是在这样的一个背景下被抽象出来的开发框架，目的为了让大家更容易的使用Spring、更容易的集成各种常用的中间件、开源软件

Spring Boot基于Spring 开发，Spirng Boot本身并不提供Spring框架的核心特性以及扩展功能，只是用于快速，敏捷地开发新，代基于Spring框架的应用程序。也就是说，它并不是用来替代Spring的解决方案，而是和Spring框架紧密结合用于提升Spring开发者体验的工赛。SpringBoot以约定大于配置的核心思想，默以替我有们进行了很多设置， 多数Spring Boot应带只需要很少的 Spring配置。同时它集成了大量常用的第三方库配器(例如Redis、MongoDB、Jpa、RabbitMQ. Quartz等等)。Spring Boot应用中这些第三方阵几乎可以零配置的开箱即用

简单来说就是SpringBoot其实不是什么新的框架，它默认配置了很多框架的使用方式，就像Maven整合了所有的jar包，SpringBoot整合了所有的框架

SpringBoot出生名门，从一开始就站在一个比较高的起点，又经过这几年的发展，生态足够完善，SpringBoot已经当之无愧称为Java领域最热门的技术

### SpringBoot的主要优点

- 为所有Spring开发者更快的入门
- **开箱即用**，提供各种默认配置来简化项目配置
- 内嵌式容器简化Web项目
- 没有冗余代码生成和XML配置的要求

## 微服务

### 什么是微服务

微服务是一种架构风格，它要求我们在开发一个应用的时候，这个应用必须构建成一系列小服务的组合；可以通过http的方式进行互通。要说微服务架构，先得说说过去我们的单体应用架构

### 单体应用架构

所谓单体应用架构（all in one）是指，我们将一个应用中的所有应用服务都封装在一个应用中。

无论是ERP、CRM或是其他什么系统，你都把数据库访问，web访问等等各个功能放到一个war包内。

- 这样做的好处是，易于开发和测试；也十分方便部署；当需要扩展时，只需要将war复制多份，然后放到多个服务器上，再做个负载均衡就可以了
- 单体应用架构的缺点是，哪怕我要修改一个非常小的地方，我都需要停掉整个服务，重新打包，部署这个应用war包。特别是对于一个大型应用，我们不可能把所有内容都放在一个应用里面，我们如何维护、如何分工合作都是问题

![](https://i.loli.net/2021/02/16/o4eFfhKmz8tiZWp.png)

### 微服务架构

all in one的架构方式，我们把所有的功能单元放在一个应用里面。然后我们把整个应用部署到服务器上。如果负载能力不行，我们将整个应用进行水平复制，进行扩展，然后在负载均衡。

所谓微服务架构，就是打破之前all in one 的架构方式，把每个功能元素单独出来。把单独出来的功能元素的动态组合，需要的功能元素才去拿来组合，需要多一些时可以整个多个功能元素。所以微服务架构是对功能元素进行复制，而没有对整个应用进行复制。

这样做的好处是：

1. 节省了调用资源
2. 每个功能元素的服务都是一个可替换的、可独立升级的软件代码

![](https://i.loli.net/2021/02/16/i51CJNqZgvEyMRG.png)

Martin Flower 于2014年3月25日写的《Microservices》，详细的阐述了什么是微服务。

- 原文地址：http://martinfowler.com/articles/microservices.html
- 翻译：https://www.cnblogs.com/liuning8023/p/4493156.html

### 如何构建微服务

一个大型系统的微服务架构，就像一个复杂交织的神经网络，每一个神经元都是一个功能元素，它们各自完成自己的功能，然后通过 http 相互请求调用。比如一个电商系统，查缓存、连数据库、浏览页面、结账、支付等服务都是一个个独立的功能服务，都被微化了，它们作为一个个微服务共同构建了一个庞大的系统。如果修改其中的一个功能，只需要更新升级其中一个功能服务单元即可。

但是这种庞大的系统架构给部署和运维带来很大的难度。于是，spring 为我们带来了构建大型分布式微服务的全套、全程产品：

- 构建一个个功能独立的微服务应用单元，可以使用springboot，可以帮我们快速构建一个应用
- 大型分布式网络服务的调用，这部分由spring cloud来完成，实现分布式
- 在分布式中间，进行流式数据计算、批处理、我们有spring cloud data flow
- spring为我们想清楚了整个从开始构建应用到大型分布式应用全流程方案

![](http://www.mooooc.com/assets/images/2017/chat/spring.png)

## 第一个SpringBoot程序

### 环境准备

- jdk1.8
- Maven 3.6.1
- SpringBoot最新版本
- IDEA

**官方提供了一个快速生成的网站**

- 可以在官网直接下载后，导入IDEA开发
- 直接使用IDEA创建一个springboot项目（一般开发直接在IDEA中创建）

### 创建基础项目

Spring官方提供了非常方便的工具

Spring Initializr：https://start.spring.io/ 来帮助我们创建SpringBoot应用

**【目标一：使用Spring Initializr页面创建项目】**

步骤：

1. 打开 https://start.spring.io/

2. 填写项目信息

3. 点击 “Generate Project” 按钮生成项目，下载此项目

   ![](https://i.loli.net/2021/02/16/346f9yTVnMQkgaE.png)

4. 解压项目包，并用编译器以Maven项目导入，以IntelliJ IDEA为例

5. 导入这个Maven项目，一路下一步即可，直到项目导入完毕，**如果是第一次使用，可能速度会比较慢，需要耐心等待一切就绪**

   ![](https://i.loli.net/2021/02/16/WgQ5zB6aYXF2ScN.png)

### 项目结构分析

通过上面步骤完成了基础项目的创建，就会生成一下文件



- 程序的主程序类

- 一个 application.properties 配置文件

- 一个测试类

  生成`DemoApplication`和测试包下的`DemoApplicationTests`类都可以直接运行来启动当前创建的项目，由于目前该项目未配合任何数据访问或Web模块，程序会在加载完Spring之后结束运行

  ![](https://i.loli.net/2021/02/16/SfF82LUGIlNAPQ6.png)

**使用IDEA创建也是一样的步骤，选择创建 `Spring Initializr`**

### pom.xml分析

打开`pom.xml`，查看SpringBoot项目的依赖：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<!-- 又一个父项目 -->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.4.2</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.zc</groupId>
	<artifactId>helloworld</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>helloworld</name>
	<description>Demo project for Spring Boot</description>
	<properties>
		<java.version>1.8</java.version>
	</properties>
	<dependencies>
		<!-- 所有springboot依赖都是以spring-boot-starter开头的 -->
		<!-- web依赖：tomcat，DispatcherServlet，xml -->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<!-- 单元测试 -->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<!-- 打jar包插件 -->
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>
```

如上所示，主要有四个部分：

- 项目元数据信息：创建时候输入的Project Metadata部分，也就是Maven项目的基本元素，包括：groupId、artifactId、version、name、description等
- parent：继承s`pring-boot-starter-parent`的依赖管理，控制版本与打包内容
- dependencies：项目具体依赖，这里包含了`spring-boot-starter-web`用于实现HTTP接口（该依赖中包含了SpringMVC），官网对它的描述是：使用SpringMVC构建Web（包括RESTful）应用程序的入门者，使用Tomcat作为默认嵌入式容器；`spring-boot-starter-test`用于编写单元测试的依赖包。更多功能模块的使用我们将在后面逐步展开
- build：构建配置部分。默认使用了`spring-boot-maven-plugin`，配置`spring-boot-starter-parent`就可以把SpringBoot应用打包成jar来直接运行

### 编写HTTP接口

1. 在主程序的同级目录下，新建一个controller包【一定要在同级目录下，否则识别不到】

   ![](https://i.loli.net/2021/02/16/6YU4urnBDSo51qM.png)

2. 在包中新建一个Controller类

   ```java
   package com.zc;
   
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   
   //	本身就是Spring的一个组件
   
   //	程序的主入口
   @SpringBootApplication
   public class HelloworldApplication {
   	//	SpringApplication
   	public static void main(String[] args) {
   		SpringApplication.run(HelloworldApplication.class, args);
   	}
   
   }
   ```

3. 编写完毕后，从主程序启动项目，浏览器发起请求，看页面返回

   - 控制台输出了SpringBoot的 banner

   - 控制条输出了Tomcat访问的端口号

   - 访问 hello 请求，字符串成功返回

     ![](https://i.loli.net/2021/02/16/2QftKxqEYAdczPZ.png)

4. 将项目打成jar包

5. 打成了jar包后，就可以在任何地方运行了

**彩蛋**

可以在resources目录下建一个`banner.txt`，并且将banner文字写入进去

```txt
////////////////////////////////////////////////////////////////////
//                          _ooOoo_                               //
//                         o8888888o                              //
//                         88" . "88                              //
//                         (| ^_^ |)                              //
//                         O\  =  /O                              //
//                      ____/`---'\____                           //
//                    .'  \\|     |//  `.                         //
//                   /  \\|||  :  |||//  \                        //
//                  /  _||||| -:- |||||-  \                       //
//                  |   | \\\  -  /// |   |                       //
//                  | \_|  ''\---/''  |   |                       //
//                  \  .-\__  `-`  ___/-. /                       //
//                ___`. .'  /--.--\  `. . ___                     //
//              ."" '<  `.___\_<|>_/___.'  >'"".                  //
//            | | :  `- \`.;`\ _ /`;.`/ - ` : | |                 //
//            \  \ `-.   \_ __\ /__ _/   .-` /  /                 //
//      ========`-.____`-.___\_____/___.-`____.-'========         //
//                           `=---='                              //
//      ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^        //
//            佛祖保佑       永不宕机     永无BUG                    //
////////////////////////////////////////////////////////////////////
```

启动Springboot

![](https://i.loli.net/2021/02/17/8JXfdZ65Vng7RPb.png)

## SpringBoot自动装配

springboot所有自动配置都是在启动的时候扫描并加载：`spring.factories`所有的自动配置类都在这里面，但是不一定生效，要判断条件是否成立，只要导入了对应 starter，就有对应的启动器了，有了启动器，我们自动装配就会生效，然后就配置成功

1. springboot在启动的时候，从类路径下`/META-INF/spring.factories`获取指定的值；
2. 将这些自动配置的类导入容器，自动配置就会生效，帮我们进行自动配置！
3. 以前我们需要自动配置的东西，现在springboot帮我们做了！
4. 整合javaEE，解决方案和自动配置的东西都在`spring-boot-autoconfigure-2.2.0.RELEASE.jar`这个包下
5. 它会把所有需要导入的组件，以类名的方式返回，这些组件就会被添加到容器
6. 容器中也会存在多的xxxAutoConfiguration的文件（@Bean），就是这些类给容器中导入了这个场景需要的所有组件；并自动配置。@Configuration，JavaConfig！
7. 有了自动配置类，免去了我们手动编写配置文件的工作

总结：

1. SpringBoot启动会加载大量的自动配置类

2. 我们看我们需要的功能有没有在SpringBoot默认写好的自动配置类当中

3. 我们再来看这个自动配置类中到底配置哪些组件；（只要我们要用的组件存在其中，我们就不需要再手动配置了）

4. 给容器中自动配置类添加组件的时候，会从properties类中获取某些属性。我们只需要在配置文件中指定这些属性的值即可

   xxxxAutoConfiguration：自动配置类；给容器中添加组件

   xxxxProperties：封装配置文件中相关属性

根据当前不同的条件判断，决定这个配置类是否生效

一旦这个配置类生效；这个配置类就会给容器中添加各种组件；这些组件的属性是从对应的properties类中获取的，这些类里面的每一个属性又是和配置文件绑定的

### Run

我最初以为就是运行了一个main方法，没想到却开启了一个服务

```java
package com.zc;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

//  标注这个类是一个springboot的应用
@SpringBootApplication
public class Springboot01HelloworldApplication {
    //该方法返回一个ConfigurableApplicationContext对象
    //参数一：应用入口的类  参数二：命令行参数
    public static void main(String[] args) {
        SpringApplication.run(Springboot01HelloworldApplication.class, args);
    }

}
```

**SpringApplication.run分析**

分析该方法主要分两部分。一部分是SpringApplication的实例化，二是run方法的执行

### SpringApplication

这个类主要做了以下四件事情

1. 推断应用的类型是普通的项目还是Web项目
2. 查找并加载所有可用初始化器，设置到initializers属性中
3. 找出所有的应用程序监听器，设置到listeners属性中
4. 推断并设置main方法的定义类，找到运行的主类

**查看构造器**

```java
public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources) {
        this.sources = new LinkedHashSet();
        this.bannerMode = Mode.CONSOLE;
        this.logStartupInfo = true;
        this.addCommandLineProperties = true;
        this.addConversionService = true;
        this.headless = true;
        this.registerShutdownHook = true;
        this.additionalProfiles = Collections.emptySet();
        this.isCustomEnvironment = false;
        this.lazyInitialization = false;
        this.applicationContextFactory = ApplicationContextFactory.DEFAULT;
        this.applicationStartup = ApplicationStartup.DEFAULT;
        this.resourceLoader = resourceLoader;
        Assert.notNull(primarySources, "PrimarySources must not be null");
        this.primarySources = new LinkedHashSet(Arrays.asList(primarySources));
        this.webApplicationType = WebApplicationType.deduceFromClasspath();
        this.bootstrappers = new ArrayList(this.getSpringFactoriesInstances(Bootstrapper.class));
        this.setInitializers(this.getSpringFactoriesInstances(ApplicationContextInitializer.class));
        this.setListeners(this.getSpringFactoriesInstances(ApplicationListener.class));
        this.mainApplicationClass = this.deduceMainApplicationClass();
    }
```

## 配置文件

SpringBoot使用一个全局的配置文件，配置文件名称是固定的

- application,properties
  - 语法结构：key=value
- application.yml / application.yaml
  - 语法结构：key：空格 value

配置文件的作用：修改SpringBoot自动配置的默认值，因为SpringBoot在底层都给我们自动配置好了

### YAML

YAML是“YAML Ain't a Markup Language”（YAML不是一种置标语言）的递归缩写。

在开发这种语言时，YAML的意思其实是：“Yet Another Markup Language”（仍是一种置标语言）

YAML A Markup Language：是一个标记语言

YAML isnot Markup Language：不是一个标记语言

**标记语言**

以前的配置文件，大多数都是使用xml来配置；比如一个简单的端口配置，我们来对比下yaml和xml

yaml配置：

```yaml
server:
	port: 8080
```

xml配置：

```xml
<server>
    <port>8081</port>
</server>
```

#### YAML语法

**基础语法：**

```yaml
key:(空格) value
```

以此来表示一对键值对（空格不能省略）；以空格的缩进来控制层级关系，只要是左边对齐的一列数据都是同一个层级的

注意：属性和值的大小写都是十分敏感的。例子：

```yaml
server:
	port: 8081
	path: /hello
```

#### 值的写法

字面量：普通的值 [数字，布尔值，字符串]

```yaml
key: value
```

字面量直接卸载后面就可以，字符串默认不用加上双引号或者单引号；

“” 双引号，不会转义字符串里面的特殊字符，特殊字符会作为本身想表示的意思；

比如：name： "zhao \n can" 	输出：zhao  换行  can

‘’ 单引号，会转义特殊字符，特殊字符最终会变成和普通字符一样输出

比如：name：'zhao \n can'	 输出：zhao \n can

**对象、Map（键值对）**

```yaml
k:
	v1:
	v2:
```

在下一行来写对象的属性和值的关系，注意缩进；比如：

```yaml
student:
	name: zhaocan
	age: 22
```

行内写法

```yaml
student: {name: zhaocan,age: 22}
```

**数组（List、set）**

用 - 值表示数组中的一个元素，比如：

```yaml
pets:
	- cat
	- dog
	- pig
```

行内写法

```yaml
pets: [cat,dog,pig]
```

### 修改SpringBoot的默认端口号

配置文件中添加，端口号的参数，就可以切换端口

```properties
server.port=8081
```

```yaml
server:
	port: 8081
```

### 注入配置文件

#### 程序实现

1. 如果要使用properties配置文件可能导入时存在乱码现象，需要在IDEA中进行调整，我们这里直接使用yml文件，将默认的application.properties后缀修改为yml

   ![](http://zhaocan.fym233.cn/4l1g3cfpq)

2. 导入配置文件处理器

   ```xml
   <!-- 导入配置文件处理器，配置文件进行绑定就会有提示 -->
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-configuration-processor</artifactId>
       <optional>true</optional>
   </dependency>
   ```

3. 编写yml配置文件

   ```yaml
   person:
     name: zhaocan
     age: 22
     happy: false
     birth: 1999/05/05
     maps: {k1: v1,k2: v2}
     lists:
       - code
       - music
       - girl
     dog:
       name: 旺财
       age: 3
   ```

4. 在SpringBoot的主程序的同级目录下建包，只有这样，主程序才会对这些类生效；我们建一个pojo的包放入我们的Person类和Dog类

   ```java
   package com.zc.pojo;
   
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.boot.context.properties.ConfigurationProperties;
   import org.springframework.stereotype.Component;
   
   import java.util.Date;
   import java.util.List;
   import java.util.Map;
   
   /*
   @ConfigurationPorperties作用：
   将配置文件中配置的每一个属性的值，映射到这个组件中；
   告诉SpringBoot将奔雷中的所有属性和配置文件中相关的配置进行绑定
   参数 prefix = "person" ：将配置文件中的person下面的所有属性一一对应
   
   只有这个组件是容器中的组件，才能使用容器提供的@ConfigurationProperties功能
   */
   @Component	//注册Bean
   @Data
   @AllArgsConstructor
   @NoArgsConstructor
   @ConfigurationProperties(prefix = "person")
   public class Person {
       private String name;
       private Integer age;
       private Boolean happy;
       private Date birth;
       private Map<String,Object> maps;
       private List<Object> lists;
       private Dog dog;
   }
   ```

5. 确认无误后，到测试单元中进行测试，看是否注入成功！

   ```java
   package com.zc;
   
   import com.zc.pojo.Dog;
   import com.zc.pojo.Person;
   import org.junit.jupiter.api.Test;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.test.context.SpringBootTest;
   
   @SpringBootTest
   class Springboot02ConfigApplicationTests {
   
       @Autowired
       private Dog dog;
       @Autowired
       private Person person;
   
       @Test
       void contextLoads() {
           System.out.println(person);
       }
   }
   ```

   运行结果

   ![](http://zhaocan.fym233.cn/dhcumib45i)

![](http://zhaocan.fym233.cn/ugk05zqii6)

- cp只需要写一次即可，value则需要每个字段都添加
- 松散绑定：意思就是比如我的yml中写的last-name，这个和lastName是一样的，- 后面跟着的字母默认是大写的。这就是松散绑定
- JSR303数据校验，这个就是我们可以在字段是增加一层过滤器验证，可以保证数据的合法性
- 复杂类型封装，yml中可以封装对象。使用@Value就不支持

结论：

- 配置yml和配置properties都可以获取到值，强烈推荐yml
- 如果我们在某个业务中，只需要获取配置文件中的某个值，可以使用一下@Value
- 如果说，我们专门编写了一个JavaBean来和配置文件进行映射，就直接使用@ConfigurationProperties，不要犹豫！

### JSR303数据校验

springboot中可以用@Vaildated来校验数据，如果数据异常则会统一抛出异常，方便异常中心统一处理。我们这里来写一个注解让我们的name只能支持Email格式

```java
@Component	//注册bean
@Data
@AllArgsConstructor
@NoArgsConstructor
@ConfigurationProperties(prefix = "person")
@Validated  //数据校验
public class Person {

    //@Value(value = "${person.name}")
    @Email	//name必须是邮箱格式
    private String name;
}
```

运行结果

![](http://zhaocan.fym233.cn/s5ymy0ew6x)

#### 加载指定配置文件

@PropertySource：加载指定的配置文件；使用@ConfigurationProperties默认从全局配置文件中获取值；

我们去在sources目录下新建一个person.properties文件

```properties
name=zhaocan
```

然后在我们的代码中指定加载person.properties文件

```java

@PropertySource(value = "classpath:person.properties")
@Component	//注册bean
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Person {
    
    @Value("${name}")
    private String name;
}
```

测试OK



#### 配置文件占位符

**随机数**

```properties
${random.value}、${random.int}、${random.long}、${random.int(10)}等等
```

**占位符引用其他属性的值，如果不存在可以设置默认值**

```yaml
person:
  name: zhaocan${random.uuid}
  age: ${random.int}
  happy: false
  birth: 1999/05/05
  maps: {k1: v1,k2: v2}
  lists:
    - code
    - music
    - girl
  dog:
    name: ${person.hello:hello}_旺财
    age: 3
```

#### 多环境切换

profile是Spring对不同环境提供不同配置功能的支持，可以通过激活不同的环境版本，实现快速切换环境；

**方式一：多配置文件**

我们在主配置文件编写的时候，文件名可以是 application-{profile}.properties/yml，用来指定多个环境版本

例如：application-test.properties 代表测试环境配置   application-dev.properties 代表开发环境配置

但是SpringBoot并不会直接启动这些配置文件，它默认使用 application.properties主配置文件；

我们需要通过一个配置来选择需要激活的环境

```properties
# 比如在配置文件中指定使用dev环境，我们可以通过设置不同的端口号进行测试；
# 我们启动SpringBoot，就可以看到已经切换到dev下的配置了
spring.profiles.active=dev
```

**方式二：yml的多问挡块**

和properties配置文件中一样，但是使用yml去实现不需要创建多个配置文件，更加方便了

```yaml
server:
	port: 8081
# 选择要激活哪个环境快
spring:
	profiles:
		action: prod
---
server:
	port: 8083
# 配置环境的名称
spring:
	profiles: dev
---	
server:
	port: 8084
spring:
	profiles: prod	# 配置环境的名称
```

注意：如果yml和properties同时都配置了端口，并没有激活其他环境，默认会使用properties配置文件的！

#### 配置文件加载位置

springboot启动会扫描一下位置的application.properties或者application.yml文件作为Springboot的默认配置文件

```yaml
优先级1：项目路径下的config文件夹配置文件
优先级2：项目路径下配置文件
优先级3：资源路径下的config文件夹配置文件
优先级4：资源路径下配置文件
```

优先级由高到低，高优先级的配置会覆盖低优先级的配置

SpringBoot会从这四个位置全部加载主配置文件；互补配置；

我们在最低级的配置文件中设置一个项目访问路径的配置来测试互补问题

```properties
# 配置项目的访问路径
server.servlet.context-path=/zc
```

## SpringBoot Web开发

自动装配回顾

springboot帮我们配置了什么？我们能不能进行修改？能修改哪些东西？能不能扩展？

- xxxxAutoConfiguration	向容器中自动配置组件
- xxxxProperties 	自动配置类，装配配置文件中自定义的一些内容

要解决的问题：

- 导入静态资源
- 首页
- jsp，模板引擎Thymeleaf
- 装配扩展SpringMVC
- 增删改查
- 拦截器
- 国际化

### 静态资源问题

1. 在Springboot中，我们可以使用以下方式处理静态资源

   - webjars       `localhost:8080/webjars/`

   - public，static，/**，resources    `localhost:8080/`

     ![](http://zhaocan.fym233.cn/21hyxcxitq)

2. 优先级：resources > static（默认） > public 

###  首页定制

可以将index.html放到静态资源文件中，或者放入templates下

templates只能通过controller来访问到

### Themeleaf模板引擎


前端交给我们的页面， 是htm|页面。如果是我们以前开发， 我们需要把他们转成isp页面， jsp好处就是当我们查出一些数据转发到JSP页面以后， 我们可以用jsp轻松实现数据的显示，及交互等。jsp支持非常强大的功能， 包括能写Java代码，但是呢，我们现在的这种情况，SpringBoot这个项目首先是以jar的方式，不是war，像第二，我们用的还是嵌入式的Tomcat,所以呢，他现在默认是不支持jsp的。

那不支持sp，如果我们直接用纯静态页面的方式，那给我们开发会带来非常大的麻烦那怎么办呢，Spingoot推荐你可以来使用模板引擎。

那么这模板引擎，我们其实大大家听到很多， 其实jsp就是个模板引擎，还有以用的比较多的freemarker，包括SpringBoot给我们推荐的Thymeleaf，模板引擎有非常多，但再多的模板引擎，他们的思想都是一样的，什么样一个思想呢我们来看一下这张图：

![](http://zhaocan.fym233.cn/cunw4g5vmj)

模板引擎的作用就是我们来写个页面模板，比如有些值呢，星动态的，我们写些表达式王而这些值，从哪来呢，我们来组装业数据， 我们把这些数据找到。然后把这个横板和这个数据交给我们模板引擎，模板引擎按照我们这个数据帮你把这表达式解析、填充到我们指定的位置，然后把这个数据最终生成一个我们想要的内容给我们写出去， 这就是我们这个模板引擎，不管是jsp还是其他模板引擎，都是这个思想。只不过呢，就是说不同模板引擎之间，他们可能这个语法有点不一样。 其他的我就不介绍了，我主要来介绍一下SpringBoot给我们 推荐的Thymeleaf模板引擎，这模板引擎呢，是一个高级语言的模板引擎， 他的这个语法更简单。而且呢，功能更强大。

我们呢，就来看下这个横板引擎，那既然要看这个模板引擎， 首先我们来看SpringBoot里面怎么用。

第一步：引入thymeleaf

1. Thymeleaf 官网：https://www.thymeleaf.org/

2. Thymeleaf 在Github的主页：https://github.com/thymeleaf/thymeleaf

3. Spring 官方文档：https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/htmlsingle/#using-boot-starter，找到我们对应的版本

   ```xml
   <!-- Thymeleaf -->
   <dependency>
       <groupId>org.thymeleaf</groupId>
       <artifactId>thymeleaf-spring5</artifactId>
   </dependency>
   <dependency>
       <groupId>org.thymeleaf.extras</groupId>
       <artifactId>thymeleaf-extras-java8time</artifactId>
   </dependency>
   ```

### 修改SpringBoot的默认配置

**方式一**

SpringBoot在自动配置很多组件的时候，先看容器中有没有用户自己配置的（如果用户自己配置@bean），如果有就用用户配置的，如果没有就用自动配置的；如果有些组件可以存在多个，比如我们的视图解析器，就将用户配置的和自己默认的组合起来

**扩展使用SpringMVC**

我们要做的就是编写一个@Configuration注解类，并且类型要为WebMvcConfigurer，还不能标注@EnableWebMvc注解；

新建一个包叫config，写一个类叫MyMvcConfig

```java
package com.zc.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.ViewControllerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

//  如果我们要扩展springmvc，官方建议我们这样去做！
@Configuration
public class MyMvcConfig implements WebMvcConfigurer {

    //  视图跳转
    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        //	浏览器发送/zc，就会跳转到success页面；
        registry.addViewController("/zc").setViewName("success");
    }
}
```

@EnableWebMvc注解：

导入了一个DelegatingWebMvcConfiguration，该类的作用就是从容器中获取所有的WebMvcConfig

**总结**

在springboot中，有非常多的xxxxConfiguration 帮助我们进行扩展配置，只要看见了这个东西，我们就要注意了！


## SpringData

对于数据访问层，无论是SQL（关系型数据库）还是NOSQL（非关系型数据库），SpringBoot底层都是采用SpringData的方式进行统一处理。

SpringBoot底层都是采用SpringData的方式进行统一处理各种数据库，SpringData也是Spring中与SpringBoot、SpringCloud等齐名的知名项目

SpringData官网：https://spring.io/projects/spring-data

数据库相关的启动器：可以参考官方文档：https://docs.spring.io/spring-boot/docs/2.1.7.RELEASE/reference/htmlsingle/#using-boot-starter

### 自定义数据源 Druid

**DRUID简介**

DRUID是阿里巴巴开源平台上一个数据库连接池实现，结合了C3P0、DBCP、PROXOOL等DB池的优点，同时加入了日志监控。

Druid可以很好的监控DB连接池和SQL的执行情况，天生就是针对监控而生的DB连接池

SpringBoot2.0以上默认使用Hikari数据源，可以说Hikari 与 Druid都是当前JavaWeb上最优秀的数据源

|             配置              |       缺省值       |                             说明                             |
| :---------------------------: | :----------------: | :----------------------------------------------------------: |
|             name              |                    | 配置这个属性的意义在于，如果存在多个数据源，监控的时候可以通过名字来区分开来。 <br/>如果没有配置，将会生成一个名字，格式是："DataSource-" + System.identityHashCode(this) |
|              url              |                    | 连接数据库的url，不同数据库不一样。例如： <br/>mysql : jdbc:mysql://10.20.153.104:3306/druid2 <br/>oracle : jdbc:oracle:thin:@10.20.149.85:1521:ocnauto |
|           username            |                    |                      登录数据库的用户名                      |
|           password            |                    | 连接数据库的密码。如果你不希望密码直接写在配置文件中，可以使用ConfigFilter。详细看这里：https://github.com/alibaba/druid/wiki/%E4%BD%BF%E7%94%A8ConfigFilter |
|        driverClassName        |  根据url自动识别   | 这一项可配可不配，如果不配置druid会根据url自动识别dbType，然后选择相应的driverClassName(建议配置下) |
|          initialSize          |         0          | 初始化时建立物理连接的个数。初始化发生在显示调用init方法，或者第一次getConnection时 |
|           maxActive           |         8          |                        最大连接池数量                        |
|            maxIdle            |         8          |                 已经不再使用，配置了也没效果                 |
|            minIdle            |                    |                        最小连接池数量                        |
|            maxWait            |                    | 获取连接时最大等待时间，单位毫秒。配置了maxWait之后，缺省启用公平锁，并发效率会有所下降，如果需要可以通过配置useUnfairLock属性为true使用非公平锁。 |
|    poolPreparedStatements     |       false        | 是否缓存preparedStatement，也就是PSCache。PSCache对支持游标的数据库性能提升巨大，比如说oracle。在mysql下建议关闭。 |
|   maxOpenPreparedStatements   |         -1         | 要启用PSCache，必须配置大于0，当大于0时，poolPreparedStatements自动触发修改为true。在Druid中，不会存在Oracle下PSCache占用内存过多的问题，可以把这个数值配置大一些，比如说100 |
|        validationQuery        |                    | 用来检测连接是否有效的sql，要求是一个查询语句。如果validationQuery为null，testOnBorrow、testOnReturn、testWhileIdle都不会其作用。 |
|         testOnBorrow          |        true        | 申请连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能。 |
|         testOnReturn          |       false        | 归还连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能 |
|         testWhileIdle         |       false        | 建议配置为true，不影响性能，并且保证安全性。申请连接的时候检测，如果空闲时间大于timeBetweenEvictionRunsMillis，执行validationQuery检测连接是否有效。 |
| timeBetweenEvictionRunsMillis |                    | 有两个含义： <br/>1) Destroy线程会检测连接的间隔时间2) testWhileIdle的判断依据，详细看testWhileIdle属性的说明 |
|    numTestsPerEvictionRun     |                    |      不再使用，一个DruidDataSource只支持一个EvictionRun      |
|  minEvictableIdleTimeMillis   |                    |                                                              |
|      connectionInitSqls       |                    |                物理连接初始化的时候执行的sql                 |
|        exceptionSorter        | 根据dbType自动识别 |          当数据库抛出一些不可恢复的异常时，抛弃连接          |
|            filters            |                    | 属性类型是字符串，通过别名的方式配置扩展插件，常用的插件有： <br/>监控统计用的filter:stat日志用的filter:log4j防御sql注入的filter:wall |
|         proxyFilters          |                    | 类型是List<com.alibaba.druid.filter.Filter>，如果同时配置了filters和proxyFilters，是组合关系，并非替换关系 |

#### 引入数据源

第一步需要在应用的 pom.xml 文件添加上 Druid数据源依赖，而这个依赖可以从Maven仓库官网中获取：[Maven Repository](https://mvnrepository.com/)

```xml
<!-- https://mvcrepository.com/artifact/com.alibaba/druid -->
<dependency>
	<groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.21</version>
</dependency>
```

查看项目依赖，导入成功

![](http://zhaocan.fym233.cn/24d68k9fhp)

Druid配置类

```java
package com.zc.config;

import com.alibaba.druid.pool.DruidDataSource;
import com.alibaba.druid.support.http.StatViewServlet;
import com.alibaba.druid.support.http.WebStatFilter;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.boot.web.servlet.FilterRegistrationBean;
import org.springframework.boot.web.servlet.ServletRegistrationBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.servlet.Filter;
import javax.sql.DataSource;
import java.util.HashMap;

@Configuration
public class DruidConfig {

    @ConfigurationProperties(prefix = "spring.datasource")
    @Bean
    public DataSource druidDataSource() {
        return new DruidDataSource();
    }

    //  后台监控
    //  因为springboot 内置了 servlet容器，所以没有web.xml。如果想用就要用替代方法 ServletRegistrationBean
    @Bean
    public ServletRegistrationBean statViewServlet() {
        ServletRegistrationBean<StatViewServlet> bean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");

        //  后台需要有人登录，账号密码配置
        HashMap<String, String> initParamters = new HashMap<String, String>();

        //  增加配置.
        //  登录key 是固定的 loginUsername loginPassword
        initParamters.put("loginUsername","admin");
        initParamters.put("loginPassword","123456");

        //  允许谁可以访问 value为空则所有人可访问，如果为localhost则只有本机可以访问
        initParamters.put("allow","");

        //  禁止谁来访问
        initParamters.put("zhaocan","192.168.44444.55555");

        bean.setInitParameters(initParamters);   //设置初始化参数
        return bean;
    }

    //  filter
    @Bean
    public FilterRegistrationBean webStatFilter() {
        FilterRegistrationBean<Filter> bean = new FilterRegistrationBean<Filter>();

        bean.setFilter(new WebStatFilter());

        //  可以过滤哪些请求
        HashMap<String, String> maps = new HashMap<>();

        //  这些东西不进行统计
        maps.put("exclusions","*.js,*.css,/druid/*");

        bean.setInitParameters(maps);

        return bean;
    }
}
```

## 整合MyBatis

制作一个员工管理系统并整合mybatis

**环境要求**

- IDEA
- MySQL 5.7.19
- Maven3.6
- SpringBoot + Mybatis + Themeleaf

**数据库环境**

创建一个员工表和一个部门表

员工表：

```sql
CREATE TABLE `Employee` (
  `id` int(2) NOT NULL,
  `lastname` varchar(20) NOT NULL,
  `email` varchar(30) NOT NULL,
  `gender` int(2) DEFAULT '0',
  `deid` int(2) DEFAULT NULL,
  `birth` date DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `deid` (`deid`),
  CONSTRAINT `deid` FOREIGN KEY (`deid`) REFERENCES `Department` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

部门表：

```sql
CREATE TABLE `Department` (
  `id` int(11) NOT NULL,
  `departmentName` varchar(20) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

**基本环境搭建**

1. 新建一个SpringBoot项目

2. 导入相关的pom依赖

   ```xml
   <dependencies>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-web</artifactId>
       </dependency>
   
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-test</artifactId>
           <scope>test</scope>
       </dependency>
   
       <!-- Thymeleaf -->
       <dependency>
           <groupId>org.thymeleaf</groupId>
           <artifactId>thymeleaf-spring5</artifactId>
       </dependency>
       <dependency>
           <groupId>org.thymeleaf.extras</groupId>
           <artifactId>thymeleaf-extras-java8time</artifactId>
       </dependency>
   
       <dependency>
           <groupId>org.projectlombok</groupId>
           <artifactId>lombok</artifactId>
       </dependency>
   
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <scope>runtime</scope>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-test</artifactId>
           <scope>test</scope>
       </dependency>
       <dependency>
           <groupId>org.mybatis.spring.boot</groupId>
           <artifactId>mybatis-spring-boot-starter</artifactId>
           <version>2.1.4</version>
       </dependency>
   </dependencies>
   ```

3. 建立包基本结构

   - com.zc.pojo
   - com.zc.mapper / com.zc.dao
   - com.zc.service
   - com.zc.controller
   - com.zc.config

4. 在resources下建立mybatis.mapper存放mybatis配置文件

5. 编写html页面信息

   templates.dashboard.html

   ```html
   <!DOCTYPE html>
   <!-- saved from url=(0052)http://getbootstrap.com/docs/4.0/examples/dashboard/ -->
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   <head>
       <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
       <meta name="description" content="">
       <meta name="author" content="">
   
       <title>Dashboard Template for Bootstrap</title>
       <!-- Bootstrap core CSS -->
       <link th:href="@{/css/bootstrap.min.css}" rel="stylesheet">
   
       <!-- Custom styles for this template -->
       <link th:href="@{/css/dashboard.css}" rel="stylesheet">
       <style type="text/css">
           /* Chart.js */
   
           @-webkit-keyframes chartjs-render-animation {
               from {
                   opacity: 0.99
               }
               to {
                   opacity: 1
               }
           }
   
           @keyframes chartjs-render-animation {
               from {
                   opacity: 0.99
               }
               to {
                   opacity: 1
               }
           }
   
           .chartjs-render-monitor {
               -webkit-animation: chartjs-render-animation 0.001s;
               animation: chartjs-render-animation 0.001s;
           }
       </style>
   </head>
   
   <body>
   
   <div th:replace="~{commons/commons::topbar}"></div>
   
   <div class="container-fluid">
       <div class="row">
   
           <!-- 传递参数给组件 -->
           <div th:replace="~{commons/commons::sidebar(active='main.html')}"></div>
   
           <main role="main" class="col-md-9 ml-sm-auto col-lg-10 pt-3 px-4">
               <div class="chartjs-size-monitor"
                    style="position: absolute; left: 0px; top: 0px; right: 0px; bottom: 0px; overflow: hidden; pointer-events: none; visibility: hidden; z-index: -1;">
                   <div class="chartjs-size-monitor-expand"
                        style="position:absolute;left:0;top:0;right:0;bottom:0;overflow:hidden;pointer-events:none;visibility:hidden;z-index:-1;">
                       <div style="position:absolute;width:1000000px;height:1000000px;left:0;top:0"></div>
                   </div>
                   <div class="chartjs-size-monitor-shrink"
                        style="position:absolute;left:0;top:0;right:0;bottom:0;overflow:hidden;pointer-events:none;visibility:hidden;z-index:-1;">
                       <div style="position:absolute;width:200%;height:200%;left:0; top:0"></div>
                   </div>
               </div>
               <div class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center pb-2 mb-3 border-bottom">
                   <h1 class="h2">Dashboard</h1>
                   <div class="btn-toolbar mb-2 mb-md-0">
                       <div class="btn-group mr-2">
                           <button class="btn btn-sm btn-outline-secondary">Share</button>
                           <button class="btn btn-sm btn-outline-secondary">Export</button>
                       </div>
                       <button class="btn btn-sm btn-outline-secondary dropdown-toggle">
                           <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                                stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                                class="feather feather-calendar">
                               <rect x="3" y="4" width="18" height="18" rx="2" ry="2"></rect>
                               <line x1="16" y1="2" x2="16" y2="6"></line>
                               <line x1="8" y1="2" x2="8" y2="6"></line>
                               <line x1="3" y1="10" x2="21" y2="10"></line>
                           </svg>
                           This week
                       </button>
                   </div>
               </div>
   
               <canvas class="my-4 chartjs-render-monitor" id="myChart" width="1076" height="454"
                       style="display: block; width: 1076px; height: 454px;"></canvas>
   
   
           </main>
       </div>
   </div>
   
   <!-- Bootstrap core JavaScript
   ================================================== -->
   <!-- Placed at the end of the document so the pages load faster -->
   <script type="text/javascript" src="../static/js/jquery-3.2.1.slim.min.js"></script>
   <script type="text/javascript" src="../static/js/popper.min.js"></script>
   <script type="text/javascript" src="../static/js/bootstrap.min.js"></script>
   
   <!-- Icons -->
   <script type="text/javascript" src="../static/js/feather.min.js"></script>
   <script>
       feather.replace()
   </script>
   
   <!-- Graphs -->
   <script type="text/javascript" src="../static/js/Chart.min.js"></script>
   <script>
       var ctx = document.getElementById("myChart");
       var myChart = new Chart(ctx, {
           type: 'line',
           data: {
               labels: ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"],
               datasets: [{
                   data: [15339, 21345, 18483, 24003, 23489, 24092, 12034],
                   lineTension: 0,
                   backgroundColor: 'transparent',
                   borderColor: '#007bff',
                   borderWidth: 4,
                   pointBackgroundColor: '#007bff'
               }]
           },
           options: {
               scales: {
                   yAxes: [{
                       ticks: {
                           beginAtZero: false
                       }
                   }]
               },
               legend: {
                   display: false,
               }
           }
       });
   </script>
   </body>
   </html>
   ```

   templates.index.html

   ```html
   <!DOCTYPE html>
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   <head>
       <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
       <meta name="description" content="">
       <meta name="author" content="">
       <title>Signin Template for Bootstrap</title>
       <!-- Bootstrap core CSS -->
       <link th:href="@{/css/bootstrap.min.css}" rel="stylesheet">
       <!-- Custom styles for this template -->
       <link th:href="@{/css/signin.css}" rel="stylesheet">
   </head>
   
   <body class="text-center">
   <form class="form-signin" th:action="@{/user/login}" th:method="post">
       <img class="mb-4" th:src="@{/img/bootstrap-solid.svg}" alt="" width="72" height="72">
       <h1 class="h3 mb-3 font-weight-normal" th:text="#{login.tip}">Please sign in</h1>
   
       <!-- 如果msg的值为空则不显示消息 -->
       <p style="color: red" th:text="${msg}" th:if="${not #strings.isEmpty(msg)}"></p>
   
       <label class="sr-only">Username</label>
       <input type="text" name="username" class="form-control" th:placeholder="#{login.username}" required="" autofocus="">
       <label class="sr-only">Password</label>
       <input type="password" name="password" class="form-control" th:placeholder="#{login.password}" required="">
       <div class="checkbox mb-3">
           <label>
               <input type="checkbox" value="remember-me" th:utext="#{login.remeber}">
               <!--Remember me-->
           </label>
       </div>
       <button class="btn btn-lg btn-primary btn-block" type="submit" th:text="#{login.btn}">Sign in</button>
       <p class="mt-5 mb-3 text-muted">© 2020-2021</p>
       <a class="btn btn-sm" th:href="@{/index.html(language='zh_CH')}">中文</a>
       <a class="btn btn-sm" th:href="@{/index.html(language='en_US')}">English</a>
   </form>
   </body>
   </html>
   ```

   templates.commons,commons.html

   ```html
   <!DOCTYPE html>
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   </head>
   <body>
   
   <!-- 头部导航栏 -->
   <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0" th:fragment="topbar">
       <a class="navbar-brand col-sm-3 col-md-2 mr-0" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
           [[${session.loginUser}]]</a>
       <input class="form-control form-control-dark w-100" type="text" placeholder="Search" aria-label="Search">
       <ul class="navbar-nav px-3">
           <li class="nav-item text-nowrap">
               <a class="nav-link" th:href="@{/user/logout}">注销</a>
           </li>
       </ul>
   </nav>
   
   
   <!-- 侧边栏 -->
   <nav class="col-md-2 d-none d-md-block bg-light sidebar" th:fragment="sidebar">
       <div class="sidebar-sticky">
           <ul class="nav flex-column">
               <li class="nav-item">
                   <a th:class="${active=='main.html'?'nav-link active':'nav-link'}" th:href="@{/main.html}">
                       <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                            class="feather feather-home">
                           <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
                           <polyline points="9 22 9 12 15 12 15 22"></polyline>
                       </svg>
                       首页 <span class="sr-only">(current)</span>
                   </a>
               </li>
               <li class="nav-item">
                   <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                       <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                            class="feather feather-file">
                           <path d="M13 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V9z"></path>
                           <polyline points="13 2 13 9 20 9"></polyline>
                       </svg>
                       Orders
                   </a>
               </li>
               <li class="nav-item">
                   <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                       <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                            class="feather feather-shopping-cart">
                           <circle cx="9" cy="21" r="1"></circle>
                           <circle cx="20" cy="21" r="1"></circle>
                           <path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"></path>
                       </svg>
                       Products
                   </a>
               </li>
               <li class="nav-item">
                   <a th:class="${active=='list.html'?'nav-link active':'nav-link'}" th:href="@{/emps}">
                       <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                            class="feather feather-users">
                           <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path>
                           <circle cx="9" cy="7" r="4"></circle>
                           <path d="M23 21v-2a4 4 0 0 0-3-3.87"></path>
                           <path d="M16 3.13a4 4 0 0 1 0 7.75"></path>
                       </svg>
                       员工管理
                   </a>
               </li>
               <li class="nav-item">
                   <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                       <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                            class="feather feather-bar-chart-2">
                           <line x1="18" y1="20" x2="18" y2="10"></line>
                           <line x1="12" y1="20" x2="12" y2="4"></line>
                           <line x1="6" y1="20" x2="6" y2="14"></line>
                       </svg>
                       Reports
                   </a>
               </li>
               <li class="nav-item">
                   <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                       <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                            class="feather feather-layers">
                           <polygon points="12 2 2 7 12 12 22 7 12 2"></polygon>
                           <polyline points="2 17 12 22 22 17"></polyline>
                           <polyline points="2 12 12 17 22 12"></polyline>
                       </svg>
                       Integrations
                   </a>
               </li>
           </ul>
   
           <h6 class="sidebar-heading d-flex justify-content-between align-items-center px-3 mt-4 mb-1 text-muted">
               <span>Saved reports</span>
               <a class="d-flex align-items-center text-muted"
                  href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                   <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                        class="feather feather-plus-circle">
                       <circle cx="12" cy="12" r="10"></circle>
                       <line x1="12" y1="8" x2="12" y2="16"></line>
                       <line x1="8" y1="12" x2="16" y2="12"></line>
                   </svg>
               </a>
           </h6>
           <ul class="nav flex-column mb-2">
               <li class="nav-item">
                   <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                       <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                            class="feather feather-file-text">
                           <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                           <polyline points="14 2 14 8 20 8"></polyline>
                           <line x1="16" y1="13" x2="8" y2="13"></line>
                           <line x1="16" y1="17" x2="8" y2="17"></line>
                           <polyline points="10 9 9 9 8 9"></polyline>
                       </svg>
                       Current month
                   </a>
               </li>
               <li class="nav-item">
                   <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                       <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                            class="feather feather-file-text">
                           <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                           <polyline points="14 2 14 8 20 8"></polyline>
                           <line x1="16" y1="13" x2="8" y2="13"></line>
                           <line x1="16" y1="17" x2="8" y2="17"></line>
                           <polyline points="10 9 9 9 8 9"></polyline>
                       </svg>
                       Last quarter
                   </a>
               </li>
               <li class="nav-item">
                   <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                       <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                            class="feather feather-file-text">
                           <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                           <polyline points="14 2 14 8 20 8"></polyline>
                           <line x1="16" y1="13" x2="8" y2="13"></line>
                           <line x1="16" y1="17" x2="8" y2="17"></line>
                           <polyline points="10 9 9 9 8 9"></polyline>
                       </svg>
                       Social engagement
                   </a>
               </li>
               <li class="nav-item">
                   <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                       <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                            class="feather feather-file-text">
                           <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                           <polyline points="14 2 14 8 20 8"></polyline>
                           <line x1="16" y1="13" x2="8" y2="13"></line>
                           <line x1="16" y1="17" x2="8" y2="17"></line>
                           <polyline points="10 9 9 9 8 9"></polyline>
                       </svg>
                       Year-end sale
                   </a>
               </li>
           </ul>
       </div>
   </nav>
   </body>
   </html>
   ```

   templates.emp.add.html

   ```html
   <!DOCTYPE html>
   <!-- saved from url=(0052)http://getbootstrap.com/docs/4.0/examples/dashboard/ -->
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   
   <head>
       <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
       <meta name="description" content="">
       <meta name="author" content="">
   
       <title>Dashboard Template for Bootstrap</title>
       <!-- Bootstrap core CSS -->
       <link th:href="@{/css/bootstrap.min.css}" rel="stylesheet">
   
       <!-- Custom styles for this template -->
       <link th:href="@{/css/dashboard.css}" rel="stylesheet">
       <style type="text/css">
           /* Chart.js */
   
           @-webkit-keyframes chartjs-render-animation {
               from {
                   opacity: 0.99
               }
               to {
                   opacity: 1
               }
           }
   
           @keyframes chartjs-render-animation {
               from {
                   opacity: 0.99
               }
               to {
                   opacity: 1
               }
           }
   
           .chartjs-render-monitor {
               -webkit-animation: chartjs-render-animation 0.001s;
               animation: chartjs-render-animation 0.001s;
           }
       </style>
   </head>
   
   <body>
   
   <div th:replace="~{commons/commons::topbar}"></div>
   
   <div class="container-fluid">
       <div class="row">
   
           <div th:replace="~{commons/commons::sidebar(active='list.html')}"></div>
   
           <main role="main" class="col-md-9 ml-sm-auto col-lg-10 pt-3 px-4">
               <form th:action="@{/emp}" method="post">
                   <div class="form-group">
                       <label>LastName</label>
                       <input type="text" name="lastName" class="form-control" placeholder="zhaocan">
                   </div>
                   <div class="form-group">
                       <label>Email</label>
                       <input type="text" name="email" class="form-control" placeholder="zc1872751113@gmail.com">
                   </div>
                   <div class="form-group">
                       <label>Gender</label>
                       <div class="form-check" form-check-inline>
                           <input class="form-check-input" type="radio" name="gender" value="1">
                           <label class="form-check-label">男</label>
                       </div>
                       <div class="form-check" form-check-inline>
                           <input class="form-check-input" type="radio" name="gender" value="0">
                           <label class="form-check-label">女</label>
                       </div>
                   </div>
                   <div class="form-group">
                       <label>department</label>
                       <select class="form-control" name="department.id">
                           <option th:each="dept:${departments}" th:text="${dept.getDepartmentName()}"
                                   th:value="${dept.getId()}"></option>
                       </select>
                   </div>
                   <div class="form-group">
                       <label>Birth</label>
                       <input type="text" name="birth" class="form-control" placeholder="1970-01-01">
                   </div>
                   <button type="submit" class="btn btn-primary">添加</button>
               </form>
   
           </main>
       </div>
   </div>
   
   <!-- Bootstrap core JavaScript
   ================================================== -->
   <!-- Placed at the end of the document so the pages load faster -->
   <script type="text/javascript" src="../../static/js/jquery-3.2.1.slim.min.js"></script>
   <script type="text/javascript" src="../../static/js/popper.min.js"></script>
   <script type="text/javascript" src="../../static/js/bootstrap.min.js"></script>
   
   <!-- Icons -->
   <script type="text/javascript" src="../../static/js/feather.min.js"></script>
   <script>
       feather.replace()
   </script>
   
   <!-- Graphs -->
   <script type="text/javascript" src="../../static/js/Chart.min.js"></script>
   <script>
       var ctx = document.getElementById("myChart");
       var myChart = new Chart(ctx, {
           type: 'line',
           data: {
               labels: ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"],
               datasets: [{
                   data: [15339, 21345, 18483, 24003, 23489, 24092, 12034],
                   lineTension: 0,
                   backgroundColor: 'transparent',
                   borderColor: '#007bff',
                   borderWidth: 4,
                   pointBackgroundColor: '#007bff'
               }]
           },
           options: {
               scales: {
                   yAxes: [{
                       ticks: {
                           beginAtZero: false
                       }
                   }]
               },
               legend: {
                   display: false,
               }
           }
       });
   </script>
   </body>
   </html>
   ```

   templates.emp.list.html

   ```html
   <!DOCTYPE html>
   <!-- saved from url=(0052)http://getbootstrap.com/docs/4.0/examples/dashboard/ -->
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   
   <head>
       <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
       <meta name="description" content="">
       <meta name="author" content="">
   
       <title>Dashboard Template for Bootstrap</title>
       <!-- Bootstrap core CSS -->
       <link th:href="@{/css/bootstrap.min.css}" rel="stylesheet">
   
       <!-- Custom styles for this template -->
       <link th:href="@{/css/dashboard.css}" rel="stylesheet">
       <style type="text/css">
           /* Chart.js */
   
           @-webkit-keyframes chartjs-render-animation {
               from {
                   opacity: 0.99
               }
               to {
                   opacity: 1
               }
           }
   
           @keyframes chartjs-render-animation {
               from {
                   opacity: 0.99
               }
               to {
                   opacity: 1
               }
           }
   
           .chartjs-render-monitor {
               -webkit-animation: chartjs-render-animation 0.001s;
               animation: chartjs-render-animation 0.001s;
           }
       </style>
   </head>
   
   <body>
   
   <div th:replace="~{commons/commons::topbar}"></div>
   
   <div class="container-fluid">
       <div class="row">
   
           <div th:replace="~{commons/commons::sidebar(active='list.html')}"></div>
   
           <main role="main" class="col-md-9 ml-sm-auto col-lg-10 pt-3 px-4">
               <h2><a class="btn btn-sm btn-success" th:href="@{/emp}">添加员工</a></h2>
   
               <div class="table-responsive">
                   <table class="table table-striped table-sm">
                       <thead>
                       <tr>
                           <th>id</th>
                           <th>lastName</th>
                           <th>email</th>
                           <th>gender</th>
                           <th>department</th>
                           <th>birth</th>
                           <th>操作</th>
                       </tr>
                       </thead>
                       <tbody>
                       <tr th:each="emp:${emps}">
                           <td th:text="${emp.getId()}"></td>
                           <td th:text="${emp.getLastName()}"></td>
                           <td th:text="${emp.getEmail()}"></td>
                           <td th:text="${emp.getGender()==0?'女':'男'}"></td>
                           <td th:text="${emp.getDepartment().getDepartmentName()}"></td>
                           <td th:text="${#dates.format(emp.getBirth(),'yyyy-MM-dd')}"></td>
                           <td>
                               <a class="btn btn-sm btn-primary" th:href="@{/emp/}+${emp.getId()}">编辑</a>
                               <a class="btn btn-sm btn-danger" th:href="@{/deletemp/}+${emp.getId()}">删除</a>
                           </td>
                       </tr>
                       </tbody>
                   </table>
               </div>
           </main>
       </div>
   </div>
   
   <!-- Bootstrap core JavaScript
   ================================================== -->
   <!-- Placed at the end of the document so the pages load faster -->
   <script type="text/javascript" src="../../static/js/jquery-3.2.1.slim.min.js"></script>
   <script type="text/javascript" src="../../static/js/popper.min.js"></script>
   <script type="text/javascript" src="../../static/js/bootstrap.min.js"></script>
   
   <!-- Icons -->
   <script type="text/javascript" src="../../static/js/feather.min.js"></script>
   <script>
       feather.replace()
   </script>
   
   <!-- Graphs -->
   <script type="text/javascript" src="../../static/js/Chart.min.js"></script>
   <script>
       var ctx = document.getElementById("myChart");
       var myChart = new Chart(ctx, {
           type: 'line',
           data: {
               labels: ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"],
               datasets: [{
                   data: [15339, 21345, 18483, 24003, 23489, 24092, 12034],
                   lineTension: 0,
                   backgroundColor: 'transparent',
                   borderColor: '#007bff',
                   borderWidth: 4,
                   pointBackgroundColor: '#007bff'
               }]
           },
           options: {
               scales: {
                   yAxes: [{
                       ticks: {
                           beginAtZero: false
                       }
                   }]
               },
               legend: {
                   display: false,
               }
           }
       });
   </script>
   </body>
   </html>
   ```

   templates.emp.update.html

   ```html
   <!DOCTYPE html>
   <!-- saved from url=(0052)http://getbootstrap.com/docs/4.0/examples/dashboard/ -->
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   
   <head>
       <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
       <meta name="description" content="">
       <meta name="author" content="">
   
       <title>Dashboard Template for Bootstrap</title>
       <!-- Bootstrap core CSS -->
       <link th:href="@{/css/bootstrap.min.css}" rel="stylesheet">
   
       <!-- Custom styles for this template -->
       <link th:href="@{/css/dashboard.css}" rel="stylesheet">
       <style type="text/css">
           /* Chart.js */
   
           @-webkit-keyframes chartjs-render-animation {
               from {
                   opacity: 0.99
               }
               to {
                   opacity: 1
               }
           }
   
           @keyframes chartjs-render-animation {
               from {
                   opacity: 0.99
               }
               to {
                   opacity: 1
               }
           }
   
           .chartjs-render-monitor {
               -webkit-animation: chartjs-render-animation 0.001s;
               animation: chartjs-render-animation 0.001s;
           }
       </style>
   </head>
   
   <body>
   
   <div th:replace="~{commons/commons::topbar}"></div>
   
   <div class="container-fluid">
       <div class="row">
   
           <div th:replace="~{commons/commons::sidebar(active='list.html')}"></div>
   
           <main role="main" class="col-md-9 ml-sm-auto col-lg-10 pt-3 px-4">
               <form th:action="@{/updateEmp}" method="post">
                   <input type="hidden" name="id" th:value="${emp.getId()}"/>
                   <div class="form-group">
                       <label>LastName</label>
                       <input type="text" name="lastName" th:value="${emp.getLastName()}" class="form-control"
                              placeholder="zhaocan">
                   </div>
                   <div class="form-group">
                       <label>Email</label>
                       <input type="text" name="email" th:value="${emp.getEmail()}" class="form-control"
                              placeholder="zc1872751113@gmail.com">
                   </div>
                   <div class="form-group">
                       <label>Gender</label>
                       <div class="form-check" form-check-inline>
                           <input class="form-check-input" type="radio" name="gender" value="1"
                                  th:checked="${emp.getGender()==1}">
                           <label class="form-check-label">男</label>
                       </div>
                       <div class="form-check" form-check-inline>
                           <input class="form-check-input" type="radio" name="gender" value="0"
                                  th:checked="${emp.getGender()==0}">
                           <label class="form-check-label">女</label>
                       </div>
                   </div>
                   <div class="form-group">
                       <label>department</label>
                       <select class="form-control" name="department.id">
                           <option th:selected="${dept.getId()==emp.getDepartment().getId()}" th:each="dept:${departments}"
                                   th:text="${dept.getDepartmentName()}" th:value="${dept.getId()}"></option>
                       </select>
                   </div>
                   <div class="form-group">
                       <label>Birth</label>
                       <input th:value="${#dates.format(emp.getBirth(),'yyyy-MM-dd')}" type="text" name="birth"
                              class="form-control" placeholder="1970-01-01">
                   </div>
                   <button type="submit" class="btn btn-primary">修改</button>
               </form>
   
           </main>
       </div>
   </div>
   
   <!-- Bootstrap core JavaScript
   ================================================== -->
   <!-- Placed at the end of the document so the pages load faster -->
   <script type="text/javascript" src="../../static/js/jquery-3.2.1.slim.min.js"></script>
   <script type="text/javascript" src="../../static/js/popper.min.js"></script>
   <script type="text/javascript" src="../../static/js/bootstrap.min.js"></script>
   
   <!-- Icons -->
   <script type="text/javascript" src="../../static/js/feather.min.js"></script>
   <script>
       feather.replace()
   </script>
   
   <!-- Graphs -->
   <script type="text/javascript" src="../../static/js/Chart.min.js"></script>
   <script>
       var ctx = document.getElementById("myChart");
       var myChart = new Chart(ctx, {
           type: 'line',
           data: {
               labels: ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"],
               datasets: [{
                   data: [15339, 21345, 18483, 24003, 23489, 24092, 12034],
                   lineTension: 0,
                   backgroundColor: 'transparent',
                   borderColor: '#007bff',
                   borderWidth: 4,
                   pointBackgroundColor: '#007bff'
               }]
           },
           options: {
               scales: {
                   yAxes: [{
                       ticks: {
                           beginAtZero: false
                       }
                   }]
               },
               legend: {
                   display: false,
               }
           }
       });
   </script>
   </body>
   </html>
   ```

   templates.error.404.html

   ```html
   <!DOCTYPE html>
   <!-- saved from url=(0052)http://getbootstrap.com/docs/4.0/examples/dashboard/ -->
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   <head>
       <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
       <meta name="description" content="">
       <meta name="author" content="">
   
       <title>Dashboard Template for Bootstrap</title>
       <!-- Bootstrap core CSS -->
       <link th:href="@{/css/bootstrap.min.css}" rel="stylesheet">
   
       <!-- Custom styles for this template -->
       <link th:href="@{/css/dashboard.css}" rel="stylesheet">
       <style type="text/css">
           /* Chart.js */
   
           @-webkit-keyframes chartjs-render-animation {
               from {
                   opacity: 0.99
               }
               to {
                   opacity: 1
               }
           }
   
           @keyframes chartjs-render-animation {
               from {
                   opacity: 0.99
               }
               to {
                   opacity: 1
               }
           }
   
           .chartjs-render-monitor {
               -webkit-animation: chartjs-render-animation 0.001s;
               animation: chartjs-render-animation 0.001s;
           }
       </style>
   </head>
   
   <body>
   <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0">
       <a class="navbar-brand col-sm-3 col-md-2 mr-0" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">Company
           name</a>
       <input class="form-control form-control-dark w-100" type="text" placeholder="Search" aria-label="Search">
       <ul class="navbar-nav px-3">
           <li class="nav-item text-nowrap">
               <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">Sign out</a>
           </li>
       </ul>
   </nav>
   
   <div class="container-fluid">
       <div class="row">
           <nav class="col-md-2 d-none d-md-block bg-light sidebar">
               <div class="sidebar-sticky">
                   <ul class="nav flex-column">
                       <li class="nav-item">
                           <a class="nav-link active" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="feather feather-home">
                                   <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
                                   <polyline points="9 22 9 12 15 12 15 22"></polyline>
                               </svg>
                               Dashboard <span class="sr-only">(current)</span>
                           </a>
                       </li>
                       <li class="nav-item">
                           <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="feather feather-file">
                                   <path d="M13 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V9z"></path>
                                   <polyline points="13 2 13 9 20 9"></polyline>
                               </svg>
                               Orders
                           </a>
                       </li>
                       <li class="nav-item">
                           <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="feather feather-shopping-cart">
                                   <circle cx="9" cy="21" r="1"></circle>
                                   <circle cx="20" cy="21" r="1"></circle>
                                   <path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"></path>
                               </svg>
                               Products
                           </a>
                       </li>
                       <li class="nav-item">
                           <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="feather feather-users">
                                   <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path>
                                   <circle cx="9" cy="7" r="4"></circle>
                                   <path d="M23 21v-2a4 4 0 0 0-3-3.87"></path>
                                   <path d="M16 3.13a4 4 0 0 1 0 7.75"></path>
                               </svg>
                               Customers
                           </a>
                       </li>
                       <li class="nav-item">
                           <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="feather feather-bar-chart-2">
                                   <line x1="18" y1="20" x2="18" y2="10"></line>
                                   <line x1="12" y1="20" x2="12" y2="4"></line>
                                   <line x1="6" y1="20" x2="6" y2="14"></line>
                               </svg>
                               Reports
                           </a>
                       </li>
                       <li class="nav-item">
                           <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="feather feather-layers">
                                   <polygon points="12 2 2 7 12 12 22 7 12 2"></polygon>
                                   <polyline points="2 17 12 22 22 17"></polyline>
                                   <polyline points="2 12 12 17 22 12"></polyline>
                               </svg>
                               Integrations
                           </a>
                       </li>
                   </ul>
   
                   <h6 class="sidebar-heading d-flex justify-content-between align-items-center px-3 mt-4 mb-1 text-muted">
                       <span>Saved reports</span>
                       <a class="d-flex align-items-center text-muted"
                          href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                           <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                                stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                                class="feather feather-plus-circle">
                               <circle cx="12" cy="12" r="10"></circle>
                               <line x1="12" y1="8" x2="12" y2="16"></line>
                               <line x1="8" y1="12" x2="16" y2="12"></line>
                           </svg>
                       </a>
                   </h6>
                   <ul class="nav flex-column mb-2">
                       <li class="nav-item">
                           <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="feather feather-file-text">
                                   <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                                   <polyline points="14 2 14 8 20 8"></polyline>
                                   <line x1="16" y1="13" x2="8" y2="13"></line>
                                   <line x1="16" y1="17" x2="8" y2="17"></line>
                                   <polyline points="10 9 9 9 8 9"></polyline>
                               </svg>
                               Current month
                           </a>
                       </li>
                       <li class="nav-item">
                           <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="feather feather-file-text">
                                   <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                                   <polyline points="14 2 14 8 20 8"></polyline>
                                   <line x1="16" y1="13" x2="8" y2="13"></line>
                                   <line x1="16" y1="17" x2="8" y2="17"></line>
                                   <polyline points="10 9 9 9 8 9"></polyline>
                               </svg>
                               Last quarter
                           </a>
                       </li>
                       <li class="nav-item">
                           <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="feather feather-file-text">
                                   <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                                   <polyline points="14 2 14 8 20 8"></polyline>
                                   <line x1="16" y1="13" x2="8" y2="13"></line>
                                   <line x1="16" y1="17" x2="8" y2="17"></line>
                                   <polyline points="10 9 9 9 8 9"></polyline>
                               </svg>
                               Social engagement
                           </a>
                       </li>
                       <li class="nav-item">
                           <a class="nav-link" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">
                               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="feather feather-file-text">
                                   <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                                   <polyline points="14 2 14 8 20 8"></polyline>
                                   <line x1="16" y1="13" x2="8" y2="13"></line>
                                   <line x1="16" y1="17" x2="8" y2="17"></line>
                                   <polyline points="10 9 9 9 8 9"></polyline>
                               </svg>
                               Year-end sale
                           </a>
                       </li>
                   </ul>
               </div>
           </nav>
   
           <main role="main" class="col-md-9 ml-sm-auto col-lg-10 pt-3 px-4">
               <h1>404</h1>
           </main>
       </div>
   </div>
   
   <!-- Bootstrap core JavaScript
   ================================================== -->
   <!-- Placed at the end of the document so the pages load faster -->
   <script type="text/javascript" src="../../static/js/jquery-3.2.1.slim.min.js"></script>
   <script type="text/javascript" src="../../static/js/popper.min.js"></script>
   <script type="text/javascript" src="../../static/js/bootstrap.min.js"></script>
   
   <!-- Icons -->
   <script type="text/javascript" src="../../static/js/feather.min.js"></script>
   <script>
       feather.replace()
   </script>
   
   <!-- Graphs -->
   <script type="text/javascript" src="../../static/js/Chart.min.js"></script>
   <script>
       var ctx = document.getElementById("myChart");
       var myChart = new Chart(ctx, {
           type: 'line',
           data: {
               labels: ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"],
               datasets: [{
                   data: [15339, 21345, 18483, 24003, 23489, 24092, 12034],
                   lineTension: 0,
                   backgroundColor: 'transparent',
                   borderColor: '#007bff',
                   borderWidth: 4,
                   pointBackgroundColor: '#007bff'
               }]
           },
           options: {
               scales: {
                   yAxes: [{
                       ticks: {
                           beginAtZero: false
                       }
                   }]
               },
               legend: {
                   display: false,
               }
           }
       });
   </script>
   
   </body>
   
   </html>
   ```

6. 编写dao层接口及xml

   DepartmentMapper

   ```java
   package com.zc.dao;
   
   import com.zc.pojo.Department;
   import org.springframework.stereotype.Repository;
   
   import java.util.List;
   
   @Repository
   public interface DepartmentMapper {
   
       //  获得所有部门信息
       public List<Department> getDepartments();
   
       //  通过id得到部门
       public Department getDepartmentById(Integer id);
   }
   ```

   DepartmentMapper.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.zc.dao.DepartmentMapper">
   
       <select id="getDepartments" resultType="Department">
           select * from Department
       </select>
   
       <select id="getDepartmentById" resultType="Department">
           select * from Department where id = #{id}
       </select>
   </mapper>
   ```

   EmployeeMapper

   ```java
   package com.zc.dao;
   
   import com.zc.pojo.Employee;
   import org.springframework.stereotype.Repository;
   
   import java.util.*;
   
   //  员工Dao
   @Repository
   public interface EmployeeMapper {
   
       //  增加一个员工
       public int addEmployee(Employee employee);
   
       //  查询全部员工
       public List<Employee> getAllEmployee();
   
       //  通过id查询员工
       public Employee getEmployeeById(Integer id);
   
       //  删除员工
       public int deleteEmployee(Integer id);
   
       //  修改员工
       public int updateEmployee(Employee employee);
   }
   ```

   EmployeeMapper.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.zc.dao.EmployeeMapper">
   
       <resultMap id="EmployeeDen" type="Employee">
           <result property="id" column="eid"/>
           <result property="lastName" column="lastname"/>
           <result property="email" column="email"/>
           <result property="gender" column="gender"/>
           <result property="birth" column="birth"/>
           <association property="department" javaType="Department">
               <result property="id" column="deid"/>
               <result property="departmentName" column="departmentName"/>
           </association>
       </resultMap>
   
       <insert id="addEmployee">
           insert into Employee
               (id,lastname,email,gender,deid,birth)
               values
               (#{id}, #{lastName}, #{email}, #{gender}, #{department.id}, #{birth})
       </insert>
   
       <select id="getAllEmployee" resultMap="EmployeeDen">
           select e.id eid, e.lastname,e.email, e.gender, e.birth, d.id deid, d.departmentName
           from Employee e left join Department d on e.deid = d.id
       </select>
   
       <select id="getEmployeeById" resultMap="EmployeeDen">
           select e.id eid, e.lastname,e.email, e.gender, e.birth, d.id deid, d.departmentName
           from Employee e left join Department d on e.deid = d.id
           where e.id=#{id}
       </select>
   
       <delete id="deleteEmployee">
           delete from Employee where id = #{id}
       </delete>
   
       <update id="updateEmployee">
           update Employee set lastname=#{lastName},email=#{email},gender=#{gender},deid=#{department.id},birth=#{birth} where id=#{id}
       </update>
   </mapper>
   ```

7. 编写appcalition,yaml配置文件

   ```yaml
   # 关闭模板引擎的缓存
   spring:
     thymeleaf:
       cache: false
   # 我们的配置文件的真实位置
     messages:
       basename: i18n.login
   # 时间日期格式化
     mvc:
       format:
         date: yyyy-MM-dd
     datasource:
       data-username: root
       data-password: root3306
       url: jdbc:mysql://47.98.47.51:3306/mybatis?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
       driver-class-name: com.mysql.cj.jdbc.Driver
   # 整合mybatis
   mybatis:
     type-aliases-package: com.zc.pojo
     mapper-locations: classpath:mybatis/mapper/*.xml
   server:
     servlet:
       context-path: /zc
   ```

8. 编写service层

   DepartmentService

   ```java
   package com.zc.service;
   
   import com.zc.pojo.Department;
   
   import java.util.List;
   
   public interface DepartmentService {
   
       //  获得所有部门信息
       public List<Department> getDepartments();
   
       //  通过id得到部门
       public Department getDepartmentById(Integer id);
   }
   ```

   DepartmentServiceImpl

   ```java
   package com.zc.service;
   
   import com.zc.dao.DepartmentMapper;
   import com.zc.pojo.Department;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.stereotype.Service;
   
   import java.util.List;
   
   @Service
   public class DepartmentServiceImpl implements DepartmentService{
   
       @Autowired
       DepartmentMapper departmentMapper;
   
       @Override
       public List<Department> getDepartments() {
           return departmentMapper.getDepartments();
       }
   
       @Override
       public Department getDepartmentById(Integer id) {
           return departmentMapper.getDepartmentById(id);
       }
   }
   ```

   EmployeeService

   ```java
   package com.zc.service;
   
   import com.zc.pojo.Employee;
   
   import java.util.List;
   
   public interface EmployeeService {
   
       //  增加一个员工
       public int addEmployee(Employee employee);
   
       //  查询全部员工
       public List<Employee> getAllEmployee();
   
       //  通过id查询员工
       public Employee getEmployeeById(Integer id);
   
       //  删除员工
       public int deleteEmployee(Integer id);
   
       //  修改员工
       public int updateEmployee(Employee employee);
   }
   ```

   EmployeeServiceImpl

   ```java
   package com.zc.service;
   
   import com.zc.dao.EmployeeMapper;
   import com.zc.pojo.Employee;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.stereotype.Service;
   
   import java.util.List;
   
   @Service
   public class EmployeeServiceImpl implements EmployeeService{
   
       @Autowired
       EmployeeMapper employeeMapper;
   
       public static int staticId = 1005;
   
       @Override
       public int addEmployee(Employee employee) {
           employee.setId(staticId++);
           return employeeMapper.addEmployee(employee);
       }
   
       @Override
       public List<Employee> getAllEmployee() {
           return employeeMapper.getAllEmployee();
       }
   
       @Override
       public Employee getEmployeeById(Integer id) {
           return employeeMapper.getEmployeeById(id);
       }
   
       @Override
       public int deleteEmployee(Integer id) {
           return employeeMapper.deleteEmployee(id);
       }
   
       @Override
       public int updateEmployee(Employee employee) {
           return employeeMapper.updateEmployee(employee);
       }
   }
   ```

9. 编写controller层

   EmployeeController

   ```java
   package com.zc.controller;
   
   import com.zc.dao.DepartmentMapper;
   import com.zc.dao.EmployeeMapper;
   import com.zc.pojo.Department;
   import com.zc.pojo.Employee;
   import com.zc.service.DepartmentService;
   import com.zc.service.EmployeeService;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.stereotype.Controller;
   import org.springframework.ui.Model;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.PathVariable;
   import org.springframework.web.bind.annotation.PostMapping;
   
   import java.util.Collection;
   import java.util.List;
   
   @Controller
   public class EmployeeController {
   
       @Autowired
       EmployeeService employeeService;
       @Autowired
       DepartmentService departmentService;
   
       @GetMapping(value = "/emps")
       public String list(Model model) {
           List<Employee> employees = employeeService.getAllEmployee();
           model.addAttribute("emps", employees);
           return "emp/list";
       }
   
       @GetMapping(value = "/emp")
       public String toAddPage(Model model) {
           List<Department> departments = departmentService.getDepartments();
           model.addAttribute("departments", departments);
           return "emp/add";
       }
   
       @PostMapping(value = "/emp")
       public String addEmp(Employee employee) {
           //  添加的操作
   
           employeeService.addEmployee(employee); //调用底层业务方法保存员工信息
           return "redirect:/emps";
       }
   
       //  去员工的修改页面
       @GetMapping(value = "/emp/{id}")
       public String toUpdateEmp(@PathVariable("id") Integer id, Model model) {
           Employee employee = employeeService.getEmployeeById(id);
           model.addAttribute("emp", employee);
   
           List<Department> departments = departmentService.getDepartments();
           model.addAttribute("departments", departments);
           return "emp/update";
       }
   
       @PostMapping(value = "/updateEmp")
       public String updateEmp(Employee employee) {
           System.out.println(employee);
           employeeService.updateEmployee(employee);
           return "redirect:/emps";
       }
   
       @GetMapping(value = "/deletemp/{id}")
       public String deleteEmp(@PathVariable("id") Integer id) {
           employeeService.deleteEmployee(id);
           return "redirect:/emps";
       }
   }
   ```

   LoginController

   ```java
   package com.zc.controller;
   
   import org.springframework.stereotype.Controller;
   import org.springframework.ui.Model;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestParam;
   import org.springframework.web.bind.annotation.ResponseBody;
   import org.thymeleaf.util.StringUtils;
   
   import javax.servlet.http.HttpSession;
   
   @Controller
   public class LoginController {
   
       @PostMapping(value = "/user/login")
       public String login(
               @RequestParam("username") String username,
               @RequestParam("password") String password,
               Model model, HttpSession session) {
   
           //  具体业务
           if (!StringUtils.isEmpty(username) && "123456".equals(password)) {
               session.setAttribute("loginUser", username);
               return "redirect:/main.html";
           } else {
               //  告诉用户登录失败
               model.addAttribute("msg", "用户名不存在或密码错误");
               return "index";
           }
       }
   
       @GetMapping(value = "/user/logout")
       public String logout(HttpSession session) {
           session.invalidate();
           return "redirect:/index.html";
       }
   }
   ```

10. 其他配置

    1. 拦截未登录的请求

       com.zc.config.LoginHandlerIntercepter

       ```java
       package com.zc.config;
       
       import org.springframework.web.servlet.HandlerInterceptor;
       
       import javax.servlet.http.HttpServletRequest;
       import javax.servlet.http.HttpServletResponse;
       
       public class LoginHandlerIntercepter implements HandlerInterceptor {
           @Override
           public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
       
               //  登录成功之后，应该有用户的session：
       
               Object loginUser = request.getSession().getAttribute("loginUser");
       
               if (loginUser == null) { //没有登录
                   request.setAttribute("msg", "未授权，请先登录");
                   request.getRequestDispatcher("/index.html").forward(request, response);
                   return false;
               }
       
               return true;
           }
       }
       ```

    2. 解析国际化配置的请求

       com.zc.config.MyLocaleResolver

       ```java
       package com.zc.config;
       
       import org.springframework.web.servlet.LocaleResolver;
       import org.thymeleaf.util.StringUtils;
       
       import javax.servlet.http.HttpServletRequest;
       import javax.servlet.http.HttpServletResponse;
       import java.util.Locale;
       
       
       public class MyLocaleResolver implements LocaleResolver {
       
           //  解析请求
           @Override
           public Locale resolveLocale(HttpServletRequest httpServletRequest) {
       
               //  获取请求中的语言参数
               String language = httpServletRequest.getParameter("language");
       
               Locale locale = Locale.getDefault();    //如果没有就使用默认的
       
               //  如果请求的链接携带了国际化的参数
               if (!StringUtils.isEmpty(language)) {
                   String[] split = language.split("_");
                   //  分隔后数组中存放的分别是  国家，地区  zh，CN
                   locale = new Locale(split[0], split[1]);
               }
       
               return locale;
           }
       
           @Override
           public void setLocale(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Locale locale) {
           }
       }
       ```

    3. 扩展mvc的配置及注册配置bean

       com.zc.config.MyMvcConfig

       ```java
       package com.zc.config;
       
       import org.springframework.context.annotation.Bean;
       import org.springframework.context.annotation.Configuration;
       import org.springframework.web.servlet.LocaleResolver;
       import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
       import org.springframework.web.servlet.config.annotation.ViewControllerRegistry;
       import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;
       
       //  如果我们要扩展springmvc，官方建议我们这样去做！
       @Configuration
       public class MyMvcConfig implements WebMvcConfigurer {
           @Override
           public void addViewControllers(ViewControllerRegistry registry) {
               registry.addViewController("/").setViewName("index");
               registry.addViewController("/index.html").setViewName("index");
               registry.addViewController("/main.html").setViewName("dashboard");
           }
       
           //  自定义的国际化组件就生效了！
           @Bean
           public LocaleResolver localeResolver() {
               return new MyLocaleResolver();
           }
       
           @Override
           public void addInterceptors(InterceptorRegistry registry) {
               registry.addInterceptor(new LoginHandlerIntercepter())
                       .addPathPatterns("/**")
                       //.excludePathPatterns("/index.html","/","/user/login");
                       .excludePathPatterns("/index.html", "/", "/user/login", "/css/**", "/img/**", "/js/**");
           }
       }
       ```

    4. 国际化配置

       在resources下新建一个 i18n 的目录，在下面新建 login.properties、login_zh_CN.properties、login_en_US.properties的配置文件，如图：

       ![](http://zhaocan.fym233.cn/id5z9zqc5q)

       注意点：

       1. 配置i18n文件
       2. 如果需要在项目中进行按钮自动切换，我们需要自定义一个组件`LocaleResolver`
       3. 记得将自己的组件配置到Spring容器中`@Bean`

## SpringBoot整合Redis

说明：在SpringBoot2.x之后，原来使用的jedis被替换成为了lettuce

**jedis与lettuce的区别**

- jedis：采用的直连，多个线程操作的话，是不安全的。如果想要避免不安全的问题，需要使用jedis pool 连接池。更像BIO模式
- lettuce：采用netty，实例可以在多个线程中进行共享，不存在线程不安全的情况。可以减少线程数量。更像NIO模式

源码分析：

```java
@Bean
@ConditionalOnMissingBean(name = "redisTemplate")	//可以自定义一个redisTemplate来替换掉这个默认的
public RedisTemplate<Object, Object> redisTemplate(RedisConnectionFactory redisConnectionFactory) throws UnknownHostException {
    //	默认的 RedisTemplate 没有过多的设置，redis 对象都是需要序列化的！
    //	两个泛型都是Object类型，我们使用的时候需要强制类型转换
    RedisTemplate<Object, Object>template = new RedisTemplate<>();
    template.setConnectionFactory(redisConnectionFactory);
    return template;
}

@Bean
@ConditionalOnMissingBean	//String是redis中最常用的类型，所以单独提出了一个bean
public StringRedisTemplate stringRedisTemplate(RedisConnectionFactory redisConnectionFactory) throws UnknownHostException {
    StringRedisTemplate template = new StringRedisTemplate();
    template.setConnectionFactory(redisConnectionFactory);
    return template;
}
```

1. 导入依赖

   ```xml
   <!-- redis -->
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-data-redis</artifactId>
   </dependency>
   ```

2. 配置连接

   ```yaml
   spring:
     # 配置redis
     redis:
       host: 127.0.0.1
       port: 6379
   
   ```

3. 测试

   ```java
   @Autowired
   RedisTemplate redisTemplate;
   
   //  redisTemplate   操作不同的数据类型，api和我们的指令是一样的
   
   //	操作字符串，类似String
   	redisTemplate.opsForValue()
   //  opsForList  操作List
       redisTemplate.opsForList()
   //  opsForSet
       redisTemplate.opsForSet()
   //  opsForHash
       redisTemplate.opsForHash()
   //  opsForZSet
       redisTemplate.opsForZSet()
   //  opsForGeo
       redisTemplate.opsForGeo()
   
   //	获取redis的连接对象
   RedisConnection connection = redisTemplate.getConnectionFactory().getConnection();
   connection.flushDb();
   connection.flushAll();
   ```

   ```java
   package com.zc;
   
   import org.junit.jupiter.api.Test;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.test.context.SpringBootTest;
   import org.springframework.data.redis.connection.RedisConnection;
   import org.springframework.data.redis.core.RedisTemplate;
   
   @SpringBootTest
   class Springboot10RedisApplicationTests {
   
       @Autowired
       RedisTemplate redisTemplate;
   
       @Test
       void contextLoads() {
   
           //  redisTemplate   操作不同的数据类型，api和我们的指令是一样的
   
           redisTemplate.opsForValue().set("mykey", "赵灿");
           System.out.println(redisTemplate.opsForValue().get("mykey"));
       }
   
   }
   
   ```

   测试成功

   ![](http://zhaocan.fym233.cn/pfwpj85xw)

在控制台中查看出现乱码问题

![](http://zhaocan.fym233.cn/gsjzt262w)

源码

![](http://zhaocan.fym233.cn/aqo1s4pau6)

![](http://zhaocan.fym233.cn/kbxl665zhb)

可以编写一个自己的RedisTemplate

```java
package com.zc.config;

import com.fasterxml.jackson.annotation.JsonAutoDetect;
import com.fasterxml.jackson.annotation.PropertyAccessor;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.zc.pojo.User;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.Jackson2JsonRedisSerializer;
import org.springframework.data.redis.serializer.StringRedisSerializer;

@Configuration
public class RedisConfig {

    //  编写自己的RedisTemplate
    @Bean
    @SuppressWarnings("all")
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory factory) {
        //	我们为了自己开发方便，一般直接使用<String, Object>
        RedisTemplate<String, Object>template = new RedisTemplate<String, Object>();
        template.setConnectionFactory(factory);

        //  Json的序列化配置
        Jackson2JsonRedisSerializer<User> jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer<User>(User.class);
        ObjectMapper objectMapper = new ObjectMapper();
        objectMapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
        objectMapper.enableDefaultTyping(ObjectMapper.DefaultTyping.NON_FINAL);
        jackson2JsonRedisSerializer.setObjectMapper(objectMapper);
        //  String的序列化
        StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();

        //  key采用String的序列化方式
        template.setKeySerializer(stringRedisSerializer);
        //  hash的key也采用String的序列化方式
        template.setHashKeySerializer(stringRedisSerializer);
        //  value序列化方式采用jackson
        template.setValueSerializer(jackson2JsonRedisSerializer);
        //  hash的value序列化方式采用jackson
        template.setHashValueSerializer(jackson2JsonRedisSerializer);
        template.afterPropertiesSet();

        return template;
    }

}

```

