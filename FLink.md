## 1、Flink概述

### 1.1、Flink是什么

> **Flink官网主页地址：**https://flink.apache.org

Flink核心目标，是**"数据流上的有状态计算"**(Stateful Computations over Data Streams)。

具体说明：Apache Flink是一个**框架**和**分布式处理引擎**，用于对**无界**和**有界**数据流进行**有状态计算**。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230809-130953.png)

> **有界流与无界流**

1. 无界数据流
   - 有定义流的开始，但没有定义流的结束
   - 它们会无休止的产生数据
   - 无界流的数据必须持续处理，即数据被摄取后需要立刻处理。我们不能等到所有数据都到达再处理，因为输出是无限的
2. 有界数据流
   - 有定义流的开始，也有定义流的结束
   - 有界流可以在摄取所有数据后再进行计算
   - 有界流所有数据可以被排序，所以并不需要有序摄取
   - 有界流数据通常被称为批处理  

> **有状态流处理**

把流处理需要的**额外数据保存成一个"状态"**，然后针对这条数据进行处理，并且**更新状态**。这就是所谓的**"有状态流处理"**。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230809-132348.png)

状态在内存中：

- 优点：速度快
- 缺点：可靠性差

### 1.2、Flink特点

> **Flink的发展历史**

Flink起源于一个叫做**Stratosphere的项目**，它是由3所地处柏林的大学和欧洲其他一些大学在2010～2014年共同进行的研究项目，由**柏林理工大学的教授沃克尔·马尔科(Volker Markl)领衔开发**。2014年4月，Stratosphere的代码被复制并**捐赠给了Apache软件基金会**，Flink就是在此基础上被重新设计出来的。

在德语中，"flink"一次表示"**快速、灵巧**"。项目的logo是一只彩色的松鼠。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230809-133242.png)

- 2014年8月，Flink第一个版本0.6正式发布，与此同时Flink的几位核心开发者创办Data Artisans公司
- 2014年12月，Flink项目完成孵化
- 2015年4月，Flink发布了里程碑式的重要版本0.9.0
- 2019年1月，长期对Flink投入研发的阿里巴巴，以9000万欧元的价格收购了Data Artisans公司
- 2019年8月，阿里巴巴将内部版本Blink开源，合并入Flink1.9.0版本

> **Flink特点**

Flink处理数据的目标是：**低延迟、高吞吐、结果的准确性和良好的容错性**。

Flink主要特点如下：

- **高吞吐和低延迟**。每秒处理数百万个事件，毫秒级延迟。
- **结果的准确性**。Flink提供了**事件事件**(event-time)和**处理时间**(processing-time)语义。对于乱序事件流，事件事件语义仍然能提供一致且准确的结果。
- **精准一次**(exactly-once)的状态一致性保证。
- **可以连接到最常用的存储系统**，如Kafka、Hive、JDBC、HDFS、Redis等
- **高可用**。本身高可用的设置，加上与K8s，YARN和Mesos的紧密集成，再加上从故障中快速恢复和动态扩展任务的能力，Flink能做到以极少的停机时间7X24全天候运行。

### 1.3、Flink vs SparkStreaming

- **Spark以批处理为根本**

  - Spark数据模型：Spark采用RDD模型，Spart Streaming的DStream实际上也就一组组小批数据RDD的集合

  - Spark运行时架构：Spark是批计算，将DAG划分为不同的stage，一个完成后才可以计算下一个

    ![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230809-134207.png)

- **Flink与流处理为根本**

  - Flink数据模型：Flink基本数据模型是**数据流**，以及事件(Event)排序

  - Flink运行时架构：Flink是标准的流执行模式，**一个事件在一个节点处理完成后可以直接发往下一个节点进行处理**

    ![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230809-134219.png)

表Flink和Streaming对比：

|              | Flink              | Streaming                          |
| ------------ | ------------------ | ---------------------------------- |
| **计算模型** | 流计算             | 微批处理                           |
| **时间语义** | 事件事件、处理时间 | 处理时间                           |
| **窗口**     | 多、灵活           | 少、不灵活(窗口必须是批次的整数倍) |
| **状态**     | 有                 | 没有                               |
| **流式SQL**  | 有                 | 没有                               |

### 1.4、Flink的应用场景

> **Flink在国内各个企业中大量使用。一些行业中的典型应用有：**

1. **电商和市场营销**
   - 举例：**实时**数据**报表**、**广告**投放、**实时推荐**
2. **物联网（IOT）**
   - 举例：传感器实时数据采集和显示、**实时报警**、交通运输业
3. **物流配送和服务业**
   - 举例：**订单状态实时更新**、通知信息推送
4. **银行和金融业**
   - 举例：实时结算和通知推送，**实时检测异常行为**

### 1.5、Flink分层API

- 越底层越抽象，表达含义越简明，使用越方便
- 越底层越具体，表达能力越丰富，使用越灵活

![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230809-135850.png)

- 有状态流处理：通过底层API（处理函数），对最原始数据加工处理。底层API与DataStream API相集成，可以处理复杂的计算。
- **DataStream API（流处理）和DataSet Api（批处理）**封装了底层处理函数，提供了通用的模块，比较转换（transformations，包括map、flatmap等）连接（joins），聚合（aggregations），窗口（windows）操作等。注意：Flink1.12以后，**DataSteam API已经实现真正的流批一体，所以DataSet API已经过时。**
- **Table API是以表为中心的声明式编程**，其中表可能会动态变化。Table API遵循关系模型：表有二位数据结构，类似于关系数据库中的表；同时APi提供可比较的操作，例如**（select、project、join、group-by、aggregate）**等。我们可以在表与DataStream/DataSet之间无缝切换，以允许程序将Table API与DataStream以及DataSet混合使用。
- **SQL**这一层在语法与表达能力上与Table API类似，但是是**以SQL查询表达式的形式表达程序**。SQL抽象与Table API交互密切，同时SQL查询可以直接在Table API定义的表上执行。

