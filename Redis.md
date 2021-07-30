# Redis学习笔记

## 一、Nosql概述

### 为什么使用Nosql
### 1、单机Mysql时代

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020082010365930.png#pic_center)

90年代,一个网站的访问量一般不会太大，单个数据库完全够用。随着用户增多，网站出现以下问题

数据量增加到一定程度，单机数据库就放不下了
数据的索引（B+ Tree）,一个机器内存也存放不下
访问量变大后（读写混合），一台服务器承受不住。

### 2、Memcached(缓存) + Mysql + 垂直拆分（读写分离）

网站80%的情况都是在读，每次都要去查询数据库的话就十分的麻烦！所以说我们希望减轻数据库的压力，我们可以使用缓存来保证效率！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200820103713734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

优化过程经历了以下几个过程：

1. 优化数据库的数据结构和索引(难度大)
2. 文件缓存，通过IO流获取比每次都访问数据库效率略高，但是流量爆炸式增长时候，IO流也承受不了
3. MemCache,当时最热门的技术，通过在数据库和数据库访问层之间加上一层缓存，第一次访问时查询数据库，将结果保存到缓存，后续的查询先检查缓存，若有直接拿去使用，效率显著提升。

### 3、分库分表 + 水平拆分 + Mysql集群

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200820103739584.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

### 4、如今最近的年代

 如今信息量井喷式增长，各种各样的数据出现（用户定位数据，图片数据等），大数据的背景下关系型数据库（RDBMS）无法满足大量数据要求。Nosql数据库就能轻松解决这些问题。

> 目前一个基本的互联网项目

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200820103804572.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

### 为什么要用NoSQL ？

用户的个人信息，社交网络，地理位置。用户自己产生的数据，用户日志等等爆发式增长！
这时候我们就需要使用NoSQL数据库的，Nosql可以很好的处理以上的情况！

### 什么是Nosql
**NoSQL = Not Only SQL（不仅仅是SQL）**

Not Only Structured Query Language

关系型数据库：列+行，同一个表下数据的结构是一样的。

非关系型数据库：数据存储没有固定的格式，并且可以进行横向扩展。

NoSQL泛指非关系型数据库，随着web2.0互联网的诞生，传统的关系型数据库很难对付web2.0时代！尤其是超大规模的高并发的社区，暴露出来很多难以克服的问题，NoSQL在当今大数据环境下发展的十分迅速，Redis是发展最快的。

### Nosql特点

1. 方便扩展（数据之间没有关系，很好扩展！）

2. 大数据量高性能（Redis一秒可以写8万次，读11万次，NoSQL的缓存记录级，是一种细粒度的缓存，性能会比较高！）

3. 数据类型是多样型的！（不需要事先设计数据库，随取随用）

4. 传统的 RDBMS 和 NoSQL

   ```bash
   传统的 RDBMS(关系型数据库)
   - 结构化组织
   - SQL
   - 数据和关系都存在单独的表中 row column
   - 操作，数据定义语言
   - 严格的一致性
   - 基础的事务
   - ...
   ```

   ```bash
   NoSQL
   - 不仅仅是数据
   - 没有固定的查询语言
   - 键值对存储，列存储，文档存储，图形数据库（社交关系）
   - 最终一致性
   - CAP定理和BASE
   - 高性能，高可用，高扩展
   - ...
   ```

> 了解：3V + 3高

大数据时代的3V ：主要是描述问题的

1. 海量Velume

2. 多样Variety

3. 实时Velocity


大数据时代的3高 ： 主要是**对程序的要求**

1. 高并发

2. 高可扩

3. 高性能


真正在公司中的实践：NoSQL + RDBMS 一起使用才是最强的。

阿里巴巴演进分析
推荐阅读：阿里云的这群疯子https://yq.aliyun.com/articles/653511

![1](https://img-blog.csdnimg.cn/20200820103829446.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200820103851613.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

```bash
# 商品信息
- 一般存放在关系型数据库：Mysql,阿里巴巴使用的Mysql都是经过内部改动的。
# 商品描述、评论(文字居多)
- 文档型数据库：MongoDB

# 图片
- 分布式文件系统 FastDFS
- 淘宝：TFS
- Google: GFS
- Hadoop: HDFS
- 阿里云: oss

# 商品关键字 用于搜索
- 搜索引擎：solr,elasticsearch
- 阿里：Isearch

# 商品热门的波段信息
- 内存数据库：Redis，Memcache

# 商品交易，外部支付接口
- 第三方应用
```


### NoSQL的四大分类
> KV键值对

- 新浪：Redis
- 美团：Redis + Tair
- 阿里、百度：Redis + Memcache

> 文档型数据库（bson数据格式）

> MongoDB(掌握)

- 基于分布式文件存储的数据库。C++编写，用于处理大量文档。
- MongoDB是RDBMS和NoSQL的中间产品。MongoDB是非关系型数据库中功能最丰富的，NoSQL中最像关系型数据库的数据库。
- ConthDB

> 列存储数据库

- HBase(大数据必学)
- 分布式文件系统

> 图关系数据库

用于广告推荐，社交网络

- Neo4j、InfoGrid

| 分类                    | Examples举例                                       | 典型应用场景                                                 | 数据模型                                        | 优点                                                         | 缺点                                                         |
| ----------------------- | -------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **键值对（key-value）** | Tokyo Cabinet/Tyrant, Redis, Voldemort, Oracle BDB | 内容缓存，主要用于处理大量数据的高访问负载，也用于一些日志系统等等。 | Key 指向 Value 的键值对，通常用hash table来实现 | 查找速度快                                                   | 数据无结构化，通常只被当作字符串或者二进制数据               |
| **列存储数据库**        | Cassandra, HBase, Riak                             | 分布式的文件系统                                             | 以列簇式存储，将同一列数据存在一起              | 查找速度快，可扩展性强，更容易进行分布式扩展                 | 功能相对局限                                                 |
| **文档型数据库**        | CouchDB, MongoDb                                   | Web应用（与Key-Value类似，Value是结构化的，不同的是数据库能够了解Value的内容） | Key-Value对应的键值对，Value为结构化数据        | 数据结构要求不严格，表结构可变，不需要像关系型数据库一样需要预先定义表结构 | 查询性能不高，而且缺乏统一的查询语法。                       |
| **图形(Graph)数据库**   | Neo4J, InfoGrid, Infinite Graph                    | 社交网络，推荐系统等。专注于构建关系图谱                     | 图结构                                          | 利用图结构相关算法。比如最短路径寻址，N度关系查找等          | 很多时候需要对整个图做计算才能得出需要的信息，而且这种结构不太好做分布式的集群 |

## 二、Redis入门

### 概述

### Redis是什么

Redis（**Re**mote **Di**ctionary **S**erver )，即远程字典服务。

是一个开源的使用ANSI C语言编写、支持网络、可基于内存亦可持久化的日志型、**Key-Value数据库**，并提供多种语言的API。

免费和开源！是当下最热门的NoSQL技术之一，也被人们称之为结构化数据库

### Redis能干嘛

1. 内存存储、持久化，内存中是断电即失、所以说持久化很重要（RDB、AOF）
2. 效率高，可以用于高速缓存
3. 发布订阅系统
4. 地图信息分析
5. 计时器、计数器（浏览量！）
6. ...

### Redis特性

1. 多样的数据类型
2. 持久化
3. 集群
4. 事务
5. ...

### 下载及学习地址

1. 官网：https://redis.io/
2. 中文网：http://www.redis.cn/
3. 下载地址：通过官网即可

**注意：Windows在Github上下载（停更很久了），Redis推荐都是在Linux服务器上搭建的**

### Windows安装

1. 下载安装包：https://github.com/dmajkic/redis/releases2

