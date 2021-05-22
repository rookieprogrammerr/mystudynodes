# MySQL学习笔记

## 1、初识数据库

### 1.1、为什么要学习数据库

1. 岗位需求
2. 现在的世界，大数据时代
3. 被迫需求：存数据
4. 数据库是所有软件体系中最核心的存在

### 1.2、什么是数据库

数据库（DB：DataBase）

概念：数据仓库，**软件**。安装在各大操作系统之上（Windows、Linux、....），可以存储大量的数据

作用：存储数据，管理数据

### 1.3、数据库分类

**关系型数据库**：有结构有组织的，以行和列组成

- MySQL，Oracle，SQLServer，DB2、SQLite
- 通过表和表之间，行和列之间的关系进行数据的存储

**（SQL）**

**非关系型数据库**：类似于json之类的，存储着key-value键值对

- Redis，MongDB
- 非关系型数据库，以对象存储，通过对象的自身属性来决定

**（NoSQL：Not only SQL）**



**DBMS（数据库管理系统）**

- 数据库的管理软件，科学有效的管理我们的数据。维护和获取数据
- MySQL，数据库管理系统

### 1.4、MySQL简介

MySQL是一个**关系型数据库管理系统**，是最好的RDBMS（Relational Database Management System，关系数据库管理系统）应用软件之一，是一个开源的数据库软件

前世：属于瑞典MySQL AB公司

今生：属于 Oracle 旗下产品

**优点：**

- 开源数据库软件
- 体积小、速度快、总体拥有成本低
- 可以做集群