## 2、Flink快速上手

### 2.1、创建项目

在准备好所有的开发环境之后，我们就可以开始开发自己的第一个Flink程序了。首先我们要做的，就是在IDEA中搭建一个Flink项目的骨架。我们会使用Java项目中常见的Maven来进行依赖管理。

1. 创建工程

   1. 打开IntelliJ IDEA，创建一个Maven工程。

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink1.png)

   2. 将这个Maven工程命名为FlinkTutorial。

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink2.png)

   3. 选定这个Maven工程所在存储路径，并点击Finish，Maven工程即创建成功。

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink3.png)

2. 添加项目依赖

   在项目的pom文件中，添加Flink的依赖，包括flink-java、flink-streaming-java，以及flink-clients（客户端，也可以省略）。

   ```xml
   <properties>
   	<flink.version>1.17.0</flink.version>
   </properties>
   
   <dependencies>
   	<dependency>
   		<groupId>org.apache.flink</groupId>
   		<artifactId>flink-streaming-java</artifactId>
   		<version>${flink.version}</version>
   	</dependency>
   
   	<dependency>
   		<groupId>org.apache.flink</groupId>
   		<artifactId>flink-clients</artifactId>
   		<version>${flink.version}</version>
   	</dependency>
   </dependencies>
   ```

### 2.2、WordCount代码编写

需求：统计一段文字中，每个单词出现的频次。

环境准备：在src/main/java目录下，新建一个包，命名为com.atguigu.wc。

#### 2.2.1、批处理

> **批处理基本思路：先逐行读入文件数据，然后将每一行文字拆分成单词；接着按照单词分组，统计每组数据的个数，就是对应单词的频次。**

1. 数据准备

   1. 在工程根目录下新建一个input文件夹，并在下面创建文本文件words.txt

   2. 在words.txt中输入一些文字，例如：

      ```shell
      hello flink
      hello world
      hello java
      ```

2. 代码编写

   1. 在com.atguigu.wc包下新建Java类BatchWordCount，在静态main方法中编写代码。具体代码实现如下：

      ```java
      import org.apache.flink.api.common.typeinfo.Types;
      import org.apache.flink.api.java.ExecutionEnvironment;
      import org.apache.flink.api.java.operators.AggregateOperator;
      import org.apache.flink.api.java.operators.DataSource;
      import org.apache.flink.api.java.operators.FlatMapOperator;
      import org.apache.flink.api.java.operators.UnsortedGrouping;
      import org.apache.flink.api.java.tuple.Tuple2;
      import org.apache.flink.util.Collector;
      
      public class BatchWordCount {
      
          public static void main(String[] args) throws Exception {
      
              // 1. 创建执行环境
              ExecutionEnvironment env = ExecutionEnvironment.getExecutionEnvironment();
              
              // 2. 从文件读取数据  按行读取(存储的元素就是每行的文本)
              DataSource<String> lineDS = env.readTextFile("input/words.txt");
              
              // 3. 转换数据格式
              FlatMapOperator<String, Tuple2<String, Long>> wordAndOne = lineDS.flatMap(new FlatMapFunction<String, Tuple2<String, Long>>() {
      
                  @Override
                  public void flatMap(String line, Collector<Tuple2<String, Long>> out) throws Exception {
      
                      String[] words = line.split(" ");
      
                      for (String word : words) {
                          out.collect(Tuple2.of(word,1L));
                      }
                  }
              });
      
              // 4. 按照 word 进行分组
              UnsortedGrouping<Tuple2<String, Long>> wordAndOneUG = wordAndOne.groupBy(0);
              
              // 5. 分组内聚合统计
              AggregateOperator<Tuple2<String, Long>> sum = wordAndOneUG.sum(1);
      
              // 6. 打印结果
              sum.print();
          }
      }
      ```

   2. 输出

      ```shell
      (flink,1)
      (world,1)
      (hello,3)
      (java,1)
      ```

   需要注意的是，这种代码的实现方式，是基于DataSet API的，也就是我们对数据的处理转换，是看作数据集来进行操作的。事实上Flink本身是流批统一的处理架构，批量的数据集本质上也是流，没有必要用两套不同的API来实现。所以从Flink 1.12开始，官方推荐的做法是直接使用DataStream API，在提交任务时通过将执行模式设为BATCH来进行批处理：

   ```shell
   $ bin/flink run -Dexecution.runtime-mode=BATCH BatchWordCount.jar
   ```

   这样，DataSet API就没什么用了，在实际应用中我们只要维护一套DataStream API就可以。这里只是为了方便大家理解，我们依然用DataSet API做了批处理的实现。

#### 2.2.2、流处理

对于Flink而言，流才是整个处理逻辑的底层核心，所以流批统一之后的DataStream API更加强大，可以直接处理批处理和流处理的所有场景。

下面我们就针对不同类型的输入数据源，用具体的代码来实现流处理。