2. 下载完毕得到压缩包：

   ![](http://zhaocan.fym233.cn/4dics3dl69)

3. 解压到自己电脑上的环境目录下就可以了

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200820103922318.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

4. 开启Redis，双击运行服务即可！

5. 使用Redis客户端来连接Redis

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200820103950934.png#pic_center)

### Linux安装

1. 下载安装包！`redis-5.0.8.tar.gz`

2. 解压Redis的安装包！程序一般放在 `/opt` 目录下

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200820104016426.png#pic_center)

3. 基本环境安装

   ```shell
   yum install gcc-c++
   # 然后进入redis目录下执行
   make
   # 然后执行
   make install
   ```

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200820104048327.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

4. redis默认安装路径 `/usr/local/bin`

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200820104140692.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

5. 将redis的配置文件复制到 程序安装目录 `/usr/local/bin/kconfig`下

   ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-hxvGQ47d-1597890996509)(狂神说 Redis.assets/image-20200813114000868.png)]](https://img-blog.csdnimg.cn/20200820104157817.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

6. redis默认不是后台启动的，需要修改配置文件！

   ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-dDdKTUgd-1597890996510)(狂神说 Redis.assets/image-20200813114019063.png)]](https://img-blog.csdnimg.cn/20200820104213706.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

7. 通过制定的配置文件启动redis服务

   ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-jOypL57Z-1597890996511)(狂神说 Redis.assets/image-20200813114030597.png)]](https://img-blog.csdnimg.cn/20200820104228556.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

8. 使用redis-cli连接指定的端口号测试，**Redis的默认端口6379**

   ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-LnDaISQ4-1597890996512)(狂神说 Redis.assets/image-20200813114045299.png)]](https://img-blog.csdnimg.cn/20200820104243223.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

9. 查看redis进程是否开启

   ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-9PhN1jC1-1597890996513)(狂神说 Redis.assets/image-20200813114103769.png)]](https://img-blog.csdnimg.cn/20200820104300532.png#pic_center)

10. 关闭Redis服务 `shutdown`

    ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-Y54EuOYm-1597890996514)(狂神说 Redis.assets/image-20200813114116691.png)]](https://img-blog.csdnimg.cn/20200820104314297.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

11. 再次查看进程是否存在

12. 后面我们会使用单机多Redis启动集群测试

### 测试性能

**redis-benchmark** 是一个压力测试工具！

官方自带的性能测试工具，参数选项如下：

![](https://img-blog.csdnimg.cn/20200513214125892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg3MzIyNw==,size_16,color_FFFFFF,t_70)

**简单测试：**

```bash
# 测试：100个并发连接  100000请求
redis-benchmark -h localhost -p 6379 -c 100 -n 100000
```

![](https://img-blog.csdnimg.cn/20200820104343472.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

### 基础知识

>  **redis默认有16个数据库**

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-v2S3n3Si-1597890996516)(狂神说 Redis.assets/image-20200813114158322.png)]](https://img-blog.csdnimg.cn/20200820104357466.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

默认使用的是第0个

默认使用DB 0 ，可以使用`select n`切换到DB n，`dbsize`可以查看当前数据库的大小，与key数量相关。

```shell
127.0.0.1:6379> config get databases # 命令行查看数据库数量databases
1) "databases"
2) "16"

127.0.0.1:6379> select 8 # 切换数据库 DB 8
OK
127.0.0.1:6379[8]> dbsize # 查看数据库大小
(integer) 0

# 不同数据库之间 数据是不能互通的，并且dbsize 是根据库中key的个数。
127.0.0.1:6379> set name sakura 
OK
127.0.0.1:6379> SELECT 8
OK
127.0.0.1:6379[8]> get name # db8中并不能获取db0中的键值对。
(nil)
127.0.0.1:6379[8]> DBSIZE
(integer) 0
127.0.0.1:6379[8]> SELECT 0
OK
127.0.0.1:6379> keys *
1) "counter:__rand_int__"
2) "mylist"
3) "name"
4) "key:__rand_int__"
5) "myset:__rand_int__"
127.0.0.1:6379> DBSIZE # size和key个数相关
(integer) 5
127.0.0.1:6379> flushdb # 清除当前数据库
OK
127.0.0.1:6379> flushall # 清除全部数据库内容
OK
```

**`keys *`** ：查看当前数据库中所有的key。

**`flushdb`**：清空当前数据库中的键值对。

**`flushall`**：清空所有数据库的键值对。



> **Redis是单线程的！**

Redis是很快的，官方表示：Redis是基于内存操作，CPU不是Redis性能瓶颈，Redis的瓶颈是根据机器的内存和网络带宽，既然可以使用单线程来实现，就使用单线程了！所以就使用了单线程！

Redis是C语言写的，官方提供的数据为 100000+ 的QPS，完全不比同样是使用`key-value`的Memecache差

**Redis为什么单线程还这么快**

1. 误区1：高性能的服务器一定是多线程的
2. 误区2：多线程（CPU上下文会切换）一定比单线程效率高

**核心：Redis是将所有的数据全部放在内存中，所以说使用单线程去操作效率就是最高的，多线程（CPU上下文会切换：耗时的操作），对于内存系统来说，如果没有上下文切换效率就是最高的。多次读写都是在一个CPU上的，在内存情况下，这个就是最佳的方案**

## 三、五大数据类型

Redis是一个开源（BSD许可），内存存储的数据结构服务器，可用作**数据库，高速缓存和消息队列代理**。它支持字符串、哈希表、列表、集合、有序集合，位图，hyperloglogs等数据类型。内置复制、Lua脚本、LRU收回、事务以及不同级别磁盘持久化功能，同时通过Redis Sentinel提供高可用，通过Redis Cluster提供自动分区。

### Redis-key

> **在redis中无论什么数据类型，在数据库中都是以key-value形式保存，通过进行对Redis-key的操作，来完成对数据库中数据的操作。**

下面学习的命令：

- **`exists key`**：判断键是否存在
- **`del key`**：删除键值对
- **`move key db`**：将键值对移动到指定数据库
- **`expire key second`**：设置键值对的过期时间
- **`type key`**：查看value的数据类型

```shell
127.0.0.1:6379> keys * # 查看当前数据库所有key
(empty list or set)
127.0.0.1:6379> set name qinjiang # set key
OK
127.0.0.1:6379> set age 20
OK
127.0.0.1:6379> keys *
1) "age"
2) "name"
127.0.0.1:6379> move age 1 # 将键值对移动到指定数据库
(integer) 1
127.0.0.1:6379> EXISTS age # 判断键是否存在
(integer) 0 # 不存在
127.0.0.1:6379> EXISTS name
(integer) 1 # 存在
127.0.0.1:6379> SELECT 1
OK
127.0.0.1:6379[1]> keys *
1) "age"
127.0.0.1:6379[1]> del age # 删除键值对
(integer) 1 # 删除个数


127.0.0.1:6379> set age 20
OK
127.0.0.1:6379> EXPIRE age 15 # 设置键值对的过期时间

(integer) 1 # 设置成功 开始计数
127.0.0.1:6379> ttl age # 查看key的过期剩余时间
(integer) 13
127.0.0.1:6379> ttl age
(integer) 11
127.0.0.1:6379> ttl age
(integer) 9
127.0.0.1:6379> ttl age
(integer) -2 # -2 表示key过期，-1表示key未设置过期时间

127.0.0.1:6379> get age # 过期的key 会被自动delete
(nil)
127.0.0.1:6379> keys *
1) "name"

127.0.0.1:6379> type name # 查看value的数据类型
string
```

**关于TTL命令**

Redis的key，通过TTL命令返回key的过期时间，一般来说有3种：

- 当前key没有设置过期时间，所以会返回-1.
- 当前key有设置过期时间，而且key已经过期，所以会返回-2.
- 当前key有设置过期时间，且key还没有过期，故会返回key的正常剩余时间.

**关于重命名RENAME和RENAMENX**

- RENAME key newkey修改 key 的名称
- RENAMENX key newkey仅当 newkey 不存在时，将 key 改名为 newkey 。

更多命令学习：https://www.redis.net.cn/order/

### String（字符串）

```shell
#######################################
127.0.0.1:6379> set key1 v1		# 设置值
OK
127.0.0.1:6379> get key1		# 获得值
"v1"
127.0.0.1:6379> keys *			# 获得所有的key
1) "key1"
127.0.0.1:6379> EXISTS key1		# 判断某一个key是否存在
(integer) 1
127.0.0.1:6379> APPEND key1 "hello"	# 追加字符串，如果当前key不存在，就相当于setkey
(integer) 7
127.0.0.1:6379> get key1
"v1hello"
127.0.0.1:6379> STRLEN key1		# 获取字符串的长度
(integer) 7
127.0.0.1:6379> APPEND key1 ",zhaocan"
(integer) 15
127.0.0.1:6379> STRLEN key1
(integer) 17
127.0.0.1:6379> get key1
"v1hello,zhaocan"
#######################################
# 步长
127.0.0.1:6379> set views 0	# 初始浏览量为0
OK
127.0.0.1:6379> get views
"0"
127.0.0.1:6379> incr views	# 自增1，浏览量+1
(integer) 1
127.0.0.1:6379> incr views
(integer) 2
127.0.0.1:6379> get views
"2"
127.0.0.1:6379> decr views	# 自减一，浏览量-1
(integer) 1
127.0.0.1:6379> decr views
(integer) 0
127.0.0.1:6379> decr views
(integer) -1
127.0.0.1:6379> get views
"-1"
127.0.0.1:6379> INCRBY views 10	# 可以设置步长，指定增量
(integer) 9
127.0.0.1:6379> INCRBY views 10
(integer) 19
127.0.0.1:6379> DECRBY views 5
(integer) 14

#######################################
# 字符串范围 range
127.0.0.1:6379> set key1 "hello,zhaocan"	# 设置key1的值
OK
127.0.0.1:6379> get key1
"hello,zhaocan"
127.0.0.1:6379> GETRANGE key1 0 3	# 截取字符串[0,3]
"hell"
127.0.0.1:6379> GETRANGE key1 0 -1	# 获取全部的字符串 和 get key是一样的
"hello,zhaocan"

# 替换
127.0.0.1:6379> set key2 abcdefg
OK
127.0.0.1:6379> get key2
"abcdefg"
127.0.0.1:6379> SETRANGE key2 1 xx	# 替换指定位置开始的字符串
(integer) 7
127.0.0.1:6379> get key2
"axxdefg"

#######################################
# setex(set with expire)	设置过期时间
# setnx(set if not expire)	不存在再设置（在分布式锁中会常常使用）

127.0.0.1:6379> setex key3 30 "hello"	# 设置key3 值为hello，30秒后过期
OK
127.0.0.1:6379> ttl key3
(integer) 26
127.0.0.1:6379> get key3
"hello"
127.0.0.1:6379> setnx mykey "redis"	# 如果mykey不存在，创建mykey
(integer) 1
127.0.0.1:6379> keys *
1) "key2"
2) "mykey"
3) "key1"
127.0.0.1:6379> ttl key3
(integer) -2
127.0.0.1:6379> setnx mykey "mongodb"	# 如果mykey存在，创建失败
(integer) 0
127.0.0.1:6379> get mykey
"redis"

#######################################
# mset
# mget

127.0.0.1:6379> mset k1 v1 k2 v2 k3 v3	# 同时设置多个值
OK
127.0.0.1:6379> keys *
1) "k1"
2) "k2"
3) "k3"
127.0.0.1:6379> mget k1 k2 k3	# 同时获取多个值
1) "v1"
2) "v2"
3) "v3"
127.0.0.1:6379> msetnx k1 v1 k4 v4	# msetnx 是一个原子性操作，要么一起成功，要么一起失败
(integer) 0
127.0.0.1:6379> get k4
(nil)

# 对象
set user:1 {name:zhangsan,age:3}	# 设置一个user:1 对象，值为json字符串来保存一个对象

# 这里的key是一个巧妙的设计： user:{id}:{filed}，如此设计在Redis中是完全OK的

127.0.0.1:6379> mset user:1:name zhangsan user:1:age 2
OK
127.0.0.1:6379> mget user:1:name user:1:age
1) "zhangsan"
2) "2"
#######################################
getset	# 先get再set

127.0.0.1:6379> getset db redis		# 如果不存在值，则返回nil
(nil)
127.0.0.1:6379> get db
"redis"
127.0.0.1:6379> getset db mongodb	# 如果存在值，获取原来的值，并设置新的值
"redis"
127.0.0.1:6379> get db
"mongodb"
```

数据结构是相同的！

##### String类型的使用场景

value除了是我们的字符串还可以是我们的数字！

- 计数器
- 统计多单位的数量
- 粉丝数量
- 对象缓存存储

|                命令                |                             描述                             |                           **示例**                           |
| :--------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|          APPEND key value          |                向指定的key的value后追加字符串                | 127.0.0.1:6379> set msg hello OK 127.0.0.1:6379> append msg " world" (integer) 11 127.0.0.1:6379> get msg “hello world” |
|           DECR/INCR key            |          将指定key的value数值进行+1/-1(仅对于数字)           | 127.0.0.1:6379> set age 20 OK 127.0.0.1:6379> incr age (integer) 21 127.0.0.1:6379> decr age (integer) 20 |
|        INCRBY/DECRBY key n         |                  按指定的步长对数值进行加减                  | 127.0.0.1:6379> INCRBY age 5 (integer) 25 127.0.0.1:6379> DECRBY age 10 (integer) 15 |
|         INCRBYFLOAT key n          |                     为数值加上浮点型数值                     |          127.0.0.1:6379> INCRBYFLOAT age 5.2 “20.2”          |
|             STRLEN key             |                  获取key保存值的字符串长度                   | 127.0.0.1:6379> get msg “hello world” 127.0.0.1:6379> STRLEN msg (integer) 11 |
|       GETRANGE key start end       |         按起止位置获取字符串（闭区间，起止位置都取）         | 127.0.0.1:6379> get msg “hello world” 127.0.0.1:6379> GETRANGE msg 3 9 “lo worl” |
|     SETRANGE key offset value      |            用指定的value 替换key中 offset开始的值            | 127.0.0.1:6379> SETRANGE msg 2 hello (integer) 7 127.0.0.1:6379> get msg “tehello” |
|          GETSET key value          |  将给定 key 的值设为 value ，并返回 key 的旧值(old value)。  |        127.0.0.1:6379> GETSET msg test “hello world”         |
|          SETNX key value           |                    仅当key不存在时进行set                    | 127.0.0.1:6379> SETNX msg test (integer) 0 127.0.0.1:6379> SETNX name sakura (integer) 1 |
|      SETEX key seconds value       |                   set 键值对并设置过期时间                   | 127.0.0.1:6379> setex name 10 root OK 127.0.0.1:6379> get name (nil) |
|  MSET key1 value1 [key2 value2..]  |                        批量set键值对                         |          127.0.0.1:6379> MSET k1 v1 k2 v2 k3 v3 OK           |
| MSETNX key1 value1 [key2 value2..] |      批量设置键值对，仅当参数中所有的key都不存在时执行       |        127.0.0.1:6379> MSETNX k1 v1 k4 v4 (integer) 0        |
|         MGET key1 [key2..]         |                   批量获取多个key保存的值                    |    127.0.0.1:6379> MGET k1 k2 k3 1) “v1” 2) “v2” 3) “v3”     |
|   PSETEX key milliseconds value    |   和 SETEX 命令相似，但它以毫秒为单位设置 key 的生存时间，   |                                                              |
|          getset key value          | 如果不存在值，则返回nil，如果存在值，获取原来的值，并设置新的值 |                                                              |

### List(列表)

> **Redis列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边）**
>
> **一个列表最多可以包含 232 - 1 个元素 (4294967295, 每个列表超过40亿个元素)。**