官网：[https://www.mysql.com](https://www.mysql.com)

下载地址：[https://dev.mysql.com/download/mysql/](https://dev.mysql.com/download/mysql/)

### 1.5、安装MySQL

安装步骤：

1. 解压压缩包

2. 把包放到自己的电脑环境目录下

3. 配置环境变量

   1. 我的电脑==>属性==>高级==>环境变量
   2. 选择path，在其后面添加：mysql安装目录下bin文件夹的路径

4. 新建mysql配置文件

   1. 在mysql安装根目录下新建`my.ini`配置文件

   2. 编辑`my.ini`文件，注意替换路径位置

      ```ini
      [mysqld]
      # 目录一定要换成自己的
      basedir=D:\mysql-5.7\
      datadir=D:\mysql-5.7\data\
      port=3306
      skip-grant-tables
      ```

5. 启动管理员模式下的CMD，进入mysql下bin目录运行所有的命令

   1. 输入`mysqld -install`（安装mysql）

      ```shell
      mysqld -install
      ```

   2. 输入`mysqld -initialize-insecure --user=mysql`（初始化数据）

      ```shell
      mysqld -initialize-insecure --user=mysql
      ```

   3. 启动mysql，进去修改密码

      ```shell
      net start mysql
      ```

   4. 进入mysql

      ```shell
      # -p后没有空格！
      mysql -u root -p
      ```

   5. 修改密码

      ```shell
      # 后面有分号
      update mysql.user set authentacation string=password('123456') where user='root' and Host='localhost';
      ```

   6. 刷新权限

      ```shell
      flush privileges;
      ```

6. 将mysql配置文件中最后一行注释掉

   ```ini
   [mysqld]
   basedir=D:\mysql-5.7\
   datadir=D:\mysql-5.7\data\
   port=3306
   # skip-grant-tables
   ```

7. 重启mysql

   ```shell
   exit
   net stop mysql
   net start mysql
   ```

安装建议：

1. 建议不要使用exe，会使用注册表
2. 尽可能使用压缩包安装

### 1.6、安装SQLyog

1. 无脑下一步安装
2. 注册
3. 打开连接数据库
4. 新建一个数据库
5. 新建一张表`student`
6. 查看表

**每一个sqlyog的执行操作，本质就是对应了一个sql，可以在软件的历史记录中查看**

### 1.7、连接数据库

命令行连接

```sql
mysql -uroot -p123456 -- 连接数据库

update mysql.user set authentication_string=password('123456') where user='root' and Host='localhost'; -- 修改用户密码

flush privileges; -- 刷新权限

--------------------------------------------------
-- 所有的语句都用分号结尾;
show databases; -- 查看所有的数据库
use school; -- 切换数据库 use 数据库名称
show tables; -- 查看数据库中所有的表
describe student; -- 显示数据库中表的信息
create database westos; -- 创建一个数据库
exit; -- 退出连接

-- 单行注释（SQL本来的注释）
/**/ 多行注释
```

DDL：定义语言

DML：操作语言

DQL：查询语言

DCL：控制语言

## 2、操作数据库

操作数据库==>操作数据库中的表==>操作数据库中表的数据

**mysql关键字不区分大小写**

### 2.1、操作数据库

1. 创建数据库

   ```sql
   CREATE DATABASE [IF NOT EXISTS] westos;
   ```

2. 删除数据库

   ```sql
   DROP DATABASE [IF EXISTS] westos;
   ```

3. 使用数据库

   ```sql
   -- 如果你的表名或者字段名是一个特殊字符，需要加上``
   USE `westos`;
   ```

4. 查看数据库

   ```sql
   SHOW DATABASE;
   ```

### 2.2、数据库的数据类型

**数值**

|  数据类型   |        作用         | 存储空间 | 是否常用 |
| :---------: | :-----------------: | :------: | :------: |
|   tinyint   |    十分小的数据     | 1个字节  |          |
|  smallint   |     较小的数据      | 2个字节  |          |
|  mediumint  |      中等大小       | 3个字节  |          |
|   **int**   |     标准的整数      | 4个字节  |    √     |
|   bigint    |     较大的数据      | 8个字节  |          |
|    float    |       浮点数        | 4个字节  |          |
|   double    |       浮点数        | 8个字节  |          |
| **decimal** | 字符串浮点数8个字节 | 8个字节  |    √     |

**字符串**

|  数据类型   |      作用      | 存储空间 | 是否常用 |
| :---------: | :------------: | :------: | :------: |
|    char     | 字符串固定大小 |  0~255   |          |
| **varchar** |   可变字符串   | 0~65535  |    √     |
|  tinytext   |    微型文本    |  2^8-1   |          |
|    text     |     文本串     |  2^16-1  |          |

**日期**

|   数据类型    |              作用              | 是否常用 |
| :-----------: | :----------------------------: | :------: |
|     date      |           yyyy-MM-dd           |          |
|     time      |            hh:mm:ss            |          |
| **datetime**  |      yyyy-MM-dd hh:mm:ss       |    √     |
| **timestamp** | 时间戳，1970-1-1到现在的毫秒数 |    √     |
|     year      |            年份表示            |          |

**null**

- 没有值，未知
- 注意：不要使用 null 进行运算，结果为 null

### 2.3、数据库字段属性

**Unsigned：**

- 无符号的整数
- 声明了该列不能声明为负数

**zerofill：**

- 0填充
- 不足的位数使用0来填充

**自增**

- 通常理解为自增，自动在上一条记录的基础上+1（默认）
- 通常用来设计唯一的主键，必须是整数类型
- 可以自定义设计主键自增的起始值和步长

**非空：null/not null**

- 设置为 not null，如果不给赋值就会报错
- null，如果不填写值，默认就是null

**默认**

- 设置默认的值
- 如果不指定该列的值则有默认的值

### 2.4、创建数据库表

```sql
-- 目标：创建一个school数据库
-- 创建学生表(列，字段)	使用SQL  创建
/*
学号 int
登陆密码 varchar(20)
姓名 varchar(30)
性别 varchar(3)
出生日期 datetime
家庭住址 varchar(100)
*/

-- 注意点：使用英文()，表的名称、字段尽量使用 `` 括起来
-- AUTO_INCREMENT 自增
-- 字符串使用 '' 单引号括起来
-- 所有的语句后面加 , 逗号(英文的)，最后一个不用加
-- PRIMARY KEY 主键，一般一个表只有一个唯一的主键
CREATE DATABASE school;

USE school;

CREATE TABLE IF NOT EXISTS student (
	`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
    `name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
    ·pwd· VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
    `sex` VARCHAR(20) NOT NULL DEFAULT '女' COMMENT '性别',
    `birthday` DATETIME DEFAULT NULL COMMENT '生日',
    address VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
    PRIMARY KEY('id')
)ENGINE=INNODB DEFAULT CHARSET=utf8
```

格式

```sql
CREATE TABLE [IF NOT EXISTS] 表名 (
	`字段名` 列类型 [属性] [索引] [注释],
    ....
    `字段名` 列类型 [属性] [索引] [注释]
)[表类型][字符集设置][注释]
```

常用命令

```sql
SHOW CREATE DATABASE school  --查看创建数据库语句
SHOW CREATE TABLE student  --查看student数据表的定义语句
DESC student  --显示表的结构
```

### 2.5、数据表的类型

```sql
-- 关于数据库引擎
/*
INNODB：默认使用
MYISAM：早些年使用的
*/
```

|              | MYISAM |        INNODB         |
| :----------: | :----: | :-------------------: |
|   事务支持   | 不支持 |         支持          |
|  数据行锁定  | 不支持 |         支持          |
|   外键约束   | 不支持 |         支持          |
|   全文索引   |  支持  |        不支持         |
| 表空间的大小 |  较小  | 较大，约为MYISAM的2倍 |

常规使用操作：

- MYISAM：节约空间，速度较快
- INNODB：安全性高，事物的处理，多表多用户的操作

> 在物理空间存在的位置

所有的数据库文件都存在data目录下，一个文件夹就对应一个数据库

本质还是文件的存储

MySQL引擎在物理文件上的区别

- InnoDB在数据库表中只有一个 *.frm 文件，以及上级目录下的ibdata1文件
- MYISAM对应文件
  - *.frm    -表结构的定义文件
  - *.MYD    -数据文件（data）
  - *.MYI      -索引文件（index）

> 设置数据库表的字符集编码

```sql
CHARSET=utf8
```

不设置的话，会是mysql默认的字符集编码（不支持中文）

MySQL的默认编码是Latin1，不支持中文

在my.ini中配置默认的编码

```ini
character-set-server=utf8
```

### 2.6、修改删除表

> 修改

```sql
-- 修改表名：ALTER TABLE 旧表名 RENAME AS 新表名
ALTER TABLE teacher RENAME AS teacher1

-- 增加表的字段：ALTER TABLE 表名 ADD 字段名 列属性
ALTER TABLE teacher1 ADD age INT(11)

-- 修改表的字段（重命名，修改约束！）
-- ALTER TABLE 表名 MODIFY 字段名 列属性 []
ALTER TABLE teacher1 MODIFY age varchar(11)

-- ALTER TABLE 表名 CHANGE 旧名字 新名字 列属性 []
ALTER TABLE teacher1 CHANGE age age1 INT(11)

-- 删除表的字段：ALTER TABLE 表名 DROP 字段名
ALTER TABLE teacher1 DROP age1
```

> 删除

```sql
-- DROP TABLE 表名
DROP TABLE IF EXISTS teacher1
```

**所有的创建和删除操作尽量加上判断（`IF EXISTS`），以免报错**

注意点：

- 字段名尽量使用 ``包裹
- 注释：--  和 /**/
- SQL关键字大小写不敏感，建议小写
- 所有符号用英文

## 3、MySQL数据管理

### 3.1、外键

> 方式一：在创建表的时候，增加约束（麻烦，比较复杂）

```sql
CREATE TABLE `grade` (
	`gradeid` INT(10) NOT NULL AUTO_INCREMENT COMMENT '年级id',
    `gradename` VARCHAR(50) NOT NULL COMMENT '年级名字',
    PRIMARY KEY (`gradeid`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;

-- 学生表的 gradeid 字段要去引用年级表的 gradeid
-- 定义外键key
-- 给这个外键添加约束（执行引用）  references引用

CREATE TABLE IF NOT EXISTS student (
	`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
    `name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
    ·pwd· VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
    `sex` VARCHAR(20) NOT NULL DEFAULT '女' COMMENT '性别',
    `birthday` DATETIME DEFAULT NULL COMMENT '生日',
    `gradeid` INT(10) NOT NULL COMMENT '学生年级',
    `address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
    `email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
    PRIMARY KEY('id'),
    KEY `FK_gradeid` (`gradeid`),
    CONSTRAINT `FK_gradeid` FOREIGN KEY (`gradeid`) REFERENCES `grade`(`gradeid`)
)ENGINE=INNODB DEFAULT CHARSET=utf8
```

> 方式二：创建表成功后，添加外键约束

```sql
CREATE TABLE `grade` (
	`gradeid` INT(10) NOT NULL AUTO_INCREMENT COMMENT '年级id',
    `gradename` VARCHAR(50) NOT NULL COMMENT '年级名字',
    PRIMARY KEY (`gradeid`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;

-- 学生表的 gradeid 字段要去引用年级表的 gradeid
-- 定义外键key
-- 给这个外键添加约束（执行引用）  references引用

CREATE TABLE IF NOT EXISTS student (
	`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
    `name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
    ·pwd· VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
    `sex` VARCHAR(20) NOT NULL DEFAULT '女' COMMENT '性别',
    `birthday` DATETIME DEFAULT NULL COMMENT '生日',
    `gradeid` INT(10) NOT NULL COMMENT '学生年级',
    `address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
    `email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
    PRIMARY KEY('id')
)ENGINE=INNODB DEFAULT CHARSET=utf8;

-- 创建表的时候没有外键关系
ALTER TABLE `student` ADD CONSTRAINT `FK_gradeid` FOREIGN KEY(`gradeid`) REFERENCES `grade`(`gradeid`);

-- ALTER TABLE 表名 ADD CONSTRAINT 约束名 FOREIGN KEY（作为外键的列） REFERENCES 外键引用表名（外键引用字段）
```

以上的操作都是物理外键，数据库级别的外键，不建议使用！（避免数据库过多造成困扰）

**最佳实践**

- 数据库就是单纯的表，只用来存数据，只有行（数据）和列（字段）
- 我们想使用多张表的数据，想使用外键（程序去实现）

### 3.2、DML语言

数据库的意义：数据存储和数据管理

DML语言：数据操作语言

1. Insert
2. update
3. delete

### 3.3、添加

> insert

```sql
-- 插入语句（添加）
-- insert into 表名([字段名1，字段2...]) values ('值1'，'值2'...)
INSERT INTO `grade` (`gradename`) VALUES('大四')

-- 由于主键自增可以省略（如果不写表字段就会一一对应）
INSERT INTO `grade` VALUES('大三')

-- 一般写插入语句，一定要数据和字段一一对应！

-- 插入多个字段
INSERT INTO `grade`(`gradename`) VALUES('大二'),('大一')

INSERT INTO `student`(`name`,`pwd`,`sex`) VALUES('张三','aaaaaa','男')

INSERT INTO `student`(`name`,`pwd`,`sex`) VALUES('张三','aaaaaa','男'),('王五','bbbbbb','女')
```

语法：`insert into 表名([字段名1，字段2...]) values ('值1'，'值2'...)`

注意事项：

- 字段和字段之间使用 英文逗号 隔开
- 字段是可以省略的，但是后面的值必须一一对应
- 可以同时插入多条数据，VALUES后面的值需要用逗号隔开

### 3.4、修改

> update

```sql
-- 修改学员名字
UPDATE `student` SET `name`='赵四' WHERE id = 1;

-- 不指定条件的情况下，会改动所有数据
UPDATE `student` SET `name`='长江七号'

-- 语句：
-- UPDATE 表名 set colnum_name = value where 条件[]

-- 修改多个属性
UPDATE `student` SET `name`='赵四',`email`='11111@gmail.com' WHERE id = 1;

-- 通过多个条件定位数据，无上限。
UPDATE `student` SET `name`='六五三',`email`='11111@gmail.com' WHERE `name`='长江七号' and `sex`='女'
```

条件：where子句 运算符 id 等于某个值，大于某个值，在某个区间内修改

|       操作符        |     含义     |      范围       | 结果  |
| :-----------------: | :----------: | :-------------: | :---: |
|          =          |     等于     |       5=6       | false |
|      <> 或 !=       |    不等于    |      5<>6       | true  |
|         <=          |   小于等于   |      5<=5       | true  |
|         >=          |   大于等于   |      1>=2       | false |
| BETWEEN ... and ... | 在某个范围内 | between 2 and 5 |       |
|         AND         |    和  &&    |   5>1 and 1>2   | false |
|         OR          |   或 \|\|    |   5>1 or 1>2    | true  |

语法：`UPDATE 表名 set colnum_name = value where 条件[]`

注意事项：

- colnum_name 是数据库的列，尽量带上 `` 符号
- 筛选的条件。如果没有指定，则会修改所有的列
- value，是一个具体的值，也可以是一个变量
- 多个设置的属性之间，使用英文逗号隔开

### 3.5、删除

> delete

```sql
-- 删除数据（避免这样写，会全部删除）
DELETE FROM `student`

-- 删除指定数据
DELETE FROM `student` WHERE id = 1
```

> truncate

作用：完全清空一个数据库表，表的结构和索引约束不会变

```sql
-- 清空 student 表
TUANCATE `student`
```

> delete 和 truncate 的区别

- 相同点：都能删除数据，都不会删除表
- 不同点：
  - truncate：重新设置 自增列，计数器会归零。不会影响事务
  - delete：不会影响自增列

```sql
-- 测试 delete 和 truncate 的区别
CREATE TABLE `test`(
	`id` INT(4) NOT NULL AUTO_INCREMENT,
    `coll` VARCHAR(20) NOT NULL,
    PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO `test`(`coll`) VALUES('1'),('2'),('3');

-- 不会影响自增
DELETE FROM `test`

-- 自增归零
TRUNCATE TABLE `test`
```

**delete删除的问题**

重启数据库后出现问题的现象

- InnoDB：自增列会从1开始（存在内存中的，断电即失）
- MyISAM：继续从上一个自增量开始（存在文件中，不会丢失）

## 4、DQL查询数据

### 4.1、DQL

（Data Query LANGUAGE：数据查询语言）

- 所有的查询操作都用它 Select
- 简单的查询，复杂的查询它都能做
- 数据库中最核心的语言，最重要的语句
- 使用频率最高的语句

### 4.2、指定查询字段

> select

```sql
-- 查询全部的学生   SELECT 字段 FROM 表
SELECT * FROM student

-- 查询指定字段
SELECT `StudentName`,`StudentNo` FROM student

-- 别名，给结果起一个名字 AS  可以给字段和表起别名
SELECT `StudentName` AS 学号,`StudentNo` AS 学生姓名 FROM student AS Stu

-- 函数 Concat
SELECT CONCAT('姓名：',`StudentName`) AS 新名字 FROM student
```

语法：`SELECT 字段,.... FROM 表`

![](http://zhaocan.fym233.cn/tnr8qew3id)

**有的时候，列名字不是那么的见名知意。可以起别名**



> 去重 distinct

作用：去除SELECT 查询出来的结果中重复的数据，重复的数据只显示一条

```sql
-- 查询一下有哪些同学参加了考试，成绩
SELECT * FROM result   -- 查询全部的考试成绩
SELECT `StudentNo` FROM result	--查询有哪些同学参加了考试
SELECT DISTINCT `StudentNo` FROM result	-- 发现重复数据，去重
```

> 数据库的列（表达式）

```sql
SELECT VERSION()	-- 查询系统版本（函数）
SELECT 100*3-1 AS 计算结果	-- 用来计算（表达式）
SELECT @@auto_increment_increment	-- 查询自增的步长（变量）

** 学员考试成绩 +1 分查看
SELECT `StudentResult`+1 AS '提分后' FROM result
```

数据库中的表达式：

- 文本值
- 列
- Null
- 函数
- 计算表达式
- 系统变量
- ....

语法：`SELECT 表达式 FROM 表`

### 4.3、where条件子句

作用：检索数据中符合条件的值

搜索的条件由一个或多个表达式组成！结果为布尔值

> 逻辑运算符

| 运算符  |        语法         |               描述               |
| :-----: | :-----------------: | :------------------------------: |
| and &&  |  a and b    a && b  |   逻辑与，两个都为真，结果为真   |
| or \|\| | a or b     a \|\| b | 逻辑或，其中一个为真，则结果为真 |
|  not !  |    not a     !a     |      逻辑非，真为假，假为真      |

**尽量使用英文字母**

```sql
-- 查询所有学生的成绩
SELECT `StudentNo`,`StudentResult` FROM result;

-- 查询考试成绩在 95~100 分之间的 and也可以换成&&
SELECT `StudentNo`,`StudentResult` FROM result WHERE StudentResult>=95 AND StudentResult<=100;

-- 区间查询
SELECT `StudentNo`,`StudentResult` FROM result WHERE StudentResult BETWEEN 95 AND 100;

-- 除了1000号学生之外的同学成绩  !=也可以换成not
SELECT `StudentNo`,`StudentResult` FROM result WHERE StudentNo!=1000;
```

> 模糊查询：比较运算符

|   运算符    |        语法         |                    描述                     |
| :---------: | :-----------------: | :-----------------------------------------: |
|   IS NULL   |      a is null      |         如果操作符为null，结果为真          |
| IS NOT NULL |    a is not null    |       如果操作符为 not null，结果为真       |
|   BETWEEN   |  a between b and c  |          若a在b和c之间，则结果为真          |
|  **Like**   |      a like b       |       SQL匹配，如果a匹配b，则结果为真       |
|   **In**    | a in (a1,a2,a3,...) | 假如a在a1，a2....其中的某一个值中，结果为真 |

```sql
--查询姓刘的同学
-- like结合	%（代表0到任意个字符）  _（一个字符）
SELECT `StudentNo`,`StudentName` FROM `student` WHERE StudentName LIKE '刘%'

-- 查询姓刘的同学，名字后面只有一个字的
SELECT `StudentNo`,`StudentName` FROM `student` WHERE StudentName LIKE '刘_'

-- 查询姓刘的同学，名字后面只有两个字的
SELECT `StudentNo`,`StudentName` FROM `student` WHERE StudentName LIKE '刘__'

-- 查询姓刘的同学，名字后面中间有嘉字的同学
SELECT `StudentNo`,`StudentName` FROM `student` WHERE StudentName LIKE '%嘉%'

-- ======== in （具体的一个或多个值）========
-- 查询 1001，1002，1003号学员
SELECT `StudentNo`,`StudentName` FROM `student` WHERE StudentName IN (1001,1002,1003)

-- 查询在北京的学生
SELECT `StudentNo`,`StudentName` FROM `student` WHERE  Address IN ('北京')

-- ======= null    not null =======
-- 查询地址为空的学生 null ''
SELECT `StudentNo`,`StudentName` FROM `student` WHERE Address='' OR Address IS NULL

--	查询有出生日期的同学
SELECT `StudentNo`,`StudentName` FROM `student` WHERE `BornDate` IS NOT NULL

-- 查询没有出生日期的同学
SELECT `StudentNo`,`StudentName` FROM `student` WHERE `BornDate` IS NULL
```

### 4.4、联表查询

> JOIN 对比

![](https://img-blog.csdnimg.cn/2020021721220879.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NoZW5fY2hlbmdmZW5n,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/20191205175657936.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjA3Mjc1NA==,size_16,color_FFFFFF,t_70)

```sql
-- ======= 联表查询 =======
-- 查询参加了考试的同学（学号，姓名，科目编号，分数）
SELECT * FROM student
SELECT * FROM result

/*
1. 分析需求，分析查询的字段来自哪些表，（连接查询）
2. 确定使用哪种连接查询
确定交叉点（这两个表中哪个数据是相同的）
判断的条件：Student表中 StudentNo = 成绩表中 StudentNo
*/


-- join（连接的表） on （判断的条件） ：连接查询
-- where ：等值查询

SELECT s.StudentNo,StudentName,SubjectNo,StudentResult FROM student s INNER JOIN result r WHERE s.StudentNo=r.StudentNo

-- Right Join
SELECT s.StudentNo,StudentName,SubjectNo,StudentResult FROM student s RIGHT JOIN result r ON s.StudentNo=r.StudentNo

-- Left Join
SELECT s.StudentNo,StudentName,SubjectNo,StudentResult FROM student s LEFT JOIN result r ON s.StudentNo=r.StudentNo

-- 查询缺考的同学
SELECT s.StudentNo,StudentName,SubjectNo,StudentResult FROM student s LEFT JOIN result r ON s.StudentNo=r.StudentNo WHERE StudentResult IS NULL

-- 查询参加了考试的同学信息：学号，学生姓名，科目名，分数
-- Student，Result，Subject
SELECT s.StudentNo,StudentName,SubjectName,StudentResult FROM student s RIGHT JOIN result r ON r.StudentNo=s.StudentNo INNER JOIN subject sub ON r.SubjectNo=sub.SubjectNo
```

|    操作    |                   描述                   |
| :--------: | :--------------------------------------: |
| Inner join |     如果表中至少有一个匹配，就返回行     |
| left join  | 会从左表中返回所有值，即使右表中没有匹配 |
| right join | 会从右表中返回所有值，即使左表中没有匹配 |

> 自连接：自己的表和自己的表连接
>
> 核心：**一张表拆成两张一样的表即可**

父类：

- categoryid：id
- categoryName：名字

| categoryid | categoryName |
| :--------: | :----------: |
|     2      |   信息技术   |
|     3      |   软件开发   |
|     5      |   美术设计   |

子类：

- pid：父id
- categoryid：id
- categoryName：名字

| pid  | categoryid | categoryName |
| :--: | :--------: | :----------: |
|  3   |     4      |    数据库    |
|  2   |     8      |   办公信息   |
|  3   |     6      |   web开发    |
|  5   |     7      |    ps技术    |

操作：查询父类对应的子类关系

|   父类   |   子类   |
| :------: | :------: |
| 信息技术 | 办公信息 |
| 软件开发 |  数据库  |
| 软件开发 | web开发  |
| 美术设计 |  ps技术  |

```sql
-- 查询父子信息：把一张表看为两个一模一样的表
SELECT `categoryName` AS '父栏目',`categoryName` AS '子栏目' FROM `category` AS a,`category` AS b WHERE a.`categoryid`=b.`pid`

-- 查询学员所属的年级（学号，学生姓名，年级名称）
SELECT StudentNo,StudentName,GradeName FROM student s INNER JOIN grade g ON s.GradeID=g.GradeID

-- 查询科目所属的年级（科目名称，年级名称）
SELECT SubjectName,GradeName FROM subject sub INNER JOIN grade g ON sub.GradeID=g.GradeID

-- 查询参加了数据库结构-1 考试的同学信息（学号，学生姓名，科目名，分数）
SELECT s.StudentNo,StudentName,SubjectName,StudentResult FROM student s INNER JOIN result r ON s.StudentNo=r.StudentNo INNER JOIN subject sub ON r.SubjectNo=sub.SubjectNo WHERE SubjectName='数据库结构-1'
```

### 4.5、分页和排序

> 排序：ORDER BY

```sql
-- 排序：升序 ASC 降序 DESC
-- 语法：ORDER BY 通过哪个字段排序，怎么排

-- 查询参加了数据库结构-1 考试的同学信息，查询的结果根据成绩降序排序（学号，学生姓名，科目名，分数）
SELECT s.StudentNo,StudentName,SubjectName,StudentResult FROM student s INNER JOIN result r ON s.StudentNo=r.StudentNo INNER JOIN subject sub ON r.SubjectNo=sub.SubjectNo WHERE SubjectName='数据库结构-1' ORDER BY StudentResult ASC
```

> 分页

为什么要分页

- 缓解数据库压力，给用户更好的体验

```sql
-- 查询参加了数据库结构-1 考试的同学信息，查询的结果根据成绩降序排序，每页只显示五条数据（学号，学生姓名，科目名，分数）
-- 语法：limit 当前页，页面的大小
-- LIMIT 0,5	1~5
-- LIMIT 1,5	2~6
SELECT s.StudentNo,StudentName,SubjectName,StudentResult FROM student s INNER JOIN result r ON s.StudentNo=r.StudentNo INNER JOIN subject sub ON r.SubjectNo=sub.SubjectNo WHERE SubjectName='数据库结构-1' ORDER BY StudentResult ASC LIMIT 0,5

-- 第一页 limit 0,5	(1-1)*5
-- 第二页 limit 5,5	(2-1)*5
-- 第三页 limit 10,5	(3-1)*5
-- ...
-- 第N页  limit 		(n-1) * pageSize,pageSize
-- 【pageSize：页面大小】
-- 【(n-1) * pageSize：起始值】
-- 【n：当前页】
-- 【数据总数/页面大小 = 总页数】

-- 查询 Java第一学年，课程成绩排名前十的学生，并且分数要大于80的学生信息（学号，姓名，课程名称，分数）
SELECT s.StudentNo,StudentName,SubjectName,StudentResult 
FROM student s 
INNER JOIN result r 
ON s.StudentNo=r.StudentNo 
INNER JOIN subject sub 
ON r.SubjectNo=sub.SubjectNo 
WHERE SubjectName='Java第一学年' AND StudentResult>=80
ORDER BY StudentResult DESC
LIMIT 0,10
```

语法：`limit(查询起始下标，页面大小）` 

### 4.6、子查询

本质：`在where语句中嵌套一个子查询语句`

```sql
-- 查询数据库结构-1 的所有考试结果（学号，科目编号，成绩），降序排列
-- 方式一：使用连接查询
SELECT StudentNo,r.SubjectNo,StudentResult 
FROM result r
INNER JOIN subject sub
ON r.StudentNo=sub.StudentNo
WHERE SubjectName='数据库结构-1'
ORDER BY StudentResult DESC

-- 方式二：使用子查询
SELECT StudentNo,r.SubjectNo,StudentResult 
FROM result 
WHERE SubjectNo =(
    SELECT SubjectNo FROM subject
	WHERE SubjectName='数据库结构-1'
)
ORDER BY StudentResult DESC

-- 分数不小于80分的学生的学号和姓名
SELECT DISTINCT s.StudentNo,StudentName 
FROM student s
INNER JOIN result r
ON s.StudentNo=r.StudentNo
WHERE StudentResult>=80

-- 上一题基础上再增加一个科目，高等数学-2
SELECT DISTINCT s.StudentNo,StudentName 
FROM student s
INNER JOIN result r
ON s.StudentNo=r.StudentNo
WHERE StudentResult>=80 AND SubjectNo = (
	SELECT SubjectNo FROM subject
    WHERE SubjectName='高等数学-2'
)

-- 查询 C语言-1 前5名同学的成绩的信息（学号，姓名，分数）
SELECT StudentNo,StudentName,StudentResult 
FROM student
WHERE StudentNo = (
	SELECT StudentNo FROM result
) AND SubjectNo = (
	SELECT SubjectNo FROM subject 
    WHERE SubjectName='C语言-1'
)
ORDER BY 
LIMIT 0,5
```

### 4.7、分组和过滤

```sql
-- 查询不同课程的平均分，最高分，最低分,平均分大于80
-- 核心：根据不同的课程分组
SELECT SubjectName,AVG(StudentResult) AS 平均分,MAX(StudentResult) AS 最高分,MIN(StudentResult) AS 最低分
FROM result r
INNER JOIN subject sub
ON r.SubjectNo=sub.SubjectNo
GROUP BY r.SubjectNo	--通过什么字段来分组
HAVING 平均分>80
```

## 5、MySQL函数

官方文档：[https://dev.mysql.com/doc/refman/5.7/en/func-op-summary-ref.html](https://dev.mysql.com/doc/refman/5.7/en/func-op-summary-ref.html)

### 5.1、常用函数

```sql
-- 数学运算
SELECT ABS(-8)		--绝对值
SELECT CEILING(9.4)	--向上取整
SELECT FLOOR(9.4)	--向下取整
SELECT RAND()		--返回一个0~1之间的随机数
SELECT SIGN(-10)	--判断一个数的符号，负数返回-1，正数返回1

-- 字符串函数
SELECT CHAR_LENGTH("啦啦啦")	--字符串长度
SELECT CONCAT('啊','阿','六')	--拼接字符串
SELECT INSERT('我爱java',1,2,'超级热爱')--查询，替换。从某个位置开始替换某个长度（第1个下标开始替换2个字符）
SELECT LOWER('ZHAOCAN')		--转小写
SELECT UPPER('zhaocan')		--转大写
SELECT INSTR('zhaocan','c')	--返回第一次出现的字符串的索引
SELECT REPLACE('Java天下第一','Java','MySQL')--替换出现的指定的字符串
SELECT SUBSTR('Java天下第一',1,4)	--返回指定的字符串（源字符串，截取位置，截取长度）
SELECT REVERSE('Java天下第一')	--字符串反转

-- 查询姓周的同学，把姓氏改为邹
SELECT REPLACE(StudentName,'周','邹') FROM student
WHERE StudentName LIKE '周%'

-- 时间和日期函数
SELECT CURRENT_DATE()	--获取当前日期
SELECT CURDATE()		--获取当前日期
SELECT NOW()			--获取当的时间
SELECT LOCALTIME()		--获取本地时间
SELECT SYSDATE()		--获取系统时间
SELECT YEAR(NOW())		--获取当前年份
SELECT MONTH(NOW())		--获取当前月份
SELECT DAY(NOW())		--获取当天日期
SELECT HOUR(NOW())		--获取当前小时数
SELECT MINUTE(NOW())	--获取当前分钟数
SELECT SECOND(NOW())	--获取当前秒数

-- 系统
SELECT SYSTEM_USER()	--获取系统用户信息
SELECT USER()			--获取系统用户信息
SELECT VERSION			--获取当前数据库版本
```

### 5.2、聚合函数

| 函数名称 |  描述  |
| :------: | :----: |
| COUNT()  |  计算  |
|  SUM()   |  求和  |
|  AVG()   | 平均值 |
|  MAX()   | 最大值 |
|  MIN()   | 最小值 |

```sql
-- 都能够统计表中的数据
SELECT COUNT(StudentName) FROM student;	--Count(字段)
SELECT COUNT(*) FROM student
SELECT COUNT(1) FROM result

SELECT SUM(StudentResult) AS 总和 FROM result
SELECT AVG(StudentResult) AS 平均分 FROM result
SELECT MAX(StudentResult) AS 最高分 FROM result
SELECT MIN(StudentResult) AS 最低分 FROM result
```

COUNT()的区别：

- COUNT(字段)：忽略所有 null 值，效率最高（查询主键列）
- COUNT(*)：不会忽略 null 值，计算行数
- COUNT(1)：不会忽略 null 值，计算行数

### 5.3、数据库级别的MD5加密

**什么是MD5**

- 主要增强算法复杂度和不可逆性
- MD5不可逆，具体的值的MD5是一样的
- MD5破解网站的原理，背后有一个字典，MD5加密后的值，加密的前值

```sql
-- ======= 测试MD5 加密 =======
CREATE TABLE `testmd5`(
	`id` INT(4) NOT NULL,
    `name` VARCHAR(20) NOT NULL,
    `pwd` VARCHAR(50) NOT NULL,
    PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;

-- 明文密码
INSERT INTO `testmd5` VALUES(1,'张三','123456'),(2,'李四','123456'),(3,'王五','123456')

-- 加密
UPDATE testmd5 SET pwd=MD5(pwd)

-- 插入的时候加密
INSERT INTO `testmd5` VALUES(4,'小明',MD5('123456'))

-- 如何校验：将用户传递进来的密码，进行md5加密，然后比对加密后的值
```

## 6、事务

### 6.1、什么是事务

**要么都成功，要么都失败**

将一组SQL放在一个批次中执行

> 事务原则：ACID原则

- **原子性（Atomicity）**：要么都成功，要么都失败
- **一致性（Consistency）**：事务前后的数据完整性保证一致
- **隔离性（Durability）**：事物的隔离性是多个用户并发访问数据库时，数据库为每一个用户开启的事务，不能被其他事务的操作数据所干扰，事务之间要相互隔离
- **持久性（Isolation）**：事务一旦提交则不可逆，被持久化到数据库中

> 隔离所导致的问题

- **脏读**：指一个事务读取了另一个事务未提交的数据
- **不可重复读**：在一个事务内读取表中的某一行数据，多次读取结果不同（这个不一定是错误，只是某些场合不同）
- **虚读（幻读）**：是指在一个事务内读取到了别的事务插入的数据，导致前后读取不一致

> 执行事务

**MySQL是默认开启事务自动提交的**

```sql
SET autocommit = 0 	-- 关闭
SET autocommit = 1	-- 开启（默认的）

-- 手动处理事务

-- 事务开始
START TRANSACTION	-- 标记一个事务的开始，从这个之后的SQL都在同一个事务内

-- 提交：持久化（成功）
COMMIT
-- 回滚：回到原来的样子（失败）
ROLLBACK

-- 事务结束
SET autocommit = 1	-- 开启自动提交

SAVEPOINT 保存点名	-- 设置一个事务的保存点
ROLLBACK TO SAVEPOINT 保存点名	-- 回滚到保存点
RELEACE SAVEPOINT 保存点名	-- 删除保存点
```

```sql
-- 模拟转账：事务
SET autocommit = 0;	-- 关闭自定提交
START TRANSACTION	-- 开启一个事务

UPDATE account SET money=money-500 WHERE `name` = 'A'	-- A用户-500
UPDATE account SET money=money+500 WHERE `name` = 'B'	-- B用户+500

COMMIT;	-- 提交事务
ROLLBACK;	-- 回滚

SET autocommit = 1;	-- 恢复默认值
```

## 7、索引

> MySQL官方对索引的定义为：**索引（index）是帮助MySQL高效获取数据结构**。提取句子主干，就可以得到索引的本质：索引是数据结构

### 7.1、索引的分类

- 主键索引（PRIMARY KEY）
  - 唯一标识，主键不可重复，只能有一个列作为主键
- 唯一索引（UNIQUE KEY）
  - 避免重复的列出现，唯一索引可以重复：多个列都可以标识为唯一索引
- 常规索引（KEY / INDEX）
  - 默认的，使用index 或 key 关键字来设置
- 全文索引（FullText）
  - 在特定的数据库引擎下才有
  - 快速定位数据

```sql
-- 索引的使用
-- 1、在创建表的时候给字段增加索引
-- 2、创建完毕后，增加索引

-- 显示所有的索引信息
SHOW INDEX FROM student

-- 增加一个索引
ALTER TABLE `student` ADD FULLTEXT INDEX 'studentName'

-- EXPLAIN 分析sql执行的状况
EXPLAIN SELECT * FROM student;	--全文索引
EXPLAIN SELECT * FROM student WHERE MATCH(StudentName) AGAINST('刘');
```

### 7.2、测试索引

```sql
`app_user`


-- 插入100万条数据
DELIMITER $$	-- 写函数之前必须要写，标志

CREATE FUNCTION mock_data()
RETURNS INT
BEGIN
   DECLARE num INT DEFAULT 1000000;
   DECLARE i INT DEFAULT 0;
   WHILE i<num DO
      INSERT INTO app_user(`name`,`email`,`phone`,`gender`,`password`,`age`) VALUES (CONCAT('用户',i),'1872751113@qq.com',CONCAT('18',FLOOR(RAND()*((999999999-100000000)+100000000))),FLOOR(RAND()*2),UUID(),FLOOR(RAND()*100));
      SET i=i+1;
   END WHILE;
   RETURN i;
END;


SELECT * FROM app_user WHERE `name`='用户99999'; -- 执行耗时   : 1.138 sec

SELECT * FROM app_user; -- 执行耗时   : 0.046 sec

-- id_表名_字段名
-- CREATE INDEX 索引名 on 表名（字段名）
CREATE INDEX id_app_user_name ON app_user(`name`); -- 添加索引

SELECT * FROM app_user WHERE `name`='用户99999'; -- 执行耗时   : 0.046 sec

EXPLAIN SELECT * FROM app)user WHERE `name`='用户99999';
```

**索引在小数据量的时候，用出不大。但是在大数据的时候，区别十分明显~**

### 7.3、索引原则

- 索引不是越多越好
- 不要对经常变动的数据加索引
- 小数据量的表不需要加索引
- 索引一般加在常用来查询的字段上

> 索引的数据结构

- Hash类型的索引
- BTree：InnoDB的默认数据结构

## 8、权限管理和备份

### 8.1、用户管理

> SQL yog 可视化管理

![](http://zhaocan.fym233.cn/41z2gpe1ls)

> SQL 命令操作

用户表：mysql.user

本质：对这张表进行增删改查

```sql
-- 创建用户	
-- CREATE USER 用户名 IDENTIFIED BY '密码'
CREATE USER zhaocan IDENTIFIED BY '123456'

-- 修改密码（修改当前用户密码）
SET PASSWORD = PASSWORD('111111')

-- 修改密码（修改指定用户密码）
SET PASSWORD FOR zhaocan = PASSWORD('111111')

-- 重命名
-- RENAME USER 原名 TO 新名字
RENAME USER zhaocan TO zhaocan666

-- 用户授权 ALL PRIVILEGES 全部的权限
-- ALL PRIVILEGES 除了给别人权限，其余都可以做
GRANT ALL PRIVILEGES ON *.* TO zhaocan

-- 查询权限
SHOW GRANTS FOR zhaocan	-- 查看指定用户的权限
SHOW GRANT FOR root@localhost

-- 撤销权限 REVOKE 哪些权限 在哪个库撤销 给谁撤销
REVOKE ALL PRIVILEGES ON *.* FROM zhaocan

-- 删除用户
DROP USER zhaocan
```

### 8.2、MySQL备份

**为什么要备份：**

- 保证重要的数据不丢失
- 数据转移

**MySQL数据库备份的方式**

- 直接拷贝物理文件

- 在SQLyog等可视化工具中手动导出

  - 在想要导出的表或者库中，右键选择备份或导出

    ![](http://zhaocan.fym233.cn/gyh28juvsk)

- 使用命令行导出   mysqldump

  ```shell
  # mysqldump -h主机 -u用户名 -p密码 数据库 表名 > 物理磁盘位置/文件名
  mysqldump -hlocalhost -uroot -p123456 school student >D:/a.sql
  
  # 多张表中间加空格
  mysqldump -hlocalhost -uroot -p123456 school student result >D:/b.sql
  
  # 导出库
  mysqldump -hlocalhost -uroot -p123456 school > D:/b.sql
  
  # 导入先登录
  mysql -uroot -p123456
  use school;
  source D:/a.sql
  ```

  

## 9、规范数据库设计

### 9.1、为什么需要设计

**当数据库比较复杂的时候，就需要设计了**

糟糕的数据库设计：

- 数据冗余，浪费空间
- 数据插入和删除都会麻烦、异常【屏蔽使用物理外键】
- 程序性能差

良好的数据库设计：

- 节省内存空间
- 保证数据的完整性
- 方便开发系统

**软件开发中，关于数据库的设计**

- 分析需求：分析业务和需要处理的数据库的需求
- 概要设计：设计关系图 E-R图

**设计数据库的步骤：（个人博客）**

- 收集信息，分析需求
  - 用户表（用户登录注销，用户的个人信息，写博客，创建分类）
  - 分类表（文章分类，作者）
  - 文章表（文章的信息）
  - 评论表（文章下方的评论）
  - 友链表（友链信息）
  - 自定义表（系统信息，某个关键的字，或者一些主字段）
- 标识实体类（把需求落地到每个字段）
- 标识实体之间的关系
  - 写博客：user --> blog
  - 创建分类：user -->categary
  - 关注：user -->user
  - 友联：links
  - 评论表：user-->user-->blog

### 9.2、三大范式

**为什么需要数据规范化**

- 信息重复
- 更新异常
- 插入异常
  - 无法正常显示信息
- 删除异常
  - 丢失有效的信息

> 三大范式

**第一范式**

原子性：保证每一列不可再分

**第二范式**

前提：必须满足第一范式

每张表只描述一件事情

**第三范式**

前提：必须满足第一范式和第二范式

需要确保表中的每一列数据都和主键直接相关，而不能间接相关



**规范性 和 性能的问题**

关联查询的表不得超过三张表

- 考虑商业化的需求和目标，（成本，用户体验）数据库的性能更加重要
- 在规范性能的问题的时候，需要适当的考虑一下 规范性
- 故意给某些表增加一些冗余的字段。（从多表查询中变为单表查询）
- 故意增加一些计算列（从大数据量降低为小数据量的查询）