1. 读取文件

   我们同样试图读取文档words.txt中的数据，并统计每个单词出现的频次。整体思路与之前的批处理非常类似，代码模式也基本一致。

   在com.atguigu.wc包下新建Java类StreamWordCount，在静态main方法中编写代码。具体代码实现如下：

   ```java
   import org.apache.flink.api.common.typeinfo.Types;
   import org.apache.flink.api.java.tuple.Tuple2;
   import org.apache.flink.streaming.api.datastream.DataStreamSource;
   import org.apache.flink.streaming.api.datastream.SingleOutputStreamOperator;
   import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
   import org.apache.flink.util.Collector;
   
   import java.util.Arrays;
   
   public class StreamWordCount {
   
       public static void main(String[] args) throws Exception {
       
           // 1. 创建流式执行环境
           StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
           
           // 2. 读取文件
           DataStreamSource<String> lineStream = env.readTextFile("input/words.txt");
           
           // 3. 转换、分组、求和，得到统计结果
           SingleOutputStreamOperator<Tuple2<String, Long>> sum = lineStream.flatMap(new FlatMapFunction<String, Tuple2<String, Long>>() {
               @Override
               public void flatMap(String line, Collector<Tuple2<String, Long>> out) throws Exception {
   
                   String[] words = line.split(" ");
   
                   for (String word : words) {
                       out.collect(Tuple2.of(word, 1L));
                   }
               }
           }).keyBy(data -> data.f0)
              .sum(1);
   
           // 4. 打印
           sum.print();
           
           // 5. 执行
           env.execute();
       }
   }
   ```

   输出：

   ```shell
   3> (java,1)
   5> (hello,1)
   5> (hello,2)
   5> (hello,3)
   13> (flink,1)
   9> (world,1)
   ```

   主要观察与批处理程序BatchWordCount的不同：

   - 创建执行环境的不同，流处理程序使用的是**StreamExecutionEnvironment**。
   - 转换处理之后，得到的数据对象类型不同。
   - 分组操作调用的是keyBy方法，可以传入一个匿名函数作为键选择器（KeySelector），指定当前分组的key是什么。
   - 代码末尾需要调用env的execute方法，开始执行任务。