首先我们列表，可以经过规则定义将其变为队列、栈、双端队列等

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-VPvbIltc-1597890996518)(狂神说 Redis.assets/image-20200813114255459.png)]](https://img-blog.csdnimg.cn/20200820104440398.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

在redis里面，我们可以把list玩成，栈、队列、阻塞队列！

所有的list命令都是用`l`开头的，Redis不区分大小写命令

|                 命令                  |                           **描述**                           |
| :-----------------------------------: | :----------------------------------------------------------: |
|   LPUSH/RPUSH key value1[value2..]    |          从左边/右边向列表中PUSH值(一个或者多个)。           |
|         LRANGE key start end          |          获取list 起止元素==（索引从左往右 递增）==          |
|        LPUSHX/RPUSHX key value        |            向已存在的列名中push值（一个或者多个）            |
| LINSERT key BEFORE\|AFTER pivot value |               在指定列表元素的前/后 插入value                |
|               LLEN key                |                         查看列表长度                         |
|           LINDEX key index            |                     通过索引获取列表元素                     |
|         LSET key index value          |                      通过索引为元素设值                      |
|             LPOP/RPOP key             |                 从最左边/最右边移除值 并返回                 |
|     RPOPLPUSH source destination      | 将列表的尾部(右)最后一个值弹出，并返回，然后加到另一个列表的头部 |
|          LTRIM key start end          |                 通过下标截取指定范围内的列表                 |
|         LREM key count value          | List中是允许value重复的 `count > 0`：从头部开始搜索 然后删除指定的value 至多删除count个 `count < 0`：从尾部开始搜索… `count = 0`：删除列表中所有的指定value。 |
|     BLPOP/BRPOP key1[key2] timout     | 移出并获取列表的第一个/最后一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。 |
| BRPOPLPUSH source destination timeout | 和`RPOPLPUSH`功能相同，如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。 |



```shell
#######################################
127.0.0.1:6379> LPUSH list one	# 将一个值或者多个值，插入到列表头部（左）
(integer) 1
127.0.0.1:6379> LPUSH list two
(integer) 2
127.0.0.1:6379> LPUSH list three
(integer) 3
127.0.0.1:6379> LRANGE list 0 -1	# 获取list中的值
1) "three"
2) "two"
3) "one"
127.0.0.1:6379> LRANGE list 0 1	# 通过区间获取具体的值
1) "three"
2) "two"
127.0.0.1:6379> Rpush list right	# 将一个值或者多个值，插入到列表尾部（右）	
(integer) 4
127.0.0.1:6379> LRANGE list 0 -1	
1) "three"
2) "two"
3) "one"
4) "right"

#######################################
# 移除元素
LPOP
RPOP
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
3) "one"
4) "right"
127.0.0.1:6379> Lpop list	# 移除list的第一个元素
"three"
127.0.0.1:6379> Rpop list	# 移除list的最后一个元素
"right"
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"

#######################################
# 下标
Lindex
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"
127.0.0.1:6379> lindex list 1	# 通过下标获得 list 中的某一个值
"one"
127.0.0.1:6379> lindex list 0
"two"

#######################################
# 获得长度
Llen
127.0.0.1:6379> Llen list	# 返回列表的长度
(integer) 2

#######################################
# 移除指定的值
Lrem
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "three"
3) "two"
4) "one"
127.0.0.1:6379> lrem list 1 one		# 移除list集合中指定个数的value，精确匹配
(integer) 1
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "three"
3) "two"
127.0.0.1:6379> lrem list 1 three
(integer) 1
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
127.0.0.1:6379> Lpush list three
(integer) 3
127.0.0.1:6379> lrem list 2 three
(integer) 2
127.0.0.1:6379> LRANGE list 0 -1
1) "two"

#######################################
# 修剪，截断
ltrim 
127.0.0.1:6379> keys *
(empty list or set)
127.0.0.1:6379> Rpush mylist "hello"
(integer) 1
127.0.0.1:6379> Rpush mylist "hello1"
(integer) 2
127.0.0.1:6379> Rpush mylist "hello2"
(integer) 3
127.0.0.1:6379> Rpush mylist "hello3"
(integer) 4
127.0.0.1:6379> ltrim mylist 1 2	# 通过下标截取指定的长度，这个list已经被改变了，截断了只剩下截取的元素！
OK
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello1"
2) "hello2"

#######################################
rpoplpush	# 移除列表的最后一个元素，并将它移动到新的list中
127.0.0.1:6379> Rpush mylist "hello"
(integer) 1
127.0.0.1:6379> Rpush mylist "hello1"
(integer) 2
127.0.0.1:6379> Rpush mylist "hello2"
(integer) 3
127.0.0.1:6379> rpoplpush mylist myotherlist	# 移除列表的最后一个元素，将他移动到新的列表中
"hello2"
127.0.0.1:6379> LRANGE mylist 0 -1	# 查看原来的列表
1) "hello"
2) "hello1"
127.0.0.1:6379> LRANGE myotherlist 0 -1	# 查看目标列表中，存在该值
1) "hello2"

#######################################
lset	# 将列表中指定下标的值替换为另外一个值
127.0.0.1:6379> EXISTS list		# 判断这个列表是否存在
(integer) 0
127.0.0.1:6379> lset list 0 item	# 如果不存在列表我们去更新就会报错
(error) ERR no such key
127.0.0.1:6379> lpush list value1
(integer) 1
127.0.0.1:6379> LRANGE list 0 0
1) "value1"
127.0.0.1:6379> lset list 0 item	# 如果存在，更新当前下标的值
OK
127.0.0.1:6379> LRANGE list 0 0
1) "item"
127.0.0.1:6379> lset list 1 other	# 如果不存在，则会报错
(error) ERR index out of range

#######################################
linsert	# 将某个具体的value插入到列中某个元素的前面或者后面
127.0.0.1:6379> Rpush mylist "hello"
(integer) 1
127.0.0.1:6379> Rpush mylist "world"
(integer) 2
127.0.0.1:6379> LINSERT mylist before "world" "before"
(integer) 3
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "before"
3) "world"
127.0.0.1:6379> LINSERT mylist after "world" "after"
(integer) 4
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "before"
3) "world"
4) "after"
```

> 小结

- 实际上是一个链表，before Node after，left，right都可以插入值
- 如果key不存在，创建新的链表
- 如果key存在，新增内容
- 如果移除了所有值，空链表，也代表不存在
- 在两边插入或者改动值，效率最高！中间元素，相对来说效率会低一些

**应用：**

**消息排队！消息队列（Lpush Rpop）,栈（Lpush Lpop）**

### Set(集合)

> **Redis的Set是string类型的无序集合。集合成员是唯一的，这就意味着集合中不能出现重复的数据。**
>
> **Redis 中 集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是O(1)。**
>
> **集合中最大的成员数为 232 - 1 (4294967295, 每个集合可存储40多亿个成员)。**

set中的值是不能重复的

|                  命令                   |                             描述                             |
| :-------------------------------------: | :----------------------------------------------------------: |
|       SADD key member1[member2..]       |                向集合中无序增加一个/多个成员                 |
|                SCARD key                |                       获取集合的成员数                       |
|              SMEMBERS key               |                     返回集合中所有的成员                     |
|          SISMEMBER key member           |         查询member元素是否是集合的成员,结果是无序的          |
|         SRANDMEMBER key [count]         |          随机返回集合中count个成员，count缺省值为1           |
|            SPOP key [count]             |       随机移除并返回集合中count个成员，count缺省值为1        |
|     SMOVE source destination member     |        将source集合的成员member移动到destination集合         |
|       SREM key member1[member2..]       |                   移除集合中一个/多个成员                    |
|           SDIFF key1[key2..]            |              返回所有集合的差集 key1- key2 - …               |
|   SDIFFSTORE destination key1[key2..]   | 在SDIFF的基础上，将结果保存到集合中==(覆盖)==。不能保存到其他类型key噢！ |
|          SINTER key1 [key2..]           |                      返回所有集合的交集                      |
|  SINTERSTORE destination key1[key2..]   |           在SINTER的基础上，存储结果到集合中。覆盖           |
|          SUNION key1 [key2..]           |                      返回所有集合的并集                      |
|  SUNIONSTORE destination key1 [key2..]  |           在SUNION的基础上，存储结果到及和张。覆盖           |
| SSCAN KEY [MATCH pattern] [COUNT count] |   在大量数据环境下，使用此命令遍历集合中元素，每次遍历部分   |



```shell
#######################################
127.0.0.1:6379> sadd myset "hello"	# set集合中添加元素
(integer) 1
127.0.0.1:6379> sadd myset "zhaocan"	
(integer) 1
127.0.0.1:6379> sadd myset "23333"
(integer) 1
127.0.0.1:6379> SMEMBERS myset	# 查看指定set的所有值
1) "hello"
2) "zhaocan"
3) "23333"
127.0.0.1:6379> SISMEMBER myset hello	# 判断某一个值是不是在set集合中
(integer) 1
127.0.0.1:6379> SISMEMBER myset world
(integer) 0

#######################################
127.0.0.1:6379> scard myset	# 获取set集合中的内容元素个数
(integer) 4

#######################################
127.0.0.1:6379> srem myset hello	# 移除set集合中的指定元素
(integer) 1
127.0.0.1:6379> scard myset
(integer) 3
127.0.0.1:6379> SMEMBERS myset
1) "zhaocan1"
2) "zhaocan"
3) "23333"

#######################################
set 无序不重复集合

127.0.0.1:6379> SMEMBERS myset
1) "zhaocan1"
2) "zhaocan"
3) "23333"
127.0.0.1:6379> SRANDMEMBER myset	# 随机抽取选出一个元素
"zhaocan"
127.0.0.1:6379> SRANDMEMBER myset
"zhaocan"
127.0.0.1:6379> SRANDMEMBER myset
"zhaocan"
127.0.0.1:6379> SRANDMEMBER myset 2	# 随机抽取出指定个数的元素
1) "zhaocan"
2) "zhaocan1"
127.0.0.1:6379> SRANDMEMBER myset
"23333"

#######################################
随机删除key
127.0.0.1:6379> SMEMBERS myset
1) "zhaocan1"
2) "zhaocan"
3) "23333"
127.0.0.1:6379> spop myset	# 随机删除一些set集合中的元素
"zhaocan1"
127.0.0.1:6379> spop myset
"zhaocan"
127.0.0.1:6379> SMEMBERS myset
1) "23333"

#######################################
将一个指定的值，移动到另一个set集合中
127.0.0.1:6379> sadd myset "hello"
(integer) 1
127.0.0.1:6379> sadd myset "world"
(integer) 1
127.0.0.1:6379> sadd myset "zhaocan"
(integer) 1
127.0.0.1:6379> sadd myset2 "set2"
(integer) 1
127.0.0.1:6379> smove myset myset2 "zhaocan"	# 将一个指定的值，移动到另一个set集合中
(integer) 1
127.0.0.1:6379> SMEMBERS myset
1) "world"
2) "hello"
127.0.0.1:6379> SMEMBERS myset2
1) "zhaocan"
2) "set2"

#######################################
共同关注（并集）
数字集合类：
	- 差集
	- 交集
	- 并集
127.0.0.1:6379> SDEFF key1 key2		# 差集
1) "b"
2) "a"
127.0.0.1:6379> SINTER key1 key2	# 交集，共同好友就可以这样实现
1) "c"
127.0.0.1:6379> SUNION key1 key2	# 并集
1) "b"
2) "c"
3) "e"
4) "a"
5) "d"
```

### Hash（哈希）

> **Redis hash 是一个string类型的field和value的映射表，hash特别适合用于存储对象。**
>
> **Set就是一种简化的Hash,只变动key,而value使用默认值填充。可以将一个Hash表作为一个对象进行存储，表中存放对象的信息。**

|                    **命令**                    |                           **描述**                           |
| :--------------------------------------------: | :----------------------------------------------------------: |
|              HSET key field value              | 将哈希表 key 中的字段 field 的值设为 value 。重复设置同一个field会覆盖,返回0 |
|   HMSET key field1 value1 [field2 value2..]    |    同时将多个 field-value (域-值)对设置到哈希表 key 中。     |
|             HSETNX key field value             |       只有在字段 field 不存在时，设置哈希表字段的值。        |
|               HEXISTS key field                |           查看哈希表 key 中，指定的字段是否存在。            |
|              HGET key field value              |                获取存储在哈希表中指定字段的值                |
|          HMGET key field1 [field2..]           |                     获取所有给定字段的值                     |
|                  HGETALL key                   |                获取在哈希表key 的所有字段和值                |
|                   HKEYS key                    |                  获取哈希表key中所有的字段                   |
|                    HLEN key                    |                    获取哈希表中字段的数量                    |
|                   HVALS key                    |                      获取哈希表中所有值                      |
|           HDEL key field1 [field2..]           |              删除哈希表key中一个/多个field字段               |
|              HINCRBY key field n               | 为哈希表 key 中的指定字段的整数值加上增量n，并返回增量后结果 一样只适用于整数型字段 |
|            HINCRBYFLOAT key field n            |       为哈希表 key 中的指定字段的浮点数值加上增量 n。        |
| HSCAN key cursor [MATCH pattern] [COUNT count] |                    迭代哈希表中的键值对。                    |

相当于java中的Map集合，key-map！这个值是一个map集合！本质和String类型没有太大区别，还是一个简单的key-value

```shell
127.0.0.1:6379> hset myhash field1 "zhaocan"	# set一个具体的key-value
(integer) 1
127.0.0.1:6379> hget myhash field1
"zhaocan"
127.0.0.1:6379> hmset myhash field1 "hello" field2 "world"	# set多个key-value
OK
127.0.0.1:6379> hmget myhash field1 field2	# 获取多个字段值
1) "hello"
2) "world"
127.0.0.1:6379> hgetall myhash	# 获取全部的数据
1) "field1"
2) "hello"
3) "field2"
4) "world"
127.0.0.1:6379> hdel myhash field1	# 删除hash指定的key字段！对应的value值也就消失了
(integer) 1
127.0.0.1:6379> hgetall myhash
1) "field2"
2) "world"

#######################################
hlen
127.0.0.1:6379> hmset myhash field1 "hello" field2 "world"
OK
127.0.0.1:6379> hgetall myhash
1) "field2"
2) "world"
3) "field1"
4) "hello"
127.0.0.1:6379> hlen myhash	# 获取hash表的字段数量
(integer) 2

#######################################
127.0.0.1:6379> HEXISTS myhash field1	# 判断hash中的指定的字段是否存在
(integer) 1
127.0.0.1:6379> HEXISTS myhash field3
(integer) 0

#######################################
# 只获得所有的field
# 只获得所有的value
127.0.0.1:6379> hkeys myhash	# 只获得所有field
1) "field2"
2) "field1"
127.0.0.1:6379> hvals myhash	# 只获得所有value
1) "world"
2) "hello"

#######################################
incr	decr

127.0.0.1:6379> hset myhash field3 5	# 指定增量
(integer) 1
127.0.0.1:6379> HINCRBY myhash field3 1
(integer) 6
127.0.0.1:6379> HINCRBY myhash field3 -1
(integer) 5
127.0.0.1:6379> hsetnx myhash field4 hello	# 如果不存在则可以设置
(integer) 1
127.0.0.1:6379> hsetnx myhash field4 world	# 如果存在则不可设置
(integer) 0
```

hash变更的数据，尤其是用户信息之类的，经常变动的信息！hash更适合于对象的存储，String更适合字符串存储

### Zset（有序集合）

> **不同的是每个元素都会关联一个double类型的分数（score）。redis正是通过分数来为集合中的成员进行从小到大的排序。**
>
> **score相同：按字典顺序排序**
>
> **有序集合的成员是唯一的,但分数(score)却可以重复。**

|                    **命令**                     |                             描述                             |
| :---------------------------------------------: | :----------------------------------------------------------: |
|     ZADD key score member1 [score2 member2]     |    向有序集合添加一个或多个成员，或者更新已存在成员的分数    |
|                    ZCARD key                    |                     获取有序集合的成员数                     |
|               ZCOUNT key min max                |            计算在有序集合中指定区间score的成员数             |
|              ZINCRBY key n member               |             有序集合中对指定成员的分数加上增量 n             |
|                ZSCORE key member                |                  返回有序集中，成员的分数值                  |
|                ZRANK key member                 |                 返回有序集合中指定成员的索引                 |
|              ZRANGE key start end               |          通过索引区间返回有序集合成指定区间内的成员          |
|             ZRANGEBYLEX key min max             |                通过字典区间返回有序集合的成员                |
|            ZRANGEBYSCORE key min max            | 通过分数返回有序集合指定区间内的成员==-inf 和 +inf分别表示最小最大值，只支持开区间()== |
|              ZLEXCOUNT key min max              |            在有序集合中计算指定字典区间内成员数量            |
|          ZREM key member1 [member2..]           |                 移除有序集合中一个/多个成员                  |
|           ZREMRANGEBYLEX key min max            |            移除有序集合中给定的字典区间的所有成员            |
|         ZREMRANGEBYRANK key start stop          |            移除有序集合中给定的排名区间的所有成员            |
|          ZREMRANGEBYSCORE key min max           |            移除有序集合中给定的分数区间的所有成员            |
|             ZREVRANGE key start end             |     返回有序集中指定区间内的成员，通过索引，分数从高到底     |
|          ZREVRANGEBYSCORRE key max min          |      返回有序集中指定分数区间内的成员，分数从高到低排序      |
|           ZREVRANGEBYLEX key max min            |       返回有序集中指定字典区间内的成员，按字典顺序倒序       |
|               ZREVRANK key member               | 返回有序集合中指定成员的排名，有序集成员按分数值递减(从大到小)排序 |
| ZINTERSTORE destination numkeys key1 [key2 ..]  | 计算给定的一个或多个有序集的交集并将结果集存储在新的有序集合 key 中，numkeys：表示参与运算的集合数，将score相加作为结果的score |
|  ZUNIONSTORE destination numkeys key1 [key2..]  | 计算给定的一个或多个有序集的交集并将结果集存储在新的有序集合 key 中 |
| ZSCAN key cursor [MATCH pattern\] [COUNT count] |        迭代有序集合中的元素（包括元素成员和元素分值）        |

在set的基础上，增加了一个值

```shell
127.0.0.1:6379> zadd myset 1 one	# 添加一个值
(integer) 1
127.0.0.1:6379> zadd myset 2 two 3 three	# 添加多个值
(integer) 2
127.0.0.1:6379> ZRANGE myset 0 -1
1) "one"
2) "two"
3) "three"

#######################################
# 排序如何实现
127.0.0.1:6379> zadd salary 2500 xiaohong	# 添加3个用户
(integer) 1
127.0.0.1:6379> zadd salary 5000 zhangsan
(integer) 1
127.0.0.1:6379> zadd salary 500 lisi
(integer) 1
# ZRANGEBYSCORE key min max
127.0.0.1:6379> ZRANGEBYSCORE salary -inf +inf	# 显示全部的用户，从小到大排序
1) "lisi"
2) "xiaohong"
3) "zhangsan"
127.0.0.1:6379> ZREVRANGE salary 0 -1	# 从大到小排序
1) "zhangsan"
2) "xiaohong"
3) "lisi"
127.0.0.1:6379> ZRANGEBYSCORE salary -inf +inf withscores	# 显示全部的用户，并且携带成绩
1) "lisi"
2) "500"
3) "xiaohong"
4) "2500"
5) "zhangsan"
6) "5000"
127.0.0.1:6379> ZRANGEBYSCORE salary -inf 2500 withscores	# 显示工资小于2500员工的降序排列
1) "lisi"
2) "500"
3) "xiaohong"
4) "2500"

#######################################
# 移除rem中的元素
127.0.0.1:6379> ZRANGE salary 0 -1
1) "lisi"
2) "xiaohong"
3) "zhangsan"
127.0.0.1:6379> zrem salary xiaohong	# 移除有序集合中的指定元素
(integer) 1
127.0.0.1:6379> zrem salary 0 -1
1) "lisi"
2) "zhangsan"
127.0.0.1:6379> zcard salary	# 获取有序集合中的个数
(integer) 2

#######################################
127.0.0.1:6379> zadd myset 1 "hello" 2 "world" 3 "zhaocan"
(integer) 3
127.0.0.1:6379> zcount myset 1 3	# 获取指定区间的成员数量
(integer) 3
127.0.0.1:6379> zcount myset 1 2
(integer) 2
```

应用案例：

- set排序 存储班级成绩表 工资表排序！
- 普通消息，1.重要消息 2.带权重进行判断
- 排行榜应用实现，取Top N测试

### Geospatial

可以推算地理位置的信息，两地之间的距离，方圆几公里之内的人

需要注意：

- 地球南北两极无法直接添加，
- 一般会下载城市数据，直接通过Java程序一次性导入
- 有效经纬度范围从-180到180，超出范围时会返回错误，
- key由（纬度，经度，名称）构成

查看官网，一共有六个相关命令

![image-20201121151049547](https://img-blog.csdnimg.cn/img_convert/cc6822bd1dd72a093e473b845255785c.png)

- add、dist、hash、pos、radius、rediusbymember
- geodist 返回两个给定位置之间的距离
- geohash 返回geohash对位置进行的编码，用于内部调试，一般用不到
- geopos 返回指定member的经纬度信息
- georadius ： 根据半径查找，需要给定中心点数据
- georadiusbymember ： 也是根据半径查找，但是中心点是已经存在的member
- zrange 遍历member
- zrem 移除member

> geoadd

```shell
# geoadd 添加地理位置
# 规则：两级无法直接添加，一般会下载城市数据，直接通过java程序一次性
# 参数 key 值（经度、纬度、名称）
127.0.0.1:6379[1]> geoadd china:city 116.40 39.90 beijing
(integer) 1
127.0.0.1:6379[1]> geoadd china:city 121.47 31.23 shanghai
(integer) 1
127.0.0.1:6379[1]> geoadd china:city 106.50 29.53 chongqing
(integer) 1
127.0.0.1:6379[1]> geoadd china:city 114.08 22.54 shenzhen 
(integer) 1
127.0.0.1:6379[1]> geoadd china:city 120.16 30.24 hangzhou 108.96 34.26 xian
(integer) 2
```

## 四、事务

Redis事务本质：一组命令的集合！一个事务中的所有命令都会被序列化，在事务执行的过程中，会按照顺序执行

一次性、顺序性、排他性！执行一系列的命令！

**Redis事务没有隔离级别的概念！**

**所有的命令在事务中，并没有直接被执行！只有发起执行命令的时候才会执行！Exec**

**Redis单条命令是保证原子性的，但是事务不保证原子性！**

redis的事务：

- 开启事务（multi）
- 命令入队（...）
- 执行事务（exec）

> 正常执行事务！

```shell
127.0.0.1:6379[1]> multi	# 开启事务
OK
# 命令入队
127.0.0.1:6379[1](TX)> set k1 v1
QUEUED
127.0.0.1:6379[1](TX)> set k2 v2
QUEUED
127.0.0.1:6379[1](TX)> get k2
QUEUED
127.0.0.1:6379[1](TX)> set k3 v3
QUEUED
127.0.0.1:6379[1](TX)> exec	# 执行事务
1) OK
2) OK
3) "v2"
4) OK
```

> 放弃事务

```shell
127.0.0.1:6379[1]> multi	# 开启事务
OK
127.0.0.1:6379[1](TX)> set k1 v1
QUEUED
127.0.0.1:6379[1](TX)> set k2 v2
QUEUED
127.0.0.1:6379[1](TX)> set k4 v4
QUEUED
127.0.0.1:6379[1](TX)> discard 	# 取消事务
OK
127.0.0.1:6379[1]> get k4	# 事务队列中的命令都不会被执行
(nil)
```

> 编译型异常（代码有问题！命令有错！），事务中所有的命令都不会被执行

```shell
127.0.0.1:6379[1]> multi
OK
127.0.0.1:6379[1](TX)> set k1 v1
QUEUED
127.0.0.1:6379[1](TX)> set k2 v2
QUEUED
127.0.0.1:6379[1](TX)> set k3 v3
QUEUED
127.0.0.1:6379[1](TX)> getset k3	# 错误的命令
(error) ERR wrong number of arguments for 'getset' command
127.0.0.1:6379[1](TX)> set k4 v4
QUEUED
127.0.0.1:6379[1](TX)> set k5 v5
QUEUED
127.0.0.1:6379[1](TX)> exec		# 执行事务报错
(error) EXECABORT Transaction discarded because of previous errors.
127.0.0.1:6379[1]> get k4	# 所有的命令都不会被执行
(nil)

```



> 运行时异常，如果事务队列中存在语法型错误，那么执行命令的时候，其他命令是可以正常执行的，错误命令抛出异常！

```shell
127.0.0.1:6379[1]> set k1 "v1"
OK
127.0.0.1:6379[1]> multi
OK
127.0.0.1:6379[1](TX)> incr k1	# 会执行的时候失败
QUEUED
127.0.0.1:6379[1](TX)> set k2 v2
QUEUED
127.0.0.1:6379[1](TX)> set k3 v3
QUEUED
127.0.0.1:6379[1](TX)> get k3
QUEUED
127.0.0.1:6379[1](TX)> exec
1) (error) ERR value is not an integer or out of range	# 虽然第一条命令报错了，但是依旧正常执行成功了
2) OK
3) OK
4) "v3"
127.0.0.1:6379[1]> get k2
"v2"
127.0.0.1:6379[1]> get k3
"v3"
```

### 监控

Watch

**悲观锁**：

- 悲观，认为什么时候都会出问题，无论做什么都会加锁！

**乐观锁**：

- 乐观，认为什么时候都不会出现问题，所以不会上锁！更新数据的时候去判断一下，在此期间是否有人修改过这个数据



> Redis监视测试

正常执行成功！

```shell
127.0.0.1:6379[1]> set money 100
OK
127.0.0.1:6379[1]> set out 0
OK
127.0.0.1:6379[1]> watch money	# 监视money对象
OK
127.0.0.1:6379[1]> multi	# 事务正常结束，数据期间没有发生变动，这个时候就正常执行成功
OK
127.0.0.1:6379[1](TX)> decrby money 20
QUEUED
127.0.0.1:6379[1](TX)> incrby out 20
QUEUED
127.0.0.1:6379[1](TX)> exec
1) (integer) 80
2) (integer) 20

```

> 测试多线程修改值，使用watch 可以当做redis的乐观锁操作！

```shell
127.0.0.1:6379[1]> watch money	# 监视money
OK
127.0.0.1:6379[1]> multi
OK
127.0.0.1:6379[1](TX)> decrby money 10
QUEUED
127.0.0.1:6379[1](TX)> incrby out 10
QUEUED
127.0.0.1:6379[1](TX)> exec	# 执行之前，另一个线程修改了我们的值，这个时候，就会导致事务执行失败
(nil)
```

> 解锁

```shell
127.0.0.1:6379[1]> unwatch	# 1、如果发现事务执行失败，就先解锁
OK
127.0.0.1:6379[1]> watch money	# 2、获取最新的值，再次监视
OK
127.0.0.1:6379[1]> multi
OK
127.0.0.1:6379[1](TX)> decrby money 10
QUEUED
127.0.0.1:6379[1](TX)> incrby out 10
QUEUED
127.0.0.1:6379[1](TX)> exec		# 3、对比监视的值是是否发生了变化。如果没有变化，那么可以执行成功；如果发生变化则执行失败
1) (integer) 990
2) (integer) 30
```

**如果修改失败，获取最新的值就好**

## 五、Jedis

使用Java来操作Redis

### 什么是jedis

jedis是官方推荐的java连接开发工具！使用java来操作Redis 中间件！如果要使用java操作redis，那么一定要对jedis十分的熟悉

> 测试

1. 导入对应的依赖

   ```xml
   <dependencies>
       <!-- https://mvnrepository.com/artifact/redis.clients/jedis -->
       <dependency>
           <groupId>redis.clients</groupId>
           <artifactId>jedis</artifactId>
           <version>3.6.0</version>
       </dependency>
       <dependency>
           <groupId>com.alibaba</groupId>
           <artifactId>fastjson</artifactId>
           <version>1.2.70</version>
       </dependency>
   </dependencies>
   ```

2. 编码测试

   - 连接数据库
   - 操作命令
   - 断开连接

```java
package com.zc;

import redis.clients.jedis.Jedis;

public class TestPing {
    public static void main(String[] args) {
        //  1、new Jedis对象即可
        Jedis jedis = new Jedis("127.0.0.1", 6379);
        //  jedis 所有的命令就是之前学习的所有指令
        jedis.auth("123456");
        System.out.println(jedis.ping());
    }
}

```

输出：

![](http://zhaocan.fym233.cn/wixiwruruo)

#### 常用的API

- String
- List
- Set
- Hash
- Zset

> 事务

```java
package com.zc;

import com.alibaba.fastjson.JSONObject;
import redis.clients.jedis.Jedis;
import redis.clients.jedis.Transaction;

public class TestTX {
    public static void main(String[] args) {
        Jedis jedis = new Jedis("127.0.0.1", 6379);
        jedis.auth("123456");

        jedis.flushDB();
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("hello", "world");
        jsonObject.put("name", "zhaocan");
        //  开启事务
        Transaction multi = jedis.multi();
        String result = jsonObject.toJSONString();

        try{
            multi.set("user1", result);
            multi.set("user2", result);
            int i = 1/0;    //代码抛出异常
            multi.exec();   //执行事务
        } catch (Exception e) {
            multi.discard();    //放弃事务
            e.printStackTrace();
        } finally {
            System.out.println(jedis.get("user1"));
            System.out.println(jedis.get("user2"));
            //  关闭连接
            jedis.close();
        }

    }
}

```

## 六、SpringBoot整合

SpringBoot操作数据：spring-data、jpa、jdbc、mongodb、redis！

SpringData 也是和 SpringBoot齐名的项目

说明：在SpringBoot2.x之后，原来使用的Jedis被替换为了lettuce

- jedis：采用的是直连，多个线程操作的话是不安全地。如果想要避免不安全，使用 jedis pool 连接池！更像BIO模式
- lettuce：采用netty，实例可以在多个线程中进行共享，不存在线程不安全的情况！可以减少线程数量！更像NIO模式

> **源码分析**

```java
@Bean
@ConditionalOnMissingBean(
    name = {"redisTemplate"}
)	//可以自定义一个RedisTemplate来替换默认的
@ConditionalOnSingleCandidate(RedisConnectionFactory.class)
public RedisTemplate<Object, Object> redisTemplate(RedisConnectionFactory redisConnectionFactory) {
    //	默认的RedisTemplate 没有过多的设置，redis 对象都是需要序列化的
    //	两个泛型都是Object类型，后续使用的时候需要强制类型转换
    RedisTemplate<Object, Object> template = new RedisTemplate();
    template.setConnectionFactory(redisConnectionFactory);
    return template;
}

@Bean
@ConditionalOnMissingBean	//由于String是redis中最常使用的类型，所以单独提出来了一个Bean
@ConditionalOnSingleCandidate(RedisConnectionFactory.class)
public StringRedisTemplate stringRedisTemplate(RedisConnectionFactory redisConnectionFactory) {
    StringRedisTemplate template = new StringRedisTemplate();
    template.setConnectionFactory(redisConnectionFactory);
    return template;
}
```



> **整合测试**

1. 导入依赖

   ```xml
   <dependencies>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-data-redis</artifactId>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-web</artifactId>
       </dependency>
       <dependency>
           <groupId>org.springframework.experimental</groupId>
           <artifactId>spring-native</artifactId>
           <version>${spring-native.version}</version>
       </dependency>
   
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-devtools</artifactId>
           <scope>runtime</scope>
           <optional>true</optional>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-configuration-processor</artifactId>
           <optional>true</optional>
       </dependency>
       <dependency>
           <groupId>org.projectlombok</groupId>
           <artifactId>lombok</artifactId>
           <optional>true</optional>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-test</artifactId>
           <scope>test</scope>
       </dependency>
   </dependencies>
   ```

2. 配置连接

   ```yaml
   # SpringBoot 所有的配置类，都有一个自动配置类 RedisAutoConfiguration
   # 自动配置类都会绑定一个properties 配置文件  RedisProperties
   
   # 配置redis
   spring:
     redis:
       host: 121.196.198.98
       port: 6379
       password: red123456
       database: 0
   ```

3. 测试

   ```java
   package com.zc.redis02springboot;
   
   import org.junit.jupiter.api.Test;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.test.context.SpringBootTest;
   import org.springframework.data.redis.connection.RedisConnection;
   import org.springframework.data.redis.core.RedisTemplate;
   
   @SpringBootTest
   class Redis02SpringbootApplicationTests {
   
       @Autowired
       RedisTemplate redisTemplate;
   
       @Test
       void contextLoads() {
   
           //  redisTemplate
           //  opsForValue：操作字符串，类似String
           //  opsForList：操作List，类似List
           //  opsForSet
           //  opsForHash
           //  opsForZSet
           //  opsForGeo
           //  opsForHyperLogLog
   
           //  除了基本的操作，常用的方法都可以直接通过redisTemplate来从操作，比如事务、和基本的CRUD
   
           //  获取redis的连接对象
           /*RedisConnection connection = redisTemplate.getConnectionFactory().getConnection();
           connection.flushDb();
           connection.flushAll();*/
   
           redisTemplate.opsForValue().set("mykey", "赵灿");
           System.out.println(redisTemplate.opsForValue().get("mykey"));
       }
   
   }
   ```

![](http://zhaocan.fym233.cn/9n2iae4dro)

![](http://zhaocan.fym233.cn/rsep3bl6m)

> 关于对象的保存

![](http://zhaocan.fym233.cn/w9r8puj9ij)

编写一个自己的RedisTemplate

```java
package com.zc.redis02springboot.config;

import com.fasterxml.jackson.annotation.JsonAutoDetect;
import com.fasterxml.jackson.annotation.PropertyAccessor;
import com.fasterxml.jackson.databind.ObjectMapper;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.Jackson2JsonRedisSerializer;
import org.springframework.data.redis.serializer.StringRedisSerializer;

@Configuration
public class RedisConfig {

    //  固定模板，企业中直接就可使用
    //  编写我们自己的 redisTemplate
    @Bean
    public RedisTemplate<String, Object> getTemplate(RedisConnectionFactory redisConnectionFactory) {
        //  为了开发方便，一般直接使用 <String, Object>
        RedisTemplate<String, Object> template = new RedisTemplate();
        template.setConnectionFactory(redisConnectionFactory);

        //  Json序列化配置
        Jackson2JsonRedisSerializer<Object> jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer<>(Object.class);
        template.setKeySerializer(jackson2JsonRedisSerializer);
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

### RedisUtil工具类

```java
package com.zc.redis02springboot.utils;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.connection.RedisConnection;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.stereotype.Component;
import org.springframework.util.CollectionUtils;

import java.util.Collection;
import java.util.List;
import java.util.Map;
import java.util.Set;
import java.util.concurrent.TimeUnit;

@Component
public final class RedisUtil {

    @Autowired
    private RedisTemplate<String, Object> redisTemplate;

    // =============================common============================
    /**
     * 指定缓存失效时间
     * @param key  键
     * @param time 时间(秒)
     */
    public boolean expire(String key, long time) {
        try {
            if (time > 0) {
                redisTemplate.expire(key, time, TimeUnit.SECONDS);
            }
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }

    /**
     * 根据key 获取过期时间
     * @param key 键 不能为null
     * @return 时间(秒) 返回0代表为永久有效
     */
    public long getExpire(String key) {
        return redisTemplate.getExpire(key, TimeUnit.SECONDS);
    }


    /**
     * 判断key是否存在
     * @param key 键
     * @return true 存在 false不存在
     */
    public boolean hasKey(String key) {
        try {
            return redisTemplate.hasKey(key);
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }


    /**
     * 删除缓存
     * @param key 可以传一个值 或多个
     */
    @SuppressWarnings("unchecked")
    public void del(String... key) {
        if (key != null && key.length > 0) {
            if (key.length == 1) {
                redisTemplate.delete(key[0]);
            } else {
                redisTemplate.delete((Collection<String>) CollectionUtils.arrayToList(key));
            }
        }
    }


    // ============================String=============================

    /**
     * 普通缓存获取
     * @param key 键
     * @return 值
     */
    public Object get(String key) {
        return key == null ? null : redisTemplate.opsForValue().get(key);
    }

    /**
     * 普通缓存放入
     * @param key   键
     * @param value 值
     * @return true成功 false失败
     */

    public boolean set(String key, Object value) {
        try {
            redisTemplate.opsForValue().set(key, value);
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }


    /**
     * 普通缓存放入并设置时间
     * @param key   键
     * @param value 值
     * @param time  时间(秒) time要大于0 如果time小于等于0 将设置无限期
     * @return true成功 false 失败
     */

    public boolean set(String key, Object value, long time) {
        try {
            if (time > 0) {
                redisTemplate.opsForValue().set(key, value, time, TimeUnit.SECONDS);
            } else {
                set(key, value);
            }
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }


    /**
     * 递增
     * @param key   键
     * @param delta 要增加几(大于0)
     */
    public long incr(String key, long delta) {
        if (delta < 0) {
            throw new RuntimeException("递增因子必须大于0");
        }
        return redisTemplate.opsForValue().increment(key, delta);
    }


    /**
     * 递减
     * @param key   键
     * @param delta 要减少几(小于0)
     */
    public long decr(String key, long delta) {
        if (delta < 0) {
            throw new RuntimeException("递减因子必须大于0");
        }
        return redisTemplate.opsForValue().increment(key, -delta);
    }


    // ================================Map=================================

    /**
     * HashGet
     * @param key  键 不能为null
     * @param item 项 不能为null
     */
    public Object hget(String key, String item) {
        return redisTemplate.opsForHash().get(key, item);
    }

    /**
     * 获取hashKey对应的所有键值
     * @param key 键
     * @return 对应的多个键值
     */
    public Map<Object, Object> hmget(String key) {
        return redisTemplate.opsForHash().entries(key);
    }

    /**
     * HashSet
     * @param key 键
     * @param map 对应多个键值
     */
    public boolean hmset(String key, Map<String, Object> map) {
        try {
            redisTemplate.opsForHash().putAll(key, map);
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }


    /**
     * HashSet 并设置时间
     * @param key  键
     * @param map  对应多个键值
     * @param time 时间(秒)
     * @return true成功 false失败
     */
    public boolean hmset(String key, Map<String, Object> map, long time) {
        try {
            redisTemplate.opsForHash().putAll(key, map);
            if (time > 0) {
                expire(key, time);
            }
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }


    /**
     * 向一张hash表中放入数据,如果不存在将创建
     *
     * @param key   键
     * @param item  项
     * @param value 值
     * @return true 成功 false失败
     */
    public boolean hset(String key, String item, Object value) {
        try {
            redisTemplate.opsForHash().put(key, item, value);
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }

    /**
     * 向一张hash表中放入数据,如果不存在将创建
     *
     * @param key   键
     * @param item  项
     * @param value 值
     * @param time  时间(秒) 注意:如果已存在的hash表有时间,这里将会替换原有的时间
     * @return true 成功 false失败
     */
    public boolean hset(String key, String item, Object value, long time) {
        try {
            redisTemplate.opsForHash().put(key, item, value);
            if (time > 0) {
                expire(key, time);
            }
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }


    /**
     * 删除hash表中的值
     *
     * @param key  键 不能为null
     * @param item 项 可以使多个 不能为null
     */
    public void hdel(String key, Object... item) {
        redisTemplate.opsForHash().delete(key, item);
    }


    /**
     * 判断hash表中是否有该项的值
     *
     * @param key  键 不能为null
     * @param item 项 不能为null
     * @return true 存在 false不存在
     */
    public boolean hHasKey(String key, String item) {
        return redisTemplate.opsForHash().hasKey(key, item);
    }


    /**
     * hash递增 如果不存在,就会创建一个 并把新增后的值返回
     *
     * @param key  键
     * @param item 项
     * @param by   要增加几(大于0)
     */
    public double hincr(String key, String item, double by) {
        return redisTemplate.opsForHash().increment(key, item, by);
    }


    /**
     * hash递减
     *
     * @param key  键
     * @param item 项
     * @param by   要减少记(小于0)
     */
    public double hdecr(String key, String item, double by) {
        return redisTemplate.opsForHash().increment(key, item, -by);
    }


    // ============================set=============================

    /**
     * 根据key获取Set中的所有值
     * @param key 键
     */
    public Set<Object> sGet(String key) {
        try {
            return redisTemplate.opsForSet().members(key);
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }


    /**
     * 根据value从一个set中查询,是否存在
     *
     * @param key   键
     * @param value 值
     * @return true 存在 false不存在
     */
    public boolean sHasKey(String key, Object value) {
        try {
            return redisTemplate.opsForSet().isMember(key, value);
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }


    /**
     * 将数据放入set缓存
     *
     * @param key    键
     * @param values 值 可以是多个
     * @return 成功个数
     */
    public long sSet(String key, Object... values) {
        try {
            return redisTemplate.opsForSet().add(key, values);
        } catch (Exception e) {
            e.printStackTrace();
            return 0;
        }
    }


    /**
     * 将set数据放入缓存
     *
     * @param key    键
     * @param time   时间(秒)
     * @param values 值 可以是多个
     * @return 成功个数
     */
    public long sSetAndTime(String key, long time, Object... values) {
        try {
            Long count = redisTemplate.opsForSet().add(key, values);
            if (time > 0)
                expire(key, time);
            return count;
        } catch (Exception e) {
            e.printStackTrace();
            return 0;
        }
    }


    /**
     * 获取set缓存的长度
     *
     * @param key 键
     */
    public long sGetSetSize(String key) {
        try {
            return redisTemplate.opsForSet().size(key);
        } catch (Exception e) {
            e.printStackTrace();
            return 0;
        }
    }


    /**
     * 移除值为value的
     *
     * @param key    键
     * @param values 值 可以是多个
     * @return 移除的个数
     */

    public long setRemove(String key, Object... values) {
        try {
            Long count = redisTemplate.opsForSet().remove(key, values);
            return count;
        } catch (Exception e) {
            e.printStackTrace();
            return 0;
        }
    }

    // ===============================list=================================

    /**
     * 获取list缓存的内容
     *
     * @param key   键
     * @param start 开始
     * @param end   结束 0 到 -1代表所有值
     */
    public List<Object> lGet(String key, long start, long end) {
        try {
            return redisTemplate.opsForList().range(key, start, end);
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }


    /**
     * 获取list缓存的长度
     *
     * @param key 键
     */
    public long lGetListSize(String key) {
        try {
            return redisTemplate.opsForList().size(key);
        } catch (Exception e) {
            e.printStackTrace();
            return 0;
        }
    }


    /**
     * 通过索引 获取list中的值
     *
     * @param key   键
     * @param index 索引 index>=0时， 0 表头，1 第二个元素，依次类推；index<0时，-1，表尾，-2倒数第二个元素，依次类推
     */
    public Object lGetIndex(String key, long index) {
        try {
            return redisTemplate.opsForList().index(key, index);
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }


    /**
     * 将list放入缓存
     *
     * @param key   键
     * @param value 值
     */
    public boolean lSet(String key, Object value) {
        try {
            redisTemplate.opsForList().rightPush(key, value);
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }


    /**
     * 将list放入缓存
     * @param key   键
     * @param value 值
     * @param time  时间(秒)
     */
    public boolean lSet(String key, Object value, long time) {
        try {
            redisTemplate.opsForList().rightPush(key, value);
            if (time > 0)
                expire(key, time);
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }

    }


    /**
     * 将list放入缓存
     *
     * @param key   键
     * @param value 值
     * @return
     */
    public boolean lSet(String key, List<Object> value) {
        try {
            redisTemplate.opsForList().rightPushAll(key, value);
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }

    }


    /**
     * 将list放入缓存
     *
     * @param key   键
     * @param value 值
     * @param time  时间(秒)
     * @return
     */
    public boolean lSet(String key, List<Object> value, long time) {
        try {
            redisTemplate.opsForList().rightPushAll(key, value);
            if (time > 0)
                expire(key, time);
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }


    /**
     * 根据索引修改list中的某条数据
     *
     * @param key   键
     * @param index 索引
     * @param value 值
     * @return
     */

    public boolean lUpdateIndex(String key, long index, Object value) {
        try {
            redisTemplate.opsForList().set(key, index, value);
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }


    /**
     * 移除N个值为value
     *
     * @param key   键
     * @param count 移除多少个
     * @param value 值
     * @return 移除的个数
     */

    public long lRemove(String key, long count, Object value) {
        try {
            Long remove = redisTemplate.opsForList().remove(key, count, value);
            return remove;
        } catch (Exception e) {
            e.printStackTrace();
            return 0;
        }
    }

    /**
     * 切换数据库
     * @param dbIndex 数据库下标
     */
    public void setDatabase(Integer dbIndex) {
        if(dbIndex == null || dbIndex > 15 || dbIndex < 0) {
            dbIndex = 0;
        }
        LettuceConnectionFactory lettuceConnectionFactory = (LettuceConnectionFactory) redisTemplate
                .getConnectionFactory();

        lettuceConnectionFactory.setDatabase(dbIndex);
        redisTemplate.setConnectionFactory(lettuceConnectionFactory);
        lettuceConnectionFactory.afterPropertiesSet();
    }
}
```

## 七、Redis.conf详解

启动的时候，就通过配置文件来启动

> 单位

![](http://zhaocan.fym233.cn/tyep3xh8ck)

1、配置文件 unit单位对大小写不敏感

> 包含

![](http://zhaocan.fym233.cn/w826reo7bx)

好比Spring中import

> 网络

```shell
bind  127.0.0.1	# 绑定ip
protected-mode  yes	# 保护模式
port  6379	# 端口设置
```

> 通用 GENERAL

```shell
daemonize  yes	# 以守护进程的方式运行，默认是no，我们需要自己开启为yes
pidfile  /var/run/redis_6379.pid	# 如果以后台的方式运行，我们就需要指定一个pid进程文件

# 日志
# Specify the server verbosity level.
# This can be one of:
# debug (a lot of information, useful for development/testing)	
# verbose (many rarely useful info, but not a mess like the debug level)
# notice (moderately verbose, what you want in production probably)	生产环境（默认）
# warning (only very important / critical messages are logged)
loglevel notice

logfile  ""	# 日志的文件位置名
databases  16	# 数据库的数量，默认是16个数据库
always-show-logo  yes	# 是否总显示LOGO
```

> 快照

持久化，在规定的时间内，执行了多少次操作，则会持久化到文件.rdb、.aof

redis是内存数据库，如果没有持久化，那么数据断电即失

```shell
# 如果900秒内，如果至少有1个key进行了修改，我们即进行持久化操作
save  900  1
# 如果300秒内，如果至少有10个key进行了修改，我们即进行持久化操作
save  300  10
# 如果60秒内，如果至少有10000个key进行了修改，我们即进行持久化操作
save  60  10000

stop-writes-on-bgsave-error  yes	# 持久化如果出错，是否还需要继续工作
rdbcompression  yes	# 是否压缩rdb文件，需要消耗一些cpu的资源
rdbchecksum  yes	# 保存rdb文件的时候，进行错误的检查校验
dir  ./	# rbd文件保存的目录
```

> REPLICATION复制

主从机配置信息，可以在这里配置主机的信息

```bash
# 主机ip 主机端口号
# replicaof <masterip> <masterport>	
# 主机身份验证（密码）
# masterauth <master-password>
```

> SECURITY

可以在这里设置redis的密码，默认是没有密码的！

```shell
127.0.0.1:6379> ping
PONG
127.0.0.1:6379> config get requirepass	# 获取redis的密码
1) "requirepass"
2) ""
127.0.0.1:6379> config set requirepass "123456"	# 设置redis密码
OK
127.0.0.1:6379> config get requirepass	# 发现所有的命令都没有权限了
(error) NOAUTH Authentication required
127.0.0.1:6379> ping
(error) NOAUTH Authentication required
127.0.0.1:6379> auth 123456	# 使用密码进行登录
OK
127.0.0.1:6379> config get requirepass
1) "requirepass"
2) "123456"
```

> 限制CLIENT

```shell
maxclients  10000	# 设置能连接上redis的最大客户端的数量
maxmemory  <bytes>	# redis配置最大的内存容量
maxmemory-policy  noeviction	# 内存到达上限之后的处理策略

1、volatile-lru:只对设置了过期时间的key进行LRU（默认值）
2、allkeys-lru:删除lru算法的key
3、volatile-random:速记删除即将过期key
4、allkeys-random:随机删除
5、volatile-ttl:删除即将过期的
6、noeviction:永不过期，返回错误
```

> APPEND ONLY 模式  aof配置

```shell
appendonly  no	# 默认是不开启aof格式的，默认是使用rdb方式持久化的，在大部分所有情况下，rdb完全够用了
appendfilename  "appendonly.aof"	# 持久化的文件名字

# appendfsync  always	# 每次修改都会写入sync，消耗性能
appendfsync  everysec	# 每秒执行一次 sync，可能会丢失这一秒的数据
# appendfsync  no	# 不执行sync，这个时候操作系统自己同步数据，速度最快
```

## 八、Redis持久化

Redis是内存数据库，如果不将内存中的数据库状态保存到磁盘，那么一旦服务器进程退出，服务器中的数据库状态也会消失。所以Redis提供了持久化功能

### RDB（Redis DataBase）

> **什么是RDB**

在主从复制中，rdb就是备用的！

![img](https://img-blog.csdnimg.cn/img_convert/bb94b1efe517caba5b700d9ae904f204.png)

在指定的时间间隔内将内存中的数据集快照写入磁盘，也就是行话讲的Snapshot快照，它恢复时是将快照文件直接读到内存里。

Redis会单独创建（fork）一个子进程来进行持久化，会先将数据写入到一个临时文件中，待持久化过程都结束了，再用这个临时文件替换上次持久化好的文件。整个过程中，主进程是不进行任何IO操作的。这就确保了极高的性能。如果需要进行大规模数据的恢复，且对于数据恢复的完整性不是非常敏感，那RDB方式要比AOF方式更加的高效。RDB的缺点是最后一次持久化后的数据可能丢失。我们默认的就是RDB，一般情况下不需要修改这个配置！

**RDB保存的文件是：`dump.rdb`** 都是在我们的配置文件中快照中进行配置的！

![](http://zhaocan.fym233.cn/fof2q3e5sd)

> 触发机制

1. save的规则满足的情况下，会自动触发rdb规则
2. 执行 flushall 命令，也会触发我们的rdb规则！
3. 退出redis，也会产生rdb文件

备份就自动生成一个dump.rdb

> **如何恢复rdb文件**

1. 只需要将rdb文件放在我们redis启动目录下就可以，redis启动的时候会自动检查dump.rdb文件，恢复其中的数据！

2. 查看需要存放的位置

   ```shell
   127.0.0.1:6379> config get dir
   1) "dir"
   2) "/usr/local/bin"	#如果在这个目录下存在 dump.rdb 文件，启动就会自动恢复其中的数据
   ```

> **几乎就他自己默认的配置就够用了**

- 优点：
  1. 和大规模的数据恢复！dump.rdb
  2. 对数据的完整性要求不高
- 缺点：
  1. 需要一定的时间间隔进行操作！如果redis意外宕机了，最后一次修改的数据就会丢失
  2. fork进程的时候，会占用一定的内存空间！

### AOF（Append Only File）

将我们的所有命令都记录下来，history，恢复的时候就把这个文件全部执行一遍

> **AOF是什么**

![image-20201127214428307](https://img-blog.csdnimg.cn/img_convert/d2fce3b35567d382ebfa7e8f51c27326.png)

1. fork分支出子进程
2. 根据内存中的数据子进程创建临时aof文件
3. 父进程执行的命令存放在缓存中，并且写入原aof文件
4. 子进程完成新aof文件通知父进程
5. 父进程将缓存中的命令写入临时文件
6. 父进程用临时文件替换旧aof文件并重命名
7. 后面的命令都追加到新的aof文件中



以日志的形式来记录每个写操作，将Redis执行过的所有指令记录下来（读操作不记录），只许追加文件但不可以改写文件，redis启动之初会读取该文件重新构建数据，换言之，redis重启的话就根据日志文件的内容将写指令从前到后执行一次以完成数据的恢复工作

**AOF保存的是 `appendonly.aof`文件**

> **append**

![](http://zhaocan.fym233.cn/yi7wfvak2s)

默认是不开启的，需要手动进行配置！只需要将appendonly改为yes即可开启aof！

重启redis就可以生效了！

如果aof文件有错误，这个时候redis是启动不起来的！我们需要修复这个配置文件

redis提供了一个工具`redis-check-aof --fix appendonly.aof`

![](http://zhaocan.fym233.cn/4194wfshvf)

如果文件正常，重启就可以直接恢复了！

![](http://zhaocan.fym233.cn/k1t7wjywhd)

> **重写规则说明**

AOF默认就是文件的无限追加，文件会越来越大！

![](http://zhaocan.fym233.cn/jugxnjlppl)

如果AOF文件大于64mb，就会fork一个新的进程来将文件进行重写！

> **优点和缺点**

```bash
appendonly  no	# 默认是不开启aof格式的，默认是使用rdb方式持久化的，在大部分所有情况下，rdb完全够用了
appendfilename  "appendonly.aof"	# 持久化的文件名字

# appendfsync  always	# 每次修改都会写入sync，消耗性能
appendfsync  everysec	# 每秒执行一次 sync，可能会丢失这一秒的数据
# appendfsync  no	# 不执行sync，这个时候操作系统自己同步数据，速度最快
```

- 优点：
  1. 每次修改都同步，文件的完整性会更加完整
  2. 每秒同步一次，可能会丢失一秒的数据
  3. 从不同步，效率是最高的1
- 缺点：
  1. 相对于数据文件来说，aof远远大于rdb，修复的速度也比rdb慢
  2. AOF运行效率也要比RDB慢，所以Redis默认的配置就是配置RDB持久化，而不是AOF

**扩展**

1. RDB持久化方式能够在指定的时间间隔内对你的数据进行快照存储
2. AOF持久化方式记录每次对服务器写的操作，当服务器重启的时候会重新执行这些命令来恢复原始的数据，AOF命令以Redis协议追加保存每次写的操作到文件末尾，Redis还能对AOF文件进行后台重写，使得AOF文件的体积不至于过大
3. 只做缓存，如果你只希望你的数据在服务器运行的时候存在，你也可以不使用任何持久化
4. 同时开启两种持久化方式
   - 在这种情况下，当redis重启的时候会优先载入AOF文件来恢复原始的数据，因为在通常情况下AOF文件保存的数据集要比RDB文件保存的数据集要完整。
   - RDB的数据不实时，同时使用两者时服务器重启也只会找AOF文件，那要不要只使用AOF呢？建议不要，因为RDB更适合用于备份数据库（AOF在不断变化不好备份），快速重启，而且不会有AOF可能潜在的Bug，留着作为一个万一手段。
5. 性能建议
   - 因为RDB文件只用作后背用途，建议只在Slave上持久化RDB文件，而且只要15分钟备份一次就够了，只保留 `save 900 1` 这条规则。
   - 如果Enable AOF，好处是在更恶劣情况下也只会丢失不超过两秒数据，启动脚本较简单只load自己的AOF文件就可以了，代价一是带来了持续的IO，二是AOF rewrite 的最后将 rewrite 过程中产生的新数据写到新文件造成的阻塞几乎是不可避免的。只要硬盘许可，应该尽量减少AOF rewirte 的频率，AOF重写的基础大小默认值64M太小了，可以设到5G以上，默认超过原大小100%大小重写可以改到适当的数值。
   - 如果不Enable AOF，仅靠Master-Slave Repllcation 实现高可用性也可以，能省掉一大笔IO，也减少了 rewrite时带来的系统波动。代价是如果Master/Slave 同时挂掉，会丢失十几分钟的数据，启动脚本也要比较两个 Master/Slave 中的RDB文件，载入较新的那个，微博就是这种架构。

## 九、Redis发布订阅

Redis发布订阅（pub/sub）是一种消息通信模式：发送者（pub）发送消息，订阅者（sub）接收消息。

Redis客户端可以订阅任何数量的频道。

订阅/发布消息图：

- 消息发送者
- 频道
- 消息订阅者

![](http://zhaocan.fym233.cn/wu93vejoj)

下面展示了频道channel1，以及订阅这个频道的三个客户端——client2、client5 和 client1 之间的关系：

![](http://zhaocan.fym233.cn/ij3s50k63n)

当有新消息通过 PUBLISH 命令发送给频道 channel1 时，这个消息就会被发送给订阅它的三个客户端：

![](http://zhaocan.fym233.cn/iph1r5smxr)

> **命令**

这些命令被广泛用于构建即时通信应用，比如网络聊天室（chatroom）和实时广播、实时提醒等。

![](http://zhaocan.fym233.cn/wwuw4zqyt)

> **测试**

订阅端：

```bash
127.0.0.1:6379> SUBSCIBE zhaocan	# 订阅一个频道的名字  zhaocan
Reading message... (press Ctrl-C to quit)
1) "subscribe"
2) "zhaocan"
3) (integer) 1
# 等待读取推送的信息
1) "message"	# 消息
2) "zhaocan"	# 具体的频道
3) "hello,zhaocan"	# 消息的具体内容
1) "message"
2) "zhaocan"
3) "hello,redis"
```

发送端：

```bash
127.0.0.1:6379> PUBLISH zhaocan "hello,zhaocan"	# 发布者发布消息到频道！
(integer) 1
127.0.0.1:6379> PUBLISH zhaocan "hello,redis"	# 发布者发布消息到频道！
(integer) 1
```

> **原理**

- Redis是使用C实现的，通过分析 Redis 源码里的  pubsub.c 文件，了解发布和订阅机制的底层实现，藉此加深对 Redis 的理解。
- Redis通过 PUBLISH、SUBSCRIBE 和 PSUBSCRIBE 等命令实现发布和订阅功能。
- 通过 SUBSCRIBE 命令订阅某频道后，redis-server 里维护一个字典，字典的键就是一个个 channel 的订阅链表中。
- 通过 PUBLISH 命令向订阅者发送消息，redis-server会使用给定的频道作为键，在它所维护的channel 字典中查找记录订阅了这个频道的所有客户端的链表，遍历这个链表，将消息发布给所有订阅者。
- Pub/Sub 从字面上理解就是发布（Publish）与订阅（Subscribe），在Redis中，你可以设定对某一个key值进行消息发布及消息订阅，当一个key值上进行了消息发布后，所有订阅它的客户端都会收到相应的消息。这一功能最明显的用法就是用作实时消息系统，比如普通的即时聊天，群聊等功能

> **使用场景**

1. 实时消息系统
2. 实时聊天！（频道当做聊天室，将信息回显给所有人即可）
3. 订阅，关注系统

稍微复杂一些的场景使用消息中间件（MQ）

## 十、Redis主从复制

> **概念**

主从复制，是指将一台Redis服务器的数据，复制到其他的Redis服务器。前者称为主节点（master/leader），后者称为从节点（slave/follower）；数据的复制是单向的，只能由主节点到从节点。Master以写为主，Slave以读为主。

默认情况下，每台Redis服务器都是主节点；且一个主节点可以有多个从节点（或没有从节点），但一个从节点只能有一个主节点。

**主从复制的作用主要包括：**

1. **数据冗余：**主从复制实现了数据的热备份，是持久化之外的一种数据冗余方式。
2. **故障恢复：**当主节点出现问题时，可以由从节点提供服务，实现快速的故障恢复；实际上是一种服务的冗余。
3. **负载均衡：**在主从复制的基础上，配合读写分离，可以由主节点提供写服务，由从节点提供读服务（即写Redis数据时应用连接主节点，读Redis数据时应用连接从节点），分担服务器负载；尤其是在写少读多的场景下，通过多个从节点分担负载，而已大大提高Redis服务器的并发量。
4. **高可用（集群）基石：**除了上述作用以外，主从复制还是哨兵和集群能够实施的基础，因此说主从复制是Redis高可用的基础。

一般来说，要将Redis运用于工程项目中，只使用一台Redis是万万不能的（宕机，一主二从），原因如下：

1. 从结构上，单个Redis的服务器会发生单点故障，并且一台服务器需要处理所有的请求负载，压力较大；
2. 从容量上，单个Redis服务器内存容量有限，就算一台Redis服务器内存容量为256G，也不能将所有内存用作Redis存储内存，一般来说，**单台Redis最大使用内存不应该超过20G**

电商网站上的商品，一般都是一次上传，无数次浏览的，说专业点也就是 “多读少写”

![](http://zhaocan.fym233.cn/ypnilq3lq9)

主从复制，读写分离！80% 的情况下都是在进行读操作！减缓服务器的压力。

### 环境配置

只配置从库，不用配置主库

```bash
127.0.0.1:6379> info replication	# 查看当前库信息
# Replication
role:master	# 角色
connected_slaves:0	# 0从机
master_failover_state:no-failover
master_replid:26fedb163d090b3ee21e85e8d7453ae4790788cb
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0
```

复制3个配置文件，然后修改对应的信息

1. 端口
2. pid名字
3. log文件名字
4. dump.rdb文件名字

修改完毕之后，启动我们的3个redis服务器，可以通过进程信息查询

![](http://zhaocan.fym233.cn/01skegiebh)

### 一主二从

**默认情况下，每台Redis服务器都是主节点。**一般情况下只用配置从机就好

```bash
# 从机1
127.0.0.1:6379> slaveof 127.0.0.1 6379	# SLAVEOF host port 配置主机
OK
127.0.0.1:6379> info replication
# Replication
role:slave	# 当前角色是从机
master_host:127.0.0.1	# 主机信息
master_port:6379
master_link_status:up
master_last_io_seconds_ago:1
master_sync_in_progress:0
slave_repl_offset:56
slave_priority:100
slave_read_only:1
connected_slaves:0
master_replid:c064e353938ed81207098438b23d5d05c6f328e2
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:56
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:56

# =====================================================
# 从机2
127.0.0.1:6379> slaveof 127.0.0.1 6379
OK
127.0.0.1:6379> info replication
# Replication
role:slave
master_host:127.0.0.1
master_port:6379
master_link_status:up
master_last_io_seconds_ago:6
master_sync_in_progress:0
slave_repl_offset:490
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:c064e353938ed81207098438b23d5d05c6f328e2
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:490
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:477
repl_backlog_histlen:14

# =====================================================
# 在主机中查看
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:2	# 2台从机
slave0:ip=127.0.0.1,port=6380,state=online,offset=504,lag=1	# 从机1的信息
slave1:ip=127.0.0.1,port=6381,state=online,offset=504,lag=0	# 从机2的信息
master_failover_state:no-failover
master_replid:c064e353938ed81207098438b23d5d05c6f328e2
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:504
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:504
```

真实的主从配置应该是在配置文件中配置，这样的话就是永久的。命令是暂时的

> **细节**

1. 主机可以写，从机不能写只能读！主机中的所有信息和数据，都会自动被从机保存！

   ![](http://zhaocan.fym233.cn/3v5ayivhw)

   从机只能读取内容！

   ![](http://zhaocan.fym233.cn/pvyjlivao)

   测试：主机断开连接后，从机依旧连接到主机的，但是没有写的操作了！这个时候，如果主机重新连接，从机依旧可以直接获取到主机写的信息

   如果是使用命令行配置了主从配置，这个时候如果重启了就会变回主机！只要变回了从机，立马就会从主机中获取值！

> **复制原理**

Slave 启动成功连接到 master 后会发送一个 sync 同步命令

Master 接到命令，启动后台的存盘进程，同时收集所有接收到的用于修改数据集命令，在后台进程执行完毕之后，**master 将传送整个数据文件到 slave，并完成一次完全同步。**

- **全量复制：**而slave 服务在接收到数据库文件数据后，将其存盘并加载到内存中。
- **增量复制：**Master 继续讲新的所有收集到的修改命令依次传给 slave，完成同步。

但是只要是重新连接master，一次完全同步（全量复制）将被自动执行！我们的数据一定可以在从机中看到！

> **层层链路**

上一个Master连接下一个Slave

![](http://zhaocan.fym233.cn/scss5t2w4)

这时候也可以完成我们的主从复制

> **如果没有Master了，这个时候能不能选择一个Master出来呢？**

如果主机断开了连接，可以使用**`SLAVEOF no one`**让自己变成主机！其他的节点就可以手动连接到最新的这个主节点（手动）！如果这个时候Master修复了，那就只能重新配置连接

### 哨兵模式

> **概述**

主从切换技术的方法是：当主服务器宕机后，需要手动把一台从服务器切换为主服务器，这就需要人工干预，费时费力，还会造成一段时间内服务不可用。 这不是一种推荐的方式，更多时候，我们优先考虑哨兵模式。Redis从2.8开始正式提供了Sentinel（哨兵）架构来解决这个问题。

谋朝篡位的自动版，能够后台监控主机是否故障，如果故障了根据投票数自动将从库转换为主库。

哨兵模式是一种特殊的模式，首先Redis提供了哨兵的命令，哨兵是一个独立的进程，作为进程，它会独立运行。其原理是**哨兵通过发送命令，等待Redis服务器响应，从而监控运行的多个Redis实例。**

![](http://zhaocan.fym233.cn/9til1qg9d)

这里的哨兵有两个作用

- 通过发送命令，让Redis服务器返回监控其运行状态，包括主服务器和从服务器。
- 当哨兵监测到master宕机，会自动将slave切换成master，然后通过**发布订阅模式**通知其他的从服务器，修改配置文件，让它们切换主机。

然而一个哨兵进程对Redis服务器进行监控，可能会出现问题，为此我们可以使用多个哨兵进行监控。各个哨兵之间还会进行监控，这样就形成了多哨兵模式。

![](http://zhaocan.fym233.cn/fig6hfwsp)

假设主服务器宕机，哨兵1先检测到这个结果，系统并不会马上进行failover过程，仅仅是哨兵1主观的认为主服务器不可用，这个现象称为**主观下线。**当后面的哨兵也检测到主服务器不可用，并且数量达到一定值时，那么哨兵之间就会进行一次投票，投票的结果由一个哨兵发起，进行failover [故障转移] 操作。切换成功后，就会通知发布订阅系统，让各个哨兵把自己监控的从服务器实现切换主机，这个过程称为**客观下线。**

> **测试**

目前的状态是 一主二从

1. 配置哨兵配置文件 `sentinel.conf`

   ```bash
   # sentinel monitor 被监控的名称 host port
   sentinel monitor myredis 127.0.0.1 6379 1
   ```

   后面的这个数字 1 ，代表主机挂了，slave投票看让哪个从机接替主机，票数最多的就会成为主机

2. 启动哨兵

   ```bash
   [root@iZbp150uqocpf9w8y2p7zhZ bin]# ./redis-sentinel ../config/sentinel.conf
   26672:X 09 Jun 2021 09:39:55.206 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
   26672:X 09 Jun 2021 09:39:55.206 # Redis version=6.2.4, bits=64, commit=00000000, modified=0, pid=26672, just started
   26672:X 09 Jun 2021 09:39:55.206 # Configuration loaded
   26672:X 09 Jun 2021 09:39:55.207 * monotonic clock: POSIX clock_gettime
                   _._                                                  
              _.-``__ ''-._                                             
         _.-``    `.  `_.  ''-._           Redis 6.2.4 (00000000/0) 64 bit
     .-`` .-```.  ```\/    _.,_ ''-._                                  
    (    '      ,       .-`  | `,    )     Running in sentinel mode
    |`-._`-...-` __...-.``-._|'` _.-'|     Port: 26379
    |    `-._   `._    /     _.-'    |     PID: 26672
     `-._    `-._  `-./  _.-'    _.-'                                   
    |`-._`-._    `-.__.-'    _.-'_.-'|                                  
    |    `-._`-._        _.-'_.-'    |           https://redis.io       
     `-._    `-._`-.__.-'_.-'    _.-'                                   
    |`-._`-._    `-.__.-'    _.-'_.-'|                                  
    |    `-._`-._        _.-'_.-'    |                                  
     `-._    `-._`-.__.-'_.-'    _.-'                                   
         `-._    `-.__.-'    _.-'                                       
             `-._        _.-'                                           
                 `-.__.-'                                               
   
   26672:X 09 Jun 2021 09:39:55.207 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
   26672:X 09 Jun 2021 09:39:55.210 # Sentinel ID is e8cb05a8cec1ba7da8df63161bbd124911c8ff50
   26672:X 09 Jun 2021 09:39:55.210 # +monitor master myredis 127.0.0.1 6379 quorum 1
   ```

如果Master节点断开了，这个时候就会从从机中随机选择一个服务器！（投票算法）

![](http://zhaocan.fym233.cn/l2pgkurt4)

哨兵日志

![](http://zhaocan.fym233.cn/krtc6vu7ay)

如果主机此时回来了，只能归并到新的主机下，当做从机，这就是哨兵模式的规则！

> **哨兵模式**

优点：

1. 哨兵集群，基于主从复制模式，所有的主从配置优点，它都有
2. 主从可以切换，故障可以转移，系统的可用性就会更好
3. 哨兵模式就是主从模式的升级，从手动到自动，更加健壮！

缺点：

1. Redis不好在线扩容，集群容量一旦到达上限，在线扩容就十分麻烦
2. 实现哨兵模式的配置其实是很麻烦的，里面有很多选择！

> 哨兵模式的全部配置

```bash
# Example sentinel.conf
# 哨兵sentinel实例运行的端口默认26379，如果有哨兵集群，还需要配置每个哨兵端口
port 26379
# 哨兵sentinel的工作目录
dir /tmp
# 哨兵sentinel监控的redis主节点的 ip port
# master-name可以自己命名的主节点名字只能由字母A-z、数字0-9、这三个字符".-_"组成。
# quorum 配置多少个sentinel哨兵统一认为master主节点失联 那么这时客观上认为主节点失联了
# sentinel monitor <master-name> <ip> <redis-port> <quorum> 
sentinel monitor mymaster 127.0.0.1 6379 2

# 当在Redis实例中开启了requirepass foobared 授权密码 这样所有连接Redis实例的客户端都要提供密码
# 设置哨兵sentinel 连接主从的密码 注意必须为主从设置一样的验证密码
# sentinel auth-pass <master-name> <password>
sentinel auth-pass mymaster MySUPER--secret-0123passw0rd

# 指定多少毫秒之后 主节点没有应答哨兵sentinel 此时 哨兵主观上认为主节点下线 默认30秒
# sentinel down-after-milliseconds <master-name> <milliseconds>
sentinel down-after-milliseconds mymaster 30000

# 这个配置项指定了在发生 failover 主备切换时最多可以有多少个slave同时对新的master进行同步，这个数字越小，完成failover所需的时间就越长，但是如果这个数字越大，就意味着越多的slave 因为replication而不可用。可以通过将这个值设为 1 来保证每次只有一个slave处于不能处理命令请求的状态。
# sentinel parallel-syncs <master-name> <numslaves>
sentinel parallel-syncs mymaster 1

# 故障转移的超时时间 failover-timeout 可以用在以下这些方面：
#1. 同一个sentinel对同一个master两次failover之间的间隔时间。
#2. 当一个slave从一个错误的master那里同步数据开始计算时间。直到slave被纠正为向正确的master那里同步数据时。
#3. 当想要取消一个正在进行的failover所需要的时间。
#4. 当进行failover时，配置所有slaves指向新的master所需的最大时间。不过，即使过了这个超时，slaves依然会被正确配置为指向master，但是就不按parallel-syncs所配置的规则来了
# 默认三分钟
# sentinel failover-timeout <master-name> <milliseconds>
sentinel failover-timeout mymaster 180000
# SCRIPTS EXECUTION
# 配置当某一事件发生时所需要执行的脚本，可以通过脚本来通知管理员，例如当系统运行不正常时发邮件通知相关人员。
# 对于脚本的运行结果有以下规则：
# 若脚本执行后返回1，那么该脚本稍后将会被再次执行，重复次数目前默认为10
# 若脚本执行后返回2，或者比2更高的一个返回值，脚本将不会重复执行。
# 如果脚本在执行过程中由于收到系统中断信号被终止了，则同返回值为1时的行为相同。
# 一个脚本的最大执行时间为60s，如果超过这个时间，脚本将会被一个SIGKILL信号终止，之后重新执行。
# 通知型脚本:当sentinel有任何警告级别的事件发生时（比如说redis实例的主观失效和客观失效等等），将会去调用这个脚本，这时这个脚本应该通过邮件，SMS等方式去通知系统管理员关于系统不正常运行的信息。调用该脚本时，将传给脚本两个参数，一个是事件的类型，一个是事件的描述。如果 sentinel.conf 配置文件中配置了这个脚本路径，那么必须保证这个脚本存在于这个路径，并且是可执行的，否则sentinel无法正常启动成功。
# 通知脚本
# sentinel notification-script <master-name> <script-path>
sentinel notification-script mymaster /var/redis/notify.sh

# 客户端重新配置主节点参数脚本
# 当一个master由于failover而发生改变时，这个脚本将会被调用，通知相关的客户端关于master地址已经发生改变的信息。
# 以下参数将会在调用脚本时传给脚本:
# <master-name> <role> <state> <from-ip> <from-port> <to-ip> <to-port>
# 目前 <state> 总是“failover”,
# <role> 是“leader”或者“observer”中的一个。
# 参数from-ip,from-port,to-ip,to-port是用来和旧的master和新的master(即旧的slave)通信的
# 这个脚本应该是通用的，能被多次调用，不是针对性的。
# sentinel client-reconfig-script <master-name> <script-path>
sentinel client-reconfig-script mymaster /var/redis/reconfig.sh	#一般都是由运维来配置！
```

## 十一、Redis缓存穿透和雪崩

Redis缓存的使用，极大地提升了应用程序的性能和效率，特别是数据查询方面。但同时，它也带来了一些问题。其中，最要害的问题，就是数据一致性问题，从严格意义上来讲，这个问题无解。如果对数据的一致性要求很高，那么就不能使用缓存。另外的一些典型问题就是，缓存穿透、缓存雪崩和缓存击穿。目前，业界也都有比较流行的解决方案。

### 缓存穿透

**（查不到）**

> **概念**

缓存穿透的概念很简单，用户想要查询一个数据，发现redis内存数据库没有，也就是缓存没有命中，于是向持久层数据库查询，发现也没有，于是本次查询失败。当用户很多的时候，缓存都没有命中，于是都去请求了持久层数据库。这会给持久层数据库造成很大的压力，这时候就相当于出现了缓存穿透。

> **解决方案**

**布隆过滤器**

布隆过滤器是一种数据结构，对所有可能查询的参数以hash形式存储，在控制层先进行校验，不符合则丢弃，从而避免了对底层存储系统的查询压力：

![](http://zhaocan.fym233.cn/wee28jmwu9)

**缓存空对象**

当存储层不命中后，即使返回的空对象也将其缓存起来，同事会设置一个过期时间，之后再访问这个数据将会从缓存中获取，保护了后端数据源：

![](http://zhaocan.fym233.cn/cmup2m1tjs)

但是这种方法会存在两个问题：

1. 如果空值能够被缓存起来，这就意味着缓存需要更多的空间存储更多的键，因为这当中可能会有很多的空值的键！
2. 即使对空值设置了过期时间，还是会存在缓存层和存储层的数据会有一段时间窗口的不一致，这对于需要保持一致性的业务会有影响。

### 缓存击穿

**（量太大，缓存过期）**

> **概念**

这里需要注意和缓存击穿的区别，缓存击穿，是指一个key非常热点，在不停的扛着大并发，大并发集中对这一个点进行访问，当这个key在失效的瞬间，持续的大并发就会穿破缓存，直接请求数据库，就像在一个屏障上凿开一个洞。

当某个key在过期的瞬间，有大量的请求并发访问，这类数据一般是热点数据，由于缓存过期，会同时访问数据库来查询最新数据，并且回写缓存，会导致数据库瞬间压力过大。

> 解决方案

**设置热点数据永不过期**

从缓存层面来看，没有设置过期时间，所以不会出现热点 key 过期后产生的问题。

**加互斥锁**

分布式锁：使用分布式锁，保证对于每个key同时只有一个线程去查询后端服务，其他线程没有获得分布式锁的权限，因此只需要等待即可。这种方式将高并发的压力转移到了分布式锁，因此对分布式锁的考验很大。

### 缓存雪崩

> **概念**

缓存雪崩，是指在某一个时间段，缓存集中过期失效。

产生雪崩的原因之一，比如在写文本的时候，马上就要到双十二零点了，很快就会迎来一波抢购，这波商品时间比较集中地放入了缓存，假设缓存一个小时。那么到了凌晨一点钟的时候，这批商品的缓存就过期了。而对这批商品的访问查询，都落到了数据库上，这对于数据库而言，就会产生周期性的压力波峰。于是所有的请求都会达到存储层，存储层的调用量暴增，造成持久层也会挂掉的情况。

![](http://zhaocan.fym233.cn/720bpe0qep)

其实集中过期，倒不是非常致命，比较致命的缓存雪崩，是缓存服务器某个节点宕机或断网。因为自然形成的缓存雪崩，一定是在某个时间段集中创建缓存，这个时候，数据库也是可以顶住压力的。无非就是对数据库产生周期性的压力而已。而缓存服务节点的宕机，对数据库服务器造成的压力是不可预知的，很有可能瞬间就把数据库压垮。

> **解决方案**

**redis高可用**

这个思想的含义是，既然redis有可能挂掉，那我多增设几台redis，这样一台挂掉之后其他的还可以继续工作，其实就是搭建的集群。

**限流降级**

这个解决方案的思想是，在缓存失效后，通过加锁或者队列来控制读数据库写缓存的线程数量。比如对某个key只允许一个线程查询数据和写缓存，其他线程等待。

**数据预热**

数据加热的含义就是在正式部署之前，先把可能的数据先预先访问一遍，这样部分可能大量访问的数据就会加载到缓存中。在即将发生大并发访问前手动触发加载缓存不同的key，设置不同的过期时间，让缓存失效的时间点尽量均匀。

