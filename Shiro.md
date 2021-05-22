# 1、Shiro简介

## 1.1、什么是Shiro

- Apache Shiro是一个Java安全（权限）框架
- Shiro 可以非常容易的开发出足够好的应用，其不仅可以用在JavaSE环境，也可以用在JavaEE环境
- Shiro可以完成认证、授权、加密、会话管理、Wen集成、缓存等
- 下载地址：[http://shiro.apache.org/](http://shiro.apache.org/)
- ![](http://zhaocan.fym233.cn/ue6b39x7i)

## 1.2、有哪些功能

![](http://zhaocan.fym233.cn/elc099nhn)

- Authentication：身份认证、登录、验证用户是不是拥有相应的身份
- authorization：授权，即权限验证。验证某个已认证的用户是否拥有某个权限，即判断用户能否进行什么操作。如：验证某个用户是否拥有某个角色，或者细粒度的验证某个用户对某个资源是否具有某个权限
- Session Manager：会话管理，即用户登录后就是第一次会话，在没有退出之前，它的所有信息都在会话中；会话可以是普通的JavaSE环境，也可以是Web环境；
- Cryptography：加密，保护数据的安全性，如密码加密存储到数据库中，而不是明文存储；
- Web Support：Web支持，可以非常容易的集成到Web环境；
- Caching：缓存，比如用户登录后，其用户信息，拥有的角色、权限不必每次去查，这样可以提高效率
- Concurrency：Shiro支持多线程应用的并发验证，即：如在一个线程中开启另一个线程，能把权限自动的传播过去
- Testing：提供测试支持
- Run As：允许一个用户假装为另一个用户（如果他们允许）的身份进行访问
- Remember Me：记住我，这个是非常常见的，即登陆一次后，下次再来的话不用登录了

**记住一点，Shiro不会去维护用户、维护权限；这些需要我们自己去设计/提供；然后通过相应的接口注入给Shiro即可。**

## 1.3、Shiro架构（外部）

从外部来看Shiro，即从应用程序角度来观察如何使用Shiro完成工作！

![](https://i04piccdn.sogoucdn.com/82b8dcc27f049213)

- **subject**：应用代码直接交互的对象是Subject, 也就是说Shiro的对外API核心就是Subject, Subject代表了当前的用户，这个用户不一定是一个具体的人， 与当前应用交互的任何东西都是Subject,如网络爬虫，机器人等，与Subject的所有交互都会委托给SecurityManager; Subject其实是一个门面，SecurityManager 才是实际的执行者

  ```java
  Subject subject = SecurityUtils.getSubject();
  
  subject.login();
  ```

  

- **SecurityManager**：安全管理器，即所有与安全有关的操作都会与SecurityManager交互， 并且它管理着所有的Subject,可以看出它是Shiro的核心，它负责与Shiro的其他组件进行交互，它相当于SpringMVC的DispatcherServlet的角色

  ```java
  @Bean
  public SecurityManager securityManager() {
      DefaultWebSecurityManager securityManager = new DefaultWebSecurityManager();
      // 设置realm
      securityManager.setRealm(myShiroRealm());
      // 记住我
      securityManager.setRememberMeManager(rememberMeManager());
      // 自定义缓存实现 使用redis
      securityManager.setCacheManager(redisCacheManager());
      // 自定义session管理 使用redis
      securityManager.setSessionManager(sessionManager());
      return securityManager;
  }
  ```

  

- **Realm**：Shiro从Realm获取安全数据(如用户，角色，权限)，就是说SecurityManager 要验证用户身份，那么它需要从Reaim获取相应的用户进行比较，来确定用户的身份是否合法:也需要从Realm得到用户相应的角色、权限，进行验证用户的操作是否能够进行，可以把Realm看成DataSource;

  ```java
  public class MyRealm extends AuthorizingRealm {
  
    @Override
    protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
      // 认证
      return null;
    }
  
    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken authenticationToken)
        throws AuthenticationException {
      // 授权
      return null;
    }
  }
  ```

- **Filter链**：Shiro通过其创新的URL过滤器链功能支持安全特定的过滤规则，它允许你为任何匹配的URL模式指定非正式的过滤器链。

## 1.4、Shiro架构（内部）

![](https://oscimg.oschina.net/oscnet/da22194d3e8d9e7a7c8027d40843a37e302.jpg)

- **Subject**：任何可以与应用交互的“用户”
- **Security Manager**：相当于SpringMVC中的DispatcherServlet；是Shiro的心脏，所有具体的交互都通过SecurityManager进行控制，它管理着所有的Subject，且负责进行认证、授权、会话及缓存的管理
- **Authenticator**：负责Subject认证，是一个扩展点，可以自定义实现；可以使用认证策略（Authentication Strategy），即什么情况下算用户认证通过了
- **Authorizer**：授权器，即访问控制器，用来决定主体是否有权限进行相应的操作；即控制着用户能访问应用中哪些功能
- **Realm**：可以有一个或者多个的realm，可以认为是安全实体数据源，即用于获取安全实体的，可以用JDBC实现，也可以是内存实现等等，由用户提供；所以一般在应用中都需要实现自己的realm
- **SessionManager**：管理Session生命周期的组件，而Shiro并不仅仅可以用在Web环境下，也可以用在普通的JavaSE环境中
- **CacheManager**：缓存控制器，来管理如用户、角色、权限等缓存的；因为这些数据基本上很少改变，放到缓存中后可以提高访问的性能
- **Cryptography**：密码模块，Shiro提高了一些常见的加密组件用于密码加密，解密等

# 2、HelloWorld

## 2.1、快速实践

查看官网文档：[http://shiro.apache.org/tutorial.html](http://shiro.apache.org/tutorial.html)

官方的quickstart：[https://github.com/apache/shiro/tree/master/samples/quickstart/](https://github.com/apache/shiro/tree/master/samples/quickstart/)

1. 创建一个Maven父工程，用于学习Shiro，删掉不必要的东西

2. 创建一个普通的Maven子工程：shiro-01-helloworld

3. 根据官方文档，我们来导入Shiro的依赖

   ```xml
   <dependencies>
   	<dependency>
       	<groupId>org.apache.shiro</groupId>
       	<artifactId>shiro-core</artifactId>
       	<version>1.4.1</version>
       </dependency>
       <!-- Shiro uses SLF4J for logging. We'll use the 'simple' binding in this example app. See http://www.slf4j.org for more info. -->
       <dependency>
       	<groupId>org.slf4j</groupId>
           <artifactId>slf4j</artifactId>
           <version>1.7.21</version>
           <scope>test</scope>
       </dependency>
   </dependencies>
   ```

   