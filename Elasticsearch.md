ElasticSearch

## 1、ElasticSearch作者简介

**Doug Cutting**

Doug Cutting 是一位美国工程师，迷上了搜错引擎。他做了一个用于文本搜索的函数库，命名为**Lucene. Lucene** 是用java写的，目标是为各种中小型应用软件加入全文搜索功能。**Lucene是一套信息检索工具包，**并不包含搜索引擎系统，它包含了索引结构、读写索引工具、相关性工具、排序等功能。因此在使用Lucenen时仍需关注搜索引擎系统，例如数据获取、解析、分词等方面的东西。

该项目早期被发布在Doug Cutting的个人网站，后来成为了Apache软件基金会jakarta项目的一个子项目。后来在Lucene的基础上开发了一款可以代替当时的主流搜索的开源搜索引擎，命名为**Nutch**.

**Nutch** 是一个建立在Lucene核心之上的网页搜索应用程序，它在Lucene的基础上加了爬虫和一些网页相关的功能，目的就是从一个简单的站内检索推广到全球网络上的搜索上。

随着时间的推移，作为互联网搜索引擎，都**面临对象“体积”不断增大的问题**。**需要存储大量的网页**，并不断优化自己的搜索算法，提升搜索效率。

在2004年，Doug Cutting实现了**分布式文件存储系统**，并将它命名为**NDFS(Nutch Distributed File System)**。后来他加入了雅虎，将NDFS和MapReduce进行了改造，并重新命名为**Hadoop**(NDFS也改名为**HDFS,Hadoop Distributed File System)**. 这就是大名鼎鼎的**大数据框架系统--Hadoop**的由来，而Doug Cutting则被人称为Hadoop之父。

## 2、ElasticSearch概述

ElasticSearch,简称es，**es是一个开源的高拓展的分布式全文检索引擎**，它可以近乎实施的存储、检索数据；本身**扩展性很好**，可以扩展到上百台服务器，处理PB级别的数据。es也使用java开发并**使用Lucene 作为其核心**来实现所有索引和搜索的功能，但是它的目的是**通过简单的RESTful API来隐藏Lucene的复杂性**，从而让全文搜索变得简单。

**谁在使用**

- 维基百科，类似百度百科，全文检索，高亮，搜索推荐
- 国外新闻网站，类似搜狐新闻，用户行为日志（点击，浏览，收藏，评论）+社交网络数据，数据分析。。。
- Stack Overflow国外的程序异常讨论论坛
- GitHub（开源代码管理），搜索上千亿行代码
- 电商网站，检索商品
- 日志数据分析，logstash采集日志，ES进行复杂的数据分析，ELK技术（elasticsearch+logstash+kibana）
- 商品价格监控网站
- 商业智能系统
- 站内搜索

### 2.1、ES和solr的差别

> **ElasticSearch简介**

ElasticSearch是一个实施**分布式搜索**和**分析引擎**。它让你以前所未有的速度**处理大数据**成为可能。它用于**全文搜索、结构化搜索、分析**以及将这三者混合使用：

维基百科使用es提供全文搜索并高亮关键字，以及输入实施搜索和搜索纠错等搜索建议功能；英国公报使用es结合用户日志和社交网络数据提供给他们的编辑以实施的反馈，以便了解龚总对新发表的文章的回应。。。

es是一个基于Apache Lucene(TM)的开源搜索引擎。无论在开源还是专有领域，Lucene可以被认为是迄今为止最先进、性能最好、功能最全的搜索引擎库。想要使用它，必须使用java来作为开发语言并将其直接继承到你的应用中。

> **solr简介**

Solr是Apache下的一个顶级开源项目，采用java开发，是基于Lucene的全文搜索服务器。Solr提供了比Lucene更为丰富的查询语言，同时**实现了可配置、可扩展、并对索引、搜索性能进行了优化。**它**可以独立运行**，是一个独立的企业及搜索应用服务器，它对外提供类似于web-service的API接口。用户可以通过http请求，像搜索引擎服务器提交一定格式的文件，生成索引；也可以通过提出查找请求，并得到返回结果。

**两者比较**

- 当单纯的**对已有数据进行搜索**时，Solr更快
- 当**实时建立索引**是，Solr会产生io阻塞，查询性能较差，ElasticSearch具有明显的优势
- 随着**数据量的增加**，Solr的搜索效率会变得更低，而Elasticsearch却没有明显的变化

**总结**

1. **es**基本是**开箱即用**，非常简单。而solr会有点复杂。
2. Solr利用Zookeeper进行分布式管理，而elasticsearch自身带有分布式协调管理功能
3. solr支持更多格式的数据，比如json xml csv。而es只支持json文件格式
4. solr官方提供的功能更多，而elasticsearch更注重核心功能，高级功能由第三方插件提供
5. solr查询快，但更新索引时慢，用于电商等查询多的应用
6. es建立索引宽，即实时性查询快，用于facebook新浪等搜索
7. solr较成熟，有一个更大，更成熟的用户、开发和贡献者社区，而elasticsearch相对开发维护者较少，更新太快，学习使用成本较高

### 2.2、ElasticSearch安装

**历史版本下载地址：`https://www.elastic.co/cn/downloads/past-releases#elasticsearch`**

**注：安装ElasticSearch之前必须保证JDK1.8+安装完毕，并正确的配置好JDK环境变量，否则启动ElasticSearch失败。**

> 熟悉目录

```bash
`bin`		启动文件
`config`	配置文件
	`log4j2`	日志配置文件
	`jvm.options`	java虚拟机相关的配置
	`elasticsearch.yml`	elasticsearch的配置文件  默认端口：9200
`lib`	相关jar包
`logs`	日志
`modules`	功能模块
`plgins`	插件
```

