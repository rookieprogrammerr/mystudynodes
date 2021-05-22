### 准备环境

- JDK 1.8
- Mysql 5.7
- maven 3.6.1
- IDEA

### 回顾

- JDBC
- Mysql
- java基础
- Maven
- Junit

## 1、简介

### 1.1、什么是 MyBatis

![](https://mybatis.org/images/mybatis-logo.png)

- MyBatis 是一款优秀的**持久层框架**
- 它支持自定义 SQL、存储过程以及高级映射
- MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作
- MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

MyBatis 本是apache的一个[开源项目](https://baike.baidu.com/item/开源项目/3406069)iBatis, 2010年这个[项目](https://baike.baidu.com/item/项目/477803)由apache software foundation 迁移到了[google code](https://baike.baidu.com/item/google code/2346604)，并且改名为MyBatis 。2013年11月迁移到[Github](https://baike.baidu.com/item/Github/10145341)。

#### 如何获得 Mybatis

- maven 仓库

  ```xml
  <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
  <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.6</version>
  </dependency>
  ```

- [github](https://github.com/mybatis/mybatis-3/releases)

- [中文文档](https://mybatis.org/mybatis-3/zh/index.html)

### 1.2、什么是持久化

持久化就是将程序的数据在持久状态和瞬时状态转化的过程

#### 为什么需要持久化

有一些对象不能让他丢失

### 1.3、持久层

- 完成持久化工作的代码块
- 层界限十分明显

### 1.4、为什么需要 Mybatis

- 方便
- 简化开发
- 帮助程序员将数据存入到数据库中

#### Mybatis的优点

- 简单易学
- 灵活
- sql 和代码的分离，提高了可维护性
- 提供映射标签，支持对象与数据库的 orm 字段关系
- 提供对象关系映射标签，支持对象关系组建维护
- 提供 xml 标签，支持编写动态 sql

## 2、第一个 Mybatis 程序

思路：

1. 搭建环境
2. 导入 Mybatis
3. 编写代码
4. 测试

### 2.1、搭建环境

1、搭建数据库

```sql
CREATE DATABASE mybatis;

USE mybatis;

CREATE TABLE USER ( id INT ( 20 ) NOT NULL PRIMARY KEY, NAME VARCHAR ( 30 ) DEFAULT NULL, PASSWORD VARCHAR ( 30 ) DEFAULT NULL ) ENGINE = INNODB DEFAULT CHARSET = utf8 ;

INSERT INTO USER ( id, NAME, PASSWORD ) VALUES
( 1,'admin', '123456'),
(2,'aaa','123123' ),
(3,'bbb','123321')
```

2、新建项目

1. 新建一个 Maven 项目

2. 删除 src 目录

3. 导入 maven 依赖

   ```xml
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>5.1.47</version>
       </dependency>
       <!-- Mybatis -->
       <dependency>
           <groupId>org.mybatis</groupId>
           <artifactId>mybatis</artifactId>
           <version>3.5.6</version>
       </dependency>
       <!-- junit -->
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.12</version>
       </dependency>
   ```

### 2.2、创建一个模块

- 编写 mybatis 的核心配置文件

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-config.dtd">
  <!-- 核心配置文件 -->
  <configuration>
      <environments default="development">
          <environment id="development">
              <transactionManager type="JDBC"/>
              <dataSource type="POOLED">
                  <property name="driver" value="com.mysql.jdbc.Driver"/>
                  <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                  <property name="username" value="root"/>
                  <property name="password" value="root"/>
              </dataSource>
          </environment>
      </environments>
      <mappers>
          <mapper resource="com/zc/dao/UserMapper.xml" />
      </mappers>
  </configuration>
  ```

- 编写 mybatis 的工具类

```java
package com.zc.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

//sqlSessionFactory --> sqlSession
public class MybatisUtils {

    private static SqlSessionFactory sqlSessionFactory;

    static{
        try {
            //  使用Mybatis第一步：获取sqlSessionFactory对象
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    //  既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。
    //  SqlSession 完全包含了面向数据库执行 SQL 命令所需的所有方法

    public static SqlSession getSqlSession() {
        return sqlSessionFactory.openSession();
    }
}
```

### 2.3、编写代码

- 实体类

  ```java
  package com.zc.pojo;
  
  import lombok.Data;
  
  //  实体类
  @Data
  public class User {
      private int id;
      private String name;
      private String password;
  
      public User() {
      }
  
      public User(int id, String name, String password) {
          this.id = id;
          this.name = name;
          this.password = password;
      }
  }
  ```

- Dao接口

  ```java
  package com.zc.dao;
  
  import com.zc.pojo.User;
  
  import java.util.List;
  
  public interface UserDao {
      List<User> getUserList();
  }
  ```

- 接口实现类由 UserDaoImpl 转换为一个 Mapper 配置文件

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!-- namespace => 绑定一个对应的 Dao/Mapper 接口 -->
  <mapper namespace="org.mybatis.example.BlogMapper">
      <!-- select 查询语句 -->
      <select id="getUserList" resultType="com.zc.pojo.User">
      select * from mybatis.user
    </select>
  </mapper>
  ```

### 2.4、测试

**注意点：**

org.apache.ibatis.binding.BindingException:Type interface com.zc.dao.UserDao is not known to the MapperRegistry

- junit 测试

  ```java
  package com.zc.dao;
  
  import com.zc.pojo.User;
  import com.zc.utils.MybatisUtils;
  import org.apache.ibatis.session.SqlSession;
  import org.junit.Test;
  
  import java.util.List;
  
  public class UserDaoTest {
  
      @Test
      public void test() {
  
          //  第一步：获得 SqlSession 对象
          SqlSession sqlSession = MybatisUtils.getSqlSession();
  
          try{
              //  方式一：getMapper
              UserDao userDao = sqlSession.getMapper(UserDao.class);
              List<User> userList = userDao.getUserList();
              for(User user:userList){
                  System.out.println(user);
              }
  
              //  方式二：不推荐使用
              //List<User> userList = sqlSession.selectList("com.zc.dao.UserDao.getUserList");
          }catch (Exception e){
              e.printStackTrace();
          }finally {
              sqlSession.close();
          }
      }
  }
  ```

  可能会遇到的问题：

  1. 配置文件没有注册
  2. 绑定接口错误
  3. 方法名不对
  4. 返回类型不对
  5. Maven 导出资源问题

## 3、CRUD

#### 1、namespace

namespace 中的包名要和 Dao/Mapper 接口的包名一致

#### 2、select

选择，查询语句

- id：就是对应的 namespace 中的方法名
- resultType：SQL 语句执行的返回值
- parameterType：参数类型

1. 编写接口

   ```java
   List<User> getUserList();
   ```

2. 编写对应的 mapper 中的 sql 语句

   ```xml
   <!-- select 查询语句 -->
       <select id="getUserList" resultType="com.zc.pojo.User">
           select * from mybatis.user
       </select>
   ```

3. 测试

   ```java
   @Test
       public void test() {
   
           //  第一步：获得 SqlSession 对象
           SqlSession sqlSession = MybatisUtils.getSqlSession();
   
           try{
               //  方式一：getMapper
               UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
               List<User> userList = userMapper.getUserList();
               for(User user:userList){
                   System.out.println(user);
               }
   
               //  方式二：不推荐使用
               //List<User> userList = sqlSession.selectList("com.zc.dao.UserDao.getUserList");
           }catch (Exception e){
               e.printStackTrace();
           }finally {
               sqlSession.close();
           }
       }
   ```

#### 3、Insert

```xml
<!--对象中的属性，可以直接取出来-->
<insert id="addUser" parameterType="com.zc.pojo.User" parameterType="int" resultType="com.zc.pojo.User">
	insert into mybatis.user (id, name, password) values (#{id}, #{name}, #{password});
</insert>
```

#### 4、update

```xml
<update id="updateUser" parameterType="com.zc.pojo.User" parameterType="int" resultType="com.zc.pojo.User">
	update mybatis.user set name = #{name}, password = #{password} where id = #{id};
</update>
```

#### 5、Delete

```xml
<delete id="deleteUser" parameterType="com.zc.pojo.User" parameterType="int" resultType="com.zc.pojo.User">
	delete from mybatis.user where id = #{id};
</delete>
```

**注意点：**

- 增删改需要提交事务！

#### 6、分析错误

- 标签不要匹配错
- resource 绑定 mapper，需要使用路径！
- 程序配置文件必须符合规范
- NullPointException，没有注册到资源
- 输出的 xml 文件中存在中文乱码问题
- maven 资源没有导出问题

#### 7、万能Map

假设我们的实体类，或者数据库中的表，字段或者参数过多，我们应当考虑使用 Map！

```java
int addUser2(Map<String,Object> map);
```

```xml
<insert parameterType="map">
	insert into mybatis.user (id, name, password) values (#{id}, #{name}, #{password})
</insert>
```

```java
@Test
    public void addUser2() {

        //  第一步：获得 SqlSession 对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();

        try{
            //  方式一：getMapper
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            Map<String, Object> map = new HashMap<String, Object>();
            map.put("id",4);
            map.put("name","李四");
            map.put("password","999999");
            userMapper.addUser2(map);
            sqlSession.commit();

            //  方式二：不推荐使用
            //List<User> userList = sqlSession.selectList("com.zc.dao.UserDao.getUserList");
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            sqlSession.close();
        }
    }
```

Map 传递参数，直接在 sql 中取出	【parameterType="map"】

对象传递参数，直接在 sql 中取对象的属性即可！	【parameterType="Object"】

只有一个基本类型参数的情况下，可以直接在 sql 中取到

多个参数用 Map，或者**注解**！

#### 8、模糊查询

##### 怎么写模糊查询

1. Java 代码执行的时候，传递通配符 `% %`

   ```java
   List<User> userList = mapper.getUserLike("%李%");
   ```

2. 使用`CONCAT()`函数

   ```sql
   select * from mybatis.user where name like CONCAT('%', #{name}, '%')
   ```

## 4、配置解析

### 1、核心配置文件

- mybatis-config.xml

- Mybatis 的配置文件包含了会深深影响 Mybatis 行为的设置和属性信息。

  ```xml
  configuration (配置)
  properties (属性)
  settings (设置)
  typeAliases (类型别名)
  typeHandlers (类型处理器)
  objectFactory (对象工厂)
  plugins (插件)
  environments (环境变量)
  transactionManager (事务管理器)
  dataSource (数据源)
  databaseIdProvider (数据库厂商标识)
  mappers (映射器)
  ```

### 2、环境变量（environments）

Mybatis 可以配置成适应多种环境

**不过要记住：尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。**

Mybatis 默认的事务管理器就是 **JDBC**，连接池：**POOLED**

### 3、属性（properties）

我们可以通过 properties 属性来实现引用配置文件

这些属性都可以外部配置且可动态替换的，既可以在典型的 Java 属性文件中配置，亦可通过 properties 元素的子元素来传递。

编写一个配置文件

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;serverTimezone=UTC
username=root
password=root
```

在核心配置文件中引入

**注意：properties必须写在最上面**

```xml
<!-- 引入外部配置文件 -->
    <properties resource="db.properties">
        <property name="username" value="root"/>
        <property name="password" value="root3306"/>
    </properties>
```

- 可以直接引入外部文件
- 可以在其中增加一些属性配置
- 如果两个文件有同一个字段，优先使用外部配置文件

### 4、类型别名（typeAliases）

- 类型别名是为 Java 类型设置一个短的名字
- 存在的意义仅在于用来减少类完全限定名的冗余

```xml
<!-- 类型别名 -->
    <!-- 可以给实体类起别名 -->
    <typeAliases>
        <typeAlias type="com.zc.pojo.User" alias="User" />
    </typeAliases>
```

也可以指定一个包名，Mybatis 会在包名下搜索需要的 Java Bean，比如：

扫描实体类的包，它的默认别名就为这个类的类名，首字母小写

```xml
<typeAliases>
	<package name="com.zc.pojo" />
</typeAliases>
```

在实体类比较少的情况下使用第一种

如果实体类十分多，建议使用第二种

第一种可以 DIY 别名，第二种则"不行"，如果非要改，需要在实体类上增加注解

```java
@Alias("User")
public class User {
}
```

### 5、设置

|     **设置名**     |                           **描述**                           |                          **有效值**                          | **默认值** |
| :----------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :--------: |
|    cacheEnabled    |   全局性地开启或关闭所有映射器配置文件中已配置的任何缓存。   |                          true/false                          |    true    |
| lazyLoadingEnabled | 延迟加载的全局开关。当开启时，所有关联对象都会延迟加载。 特定关联关系中可通过设置 `fetchType` 属性来覆盖该项的开关状态。 |                          true/false                          |   false    |
|      logImpl       |    指定 MyBatis 所用日志的具体实现，未指定时将自动查找。     | SLF4J/LOG4J/LOG4J2/JDK_LOGGING/COMMONS_LOGGING/STDOUT_LOGGING/NO_LOGGING |   未设置   |



### 6、其他配置

- [typeHandlers（类型处理器）](https://mybatis.org/mybatis-3/zh/configuration.html#typeHandlers)
- [objectFactory（对象工厂）](https://mybatis.org/mybatis-3/zh/configuration.html#objectFactory)
- [plugins 插件](https://mvnrepository.com/artifact/org.mybatis.generator/mybatis-generator-core)
  - mybatis-generator-core
  - mybatis-plus
  - 通用mapper

### 7、映射器（mappers）

MapperRegistry：注册绑定我们的 Mapper 文件

方式一：【推荐使用】

```xml
<!-- 每一个 Mapper.xml 都需要在 Mybatis 核心配置文件中注册 -->
<mappers>
	<mapper resource="com/zc/dao/UserMapper.xml" />
</mappers>
```

方式二：使用 class 文件绑定注册

```xml
<!-- 每一个 Mapper.xml 都需要在 Mybatis 核心配置文件中注册 -->
<mappers>
	<mapper class="com.zc.dao.UserMapper" />
</mappers>
```

**注意点：**

- 接口和他的 Mapper 配置文件必须同名
- 接口和他的 Mapper 配置文件必须在同一个包下

方式三：使用扫描包进行注入绑定

```xml
<!-- 每一个 Mapper.xml 都需要在 Mybatis 核心配置文件中注册 -->
<mappers>
	<package name="com.zc.dao" />
</mappers>
```

**注意点：**

- 接口和他的 Mapper 配置文件必须同名
- 接口和他的 Mapper 配置文件必须在同一个包下

### 8、生命周期和作用域

![](https://i.loli.net/2021/02/05/57uPdlyq2rmKwFM.png)

生命周期和作用域是至关重要的，因为错误的使用会导致非常严重的**并发问题**。

#### SqlSessionFactoryBuilder：

- 一旦创建了 SqlSessionFactory，就不再需要它了
- 局部变量

#### SqlSessionFactory

- 说白了就是可以想象为：数据库连接池
- SqlSessionFactory 一旦被创建就应该在应用的运行期间一直存在，**没有任何理由丢弃它或重新创建一个实例**。
- 因此SqlSessionFactory 的最佳作用域是应用作用域。
- 最简单的就是使用**单例模式**或者静态单例模式

#### SqlSession

- 连接到连接池的一个请求
- SqlSession 的实例不是线程安全的，因此是不能被共享的
- 用完之后需要赶紧关闭，否则资源被占用

![](https://i.loli.net/2021/02/05/sgFdW8BqNUVHTGm.png)

这里面每一个 Mapper，就代表一个具体的业务

## 5、解决属性名和字段名不一致的问题

### 1、问题

数据库中的字段

![](https://i.loli.net/2021/02/05/YzOqFHDgrox3hUI.png)

新建一个项目，拷贝之前的，测试实体类字段不一致的情况

```java
public class User {
    private int id;
    private String name;
    private String pwd;
}   
```

测试出现问题

![](https://i.loli.net/2021/02/05/dILKRelbi4WEojV.png)

解决方法：

- 起别名

  ```xml
  <select id="getUserById" resultType="com.zc.pojo.User">
  	select id,name,password as pwd from mybatis.user where id = #{id}
  </select>
  ```

### 2、resultMap

结果集映射

```xml
<!-- 结果集映射 -->
<resultMap id="UserMap" type="User">
	<!--column对应数据库中的字段，property对应实体类中的属性-->
    <result column="id" property="id" />
    <result column="name" property="name" />
    <result column="password" property="pwd" />
</resultMap>

<select id="getUserById" resultMap="UserMap">
	select * from mybatis.user where id = #{id}
</select>
```

- resultMap 元素是 Mybatis 中最重要最强大的元素
- resultMap 的设计思想是，对于简单的语句根本不需要配置显示的结果映射，而对于复杂一点的语句只需要描述它们的关系就行了。
- resultMap 最优秀的地方在于，虽然你已经对它相当了解了，但是根本不需要显示地用到他们

![](https://i.loli.net/2021/02/05/StZN2YER7UL4aAs.png)

## 6、日志

### 6.1、日志工厂

如果一个数据库操作，出现了异常，我们需要排错。日志就是最好的助手

![](http://zhaocan.fym233.cn/QQ%E6%88%AA%E5%9B%BE20210206112805.png)

- SLF4J
-  LOG4J 【重点掌握】
-  LOG4J2
- JDK_LOGGING
-  COMMONS_LOGGING 
- STDOUT_LOGGING 【重点掌握】
-  NO_LOGGING

在 Mybatis 中具体使用哪一个日志实现，在设置中设定

**STDOUT_LOGGING 标准日志输出**



```xml
<settings>
        <!-- 标准的日志工厂实现 -->

        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
```

![](http://zhaocan.fym233.cn/QQ%E6%88%AA%E5%9B%BE20210206112805.png)

### 6.2、Log4j

什么是 Log4j

- Log4j 是 Apache 的一个开源项目，通过使用 Log4j，我们可以控制日志信息输送的目的地是控制台、文件、GUI 组件

- 我们也可以控制每一条日志的输出格式

- 通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程

- 通过一个配置文件来灵活地进行配置，而不需要修改应用的代码

  

1. 先导入 Log4j 的包

   ```xml
   <!-- https://mvnrepository.com/artifact/log4j/log4j -->
   <dependency>
       <groupId>log4j</groupId>
       <artifactId>log4j</artifactId>
       <version>1.2.17</version>
   </dependency>
   ```

2. log4j.properties

   

   ```properties
   # 将登记为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
   log4j.rootLogger=DEBUG,console,file
   
   # 控制台输出的相关设置
   log4j.appender.console = org.apache.log4j.ConsoleAppender
   log4j.appender.console.Target = System.out
   log4j.appender.console.Threshold = DEBUG
   log4j.appender.console.layout = org.apache.log4j.PatternLayout
   log4j.appender.console.layout.ConversionPattern = [%c]-%m%n
   
   # 文件输出的相关设置
   log4j.appender.file = org.apache.log4j.RollingFileAppender
   log4j.appender.file.File = ./log/zc.log
   log4j.appender.file.MaxFileSize = 10mb
   log4j.appender.file.Threshold = DEBUG
   log4j.appender.file.layout = org.apache.log4j.PatternLayout
   log4j.appender.file.layout.ConversionPattern = [%p][%d{yy-MM-dd}][%c]%m%n
   
   # 日志输出级别
   log4j.logger.org.mybatis = DEBUG
   log4j.logger.java.sql = DEBUG
   log4j.logger.java.sql.Statement = DEBUG
   log4j.logger.java.sql.ResultSet = DEBUG
   log4j.logger.java.sql.PreparedStatement = DEBUG
   ```

3. 配置 log4j 为日志的实现

   ```xml
   <settings>
   	<setting name="logImpl" value="LOG4J"/>
   </settings>
   ```

4. Log4j 的使用，直接测试运行刚才的查询

   ![](![](https://i.loli.net/2021/02/07/7Q6BeHZjrTlzScq.png)

**简单使用**

1. 在要使用 Log4j 的类中，导入包 `import org.apache.log4j.Logger;`

2. 日志对象，参数为当前类的class

   ```java
   static Logger logger = Logger.getLogger(UserDaoTest.class);
   ```

3. 日志级别

   ```java
   logger.info("info：进入了testLog4j");
   logger.debug("debug：进入了testLog4j");
   logger.error("error：进入了testLog4j");
   ```

## 7、分页

**为什么要分页**

- 减少数据的处理量

### 7.1、使用 Limit 分页

```sql
select * from user limit 0,2
```

**使用Mybatis实现分页**，核心就是 SQL

1. 接口

   ```java
   List<User> getUserByLimit(Map<String, Integer> map);
   ```

2. Mapper.xml

   ```xml
   <!-- 分页 -->
   <select id="getUserByLimit" parameterType="map" resultMap="UserMap">
   	select * from mybatis.user limit #{startIndex},#{pageSize}
   </select>
   ```

3. 测试

   ```java
   @Test
       public void getUserByLimit() {
           SqlSession sqlSession = MybatisUtils.getSqlSession();
           UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
   
           Map<String, Integer> map = new HashMap<String, Integer>();
           map.put("startIndex",0);
           map.put("pageSize",2);
           List<User> userList = userMapper.getUserByLimit(map);
   
           for(User user : userList) {
               logger.info(user);
           }
           
           sqlSession.close();
       }
   ```

### 7.2、RowBounds分页

不再使用 SQL 实现分页

1. 接口

   ```java
   List<User> getUserByRowBounds(Map<String, Integer> map);
   ```

2. Mapper.xml

   ```xml
   <!-- 分页 -->
   <select id="getUserByRowBounds" resultMap="UserMap">
   	select * from mybatis.user
   </select>
   ```

3. 测试

   ```java
   @Test
       public void getUserByRowBounds() {
           SqlSession sqlSession = MybatisUtils.getSqlSession();
   
           // RowBounds 实现
           RowBounds rowBounds = new RowBounds(1, 2);
   
           //通过Java代码层面实现分页
           List<User> userList = sqlSession.selectList("com.zc.dao.UserMapper.getUserByRowBounds",null,rowBounds);
   
           for(User user : userList) {
               logger.info(user);
           }
   
           sqlSession.close();
       }
   ```

### 7.3、分页插件

![](https://i.loli.net/2021/02/07/xMLRzgKYT51tdwc.png)

[官方文档](https://pagehelper.github.io/)

## 8、使用注解

### 8.1、什么是面向接口编程

-大家之前都学习过面相对象编程，也学习过接口，但在真正的开发中，很多时候我们会选择面向接口编程

-**根本原因：解耦，可拓展，提高复用，分层开发中，上层不用管具体的实现，大家都遵守共同的标准，使得开发变得容易，规范性更好**

-在一个面向对象的系统中，系统的各种功能是由许许多多的不同对象协作完成的。在这种情况下，各个对象内部是如何实现自己的，对系统设计人员来讲就不那么重要了。

-而各个对象之间的协作关系则成为系统设计的关键。小到不同类之间的通信，大到各模块之间的交互，在系统设计之初都是要着重考虑的，这也是系统设计的主要工作内容。面向接口编程就是指按照这种思想来编程。

**关于接口的理解**

-接口从深层次的理解，应是定义（规范，约束）与实现（名实分离的原则）的分离。

-接口的本身反映了系统设计人员对系统的抽象理解。

-接口应有两类

​	-第一类是对一个个体的抽象，它可对应为一个抽象体(abstract class);

​	-第二类是对一个个体某一方面的抽象，即形成一个抽象面(interface);

-一个体有可能有多个抽象面。抽象体与抽象面是有区别的。

**三个面向区别**

- 面向对象是指，我们考虑问题时，以对象为单位，考虑它的属性及方法
- 面向过程是指，我们考虑问题时，以一个具体的流程（事物过程）为单位，考虑它的实现
- 接口设计与非接口设计是针对复用技术而言的，与面向对象（过程）不是一个问题，更多的体现就是对系统整体的架构

### 8.2、使用注解开发

1. 注解在接口上实现

   ```java
   @Select(value = "select * from user")
   List<User> getUsers();
   ```

2. 需要在核心配置文件中绑定接口

   ```xml
   <!-- 绑定接口 -->
   <mappers>
   	<mapper class="com.zc.dao.UserMapper" />
   </mappers>
   ```

3. 测试

   ```java
   @Test
   public void test() {
   	SqlSession sqlSession = MybatisUtils.getSqlSession();
   
   	//  底层主要应用反射
   	UserMapper mapper = sqlSession.getMapper(UserMapper.class);
   	List<User> userList = mapper.getUsers();
   	for(User user : userList) {
   		System.out.println(user);
   	}
   
   	sqlSession.close();
   }
   ```

**本质：反射机制实现**

**底层：动态代理**

![](https://i.loli.net/2021/02/07/INvKZCgzoEQsFrk.png)

**Mybatis 详细的执行流程**

![](https://i.loli.net/2021/02/07/LlOJNy8qv3HXeWx.png)

### 8.3、CRUD

我们可以在工具类创建的时候实现自动提交事务

```java
public static SqlSession getSqlSession() {
    return sqlSessionFactory.openSession(true);
}
```

编写接口，增加注解

```java
@Select(value = "select * from user")
List<User> getUsers();

//  方法存在多个参数，所有的参数前面必须加上@Param
@Select(value = "select * from user where id = #{id}")
User getUserById(@Param("id") int id);

@Insert(value = "insert into user(id, name, password) values(#{id}, #{name}, #{password})")
int addUser(User user);

@Update(value = "update user set name = #{name}, password = #{password} where id = #{id}")
int updateUser(User user);

@Delete(value = "delete from user where id = #{id}")
int deleteUser(@Param("id") int id);
```

测试类

```java
@Test
public void test() {
	SqlSession sqlSession = MybatisUtils.getSqlSession();

//  底层主要应用反射
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    List<User> userList = mapper.getUsers();
    for(User user : userList) {
        System.out.println(user);
    }

    sqlSession.close();
}

@Test
public void getUserById() {
    SqlSession sqlSession = MybatisUtils.getSqlSession();

    //  底层主要应用反射
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    User user = mapper.getUserById(1);
    System.out.println(user);

    sqlSession.close();
}

@Test
public void addUser() {
    SqlSession sqlSession = MybatisUtils.getSqlSession();

    //  底层主要应用反射
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    User user = new User(6,"李四","999999");
    mapper.addUser(user);

    sqlSession.close();
}

@Test
public void updateUser() {
    SqlSession sqlSession = MybatisUtils.getSqlSession();

    //  底层主要应用反射
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    User user = new User(6,"李八","888888");
    mapper.updateUser(user);

    sqlSession.close();
}

@Test
public void deleteUser() {
    SqlSession sqlSession = MybatisUtils.getSqlSession();

    //  底层主要应用反射
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    mapper.deleteUser(6);

    sqlSession.close();
}
```

**注意：我们必须要将接口注册绑定到我们的核心配置文件中**

**关于 `@Param()`注解**

- 基本类型的参数或 String 类型需要加上
- 引用类型不需要加
- 如果只有一个基本类型的话，可以省略。建议加上
- 在SQL中引用的就是我们这里的`@Param()`中设定的属性名

**`#{}`与`${}`的区别**

- `#{}`解析为一个 JDBC 预编译语句（prepared statement）的参数标记符占位符 `？`
- `${ }` 仅仅为一个纯碎的 String 替换，在 Mybatis 的动态 SQL 解析阶段将会进行变量替换

## 9、Lombok

-  java library
- plugs
- build tools
- with one annotation your class

**使用步骤**

1. 在 IDEA 安装 Lombok 插件

2. 在项目中导入 Lombok 的 jar 包

   ```xml
   <!-- Lombok -->
   <dependency>
   	<groupId>org.projectlombok</groupId>
   	<artifactId>lombok</artifactId>
   	<version>1.18.10</version>
   </dependency> 
   ```

3. 在实体类上加注解即可

   ```java
   @Data
   @AllArgsConstructor
   @NoArgsConstructor
   public class User {
       private int id;
       private String name;
       private String password;
   
   }
   ```

**说明**

- @Data：无参构造、get、set、toString、hashcode、equals
- AllArgsConstructor：有参构造
- NoArgsConstructor：无参构造

**Lombok 的优缺点**

优点：

1. 能通过注解的形式自动生成构造器、getter/setter、equals、hashcode、toString 等方法，提高了一定的开发效率
2. 让代码变得简洁，不用过多的去关注相应的方法
3. 属性做修改时，也简化了维护这些属性所生成的 getter/setter 方法等

缺点：

1. 不支持多种参数构造器的重载
2. 虽然省去了手动创建 getter/setter 方法的麻烦，但大大降低了源代码的可读性和完整性，降低了阅读源代码的舒适度

## 10、多对一处理

![](https://i.loli.net/2021/02/08/UWBDw6uLHAiNsdv.png)

- 多个学生，对应一个老师
- 对于学生而言，`关联`多个学生，关联一个老师【多对一】
- 对于老师而言，`集合`，一个老师有多个学生【一对多】

```sql
CREATE TABLE `teacher` INSERT INTO teacher (`id`, `NAME`)
VALUES
	(1, '秦老师') ; CREATE TABLE `student` (
		`id` INT (10) NOT NULL,
		`name` VAR

INSERT INTO teacher (`id`, `NAME`)
VALUES
	(1, '秦老师')CHAR (30) DEFAULT NULL,
	`tid` INT (10) DEFAULT NULL,
	PRIMARY KEY (`id`),
	KEY `fktid` (`tid`),
	CONSTRAINT `fktid` FOREIGN KEY (`tid`) REFERENCES `teacher` (`id`)
) ENGINE = INNODB DEFAULT CHARSET = utf8;

INSERT INTO `student` (`id`, `name`, `tid`)
VALUES
	('1', '小明', '1');

INSERT INTO `student` (`id`, `name`, `tid`)
VALUES
	('2', '小红', '1');

INSERT INTO `student` (`id`, `name`, `tid`)
VALUES
	('3', '小张', '1');

INSERT INTO `student` (`id`, `name`, `tid`)
VALUES
	('4', '小李', '1');

INSERT INTO `student` (`id`, `name`, `tid`)
VALUES
	('5', '小王', '1');
```

### 测试环境搭建

1. 导入 lombok
2. 新建实体类 Teacher，Student
3. 建立 Mapper 接口
4. 建立 Mapper.xml 文件
5. 在核心配置文件中绑定注册我们的 Mapper 接口或者文件
6. 测试查询是否能够成功

### 按照查询嵌套处理

```xml
<!--
    思路：
        1、查询所有的学生信息
        2、根据查询出来的学生的tid，寻找对应的老师
    -->

<select id="getStudent" resultMap="StudentTeacher">
    select * from student
</select>

<resultMap id="StudentTeacher" type="Student">
    <result property="id" column="id" />
    <result property="name" column="name" />
    <!-- 复杂的属性，我们需要单独处理 -->
    <!-- 对象：association   集合：collection -->
    <association property="teacher" column="tid" javaType="Teacher" select="getTeacher"/>
</resultMap>

<select id="getTeacher" resultType="Teacher">
    select * from teacher where id = #{id}
</select>
```

### 按照结果嵌套处理

```xml
<!-- 按照结果嵌套处理 -->
<select id="getStudent2" resultMap="StudentTeacher2">
    select s.id sid,s.name sname,t.name tname from student s,teacher t where s.tid = t.id
</select>

<resultMap id="StudentTeacher" type="Student">
    <result property="id" column="sid" />
    <result property="name" column="sname" />
    <association property="teacher" javaType="Teacher" >
        <result property="name" column="tname" />
    </association>
</resultMap>
```

**回顾Mysql 多对一查询方式：**

- 子查询
- 联表查询

## 11、一对多处理

比如：一个老师拥有多个学生

对于老师而言，就是一对多的关系

### 环境搭建

实体类

```java
package com.zc.pojo;

import lombok.Data;

@Data
public class Student {
    private int id;
    private String name;
    private int tid;
}
```

```java
package com.zc.pojo;

import lombok.Data;

import java.util.List;

@Data
public class Teacher {
    private int id;
    private String name;

    //  一个老师对应多个学生
    private List<Student> students;
}
```

### 按照结果嵌套处理

```xml
<!-- 按结果嵌套查询 -->
<select id="getTeacherById" resultMap="TeacherStudent">
    select t.id tid,t.name tname,s.id sid,s.name sname from teacher t,student s where t.id = s.tid and t.id = #{id}
</select>

<resultMap id="TeacherStudent" type="Teacher">
    <result property="id" column="tid" />
    <result property="name" column="tname" />
    <!-- 复杂的属性，我们需要单独处理  对象：association   集合：collection
        javaType="" 指定属性的类型
        集合中的泛型信息，我们使用ofType获取
        -->
    <collection property="students" ofType="Student">
        <result property="id" column="sid" />
        <result property="name" column="sname" />
        <result property="tid" column="tid" />
    </collection>
</resultMap>
```

### 按照查询嵌套处理

```xml
<!-- 按查询嵌套查询 -->
<select id="getTeacherById2" resultMap="TeacherStudent2">
    select * from mybatis.teacher where id = #{id}
</select>
<resultMap id="TeacherStudent2" type="Teacher">
    <collection property="students" column="id" javaType="ArrayList" ofType="Student" select="getStudentByTeacherId" />
</resultMap>
<select id="getStudentByTeacherId" resultType="Student">
    select * from mybatis.student where tid = #{id}
</select>
```

### 小结

1. 关联 - association 【多对一】
2. 集合 - collection 【一对多】
3. javaType & ofType
   1. javaType 用来指定实现类中属性的类型
   2. ofType 用来指定映射到 List 或者集合中的 pojo 类型，泛型中的约束类型

**注意点：**

- 保证 SQL 的可读性，尽量保证通俗易懂
- 注意一对多和多对一中，属性名和字段没问题
- 如果问题不好排查错误，可以使用日志，建议使用 `Log4j`

## 12、动态 SQL

### 什么是动态 SQL

**动态SQL 就是指根据不同的条件生成不同的 SQL 语句**

利用动态SQL这一特性可以彻底摆脱这种痛苦

```java
动态 SQL 元素和 JSTL 或给予类似 xml 的文本处理器相似。在 MyBatis 之前的版本中，有很多元素需要花时间了解。MyBatis 3大大精简了元素种类。现在只需要学习原来一半的元素便可。MyBatis 采用功能强大的基于 OGNL 的表达式来淘汰其他大部分元素。
    
if
choose (when, otherwise)
trim (where, set)
foreach
```

### 搭建环境

```sql
CREATE TABLE `blog` (
    `id` varchar(50) NOT NULL COMMENT '博客id',
    `title` varchar(100) not null comment '博客标题',
    `author` varchar(30) not null comment '博客作者',
    `create_time` datetime not null comment '创建时间',
    `views` int(30) not null comment '浏览量'
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

**创建一个基础工程**

1. 导包

2. 编写配置文件

3. 编写实体类

   ```java
   @Data
   public class Blog {
       private int id;
       private String title;
       private String author;
       private Date createTime;
       private int views;
   }
   ```

4. 编写实体类对应 Mapper 接口和 Mapper.xml

### if

```java
<select id="queryBlogIf" parameterType="map" resultType="Blog">
    select * from mybatis.blog where 1=1
    <if test="title != null">
        and title = #{title}
</if>
    <if test="author != null">
        and author = #{author}
</if>
    </select>
```

### choose

```xml
<select id="queryBlogChoose" parameterType="map" resultType="Blog">
    select * from mybatis.blog where
    <where>
        <choose>
            <when test="title != null">
                title = #{title}
            </when>
            <when test="author != null">
                and author = #{author}
            </when>
            <otherwise>
                and views = #{views}
            </otherwise>
        </choose>
    </where>
</select>
```

### trim(where,set)

```xml
<select id="queryBlogIf" parameterType="map" resultType="Blog">
    select * from mybatis.blog
    <where>
    	<if test="title != null">
        	and title = #{title}
		</if>
    	<if test="author != null">
        	and author = #{author}
		</if>
    </where>
</select>
```

```xml
<update id="updateBlog" parameterType="map">
    update mybatis.blog
    <set>
        <if test="title != null">
            title = #{title},
        </if>
        <if test="author != null">
            author = #{author}
        </if>
    </set>
    where id = #{id}
</update>
```

### SQL片段

有的时候，我们可能会将一些功能的部分抽取出来，方便复用

1. 使用SQL标签抽取公共的部分

   ```xml
   <sql id="if-title-author">
       <if test="title != null">
           and title = #{title}
       </if>
       <if test="author != null">
           and author = #{author}
       </if>
   </sql>
   ```

2. 在需要使用的地方使用 `include` 标签引用即可

   ```xml
   <select id="queryBlogIf" parameterType="map" resultType="Blog">
       select * from mybatis.blog
       <where>
           <include refid="if-title-author"></include>
       </where>
   </select>
   ```

注意事项：

- 最好基于单表来定义SQL片段
- 不要存在`where`标签

### ForEach

![](https://i.loli.net/2021/02/08/fZ47XKTh6wyR9eL.png)

![](https://i.loli.net/2021/02/08/78ZRC69gowY5tBu.png)

```xml
<select id="queryBlogForEach" parameterType="map" resultType="blog">
    select * from blog
    <where>
        <foreach collection="ids" item="id" open="and (" close=")" separator="or">
            id = #{id}
        </foreach>
    </where>
</select>
```

```java
@Test
public void queryBlogForEach() {
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
    Map map = new HashMap();
    ArrayList<Integer> ids = new ArrayList<Integer>();
    ids.add(1);
    ids.add(2);

    map.put("ids",ids);

    List<Blog> blogs = mapper.queryBlogForEach(map);
    for (Blog blog : blogs) {
        System.out.println(blog);
    }

    sqlSession.close();
}
```

**动态SQL就是在拼接SQL语句，我们只要保证SQL的正确性，按照SQL的格式，去排列组合就可以了**

## 13、缓存

### 13.1、简介

1. 什么是缓存[Cache]
   - 存在内存中的临时数据
   - 将用户经常查询的数据放在缓存（内存）中，用户去查询数据就不用从磁盘上（关系型数据库数据文件）查询，从缓存中查询，从而提高查询效率，解决了高并发系统的性能问题。
2. 为什么使用缓存
   - 减少和数据库的交互次数，减少系统开销，提高系统效率
3. 什么样的数据能使用缓存
   - 经常查询并且不经常改变的数据

### 13.2、Mybatis缓存

- MyBatis包含一个非常强大的查询缓存特性，它可以非常方便地定制和配置缓存。缓存可以极大的提升查询效率
- MyBatis系统中默认定义了两级缓存：**一级缓存**和**二级缓存**
  - 默认情况下，只有一级缓存开启。（SqlSession级别的缓存，也称为本地缓存）
  - 二级缓存需要手动开启和配置，他是基于`namespace`级别的缓存。
  - 为了提高扩展性，MyBatis定义了缓存接口Cache。我们可以通过实现Cache接口来自定义二级缓存

### 13.3、一级缓存

- 一级缓存也叫本地缓存：
  - 与数据库同一次会话期间查询到的数据会放到本地缓存中
  - 以后如果需要获取相同的数据，直接从缓存中拿，没必须再去查询数据库

测试步骤：

1. 开启日志

2. 测试在一个Session中查询两次相同记录

3. 查看日志输出

   ![](https://i.loli.net/2021/02/08/EzlVbGY2FcCAdOS.png)

缓存失效的情况：

1. 查询不同的东西

2. 增删改操作，可能会改变原来的数据，所以必定会刷新缓存

   ![](https://i.loli.net/2021/02/08/dZsAuykGPbXaQTJ.png)

3. 查询不同的Mapper

4. 手动清理缓存

   ![](https://i.loli.net/2021/02/08/9CosTuadEmkfYJS.png)

小结：一级缓存默认是开启的，只在一次SqlSession中有效，也就是拿到连接到关闭连接这个区间段

### 13.4、二级缓存

- 二级缓存也叫全局缓存，一级缓存作用域太低了，所以诞生了二级缓存
- 基于`namespace`级别的缓存，一个名称空间，对应一个二级缓存
- 工作机制：
  - 一个会话查询一条数据，这个数据就会被放在当前会话的一级缓存中
  - 如果当前会话关闭了，这个会话对应的一级缓存就没了；但是我们想要的是，会话关闭了，一级缓存中的数据会被保存到二级缓存中；
  - 新的会话查询信息，就可以从二级缓存中获取内容

步骤：

1. 开启缓存

   ```xml
   <!-- 显示的开启全局缓存 -->
   <setting name="cacheEnabled" value="true"/>
   ```

2. 在要使用二级缓存的Mapper中开启

   ```xml
   <!-- 在当前Mapper.xml中使用二级缓存 -->
   <cache />
   ```

   也可以自定义参数

   ```xml
   <cache
     eviction="FIFO"
     flushInterval="60000"
     size="512"
     readOnly="true"/>
   
   # LRU – 最近最少使用：移除最长时间不被使用的对象。
   # FIFO – 先进先出：按对象进入缓存的顺序来移除它们。(first input first output)
   # SOFT – 软引用：基于垃圾回收器状态和软引用规则移除对象。
   # WEAK – 弱引用：更积极地基于垃圾收集器状态和弱引用规则移除对象。
   ```

3. 测试

   1. 问题：我们需要将实体类序列化，否则就会报错

      ```java
      caused by: java.io.NotSerializableException: com.zc.pojo.User
      ```

小结：

- 只要开启了二级缓存，在同一个Mapper下就有效
- 所有的数据都会先放在一级缓存中；
- 只有当会话提交或者关闭的时候才会提交到二级缓存中

### 13.5、缓存原理

![](https://i.loli.net/2021/02/08/THyiAox2GwQlKf7.png)

### 13.6、自定义缓存 - ehcache

Ehcache 是一种广泛使用的开源Java分布式缓存。主要面向通用缓存

要在程序中使用ehcache，先导包

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.caches/mybatis-ehcache -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.1.0</version>
</dependency>
```

在mapper中指定使用我们的ehcache缓存实现

```xml
<!-- 在当前Mapper.xml中使用二级缓存 -->
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

ehcache.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
         updateCheck="false">
    <!--
       diskStore：为缓存路径，ehcache分为内存和磁盘两级，此属性定义磁盘的缓存位置。参数解释如下：
       user.home – 用户主目录
       user.dir  – 用户当前工作目录
       java.io.tmpdir – 默认临时文件路径
     -->
    <diskStore path="./tmpdir/Tmp_EhCache"/>
    
    <defaultCache
            eternal="false"
            maxElementsInMemory="10000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="259200"
            memoryStoreEvictionPolicy="LRU"/>
 
    <cache
            name="cloud_user"
            eternal="false"
            maxElementsInMemory="5000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="1800"
            memoryStoreEvictionPolicy="LRU"/>
    <!--
       defaultCache：默认缓存策略，当ehcache找不到定义的缓存时，则使用这个缓存策略。只能定义一个。
     -->
    <!--
      name:缓存名称。
      maxElementsInMemory:缓存最大数目
      maxElementsOnDisk：硬盘最大缓存个数。
      eternal:对象是否永久有效，一但设置了，timeout将不起作用。
      overflowToDisk:是否保存到磁盘，当系统当机时
      timeToIdleSeconds:设置对象在失效前的允许闲置时间（单位：秒）。仅当eternal=false对象不是永久有效时使用，可选属性，默认值是0，也就是可闲置时间无穷大。
      timeToLiveSeconds:设置对象在失效前允许存活时间（单位：秒）。最大时间介于创建时间和失效时间之间。仅当eternal=false对象不是永久有效时使用，默认是0.，也就是对象存活时间无穷大。
      diskPersistent：是否缓存虚拟机重启期数据 Whether the disk store persists between restarts of the Virtual Machine. The default value is false.
      diskSpoolBufferSizeMB：这个参数设置DiskStore（磁盘缓存）的缓存区大小。默认是30MB。每个Cache都应该有自己的一个缓冲区。
      diskExpiryThreadIntervalSeconds：磁盘失效线程运行时间间隔，默认是120秒。
      memoryStoreEvictionPolicy：当达到maxElementsInMemory限制时，Ehcache将会根据指定的策略去清理内存。默认策略是LRU（最近最少使用）。你可以设置为FIFO（先进先出）或是LFU（较少使用）。
      clearOnFlush：内存数量最大时是否清除。
      memoryStoreEvictionPolicy:可选策略有：LRU（最近最少使用，默认策略）、FIFO（先进先出）、LFU（最少访问次数）。
      FIFO，first in first out，这个是大家最熟的，先进先出。
      LFU， Less Frequently Used，就是上面例子中使用的策略，直白一点就是讲一直以来最少被使用的。如上面所讲，缓存的元素有一个hit属性，hit值最小的将会被清出缓存。
      LRU，Least Recently Used，最近最少使用的，缓存的元素有一个时间戳，当缓存容量满了，而又需要腾出地方来缓存新的元素的时候，那么现有缓存元素中时间戳离当前时间最远的元素将被清出缓存。
   -->

</ehcache>
```