2. 读取socket文本流

   在实际的生产环境中，真正的数据流其实是无界的，有开始却没有结束，这就要求我们需要持续地处理捕获的数据。为了模拟这种场景，可以监听socket端口，然后向该端口不断的发送数据。

   1. 将StreamWordCount代码中读取文件数据的readTextFile方法，替换成读取socket文本流的方法socketTextStream。具体代码实现如下：

      ```java
      import org.apache.flink.api.common.typeinfo.Types;
      import org.apache.flink.api.java.tuple.Tuple2;
      import org.apache.flink.streaming.api.datastream.DataStreamSource;
      import org.apache.flink.streaming.api.datastream.SingleOutputStreamOperator;
      import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
      import org.apache.flink.util.Collector;
      
      import java.util.Arrays;
      
      public class SocketStreamWordCount {
      
          public static void main(String[] args) throws Exception {
      
              // 1. 创建流式执行环境
              StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
              
              // 2. 读取文本流：hadoop102表示发送端主机名、7777表示端口号
              DataStreamSource<String> lineStream = env.socketTextStream("hadoop102", 7777);
              
              // 3. 转换、分组、求和，得到统计结果
              SingleOutputStreamOperator<Tuple2<String, Long>> sum = lineStream.flatMap((String line, Collector<Tuple2<String, Long>> out) -> {
                  String[] words = line.split(" ");
      
                  for (String word : words) {
                      out.collect(Tuple2.of(word, 1L));
                  }
              }).returns(Types.TUPLE(Types.STRING, Types.LONG))
                      .keyBy(data -> data.f0)
                      .sum(1);
      
              // 4. 打印
              sum.print();
              
              // 5. 执行
              env.execute();
          }
      }
      ```

   2. 在Linux环境的主机hadoop102上，执行下列命令，发送数据进行测试

      ```shell
      [atguigu@hadoop102 ~]$ nc -lk 7777
      ```

      **注意：要先启动端口，后启动StreamWordCount程序，否则会报超时连接异常。**

   3. 启动StreamWordCount程序

      我们会发现程序启动之后没有任何输出、也不会退出。这是正常的，因为Flink的流处理是事件驱动的，当前程序会一直处于监听状态，只有接收到数据才会执行任务、输出统计结果。

   4. 从hadoop102发送数据

      1. 在hadoop102主机中，输入“hello flink”，输出如下内容

         ```shell
         13> (flink,1)
         5> (hello,1)

      2. 再输入“hello world”，输出如下内容

         ```shell
         2> (world,1)
         5> (hello,2)
         ```

      **说明：**

      Flink还具有一个类型提取系统，可以分析函数的输入和返回类型，自动获取类型信息，从而获得对应的序列化器和反序列化器。但是，由于Java中泛型擦除的存在，在某些特殊情况下（比如Lambda表达式中），自动提取的信息是不够精细的——只告诉Flink当前的元素由“船头、船身、船尾”构成，根本无法重建出“大船”的模样；这时就需要显式地提供类型信息，才能使应用程序正常工作或提高其性能。

      因为对于flatMap里传入的Lambda表达式，系统只能推断出返回的是Tuple2类型，而无法得到Tuple2<String, Long>。只有显式地告诉系统当前的返回类型，才能正确地解析出完整数据。

## 3、Flink部署

### 3.1、集群角色

![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230810-112944.png)

**Flink提供作业和执行任务，需要几个关键组件：**

- **客户端（Client）**：代码由客户端**获取**并做**转换**，之后**提交**给JobManager
- **JobManager**：就是Flink集群里的"**管事人**"，对作业进行中央调度；而它获取到要执行的作业后，会**进一步处理转换**，然后分发任务给众多的TaskManager
- **TaskManager**：就是真正"**干活的人**"，**数据的处理操作**都是它们来做的。

注意：Flink是一个非常灵活的处理框架，它支持多种不同的部署场景，还可以和不同的资源管理平台方便地集成。所以接下来我们会先做一个简单的介绍，让大家有一个初步的认识，之后再展开讲述不同情形下的Flink部署。

### 3.2、Flink集群搭建

#### 3.2.1、集群启动

1. 集群规划

   | 节点服务器 | hadoop102                     | Hadoop103   | Hadoop104   |
   | ---------- | ----------------------------- | ----------- | ----------- |
   | 角色       | **JobManager**<br>TaskManager | TaskManager | TaskManager |

2. 下载并解压安装包

   1. 下载安装包flink-1.17.0-bin-scala_2.12.tgz，将该jar包上传到**hadoop102节点服务器**的`/opt/software`路径上。

   2. 在`/opt/software`路径上解压flink-1.17.0-bin-scala_2.12.tgz到`/opt/module`路径上。

      ```shell
      [atguigu@hadoop102 software]$ tar -zxvf flink-1.17.0-bin-scala_2.12.tgz -C /opt/module/
      ```

3. 修改集群配置

   1. 进入conf路径，修改flink-conf.yaml文件，指定hadoop102节点服务器为JobManager 

      ```shell
      [atguigu@hadoop102 conf]$ vim flink-conf.yaml
      ```

      修改如下内容：

      ```shell
      # JobManager节点地址.
      jobmanager.rpc.address: hadoop102
      jobmanager.bind-host: 0.0.0.0
      rest.address: hadoop102
      rest.bind-address: 0.0.0.0
      # TaskManager节点地址.需要配置为当前机器名
      taskmanager.bind-host: 0.0.0.0
      taskmanager.host: hadoop102
      ```

   2. 修改workers文件，指定hadoop102、hadoop103和hadoop104为TaskManager

      ```shell
      [atguigu@hadoop102 conf]$ vim workers
      ```

      修改如下内容：

      ```shell
      hadoop102
      hadoop103
      hadoop104
      ```

   3. 修改masters文件

      ```shell
      [atguigu@hadoop102 conf]$ vim masters
      ```

      修改如下内容：

      ```shell
      hadoop102:8081
      ```

   4. 另外，在flink-conf.yaml文件中还可以对集群中的JobManager和TaskManager组件进行优化配置，主要配置项如下：

      - **jobmanager.memory.process.size**：对JobManager进程可使用到的全部内存进行配置，包括JVM元空间和其他开销，默认为**1600M**，可以根据集群规模进行适当调整。
      - **taskmanager.memory.process.size**：对TaskManager进程可使用到的全部内存进行配置，包括JVM元空间和其他开销，默认为**1728M**，可以根据集群规模进行适当调整。
      - **taskmanager.numberOfTaskSlots**：对每个TaskManager能够分配的Slot数量进行配置，**默认为1**，可根据TaskManager所在的机器能够提供给Flink的CPU数量决定。所谓Slot就是TaskManager中具体运行一个任务所分配的计算资源。
      - **parallelism.default**：Flink任务执行的并行度，**默认为1**。优先级低于代码中进行的并行度配置和任务提交时使用参数指定的并行度数量。

4. 分发安装目录

   1. 配置修改完毕后，将Flink安装目录发给另外两个节点服务器。

      ```shell
      [atguigu@hadoop102 module]$ xsync flink-1.17.0/
      ```

   2. 修改hadoop103的 taskmanager.host

      ```shell
      [atguigu@hadoop103 conf]$ vim flink-conf.yaml
      ```

      修改如下内容：

      ```shell
      # TaskManager节点地址.需要配置为当前机器名
      taskmanager.host: hadoop103
      ```

   3. 修改hadoop104的 taskmanager.host

      ```shell
      [atguigu@hadoop104 conf]$ vim flink-conf.yaml
      ```

      修改如下内容：

      ```shell
      # TaskManager节点地址.需要配置为当前机器名
      taskmanager.host: hadoop104
      ```

5. 启动集群

   1. 在hadoop102节点服务器上执行start-cluster.sh启动Flink集群：

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ bin/start-cluster.sh
      ```

   2. 查看进程情况：

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ jpsall 
      =============== hadoop102 ===============
      4453 StandaloneSessionClusterEntrypoint
      4458 TaskManagerRunner
      4533 Jps
      =============== hadoop103 ===============
      2872 TaskManagerRunner
      2941 Jps
      =============== hadoop104 ===============
      2948 Jps
      2876 TaskManagerRunner
      ```

6. 访问WebUI

   启动成功后，同样可以访问http://hadoop102:8081对flink集群和任务进行监控管理。

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink4.png)

   这里可以明显看到，当前集群的TaskManager数量为3；由于默认每个TaskManager的Slot数量为1，所以总Slot数和可用Slot数都为3。

#### 3.2.2、向集群提交作业

1. 环境准备

   在hadoop102中执行以下命令启动netcat。

   ```shell
   [atguigu@hadoop102 flink-1.17.0]$ nc -lk 7777
   ```

2. 程序打包

   1. 在我们编写的Flink入门程序的pom.xml文件中添加打包插件的配置，具体如下：

      ```xml
      <build>
          <plugins>
              <plugin>
                  <groupId>org.apache.maven.plugins</groupId>
                  <artifactId>maven-shade-plugin</artifactId>
                  <version>3.2.4</version>
                  <executions>
                      <execution>
                          <phase>package</phase>
                          <goals>
                              <goal>shade</goal>
                          </goals>
                          <configuration>
                              <artifactSet>
                                  <excludes>
                                      <exclude>com.google.code.findbugs:jsr305</exclude>
                                      <exclude>org.slf4j:*</exclude>
                                      <exclude>log4j:*</exclude>
                                  </excludes>
                              </artifactSet>
                              <filters>
                                  <filter>
                                      <!-- Do not copy the signatures in the META-INF folder.
                                      Otherwise, this might cause SecurityExceptions when using the JAR. -->
                                      <artifact>*:*</artifact>
                                      <excludes>
                                          <exclude>META-INF/*.SF</exclude>
                                          <exclude>META-INF/*.DSA</exclude>
                                          <exclude>META-INF/*.RSA</exclude>
                                      </excludes>
                                  </filter>
                              </filters>
                              <transformers combine.children="append">
                                  <transformer
                                          implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
                                  </transformer>
                              </transformers>
                          </configuration>
                      </execution>
                  </executions>
              </plugin>
          </plugins>
      </build>
      ```

   2. 插件配置完毕后，可以使用IDEA的Maven工具执行package命令，出现如下提示即表示打包成功。

      ```shell
      -------------------------------------------------------------------
      [INFO] BUILD SUCCESS
      -------------------------------------------------------------------
      ```

      打包完成后，在target目录下即可找到所需JAR包，JAR包会有两个，FlinkTutorial-1.0-SNAPSHOT.jar和FlinkTutorial-1.0-SNAPSHOT-jar-with-dependencies.jar，因为集群中已经具备任务运行所需的所有依赖，所以**建议使用FlinkTutorial-1.0-SNAPSHOT.jar**。

3. 在WebUI上提交作业

   1. 任务打包完成后，我们打开Flink的WEB UI页面，在右侧导航栏点击“Submit New Job”，然后点击按钮“+ Add New”，选择要上传运行的JAR包，如下图所示。

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink7.png)

   2. 点击该JAR包，出现任务配置页面，进行相应配置。

      主要配置**程序入口主类的全类名，任务运行的并行度**，任务运行所需的配置参数和保存点路径等，如下图所示，配置完成后，即可点击按钮“Submit”，将任务提交到集群运行。

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink8.png)

   3. 任务提交成功之后，可点击左侧导航栏的“Running Jobs”查看程序运行列表情况。

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink9.png)

   4. 测试

      1. 在socket端口中输入hello

         ```shell
         [atguigu@hadoop102 flink-1.17.0]$ nc -lk 7777
         hello
         ```

      2. 先点击Task Manager，然后点击右侧的192.168.10.104服务器节点

         ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink10.png)

      3. 点击Stdout，就可以看到hello单词的统计

         ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink11.png)

         **注意：如果hadoop104节点没有统计单词数据，可以去其他TaskManager节点查看。**

      4. 点击该任务，可以查看任务运行的具体情况，也可以通过点击“Cancel Job”结束任务运行。

         ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink12.png)

4. 命令行提交作业

   除了通过WEB UI界面提交任务之外，也可以直接通过命令行来提交任务。这里为方便起见，我们可以先把jar包直接上传到目录flink-1.17.0下

   1. 首先需要启动集群。

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ bin/start-cluster.sh
      ```

   2. 在hadoop102中执行以下命令启动netcat。

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ nc -lk 7777
      ```

   3. 将flink程序运行jar包上传到`/opt/module/flink-1.17.0`路径。

   4. 进入到flink的安装路径下，在命令行使用flink run命令提交作业。

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ bin/flink run -m hadoop102:8081 -c com.atguigu.wc.SocketStreamWordCount ./FlinkTutorial-1.0-SNAPSHOT.jar
      ```

      这里的参数 -m指定了提交到的JobManager，-c指定了入口类。

   5. 在浏览器中打开Web UI，[http://hadoop102:8081查看应用执行情况](http://hadoop102:8081查看应用执行情况，)。

      用netcat输入数据，可以在TaskManager的标准输出（Stdout）看到对应的统计结果。

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink13.png)

   6. 在`/opt/module/flink-1.17.0/log`路径中，可以查看TaskManager节点。

      ```shell
      [atguigu@hadoop102 log]$ cat flink-atguigu-standalonesession-0-hadoop102.out
      
      (hello,1)
      (hello,2)
      (flink,1)
      (hello,3)
      (scala,1)
      ```


### 3.3、部署模式

在一些应用场景中，对于集群资源分配和占用的方式，可能会有特定的需求。Flink为各种场景提供了不同的部署模式，主要有以下三种：**会话模式**（Session Mode）、**单作业模式**（Per-Job Mode）、**应用模式**（Application Mode）。

它们的区别主要在于：集群的**生命周期**以及**资源的分配方式**；以及应用的**main方法到底在哪里执行**——客户端（Client）还是JobManager。

#### 3.3.1、会话模式（Session Mode）

会话模式其实最符合常规思维。我们需要先启动一个集群，保持一个会话，在这个会话中通过客户端提交作业。集群启动时所有资源就都已经确定，所以所有提交的作业会竞争集群中的资源。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230815-131250.png)

会话模式比较适合于单个规模小、执行时间短的大量作业。

#### 3.3.2、单作业模式（Per-Job Mode）

会话模式因为资源共享会导致很多问题，所以为了更好地隔离资源，我们可以考虑为每个提交的作业启动一个集群，这就是所谓的单作业（Per-Job）模式。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230815-131723.png)

作业完成后，集群就会关闭，所有资源也会释放。

这些特性使得单作业模式在生产环境运行更加稳定，所以是实际应用的首选模式。

需要注意的是，Flink本身无法直接运行，所以单作业模式一般需要借助一些资源管理框架来启动集群，比如YARN、Kubernetes（K8S）。

#### 3.3.3、应用模式（Application Mode）

**前面提到的两种模式下，应用代码都是客户端上执行**，然后由客户端提交给JobManager的。但是这种方式客户端需要占用大量网络带宽，去下载依赖和把二进制数据发送给JobManager；加上很多情况下我们提交作业用的是同一个客户端，**就会加重客户端所在节点的资源消耗**。

所以解决办法就是，我们**不要客户端了，直接把应用提交到JobManager上运行**。而这也就代表着，我们需要为每一个提交的应用单独启动一个JobManager，也就是创建一个集群。**这个JobManager只为执行这一个应用而存在，执行结束之后JobManager也就关闭了**，这就是所谓的**应用模式**。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230815-132428.png)

应用模式与单作业模式，都是提交作业之后才创建集群；单作业模式是通过客户端来提交的，客户端解析出的每一个作业对应一个集群；而**应用模式下，是直接由JobManager执行应用程序的。**

**这里我们所讲到的部署模式，相对是比较抽象的概念。实际应用时，一般需要和资源管理平台结合起来，选择特定的模式来分配资源、部署应用。接下来，我们就针对不同的资源提供者的场景，具体介绍Flink的部署方式。**

### 3.4、Standalone运行模式（了解）

独立模式是独立运行的，不依赖任何外部的资源管理平台；当然独立也是有代价的：如果**资源不足，或者出现故障，没有自动扩展或重分配资源的保证，必须手动处理**。所以独立模式一般**只用在开发测试或作业非常少的场景下**。

#### 3.4.1、会话模式部署

我们在第3.2节用的就是Standalone集群的会话模式部署。

提前启动集群，并通过Web页面客户端提交任务（可以多个任务，但是集群资源固定）。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230815-132620.png)

#### 3.4.2、单作业模式部署

**Flink的Standalone集群并不支持单作业模式部署**。因为单作业模式需要借助一些资源管理平台。

#### 3.4.3、应用模式部署

**应用模式下不会提前创建集群，所以不能调用start-cluster.sh脚本**。我们可以使用同样在bin目录下的standalone-job.sh来创建一个JobManager。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/WX20230815-132428.png)

具体步骤如下：

1. 环境准备。在hadoop102中执行以下命令启动netcat。

   ```shell
   [atguigu@hadoop102 flink-1.17.0]$ nc -lk 7777
   ```

2. 进入到Flink的安装路径下，将应用程序的jar包放到lib/目录下。

   ```shell
   [atguigu@hadoop102 flink-1.17.0]$ mv FlinkTutorial-1.0-SNAPSHOT.jar lib/
   ```

3. 执行以下命令，启动JobManager。

   ```shell
   [atguigu@hadoop102 flink-1.17.0]$ bin/standalone-job.sh start --job-classname com.atguigu.wc.SocketStreamWordCount
   ```

   这里我们直接指定作业入口类，脚本会到lib目录扫描所有的jar包。

4. 同样是使用bin目录下的脚本，启动TaskManager。

   ```shell
   [atguigu@hadoop102 flink-1.17.0]$ bin/taskmanager.sh start
   ```

5. 在hadoop102上模拟发送单词数据。

   ```shell
   [atguigu@hadoop102 ~]$ nc -lk 7777
   hello
   ```

6. 在hadoop102:8081地址中观察输出数据

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink15.png)

7. 如果希望停掉集群，同样可以使用脚本，命令如下。

   ```shell
   [atguigu@hadoop102 flink-1.17.0]$ bin/taskmanager.sh stop
   [atguigu@hadoop102 flink-1.17.0]$ bin/standalone-job.sh stop
   ```

### 3.5、YARN运行模式（重点）

YARN上部署的过程是：客户端把Flink应用提交给Yarn的ResourceManager，Yarn的ResourceManager会向Yarn的NodeManager申请容器。在这些容器上，Flink会部署JobManager和TaskManager的实例，从而启动集群。Flink会根据运行在JobManger上的作业所需要的Slot数量动态分配TaskManager资源。

#### 3.5.1、相关准备和配置

在将Flink任务部署至YARN集群之前，需要确认集群是否安装有Hadoop，保证Hadoop版本至少在2.2以上，并且集群中安装有HDFS服务。

具体配置步骤如下：

1. 配置环境变量，增加环境变量配置如下：

   ```shell
   $ sudo vim /etc/profile.d/my_env.sh
   
   HADOOP_HOME=/opt/module/hadoop-3.3.4
   export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
   export HADOOP_CONF_DIR=${HADOOP_HOME}/etc/hadoop
   export HADOOP_CLASSPATH=`hadoop classpath`
   ```

2. 启动Hadoop集群，包括HDFS和YARN。

   ```shell
   [atguigu@hadoop102 hadoop-3.3.4]$ start-dfs.sh
   [atguigu@hadoop103 hadoop-3.3.4]$ start-yarn.sh
   ```

3. 在hadoop102中执行以下命令启动netcat。

   ```shell
   [atguigu@hadoop102 flink-1.17.0]$ nc -lk 7777
   ```

#### 3.5.2、会话模式部署

YARN的会话模式与独立集群略有不同，需要首先申请一个YARN会话（YARN Session）来启动Flink集群。具体步骤如下：

1. 启动集群

   1. 启动Hadoop集群（HDFS、YARN）。

   2. 执行脚本命令向YARN集群申请资源，开启一个YARN会话，启动Flink集群。

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ bin/yarn-session.sh -nm test
      ```

   可用参数解读：

   - -d：分离模式，如果你不想让Flink YARN客户端一直前台运行，可以使用这个参数，即使关掉当前对话窗口，YARN session也可以后台运行。
   - -jm（--jobManagerMemory）：配置JobManager所需内存，默认单位MB。
   - -nm（--name）：配置在YARN UI界面上显示的任务名。
   - -qu（--queue）：指定YARN队列名。
   - -tm（--taskManager）：配置每个TaskManager所使用内存。

   注意：Flink1.11.0版本不再使用-n参数和-s参数分别指定TaskManager数量和slot数量，YARN会按照需求动态分配TaskManager和slot。所以从这个意义上讲，YARN的会话模式也不会把集群资源固定，同样是动态分配的。

   YARN Session启动之后会给出一个Web UI地址以及一个YARN application ID，如下所示，用户可以通过Web UI或者命令行两种方式提交作业。

   ```shell
   2022-11-17 15:20:52,711 INFO  org.apache.flink.yarn.YarnClusterDescriptor                  [] - Found Web Interface hadoop104:40825 of application 'application_1668668287070_0005'.
   JobManager Web Interface: http://hadoop104:40825
   ```

2. 提交作业

   1. 通过Web UI提交作业

      这种方式比较简单，与上文所述Standalone部署模式基本相同。

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink16.png)

   2. 通过命令行提交作业

      1. 将FlinkTutorial-1.0-SNAPSHOT.jar任务上传至集群。

      2. 执行以下命令将该任务提交到已经开启的Yarn-Session中运行。

         ```shell
         [atguigu@hadoop102 flink-1.17.0]$ bin/flink run
         -c com.atguigu.wc.SocketStreamWordCount FlinkTutorial-1.0-SNAPSHOT.jar
         ```

         客户端可以自行确定JobManager的地址，也可以通过-m或者-jobmanager参数指定JobManager的地址，JobManager的地址在YARN Session的启动页面中可以找到。

      3. 任务提交成功后，可在YARN的Web UI界面查看运行情况。hadoop103:8088。

         ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink17.png)

         从上图中可以看到我们创建的Yarn-Session实际上是一个Yarn的Application，并且有唯一的Application ID。

      4. 也可以通过Flink的Web UI页面查看提交任务的运行情况，如下图所示。

         ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink18.png)

   #### 3.5.3、单作业模式部署

   在YARN环境中，由于有了外部平台做资源调度，所以我们也可以直接向YARN提交一个单独的作业，从而启动一个Flink集群。

1. 执行命令提交作业

   ```shell
   [atguigu@hadoop102 flink-1.17.0]$ bin/flink run -d -t yarn-per-job -c com.atguigu.wc.SocketStreamWordCount FlinkTutorial-1.0-SNAPSHOT.jar
   ```

   注意：如果启动过程中报如下异常。

   ```shell
   Exception in thread “Thread-5” java.lang.IllegalStateException: Trying to access closed classloader. Please check if you store classloaders directly or indirectly in static fields. If the stacktrace suggests that the leak occurs in a third party library and cannot be fixed immediately, you can disable this check with the configuration ‘classloader.check-leaked-classloader’.
   at org.apache.flink.runtime.execution.librarycache.FlinkUserCodeClassLoaders
   ```

   解决办法：在flink的/opt/module/flink-1.17.0/conf/flink-conf.yaml配置文件中设置

   ```shell
   [atguigu@hadoop102 conf]$ vim flink-conf.yaml
   
   classloader.check-leaked-classloader: false
   ```

2. 在YARN的ResourceManager界面查看执行情况

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink19.png)

   点击可以打开Flink Web UI页面进行监控，如下图所示：

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink20.png)

3. 可以使用命令行查看或取消作业，命令如下

   ```shell
   [atguigu@hadoop102 flink-1.17.0]$ bin/flink list -t yarn-per-job -Dyarn.application.id=application_XXXX_YY
   
   [atguigu@hadoop102 flink-1.17.0]$ bin/flink cancel -t yarn-per-job -Dyarn.application.id=application_XXXX_YY <jobId>
   ```

   这里的`application_XXXX_YY`是当前应用的ID，`<jobId>`是作业的ID。注意如果取消作业，整个Flink集群也会停掉。

#### 3.5.4、应用模式部署

应用模式同样非常简单，与单作业模式类似，直接执行flink run-application命令即可。

1. 命令行提交

   1. 执行命令提交作业。

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ bin/flink run-application -t yarn-application -c com.atguigu.wc.SocketStreamWordCount FlinkTutorial-1.0-SNAPSHOT.jar 
      ```

   2. 在命令行中查看或取消作业。

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ bin/flink list -t yarn-application -Dyarn.application.id=application_XXXX_YY
      
      [atguigu@hadoop102 flink-1.17.0]$ bin/flink cancel -t yarn-application -Dyarn.application.id=application_XXXX_YY <jobId>
      ```

2. 上传HDFS提交

   可以通过yarn.provided.lib.dirs配置选项指定位置，将flink的依赖上传到远程。

   1. 上传flink的lib和plugins到HDFS上

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ hadoop fs -mkdir /flink-dist
      [atguigu@hadoop102 flink-1.17.0]$ hadoop fs -put lib/ /flink-dist
      [atguigu@hadoop102 flink-1.17.0]$ hadoop fs -put plugins/ /flink-dist
      ```

   2. 上传自己的jar包到HDFS

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ hadoop fs -mkdir /flink-jars
      [atguigu@hadoop102 flink-1.17.0]$ hadoop fs -put FlinkTutorial-1.0-SNAPSHOT.jar /flink-jars
      ```

   3. 提交作业

      ```shell
      [atguigu@hadoop102 flink-1.17.0]$ bin/flink run-application -t yarn-application	-Dyarn.provided.lib.dirs="hdfs://hadoop102:8020/flink-dist"	-c com.atguigu.wc.SocketStreamWordCount  hdfs://hadoop102:8020/flink-jars/FlinkTutorial-1.0-SNAPSHOT.jar
      ```

   这种方式下，flink本身的依赖和用户jar可以预先上传到HDFS，而不需要单独发送到集群，这就使得作业提交更加轻量了。

### 3.6、K8S运行模式（了解）

容器化部署是如今业界流行的一项技术，基于Docker镜像运行能够让用户更加方便地对应用进行管理和运维。容器管理工具中最为流行的就是Kubernetes（k8s），而Flink也在最近的版本中支持了k8s部署模式。基本原理与YARN是类似的，具体配置可以参见官网说明，这里我们就不做过多讲解了。

### 3.7、历史服务器

运行 Flink job 的集群一旦停止，只能去 yarn 或本地磁盘上查看日志，不再可以查看作业挂掉之前的运行的 Web UI，很难清楚知道作业在挂的那一刻到底发生了什么。如果我们还没有 Metrics 监控的话，那么完全就只能通过日志去分析和定位问题了，所以如果能还原之前的 Web UI，我们可以通过 UI 发现和定位一些问题。

Flink提供了历史服务器，用来在相应的 Flink 集群关闭后查询已完成作业的统计信息。我们都知道只有当作业处于运行中的状态，才能够查看到相关的WebUI统计信息。通过 History Server 我们才能查询这些已完成作业的统计信息，无论是正常退出还是异常退出。

此外，它对外提供了 REST API，它接受 HTTP 请求并使用 JSON 数据进行响应。Flink 任务停止后，JobManager 会将已经完成任务的统计信息进行存档，History Server 进程则在任务停止后可以对任务统计信息进行查询。比如：最后一次的 Checkpoint、任务运行时的相关配置。

1. 创建存储目录

   ```shell
   hadoop fs -mkdir -p /logs/flink-job
   ```

2. 在`flink-config-yaml`中添加如下配置

   ```shell
   jobmanager.archive.fs.dir: hdfs://hadoop102:8020/logs/flink-job
   historyserver.web.address: hadoop102
   historyserver.web.port: 8082
   historyserver.archive.fs.dir: hdfs://hadoop102:8020/logs/flink-job
   historyserver.archive.fs.refresh-interval: 5000
   ```

3. 启动历史服务器

   ```shell
   bin/historyserver.sh start
   ```

4. 停止历史服务器

   ```shell
   bin/historyserver.sh stop
   ```

5. 在浏览器地址栏输入：http://hadoop102:8082 查看已经停止的job的统计信息

## 4、Flink运行时架构

### 4.1、系统架构

![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink21.png)

1. 作业管理器（JobManager）

   JobManager是一个Flink集群中任务管理和调度的核心，是控制应用执行的主进程。也就是说，每个应用都应该被唯一的JobManager所控制执行。

   JobManger又包含3个不同的组件。

   1. JobMaster

      JobMaster是JobManager中最核心的组件，**负责处理单独的作业（Job）**。所以JobMaster和具体的Job是一一对应的，多个Job可以同时运行在一个Flink集群中, 每个Job都有一个自己的JobMaster。需要注意在早期版本的Flink中，没有JobMaster的概念；而JobManager的概念范围较小，实际指的就是现在所说的JobMaster。

      在作业提交时，JobMaster会先接收到要执行的应用。JobMaster会把JobGraph转换成一个物理层面的数据流图，这个图被叫作“执行图”（ExecutionGraph），它包含了所有可以并发执行的任务。JobMaster会向资源管理器（ResourceManager）发出请求，申请执行任务必要的资源。一旦它获取到了足够的资源，就会将执行图分发到真正运行它们的TaskManager上。

      而在运行过程中，JobMaster会负责所有需要中央协调的操作，比如说检查点（checkpoints）的协调。

   2. 资源管理器（Resource Manager）

      ResourceManager主要**负责资源的分配和管理**，在Flink 集群中只有一个。所谓“资源”，主要是指TaskManager的任务槽（task slots）。任务槽就是Flink集群中的资源调配单元，包含了机器用来执行计算的一组CPU和内存资源。每一个任务（Task）都需要分配到一个slot上执行。

      这里注意要把Flink内置的ResourceManager和其他资源管理平台（比如YARN）的ResourceManager区分开。

   3. 分发器（Dispatcher）

      Dispatcher主要负责提供一个REST接口，**用来提交应用，并且负责为每一个新提交的作业启动一个新的JobMaster 组件**。Dispatcher也会启动一个Web UI，用来方便地展示和监控作业执行的信息。Dispatcher在架构中并不是必需的，在不同的部署模式下可能会被忽略掉。

2. 任务管理器（TaskManager）

   TaskManager是Flink中的工作进程，数据流的具体计算就是它来做的。Flink集群中必须至少有一个TaskManager；每一个TaskManager都包含了一定数量的任务槽（task slots）。Slot是资源调度的最小单位，slot的数量限制了TaskManager能够并行处理的任务数量。

   启动之后，TaskManager会向资源管理器注册它的slots；收到资源管理器的指令后，TaskManager就会将一个或者多个槽位提供给JobMaster调用，JobMaster就可以分配任务来执行了。

   在执行过程中，TaskManager可以缓冲数据，还可以跟其他运行同一应用的TaskManager交换数据。

### 4.2、核心概念

#### 4.2.1、并行度（Parallelism）

1. 并行子任务和并行度

   当要处理的数据量非常大时，我们可以把一个算子操作，“复制”多份到多个节点，数据来了之后就可以到其中任意一个执行。这样一来，一个算子任务就被拆分成了多个并行的“子任务”（subtasks），再将它们分发到不同节点，就真正实现了并行计算。

   在Flink执行过程中，每一个算子（operator）可以包含一个或多个子任务（operator subtask），这些子任务在不同的线程、不同的物理机或不同的容器中完全独立地执行。

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink22.png)

   一个特定算子的**子任务（subtask）的个数**被称之为其**并行度**（parallelism）。这样，包含并行子任务的数据流，就是**并行数据流**，它需要多个分区（stream partition）来分配并行任务。一般情况下，**一个流程序的并行度**，可以认为就**是其所有算子中最大的并行度**。一个程序中，不同的算子可能具有不同的并行度。

   例如：如上图所示，当前数据流中有source、map、window、sink四个算子，其中sink算子的并行度为1，其他算子的并行度都为2。所以这段流处理程序的并行度就是2。

2. 并行度的设置

   在Flink中，可以用不同的方法来设置并行度，它们的有效范围和优先级别也是不同的。

   1. 代码中设置

      我们在代码中，可以很简单地在算子后跟着调用setParallelism()方法，来设置当前算子的并行度：

      ```shell
      stream.map(word -> Tuple2.of(word, 1L)).setParallelism(2);
      ```

      这种方式设置的并行度，只针对当前算子有效。

      另外，我们也可以直接调用执行环境的setParallelism()方法，全局设定并行度：

      ```shell
      env.setParallelism(2);
      ```

      这样代码中所有算子，默认的并行度就都为2了。我们一般不会在程序中设置全局并行度，因为如果在程序中对全局并行度进行硬编码，会导致无法动态扩容。

      这里要注意的是，由于keyBy不是算子，所以无法对keyBy设置并行度。

   2. 提交应用时设置

      在使用flink run命令提交应用时，可以增加-p参数来指定当前应用程序执行的并行度，它的作用类似于执行环境的全局设置：

      ```shell
      bin/flink run –p 2 –c com.atguigu.wc.SocketStreamWordCount 
      ./FlinkTutorial-1.0-SNAPSHOT.jar
      ```

      如果我们直接在Web UI上提交作业，也可以在对应输入框中直接添加并行度。

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/flink23.png)

   3. 配置文件中设置

      我们还可以直接在集群的配置文件flink-conf.yaml中直接更改默认并行度：

      ```shell
      parallelism.default: 2
      ```

      这个设置对于整个集群上提交的所有作业有效，初始值为1。无论在代码中设置、还是提交时的-p参数，都不是必须的；所以在没有指定并行度的时候，就会采用配置文件中的集群默认并行度。在开发环境中，没有配置文件，默认并行度就是当前机器的CPU核心数。