### 2.3、启动Elasticsearch

下载windows版本，解压压缩包，打开，看到如下目录：

![](http://zhaocan.fym233.cn/3iq34xl1z)

打开config文件夹：

![](http://zhaocan.fym233.cn/037vftdf1)

双击bin目录下的elasticsearch.bat启动

![](http://zhaocan.fym233.cn/r762zhubeu)

点击后：

![](http://zhaocan.fym233.cn/xfwng836xc)

### 2.4、启动测试

在浏览器访问127.0.0.1:9200,若得到以下信息则安装成功：

![](http://zhaocan.fym233.cn/xgj1exhqc6)

### 2.5、安装可视化界面

> **安装可视化界面 es head的插件**

1. 下载地址：https://github.com/mobz/elasticsearch-head

2. 启动

   ```shell
   npm install
   npm run start
   ```

3. 连接测试发现，存在跨域问题：

   修改 `elasticsearch.yml`，配置跨域

   ```yml
   http.cors.enabled: true
   http.cors.allow-origin: "*"
   ```

4. 重启elasticsearch，然后再次连接

   ![](http://zhaocan.fym233.cn/64dub5ywbx)

### 2.6、安装Kibana

> 安装Kibana

Kibana是一个针对Elasticsearch的开源分析及可视化平台，用来搜索、查看交互存储在Elasticsearch索引中的数据。使用Kibana，可以通过各种图表进行高级数据分析及展示。Kibana让海量数据更容易理解。它操作简单，基于浏览器的用户界面可以快速创建仪表板（bashboard）实时显示Elasticsearch查询动态。设置Kibana非常简单。无需编码或者额外的基础架构，几分钟内就可以完成Kibana安装并启动Elasticsearch索引检监测。

官网：https://www.elastic.co/cn/kibana

**Kibana版本要和Elasticsearch一致**

![](http://zhaocan.fym233.cn/2rubkx79zl)

![](http://zhaocan.fym233.cn/bkcg9yj0id)

> **启动测试**

1. 解压后的目录

   ![](http://zhaocan.fym233.cn/vhzu1jqtan)

2. 启动

   ![](http://zhaocan.fym233.cn/vv1xxhm88j)

3. 访问测试：`localhost:5601`

   ![](http://zhaocan.fym233.cn/bj3it4r1n)

4. 开发工具

   ![](http://zhaocan.fym233.cn/bjarmevga8)

5. 汉化，修改配置文件即可 `config/kibana.yml`

   ![](http://zhaocan.fym233.cn/jsc1l3vai)

   ![](http://zhaocan.fym233.cn/tf9a6vwj)

### 2.7、ELK

> **了解ELK**

ELK是Elasticsearch、Logstash、Kibana三大开源框架首字母大写简称。市面上也被称为Elastic Stack。其中Elasticsearch是一个基于Elucene、分布式、通过Restful方式进行交互的近实时搜索平台框架。像类似百度、谷歌这种大数据全文搜索引擎的场景都可以使用Elasticsearch作为底层支持框架，可见Elasticsearch提供的搜索能力确实强大，市面上很多时候我们简称Elasticsearch为es。Logstash是ELK的中央数据流引擎，用于从不同目标（文件/数据存储/MQ）收集的不同格式数据，经过过滤后支持输出到不同目的地（文件/MQ/Redis/Elasticsearch/kafka 等）。Kibana可以将Elasticsearch的数据通过友好的页面展示出来，提供实时分析的功能。

市面上很多开发只要提到ELK能够一致说出它是一个日志分析架构技术栈总称，但实际上ELK不仅仅适用于日志分析，它还可以支持其他任何数据分析和收集的场景，日志分析和收集只是更具有代表性。并非唯一性。

![](http://zhaocan.fym233.cn/da5oth3nmr)

好处：ELK基本上都是拆箱即用！

## 3、ES核心概念

1. 索引
2. 字段类型（mapping）
3. 文档（documents）

> **概述**

- 如何存储数据
- 数据结构是什么
- 如何实现搜索
- 集群，节点，索引，类型，文档，分片，映射是什么

> **elasticsearch是面向文档，关系型数据库 和 elasticsearch的客观对比！一切都是Json**

| Relational DB    | Elasticsearch |
| ---------------- | ------------- |
| 数据库(database) | 索引(indices) |
| 表(tables)       | types         |
| 行(rows)         | documents     |
| 字段(columns)    | fields        |

elasticsearch（集群）中可以包含多个索引（数据库），每个索引中都可包含多个类型（表），每个类型下又报函多个文档（行），每个文档中又报函多个字段（列）

**物理设计：**

elasticsearch在后台把每个**索引划分成多个分片**，每份分片可以在集群中的不同服务间迁移

一个人就是一个集群！默认的集群名称就是`elasticsearch`

![](http://zhaocan.fym233.cn/ho37a4rq55)

**逻辑设计：**

一个索引类型中，包含多个文档，比如说文档1，文档2。当我们索引一篇文档时，可以通过这样的一个顺序找到他： 索引 => 类型 => 文档id，通过这个组合我们就能索引到某个具体的文档。注意：id不必是整数，实际上它是一个字符串。

### 3.1、文档

之前说elasticsearch是面向文档的，那么就意味着索引和搜索数据的最小单位是文档，elasticsearch中，文档有几个重要属性：

- 自我包含，一篇文档同时博阿寒字段和对应的值，也就是同时包含 key : value
- 可以是层次型的，一个文档中报函自文档，复杂的逻辑实体就是这么来的
- 灵活的结构，文档不依赖预先定义的模式，我们知道关系型数据库中，要提前定义字段才能使用，在elasticsearch中，对于字段是非常灵活的，有时候，我们可以忽略该字段，或者动态的添加一个新的字段。

尽管我们可以随意的新增或者忽略某个字段，但是，每个字段的类型都非常重要，比如一个年龄字段类型，可以是字符串也可以是整形。因为elasticsearch会保存字段和类型之间的映射及其他的设置。这种映射具体到每个映射的每种类型，这也是为什么在elasticsearch中，类型有时候也称为映射类型。

### 3.2、类型

类型是文档的逻辑容器，就像关系型数据库一样，表格是行的容器。类型中对于字段的定义称为映射，比如name映射为字符串类型，我们说文档是无模式的，它们不需要拥有映射中所定义的所有字段，比如新增一个字段，那么elasticsearch是怎么做的呢？elasticsearch会自动的将新字段加入映射，但是这个字段的不确定它是什么类型，elasticsearch就开始猜，如果这个值是18，那么elasticssearch会认为它是整形。但是elasticsearch也可能猜不对，所以最安全的方式就是提前定义好所需要的映射，这点跟关系型数据库殊途同归了，先定义好字段，然后再使用。

### 3.3、索引

索引是映射类型的容器，elasticsearch中的索引是一个非常大的文档集合。索引存储了映射类型的字段和其他设置。然后它们被存储到了各个分片上了，我们来研究下分片是如何工作的。

**物理设计：节点和分片如何工作**

![](http://zhaocan.fym233.cn/1ehk6byhx)

一个集群至少有一个节点，而一个节点就是一个elasticsearch进程，节点可以有多个索引默认的，如果你创建索引，那么索引将会有5个分片（primary shard，又称主分片）构成的，每一个主分片会有一个副本（replica shard，又称复制分片）

![](http://zhaocan.fym233.cn/6ojftkcdq7)

上图是一个有3个节点的集群，可以看到主分片和对应的复制分片都不会在同一个节点内，这样有利于某个节点挂掉了，数据也不至于丢失。实际上，一个分片是一个Lucene索引，一个包含**倒排索引**的文件目录，倒排索引的结构使得elasticsearch在不扫描全部文档的情况下，就能告诉你哪些文档报函特定的关键字。那么倒排索引是什么呢？

### 3.4、倒排索引

elasticsearch使用的是一种称为倒排索引的结构，采用Lucene倒排索引作为底层。这种结构适用于快速的全文搜索，一个索引由文档中所有不重复的列表构成，对于每一个词，都有一个包含它的文档列表。例如，现在有两个文档，每个文档报函如下内容：

```bash
study every day, good good up to forever	# 文档1包含的内容
To forever, study every day, good good up	# 文档2包含的内容
```

为了创建倒排索引，我们首先要将每个文档拆分成独立的词（或称为词条或者tokens），然后创建一个包含所有不重复的词条的排序列表，然后列出每个词条出现在哪个文档：

| term    | doc_1 | doc_2 |
| ------- | ----- | ----- |
| Study   | √     | ×     |
| To      | ×     | ×     |
| every   | √     | √     |
| forever | √     | √     |
| day     | √     | √     |
| study   | ×     | √     |
| good    | √     | √     |
| every   | √     | √     |
| to      | √     | ×     |
| up      | √     | √     |

现在，我们试图搜索`to forever`，只需要查看包含每个词条的文档 score

| term    | doc_1 | doc_2 |
| ------- | ----- | ----- |
| to      | √     | ×     |
| forever | √     | √     |
| total   | 2     | 1     |

两个文档都匹配，但是第一个文档比第二个匹配程度更高。如果没有别的条件，现在，这两个包含关键字的文档都将返回。

再来看一个示范，比如我们通过博客标签来搜索博客文章。那么倒排索引列表就是这样的一个结构：

![](http://zhaocan.fym233.cn/kgoypoxl5o)

如果要搜索含有python标签的文章，那相对于查找所有原始数据而言，查找倒排索引后的数据将会快得多。只需要查看标签这一栏，然后获取相关的文章id即可。完全过滤掉无关的所有数据，提高效率！

elastisearch的索引和Lucene的索引对比

在elasticsearch中，索引这个词被频繁使用，这就是术语的使用。在elasticsearch中，索引被分为多个分片，每份分片是一个Lucene的索引。**所以一个elasticsearch索引是由多个Lucene索引组成的**。别问为什么，谁让elasticsearch使用Lucene作为底层呢！如无特指，说起索引都是指elasticsearch的索引。

接下来的一切操作都在Kibana中Dev Tools下的Console里完成。基础操作！

## 4、IK分词器插件

> **什么是IK分词器？**

分词：即把一段中文或者别的划分成一个个的关键字，我们在搜索时候会把自己的信息进行分词，会把数据库中或者索引库中的数据进行分词，然后进行一个匹配操作，默认的中文分词是将每个字看成一个词，比如 “谷歌搜索”会被分为“谷“，”歌“，”搜“，”索”，这显然是不符合要求的，所以我们需要安装中文分词器ik来解决这个问题。

如果要使用中文，建议使用IK分词器！

IK提供了两个分词算法：ik_smart 和 ik_max_word，其中ik_smart为最少切分，ik_max_work为最细粒度划分！

> **安装**

1. https://github.com/medcl/elasticsearch-analysis-ik

2. 下载完毕之后，放入 `elasticsearch`插件即可

   ![](http://zhaocan.fym233.cn/ksqdl5mnu2)

3. 重启观察ES，可以看到ik分词器被加载了！

   ![](http://zhaocan.fym233.cn/ps6ee9igbi)

4. `elasticsearch-plugin`可以通过这个命令来查看加载进来的插件

   ![](http://zhaocan.fym233.cn/ea33jeni7)

5. 使用Kibana测试

> **查看不同的分词器效果**

ik_smart：最少切分

![](http://zhaocan.fym233.cn/n94w7zxla5)

ik_max_word：最细粒度划分！穷尽词库的可能

![](http://zhaocan.fym233.cn/6zb6o8bl5l)

> **输入：超级喜欢狂神说Java**

![](http://zhaocan.fym233.cn/a20jnugbkq)

发现问题：狂神说被拆开了！

这种自己需要的词，需要自己加到我们的分词器的字典中！

> **ik 分词器增加自己的配置！**

![](http://zhaocan.fym233.cn/iraq5et5yh)

重启es

![](http://zhaocan.fym233.cn/f10yfuiql9)

再次测试一下狂神说，看下效果！

![](http://zhaocan.fym233.cn/dezy0hjgb)

以后的话，我们需要自己配置 分词就在自己定义的dic文件中进行配置即可！

## 5、Rest风格说明

一种软件架构风格，而不是标准，只是提供了一组设计原则和约束条件。它主要用于客户端和服务器交互类的软件。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存等机制。

基本Rest命令说明：

| method | url地址                                         | 描述                   |
| ------ | ----------------------------------------------- | ---------------------- |
| PUT    | localhost:9200/索引名称/类型名称/文档id         | 创建文档（指定文档id） |
| POST   | localhost:9200/索引名称/类型名称                | 创建文档（随机文档id） |
| POST   | localhost:9200/索引名称/类型名称/文档id/_update | 修改文档               |
| DELETE | localhost:9200/索引名称/类型名称/文档id         | 删除文档               |
| GET    | localhost:9200/索引名称/类型名称/文档id         | 查询文档通过文档id     |
| POST   | localhost:9200/索引名称/类型名称/_search        | 查询所有数据           |

### 5.1、关于索引的基本操作

1. 创建一个索引

   ```bash
   PUT /索引名/~类型名~/文档id
   {
   	请求体
   }
   ```

   ![](http://zhaocan.fym233.cn/elbvx13qqc)

2. 完成了自动增加了索引！数据也成功的添加了

   ![](http://zhaocan.fym233.cn/zm8ng6fy6a)

3. 那么name这个字段用不用指定类型呢。毕竟关系型数据库是需要指定类型的

   - 字符串类型

     text、keyword

   - 数值类型

     long、integer、short、byte、double、float、half float、scaled float

   - 日期类型

     date

   - te布尔值类型

     boolean

   - 二进制类型

     binary

   - 等等...

4. 指定字段的类型

   ![](http://zhaocan.fym233.cn/kklubs9ckt)

   获得这个规则！可以通过GET请求获得具体的信息

   ![](http://zhaocan.fym233.cn/xh4s0cmvf)

5. 查看默认的信息

   ![](http://zhaocan.fym233.cn/wnfv9rbsmj)

   ![](http://zhaocan.fym233.cn/os5xyvcdzn)

   如果自己的文档字段没有指定，那么es就会给我们默认配置字段类型

   **type类型以后会被弃用，默认的type类型就是`_doc`**

6. 扩展命令：elasticsearch 索引情况！通过`GET _cat`可以获得es当前的很多信息

   ![](http://zhaocan.fym233.cn/7zgdfa0uij)

> **修改 提交还是使用PUT即可！然后覆盖！**

​	曾经的方法：

![](http://zhaocan.fym233.cn/sa75c7e98)

现在的方法：使用POST修改

![](http://zhaocan.fym233.cn/4h9lco3afi)

> **删除索引**

通过DELETE命令实现删除，根据你的请求来判断是删除索引还是删除文档记录

![](http://zhaocan.fym233.cn/3a5fcndb9)

使用RestFul风格是我们ES推荐大家使用的！

### 5.2、关于文档的基本操作

> **基本操作**

1. 添加数据

   ![](http://zhaocan.fym233.cn/hvjuw5v5v)

2. 获取数据 GET

   ![](http://zhaocan.fym233.cn/x0qud0xoss)

3. 更新数据 PUT

   ![](http://zhaocan.fym233.cn/9a167s1ycj)

4. 更新数据 POST

   **如果PUT的值只传部分参数的话，其余参数会制空；POST只会修改想要修改的参数。推荐使用post**

> **简单搜索**

```bash
GET zhaocan/user/1
```

> **简单的条件查询**

![](http://zhaocan.fym233.cn/cc6zymul1k)

![](http://zhaocan.fym233.cn/v8dr2ydslp)

> **复杂操作查询：query**

![](http://zhaocan.fym233.cn/j9zdikpf4g)

![](http://zhaocan.fym233.cn/yzuewnzu7)

> **指定字段查询：_source**

![](http://zhaocan.fym233.cn/n5w5s4aq5t)

> **排序：sort**

![](http://zhaocan.fym233.cn/0sf1dm0fyo)

> **分页查询：from，size**

![](http://zhaocan.fym233.cn/6xfvr0sdyq)

数据下标还是从0开始的，和之前的所有数据结构是一样的！

> **布尔值查询：bool**

**must（and），所有的条件都要符合**

![](http://zhaocan.fym233.cn/c4qa2cspkf)

**should（or），条件满足其一即可**

![](http://zhaocan.fym233.cn/e5l8duwiog)

**must_not（not）**

![](http://zhaocan.fym233.cn/af8emnn6bb)

> **过滤器：filter**

![](http://zhaocan.fym233.cn/1yzvcxq5ae)

- gt：大于
- gte：大于等于
- lt：小于
- lte：小于等于

![](http://zhaocan.fym233.cn/iy4lvyzx2)

> **匹配多个条件**

![](http://zhaocan.fym233.cn/o1jqdsb9)

> **精确查询**

term查询是直接通过倒排索引指定的词条进程精确的查找的！

**关于分词：**

- term：直接查询精确的
- match：会使用分词器解析（先分析文档，然后再通过分析的文档进行查询）

**两个类型：**

- text

  ![](http://zhaocan.fym233.cn/sw8dov8mlr)

- keyword

  ![](http://zhaocan.fym233.cn/ru80zyx38)

**总结**

![](http://zhaocan.fym233.cn/kwm8puw1ji)

> **多个值匹配精确查询**

![](http://zhaocan.fym233.cn/5u202q8u5)

> **高亮查询**

![](http://zhaocan.fym233.cn/6wxdrz5c4)

![](http://zhaocan.fym233.cn/7xlbzqwsu)

这些MySQL也可以做，只是MySQL效率比较低！

- 匹配
- 按照条件匹配
- 精确匹配
- 区间范围匹配
- 匹配字段过滤
- 多条件查询
- 高亮查询

## 6、集成SpringBoot

> **官方文档**

![](http://zhaocan.fym233.cn/m5qbkrg3u9)

![](http://zhaocan.fym233.cn/er3abcinv)

![](http://zhaocan.fym233.cn/qd35ta36wj)

1. 找到原生依赖

   ```xml
   <!-- https://mvnrepository.com/artifact/org.elasticsearch.client/elasticsearch-rest-high-level-client -->
   <dependency>
       <groupId>org.elasticsearch.client</groupId>
       <artifactId>elasticsearch-rest-high-level-client</artifactId>
       <version>7.13.2</version>
   </dependency>
   ```

2. 找到对应的对象

   ![](http://zhaocan.fym233.cn/h28a9a5npo)

3. 分析这个类中的方法即可

   > **配置基本的项目**

   **问题：一定要保证导入的依赖和我们的es版本一致**

![](http://zhaocan.fym233.cn/da5qh1x7n)

​	![](http://zhaocan.fym233.cn/yalckg178)

源码中提供对象：

![](http://zhaocan.fym233.cn/p14sx8vq6)

虽然这里导入3个类，都是静态内部类 。核心类只有一个

```java
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

package org.springframework.boot.autoconfigure.data.elasticsearch;

import java.util.Collections;
import org.elasticsearch.action.support.IndicesOptions;
import org.elasticsearch.client.RestHighLevelClient;
import org.springframework.boot.autoconfigure.condition.ConditionalOnBean;
import org.springframework.boot.autoconfigure.condition.ConditionalOnClass;
import org.springframework.boot.autoconfigure.condition.ConditionalOnMissingBean;
import org.springframework.boot.autoconfigure.domain.EntityScanner;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.elasticsearch.annotations.Document;
import org.springframework.data.elasticsearch.client.reactive.ReactiveElasticsearchClient;
import org.springframework.data.elasticsearch.core.ElasticsearchOperations;
import org.springframework.data.elasticsearch.core.ElasticsearchRestTemplate;
import org.springframework.data.elasticsearch.core.ReactiveElasticsearchOperations;
import org.springframework.data.elasticsearch.core.ReactiveElasticsearchTemplate;
import org.springframework.data.elasticsearch.core.RefreshPolicy;
import org.springframework.data.elasticsearch.core.convert.ElasticsearchConverter;
import org.springframework.data.elasticsearch.core.convert.ElasticsearchCustomConversions;
import org.springframework.data.elasticsearch.core.convert.MappingElasticsearchConverter;
import org.springframework.data.elasticsearch.core.mapping.SimpleElasticsearchMappingContext;
import org.springframework.web.reactive.function.client.WebClient;

abstract class ElasticsearchDataConfiguration {
    ElasticsearchDataConfiguration() {
    }

    @Configuration(
        proxyBeanMethods = false
    )
    @ConditionalOnClass({WebClient.class, ReactiveElasticsearchOperations.class})
    static class ReactiveRestClientConfiguration {
        ReactiveRestClientConfiguration() {
        }

        @Bean
        @ConditionalOnMissingBean(
            value = {ReactiveElasticsearchOperations.class},
            name = {"reactiveElasticsearchTemplate"}
        )
        @ConditionalOnBean({ReactiveElasticsearchClient.class})
        ReactiveElasticsearchTemplate reactiveElasticsearchTemplate(ReactiveElasticsearchClient client, ElasticsearchConverter converter) {
            ReactiveElasticsearchTemplate template = new ReactiveElasticsearchTemplate(client, converter);
            template.setIndicesOptions(IndicesOptions.strictExpandOpenAndForbidClosed());
            template.setRefreshPolicy(RefreshPolicy.IMMEDIATE);
            return template;
        }
    }

    @Configuration(
        proxyBeanMethods = false
    )
    @ConditionalOnClass({RestHighLevelClient.class})
    static class RestClientConfiguration {
        RestClientConfiguration() {
        }

        @Bean
        @ConditionalOnMissingBean(
            value = {ElasticsearchOperations.class},
            name = {"elasticsearchTemplate"}
        )
        @ConditionalOnBean({RestHighLevelClient.class})
        ElasticsearchRestTemplate elasticsearchTemplate(RestHighLevelClient client, ElasticsearchConverter converter) {
            return new ElasticsearchRestTemplate(client, converter);
        }
    }

    @Configuration(
        proxyBeanMethods = false
    )
    static class BaseConfiguration {
        BaseConfiguration() {
        }

        @Bean
        @ConditionalOnMissingBean
        ElasticsearchCustomConversions elasticsearchCustomConversions() {
            return new ElasticsearchCustomConversions(Collections.emptyList());
        }

        @Bean
        @ConditionalOnMissingBean
        SimpleElasticsearchMappingContext mappingContext(ApplicationContext applicationContext, ElasticsearchCustomConversions elasticsearchCustomConversions) throws ClassNotFoundException {
            SimpleElasticsearchMappingContext mappingContext = new SimpleElasticsearchMappingContext();
            mappingContext.setInitialEntitySet((new EntityScanner(applicationContext)).scan(new Class[]{Document.class}));
            mappingContext.setSimpleTypeHolder(elasticsearchCustomConversions.getSimpleTypeHolder());
            return mappingContext;
        }

        @Bean
        @ConditionalOnMissingBean
        ElasticsearchConverter elasticsearchConverter(SimpleElasticsearchMappingContext mappingContext, ElasticsearchCustomConversions elasticsearchCustomConversions) {
            MappingElasticsearchConverter converter = new MappingElasticsearchConverter(mappingContext);
            converter.setConversions(elasticsearchCustomConversions);
            return converter;
        }
    }
}
```

> **具体的API测试**

1. 创建索引

   ```java
   //  测试索引的创建
   @Test
   void testCreateIndex() throws IOException {
       //  1、创建索引请求
       CreateIndexRequest request = new CreateIndexRequest("zhaocan_index");
       //  2、客户端执行请求，请求后获得响应
       CreateIndexResponse createIndexResponse = client.indices().create(request, RequestOptions.DEFAULT);
   
       System.out.println(createIndexResponse);
   }
   ```

2. 判断索引是否存在

   ```java
   //  获取索引，只能判断是否存在
   @Test
   void testExistIndex() throws IOException {
       GetIndexRequest getIndexRequest = new GetIndexRequest("zhaocan_index");
       boolean exists = client.indices().exists(getIndexRequest, RequestOptions.DEFAULT);
   
       System.out.println(exists);
   }
   ```

3. 删除索引

   ```java
   //  测试删除索引
   @Test
   void testDeleteIndex() throws IOException {
       DeleteIndexRequest deleteIndexRequest = new DeleteIndexRequest("zhaocan_index");
       AcknowledgedResponse delete = client.indices().delete(deleteIndexRequest, RequestOptions.DEFAULT);
       System.out.println(delete.isAcknowledged());
   }
   ```

4. 创建文档

   ```java
   //  测试添加文档
   @Test
   void testAddDocument() throws IOException {
       //  1、创建对象
       User user = new User("赵灿", 23);
       //  2、创建请求
       IndexRequest request = new IndexRequest("zhaocan_index");
   
       //  3、设置规则
       request.id("1");
       request.timeout(TimeValue.timeValueSeconds(1));
       request.timeout("1s");
   
       //  4、将数据放入请求
       IndexRequest source = request.source(JSON.toJSONString(user), XContentType.JSON);
   
       //  5、客户端发送请求，获取响应结果
       IndexResponse index = client.index(request, RequestOptions.DEFAULT);
   
       System.out.println(index.toString());
       System.out.println(index.status().toString());
   }
   ```

5. CRUD 文档

   ```java
   //  获取文档，判断是否存在
   @Test
   void testIsExists() throws IOException {
       GetRequest getRequest = new GetRequest("zhaocan_index", "1");
       //  不获取返回的_source 的上下文了
       getRequest.fetchSourceContext(new FetchSourceContext(false));
       //  排序字段
       getRequest.storedFields("_none_");
   
       boolean exists = client.exists(getRequest, RequestOptions.DEFAULT);
   
       System.out.println(exists);
   }
   
   //  获得文档的信息
   @Test
   void testGetDocument() throws IOException {
       GetRequest getRequest = new GetRequest("zhaocan_index", "1");
       GetResponse documentFields = client.get(getRequest, RequestOptions.DEFAULT);
   
       System.out.println(documentFields.getSourceAsString()); //打印文档内容
       System.out.println(documentFields); //  返回的全部内容和命令是一样的
   }
   
   //  更新文档的信息
   @Test
   void testUpdateDocument() throws IOException {
       UpdateRequest updateRequest = new UpdateRequest("zhaocan_index", "1");
       updateRequest.timeout("1s");
   
       User user = new User("张三", 3);
       updateRequest.doc(JSON.toJSONString(user), XContentType.JSON);
   
       UpdateResponse update = client.update(updateRequest, RequestOptions.DEFAULT);
   
       System.out.println(update.status());
   }
   
   //  删除文档记录
   @Test
   void testDeleteDocument() throws IOException {
       DeleteRequest deleteRequest = new DeleteRequest("zhaocan_index", "1");
       deleteRequest.timeout("1s");
   
       DeleteResponse delete = client.delete(deleteRequest, RequestOptions.DEFAULT);
   
       System.out.println(delete.status());
   }
   
   //  批量查询
   @Test
   void testBluk() throws IOException {
       BulkRequest bulkRequest = new BulkRequest();
       bulkRequest.timeout("10s");
       ArrayList<User> users = new ArrayList<>();
       users.add(new User("zhaocan1", 3));
       users.add(new User("zhaocan2", 3));
       users.add(new User("zhaocan3", 3));
       users.add(new User("zhaocan4", 3));
       users.add(new User("zhaocan5", 3));
       users.add(new User("zhaocan6", 3));
       users.add(new User("zhaocan7", 3));
       users.add(new User("zhaocan8", 3));
   
       //  批处理请求
       for (int i = 0; i < users.size(); i++) {
           bulkRequest.add(
               new IndexRequest("zhaocan_index")
               //.id(i+1+"")
               .source(JSON.toJSONString(users.get(i)),XContentType.JSON)
           );
       }
   
       BulkResponse bulk = client.bulk(bulkRequest, RequestOptions.DEFAULT);
   
       //  返回false是成功
       System.out.println(bulk.hasFailures());
   }
   
   //  查询
   //  SearchRequest：搜索请求
   //  SearchSourceBuilder：条件构造
   //  HighlightBuilder：构建高亮
   //  TermQueryBuilder：精确查询
   //  MatchAllQueryBuilder：匹配所有
   //  xxxQueryBuilder：对应之前的所有命令
   @Test
   void testSearch() throws IOException {
       SearchRequest searchRequest = new SearchRequest("zhaocan_index");
   
       //  构建搜索的条件
       SearchSourceBuilder builder = new SearchSourceBuilder();
       //  查询条件，我们可以使用QueryBuilders工具类来实现
       //  QueryBuilders.termQuery：精确匹配
       //  QueryBuilders.matchAllQuery()：匹配所有
       TermQueryBuilder termQueryBuilder = QueryBuilders.termQuery("name", "zhaocan1");
       MatchAllQueryBuilder matchAllQueryBuilder = QueryBuilders.matchAllQuery();
       builder.query(termQueryBuilder);
   
       builder.from(0);
       builder.size(10);
       builder.timeout(new TimeValue(60, TimeUnit.SECONDS));
   
       SearchRequest source = searchRequest.source(builder);
   
       SearchResponse search = client.search(searchRequest, RequestOptions.DEFAULT);
       System.out.println(JSON.toJSONString(search.getHits()));
       System.out.println("===================================");
       for (SearchHit hit : search.getHits().getHits()) {
           System.out.println(hit.getSourceAsMap());
       }
   }
   ```

## 7、爬虫

> **数据从哪里获取？一般从数据库、消息队列中获取，都可以称为数据源。也可以使用爬虫**

爬取数据：（获取请求返回的页面信息，筛选出我们想要的数据就可以了！）

jsoup包:用于解析网页，不能爬电影

新建一个utils包放网页解析的工具类

![](http://zhaocan.fym233.cn/xdgyxdpap)

本质的请求是：`https://search.jd.com/Search?keyword=java`

![](http://zhaocan.fym233.cn/6y2mfrx338)

所有在Js中的方法这里都可以使用

```java
package com.zc.utils;

import com.zc.pojo.Content;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.net.URL;
import java.util.ArrayList;
import java.util.List;

public class HtmlParseUtil {

    public static void main(String[] args) throws Exception {
        //  获取请求
        //  前提，需要联网。不能获取ajax获取
        String url = "https://search.jd.com/Search?keyword=java";

        //  解析网页（jsoup返回的document就是 js里的document对象）
        Document document = Jsoup.parse(new URL(url), 30000);

        Element element = document.getElementById("J_goodsList");
        //  获取所有的<li>元素
        Elements elements = element.getElementsByTag("li");

        ArrayList<Content> goodsList = new ArrayList<>();
        //  获取元素中的内容，这里el 就是每一个<li>标签
        for (Element el : elements) {
            //  关于这种图片特别多的网站，所有的图片都是延迟加载的
            String img = el.getElementsByTag("p-img").eq(0).attr("source-data-lazy-img");
            String price = el.getElementsByClass("p-price").eq(0).text();
            String title = el.getElementsByClass("p-name").eq(0).text();

            System.out.println("img=>"+img);
            System.out.println("price=>"+price);
            System.out.println("title=>"+title);
        }
    }
}
```

![](http://zhaocan.fym233.cn/0yt0a9isrp)

![](http://zhaocan.fym233.cn/2d89t9zmsd)

![](http://zhaocan.fym233.cn/gw67phvizg)

输出结果

![](http://zhaocan.fym233.cn/yha3ifp06)

**注意：**

**在图片较多的网站中，图片往往是延迟加载的，注意看图片的属性：**

![](http://zhaocan.fym233.cn/4x4104i3jq)

将获取到的元素 封装成对象，新建pojo，`Content.java`

```java
package com.zc.pojo;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.io.Serializable;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class Content implements Serializable {
    private String title;
    private String img;
    private String price;
}
```

再次封装工具类：

```java
package com.zc.utils;

import com.zc.pojo.Content;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.net.URL;
import java.util.ArrayList;
import java.util.List;

public class HtmlParseUtil {

    public static void main(String[] args) throws Exception {
        HtmlParseUtil.parseJD("java").forEach(System.out::println);
    }

    public static List<Content> parseJD(String searchKey) throws Exception {
        //  获取请求
        //  前提，需要联网。不能获取ajax获取
        String url = "https://search.jd.com/Search?keyword="+ searchKey;

        //  解析网页（jsoup返回的document就是 js里的document对象）
        Document document = Jsoup.parse(new URL(url), 30000);

        Element element = document.getElementById("J_goodsList");
        //  获取所有的<li>元素
        Elements elements = element.getElementsByTag("li");

        ArrayList<Content> goodsList = new ArrayList<>();
        //  获取元素中的内容，这里el 就是每一个<li>标签
        for (Element el : elements) {
            //  关于这种图片特别多的网站，所有的图片都是延迟加载的
            String img = el.getElementsByTag("p-img").eq(0).attr("source-data-lazy-img");
            String price = el.getElementsByClass("p-price").eq(0).text();
            String title = el.getElementsByClass("p-name").eq(0).text();

            Content content = new Content(title, img, price);
            goodsList.add(content);
        }
        return goodsList;
    }
}
```

编写业务层service：

```java
package com.zc.service;

import com.alibaba.fastjson.JSON;
import com.zc.pojo.Content;
import com.zc.utils.HtmlParseUtil;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.unit.TimeValue;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.index.query.TermQueryBuilder;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.concurrent.TimeUnit;

@Service
public class ContentService {
    @Autowired
    private RestHighLevelClient restHighLevelClient;

    //  1、解析数据并放入 es 索引中
    public Boolean parseContent(String keywords) throws Exception {
        List<Content> contents = HtmlParseUtil.parseJD(keywords);
        //把查询到的数据放入es中
        BulkRequest bulkRequest = new BulkRequest();
        bulkRequest.timeout("2s");

        for (int i = 0; i < contents.size(); i++) {
            bulkRequest.add(
                new IndexRequest("jd-goods")
                .source(JSON.toJSONString(contents.get(i)), XContentType.JSON)
            );
        }

        BulkResponse bulk = restHighLevelClient.bulk(bulkRequest, RequestOptions.DEFAULT);
        return !bulk.hasFailures();
    }
```

编写controller来测试：

```java
package com.zc.controller;

import com.zc.service.ContentService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

import java.io.IOException;
import java.util.List;
import java.util.Map;

@RestController
public class ContentController {
    @Autowired
    private ContentService contentService;

    @GetMapping("/parse/{keyword}")
    public Boolean parse(@PathVariable("keyword") String keyword) throws Exception {
        return contentService.parseContent(keyword);
    }
}
```

再在业务层中实现搜索功能：

```java
//  2、获取这些数据实现搜索功能
public List<Map<String, Object>> searchPage(String keyword, int pageNo, int pageSize) throws IOException {
    if(pageNo <= 1) {
        pageNo = 1;
    }

    //  条件搜索
    SearchRequest searchRequest = new SearchRequest("jd_goods");
    SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

    //  分页
    sourceBuilder.from(pageNo);
    sourceBuilder.size(pageSize);

    //  精确查询
    TermQueryBuilder title = QueryBuilders.termQuery("title", keyword);
    sourceBuilder.query(title);
    sourceBuilder.timeout(new TimeValue(60, TimeUnit.SECONDS));

    //  执行搜索
    searchRequest.source(sourceBuilder);
    SearchResponse search = restHighLevelClient.search(searchRequest, RequestOptions.DEFAULT);

    //  解析结果
    ArrayList<Map<String, Object>> list = new ArrayList<>();
    for (SearchHit hit : search.getHits().getHits()) {
        list.add(hit.getSourceAsMap());
    }

    return list;
}
```

用Controller来测：

```java
@GetMapping("/search/{keyword}/{pageNo}/{pageSize}")
public List<Map<String, Object>> search(
    @PathVariable("keyword")String keyword,
    @PathVariable("pageNo")int pageNo,
    @PathVariable("pageSize")int pageSize) throws IOException {
    return contentService.searchPage(keyword, pageNo, pageSize);
}
```

添加高亮搜索功能：

```java
//  3、获取这些数据实现搜索高亮功能
public List<Map<String, Object>> searchHighlightPage(String keyword, int pageNo, int pageSize) throws IOException {
    if (pageNo <= 1) {
        pageNo = 1;
    }

    //  条件搜索
    SearchRequest searchRequest = new SearchRequest("jd_goods");
    SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

    //  分页
    sourceBuilder.from(pageNo);
    sourceBuilder.size(pageSize);

    //  精确查询
    TermQueryBuilder title = QueryBuilders.termQuery("title", keyword);
    sourceBuilder.query(title);
    sourceBuilder.timeout(new TimeValue(60, TimeUnit.SECONDS));

    //  高亮
    HighlightBuilder highlightBuilder = new HighlightBuilder();
    highlightBuilder.field("title");
    //  是否开启多个高亮
    highlightBuilder.requireFieldMatch(false);
    highlightBuilder.preTags("<span style='color:red'>");
    highlightBuilder.postTags("</span>");
    sourceBuilder.highlighter(highlightBuilder);

    //  执行搜索
    searchRequest.source(sourceBuilder);
    SearchResponse search = restHighLevelClient.search(searchRequest, RequestOptions.DEFAULT);

    //  解析结果
    ArrayList<Map<String, Object>> list = new ArrayList<>();
    for (SearchHit hit : search.getHits().getHits()) {
        //  获取高亮字段
        Map<String, HighlightField> highlightFields = hit.getHighlightFields();
        //  获取具体的高亮字段
        HighlightField title1 = highlightFields.get("title");
        //  获取所有查询的内容
        Map<String, Object> sourceAsMap = hit.getSourceAsMap();
        //  判断是否拥有高亮字段
        if(title1 != null) {
            //  获取高亮字段
            Text[] texts = title1.getFragments();
            //  将高亮字段替换为原来未高亮的字段
            String highlight_title = "";
            for (Text text : texts) {
                highlight_title += text;
            }
            sourceAsMap.put("title", highlight_title);
        }
        list.add(sourceAsMap);
    }

    return list;
}
```

编写controller来测试

```java
@GetMapping("/searchhigh/{keyword}/{pageNo}/{pageSize}")
public List<Map<String, Object>> searchHighLight(
    @PathVariable("keyword")String keyword,
    @PathVariable("pageNo")int pageNo,
    @PathVariable("pageSize")int pageSize) throws IOException {
    return contentService.searchHighlightPage(keyword, pageNo, pageSize);
}
```

在`index.html`需要输出高亮的标题`title`添加**`v-html=item.name`**

```html
<!--标题-->
<p class="productTitle">
    <a v-html="item.name"></a>
</p>
```

