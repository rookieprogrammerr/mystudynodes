## 1、大数据的概念

### 1.1、大数据的概念

- 大数据(Big Data)：指无法在一定时间范围内用常规软件工具进行捕捉、管理和处理的数据集合，是需要新处理模式才能具有更强的决策力、洞察发现力和流程优化能力的海量、高增长率和多样化的信息资产
- 大数据主要解决，海量数据的采集、存储和分析计算问题
- 按顺序给出数据存储单位: bit、 Byte、KB、MB、GB、TB、PB、EB、ZB、YB、BB、NB、DB。
- 1Byte = 8bit 1K =1024Byte 1MB =102K
- 1G =1024M 1T = 1024G1P = 1024T

### 1.2、大数据特点(4V)

1. Volume(大量)

   - 截至目前，人类生产的所有**印刷材料的数据量是200PB**，而历史上全人类总共**说过的话的数据量大约是5EB**。当前，典型个人计算机硬盘的容量为TB量级，而**一些大企业的数据量已经接近EB量级**

2. Velocity(高速)

   - 这是大数据区分于传统数据挖掘的最显著特征。根据IDC的“数字宇宙”的报告，预计到2025年，全球数据使用量将达到163ZB。在如此海量的数据面前，处理数据的效率就是企业的生命。

   - 天猫双十一
     - 2017年3分01秒，天猫交易额超过100亿
     - 2020年96秒，天猫交易额超过100亿

3. Varuety(多样)

   - 这种类型的多样性也让数据被分为结构化数据和非结构化数据。相对于以往便于存储的以数据库/文本为主的结构化数据，非结构化数据越来越多，包括网络日志、音频、视频、图片、地理位置信息等，这些多类型的数据对数据的处理能力提出了更高要求。

4. Value(低价值密度)

   - 价值密度的高低与数据总量的大小成反比。
   - 如何快速对有价值数据“提纯”成为目前大数据背景下待解决的难题

## 2、Hadoop概述

### 2.1、Hadoop是什么

1. Hadoop是一个由Apache基金会所开发的**分布式系统基础架构**
2. 主要解决，海量数据的**存储**和海量数据的**分析计算**问题
3. 广义上来说，Hadoop通常是指一个更广泛的概念 —— **Hadoop生态圈**

### 2.2、Hadoop发展历史

1. Hadoop创始人Doug Cuting，为了实现与Google类似的全文搜索功能，他在Lucene框架基础上进行优化升级，查询引擎和索引引擎。
2. 2001年年底Lucene成为Apache基金会的一个子项目。
3. 对于海量数据的场景，Lucene框架面对与Google同样的困难，存储海量数据困难，检索海量速度慢。
4. 学习和模仿Google解决这些问题的办法:微型版Nutch。
5. 可以说Google是Hadoop的思想之源 (Google在大数据方面的三篇论文)
   - GFS --->HDFS
   - Map-Reduce--->MR
   - BigTable--->HBase
6. 2003-2004年，Google公开了部分GFS和MapReduce思想的细节，以此为基础Doug Cutting等人用了2年业余时间实现了DFS和MapReduce机制，使Nutch性能飙升。
7. 2005年Hadoop 作为 Lucene的子项目Nutch的一部分正式引入Apache基金会。
8. 2006年3 月份，Map-Reduce和Nutch Distributed File System (NDFS)分别被纳入到Hadoop 项目中，Hadoop就此正式诞生，标志着大数据时代来临。
9. 名字来源于Doug Cutting儿子的玩具大象。

### 2.3、Hadoop三大发行版本

- Hadoop 三大发行版本: Apache、Cloudera、Hortonworks。
- Apache 版本最原始(最基础) 的版本，对于入门学习最好。（2006年）
- Cloudera 内部集成了很多大数据框架，对应产品 CDH。（2008年）
- Hortonworks 文档较好，对应产品HDP。
- Hortonworks 现在已经被 Cloudera 公司收购，推出新的品牌 CDP。

1. Apache Hadoop

   - [官网地址](http://hadoop.apache.org)
   - [下载地址](https://hadoop.apache.org/releases.html)

2. Cloudera Hadoop

   - [官网地址](https://www.cloudera.com/downloads.cdh)
   - [下载地址](https://docs.cloudera.com/documentation/enterprise/6/release-notes/topics/rg_cdh_6_download.html)

   1. 2008年成立的Cloudera是最早将Hadoop商用的公司，为合作伙伴提供Hadoop 的商用解决方案，主要是包括支持、咨询服务、培训。
   2. 2009年 Hadoop 的创始人 Doug Cutting 也加盟Cloudera公司。Cloudera产品主要为CDH，Cloudera Manager，Cloudera Support。
   3. CDH是Cloudera的 Hadoop发行版，完全开源，比 Apache Hadoop在兼容性，安全性，稳定性上有所增强。Cloudera 的标价为每年每个节点10000美元。
   4. Cloudera Manager是集群的软件分发及管理监控平台，可以在几个小时内部署好一个Hadoop集群，并对集群的节点及服务进行实时监控。

3. Hortonworks Hadoop

   - [官网地址](https://hortonworks.com/products/data-center/hdp)
   - [下载地址](https://hortonworks.com/downloads/#data-platform)

   1. 2011年成立的Hortonworks是雅虎与硅谷风投公司Benchmark Capital合资组建。
   2. 公司成立之初就吸纳了大约25名至30名专门研究 Hadoop的雅虎工程师，上述工程师均在2005年开始协助雅虎开发Hadoop，贡献了Hadoop80%的代码。
   3. Hortonworks的主打产品是Hortonworks Data Platform (HDP），也同样是100%开源的产品，HDP除常见的项目外还包括了Ambari，一款开源的安装和管理系统。
   4. 2018年 Hortonworks目前已经被Cloudera 公司收购。

### 2.4、Hadoop的优势

1. 高可靠性：Hadoop底层维护多个数据副本，所以即使Hadoop某个计算元素或存储出现故障，也不会导致数据的丢失。
2. 高扩展性：在集群见分配任务数据，可方便的扩展数以千计的节点。
3. 高效性：在MapReduce的思想下，Hadoop是并行工作的，以加快任务处理速度。
4. 高容错性：能够自动将失败的任务重新分配。

### 2.5、Hadoop组成

![](https://zc-node.oss-cn-beijing.aliyuncs.com/QQ%E6%88%AA%E5%9B%BE20230212142041.png)

#### 2.5.1、HDFS架构概述

> HDFS（Hadoop Distributed File System）是一个分布式文件系统

![](https://img-blog.csdnimg.cn/97ea394f4c8a416db067876794545eef.png)

- NameNode（NN）：存储文件的元数据，如文件名、文件目录结构、文件属性，以及每个文件的块列表和块所在的DataNode等。
- DataNode（DN）：在本地文件系统存储文件块数据，以及块数据的校验和。
- Secondary NameNode（2NN）：每隔一段时间对NameNode元数据备份。

#### 2.5.2、YARN架构概述

> YARN（Yet Another Resource Negotiater）：另一种资源协调者，是Hadoop的资源管理器。

![](https://img-blog.csdnimg.cn/1d110ee13876482ba63d4dc324f165df.png)

- ResourceManager（RM）：整个集群资源（内存、CPU等）的管理者
- NodeManager（NM）：单个节点服务器资源管理者
- ApplicationMaster（AM）：单个任务运行的管理者
- Container：容器，相当于一台独立的服务器，里面封装了任务运行所需要的资源，如内存、CPU、磁盘、网络等

#### 2.5.3、MapReduce架构概述

> MapReduce将计算拆成两个阶段：Map和Reduce

- Map阶段并行处理输入数据
- Reduce阶段对Map结果进行汇总

![](https://img-blog.csdnimg.cn/bbf3557f898043c3b017e747d1ed5451.png)

#### 2.5.4、HDFS、YARN、MapReduce三者关系

![](https://img-blog.csdnimg.cn/2c2fddf66f8442dcb7a3f0e9f502f267.png)

### 2.6、大数据技术生态体系

![](https://img-blog.csdnimg.cn/f8f1aaef31e04358b9d68c45dd902c9d.png)

1. Sqoop：Sqoop是一款开源的工具，主要用于在Hadoop、Hive 与传统的数据库(MySQL)间进行数据的传递，可以将一个关系型数据库（例如:MySQL，Oracle 等）中的数据导进到Hadoop 的 HDFS 中，也可以将HDFS的数据导进到关系型数据库中。
2. Flume：Flume是一个高可用的，高可靠的，分布式的海量日志采集、聚合和传输的系统，Flume支持在日志系统中定制各类数据发送方，用于收集数据。
3. Kafka：Kafka是一种高吞吐量的分布式发布订阅消息系统。
4. Spark：Spark是当前最流行的开源大数据内存计算框架。可以基于Hadoop上存储的大数据进行计算。
5. Flink：Flink是当前最流行的开源大数据内存计算框架。用于实时计算的场景较多。
6. Oozie：Oozie是一个管理Hadoop 作业（job）的工作流程调度管理系统。
7. Hbase：HBase是一个分布式的、面向列的开源数据库。HBase不同于一般的关系数据库，它是一个适合于非结构化数据存储的数据库。
8. Hive：Hive是基于Hadoop的一个数据仓库工具，可以将结构化的数据文件映射为一张数据库表，并提供简单的SQL查询功能，可以将SQL语句转换为MapReduce任务进行运行。其优点是学习成本低，可以通过类SQL语句快速实现简单的MapReduce统计，不必开发专门的MapReduce应用，十分适合数据仓库的统计分析。
9. ZooKeeper：它是一个针对大型分布式系统的可靠协调系统.提供的功能包括：配置维护。

## 3、Hadoop运行环境搭建

### 3.1、模板模拟机环境准备

1. 安装模板虚拟机，IP地址**192.168.10.100**、主机名称**hadoop100**、内存**4G**、硬盘50G

2. hadoop100虚拟机配置要求如下（本文Linux系统全部以CentOS-7.5-x86-1804为例）

   1. 使用yum安装需要虚拟机可以正常上网，yum安装前可以先测试下虚拟机联网情况

      ```shell
      [root@hadoop100 ~]# ping www.baidu.com
      PING www.baidu.com (14.215.177.39) 56(84) bytes of data.
      64 bytes from 14.215.177.39 (14.215.177.39): icmp_seq=1 ttl=128 time=8.60 ms
      64 bytes from 14.215.177.39 (14.215.177.39): icmp_seq=2 ttl=128 time=7.72 ms
      ```

   2. 安装epel-release

      **注：Extra Packages for Enterprise Linux是为“红帽系”的操作系统提供额外的软件包，适用于RHEL、CentOS和Scientific Linux。相当于是一个软件仓库，大多数rpm包在官方 repository 中是找不到的）**

      ```shell
      [root@hadoop100 ~]# yum install -y epel-release
      ```

   3. **注意：如果Linux安装的是最小系统版，还需要安装如下工具；如果安装的是Linux桌面标准版，不需要执行如下操作**

      - net-tool：工具包集合，包含ifconfig等命令

        ```shell
        [root@hadoop100 ~]# yum install -y net-tools
        ```

      - vim：编辑器

        ```shell
        [root@hadoop100 ~]# yum install -y vim
        ```

3. 关闭防火墙，关闭防火墙开机自启

   ```shell
   [root@hadoop100 ~]# systemctl stop firewalld
   [root@hadoop100 ~]# systemctl disable firewalld.service
   ```

   **注意：在企业开发时，通常单个服务器的防火墙时关闭的。公司整体对外会设置非常安全的防火墙**

4. 创建atguigu用户，并修改atguigu用户的密码

   ```shell
   [root@hadoop100 ~]# useradd atguigu
   [root@hadoop100 ~]# passwd atguigu
   ```

5. 配置atguigu用户具有root权限，方便后期加sudo执行root权限的命令

   ```shell
   [root@hadoop100 ~]# vim /etc/sudoers
   ```

   **修改/etc/sudoers文件，在%wheel这行下面添加一行，如下所示：**

   ```shell
   ## Allow root to run any commands anywhere
   root    ALL=(ALL)     ALL
   
   ## Allows people in group wheel to run all commands
   %wheel  ALL=(ALL)       ALL
   atguigu   ALL=(ALL)     NOPASSWD:ALL
   ```

   **注意：atguigu这一行不要直接放到root行下面，因为所有用户都属于wheel组，你先配置了atguigu具有免密功能，但是程序执行到%wheel行时，该功能又被覆盖回需要密码。所以atguigu要放到%wheel这行下面。**

6. 在/opt目录下创建文件夹，并修改所属主和所属组

   1. 在/opt目录下创建module、software文件夹

      ```shell
      [root@hadoop100 ~]# mkdir /opt/module
      [root@hadoop100 ~]# mkdir /opt/software
      ```

   2. 修改module、software文件夹的所有者和所属组均为atguigu用户

      ```shell
      [root@hadoop100 ~]# chown atguigu:atguigu /opt/module 
      [root@hadoop100 ~]# chown atguigu:atguigu /opt/software
      ```

   3. 查看module、software文件夹的所有者和所属组

      ```shell
      [root@hadoop100 ~]# cd /opt/
      [root@hadoop100 opt]# ll
      总用量 12
      drwxr-xr-x. 2 atguigu atguigu 4096 5月  28 17:18 module
      drwxr-xr-x. 2 root    root    4096 9月   7 2017 rh
      drwxr-xr-x. 2 atguigu atguigu 4096 5月  28 17:18 software
      ```

7. 卸载虚拟机自带的JDK

   **注意：如果你的虚拟机是最小化安装不需要执行这一步。**

   ```shell
   [root@hadoop100 ~]# rpm -qa | grep -i java | xargs -n1 rpm -e --nodeps 
   ```

   - rpm -qa：查询所安装的所有rpm软件包
   - grep -i：忽略大小写
   - xargs -n1：表示每次只传递一个参数
   - rpm -e –nodeps：强制卸载软件

8. 重启虚拟机

   ```shell
   [root@hadoop100 ~]# reboot
   ```

### 3.2、克隆虚拟机

1. 利用模板机**hadoop100**，克隆三台虚拟机：**hadoop102**、**hadoop103**、**hadoop104**

   **注意：克隆时，要先关闭hadoop100**

2. 修改克隆机**IP**，以下以**hadoop102**举例说明

   1. 修改克隆虚拟机的静态IP

      ```shell
      [root@hadoop100 ~]# vim /etc/sysconfig/network-scripts/ifcfg-ens33
      ```

      改成

      ```shell
      DEVICE=ens33
      TYPE=Ethernet
      ONBOOT=yes
      BOOTPROTO=static
      NAME="ens33"
      IPADDR=192.168.10.102
      PREFIX=24
      GATEWAY=192.168.10.2
      DNS1=192.168.10.2
      ```

   2. 查看Linux虚拟机的虚拟网络编辑器，编辑->虚拟网络编辑器->VMnet8

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%9B%BE%E7%89%871.png)

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%9B%BE%E7%89%872.png)

   3. 查看Windows系统适配器VMware Network Adapter VMnet8的IP地址

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%9B%BE%E7%89%873.png)

   4. 保证Linux系统ifcfg-ens33文件中IP地址、虚拟网络编辑器地址和Windows系统VM8网络IP地址相同。

3. 修改克隆机主机名，以下以**hadoop102**举例说明

   1. 修改主机名称

      ```shell
      [root@hadoop100 ~]# vim /etc/hostname
      hadoop102
      ```

   2. 配置Linux克隆机主机名称映射hosts文件，打开`/etc/hosts`

      ```shell
      [root@hadoop100 ~]# vim /etc/hosts
      ```

      添加如下内容

      ```shell
      192.168.10.100 hadoop100
      192.168.10.101 hadoop101
      192.168.10.102 hadoop102
      192.168.10.103 hadoop103
      192.168.10.104 hadoop104
      192.168.10.105 hadoop105
      192.168.10.106 hadoop106
      192.168.10.107 hadoop107
      192.168.10.108 hadoop108
      ```

4. 重启克隆机**hadoop102**

   ```shell
   [root@hadoop100 ~]# reboot
   ```

5. 修改windows的主机映射文件（hosts文件）

   1. 如果操作系统是window7，可以直接修改 

      1. 进入`C:\Windows\System32\drivers\etc`路径

      2. 打开`hosts`文件并添加如下内容，然后保存

         ```shell
         192.168.10.100 hadoop100
         192.168.10.101 hadoop101
         192.168.10.102 hadoop102
         192.168.10.103 hadoop103
         192.168.10.104 hadoop104
         192.168.10.105 hadoop105
         192.168.10.106 hadoop106
         192.168.10.107 hadoop107
         192.168.10.108 hadoop108
         ```

   2. 如果操作系统是window10，先拷贝出来，修改保存以后，再覆盖即可

      1. 进入`C:\Windows\System32\drivers\etc`路径

      2. 拷贝`hosts`文件到桌面

      3. 打开桌面`hosts`文件并添加如下内容

         ```shell
         192.168.10.100 hadoop100
         192.168.10.101 hadoop101
         192.168.10.102 hadoop102
         192.168.10.103 hadoop103
         192.168.10.104 hadoop104
         192.168.10.105 hadoop105
         192.168.10.106 hadoop106
         192.168.10.107 hadoop107
         192.168.10.108 hadoop108
         ```

      4. 将桌面`hosts`文件覆盖`C:\Windows\System32\drivers\etc`路径`hosts`文件

### 3.3、在hadoop102安装JDK

1. 卸载现有JDK

   **注意：安装JDK前，一定确保提前删除了虚拟机自带的JDK。详细步骤见问文档3.1节中卸载JDK步骤。**

2. 用`XShell`传输工具将JDK导入到`opt`目录下面的`software`文件夹下面

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%9B%BE%E7%89%874.png)

3. 在`Linux`系统下的`opt`目录中查看软件包是否导入成功

   ```shell
   [atguigu@hadoop102 ~]$ ls /opt/software/
   ```

   看到如下结果：

   ```shell
   jdk-8u212-linux-x64.tar.gz
   ```

4. 解压JDK到/opt/module目录下

   ```shell
   [atguigu@hadoop102 software]$ tar -zxvf jdk-8u212-linux-x64.tar.gz -C /opt/module/
   ```

5. 配置JDK环境变量

   1. 新建`/etc/profile.d/my_env.sh`文件

      ```shell
      [atguigu@hadoop102 ~]$ sudo vim /etc/profile.d/my_env.sh
      ```

      添加如下内容

      ```shell
      #JAVA_HOME
      export JAVA_HOME=/opt/module/jdk1.8.0_212
      export PATH=$PATH:$JAVA_HOME/bin
      ```

   2. 保存后退出

      ```shell
      :wq
      ```

   3. `source`一下`/etc/profile`文件，让新的环境变量`PATH`生效

      ```shell
      [atguigu@hadoop102 ~]$ source /etc/profile
      ```

6. 测试JDK是否安装成功

   ```shell
   [atguigu@hadoop102 ~]$ java -version
   ```

   如果能看到以下结果，则代表Java安装成功。

   ```shell
   java version "1.8.0_212"
   ```

   **注意：重启（如果java -version可以用就不用重启）**

   ```shell
   [atguigu@hadoop102 ~]$ sudo reboot
   ```

### 3.4、在hadoop102安装Hadoop

[Hadoop下载地址]([https://archive.apache.org/dist/hadoop/common/hadoop-3.1.3/](https://archive.apache.org/dist/hadoop/common/hadoop-2.7.2/))

1. 用`XShell`文件传输工具将`hadoop-3.1.3.tar.gz`导入到opt目录下面的software文件夹下面

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%9B%BE%E7%89%875.png)

2. 进入到Hadoop安装包路径下

   ```shell
   [atguigu@hadoop102 ~]$ cd /opt/software/
   ```

3. 解压安装文件到`/opt/module`下面

   ```shell
   [atguigu@hadoop102 software]$ tar -zxvf hadoop-3.1.3.tar.gz -C /opt/module/
   ```

4. 查看是否解压成功

   ```shell
   [atguigu@hadoop102 software]$ ls /opt/module/
   hadoop-3.1.3
   ```

5. 将Hadoop添加到环境变量

   1. 获取`Hadoop`安装路径

      ```shell
      [atguigu@hadoop102 hadoop-3.1.3]$ pwd
      /opt/module/hadoop-3.1.3
      ```

   2. 打开`/etc/profile.d/my_env.sh`文件

      ```shell
      [atguigu@hadoop102 hadoop-3.1.3]$ sudo vim /etc/profile.d/my_env.sh
      ```

      - 在`my_env.sh`文件末尾添加如下内容：（`shift+g`）

        ```shell
        #HADOOP_HOME
        export HADOOP_HOME=/opt/module/hadoop-3.1.3
        export PATH=$PATH:$HADOOP_HOME/bin
        export PATH=$PATH:$HADOOP_HOME/sbin
        ```

      - 保存并退出： `:wq`

   3. 让修改后的文件生效

      ```shell
      [atguigu@hadoop102 hadoop-3.1.3]$ source /etc/profile
      ```

6. 测试是否安装成功

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop version
   Hadoop 3.1.3
   ```

7. 重启（如果Hadoop命令不能用再重启虚拟机）

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ sudo reboot
   ```

### 3.5、Hadoop目录结构

1. 查看Hadoop目录结构

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ ll
   总用量 52
   drwxr-xr-x. 2 atguigu atguigu  4096 5月  22 2017 bin
   drwxr-xr-x. 3 atguigu atguigu  4096 5月  22 2017 etc
   drwxr-xr-x. 2 atguigu atguigu  4096 5月  22 2017 include
   drwxr-xr-x. 3 atguigu atguigu  4096 5月  22 2017 lib
   drwxr-xr-x. 2 atguigu atguigu  4096 5月  22 2017 libexec
   -rw-r--r--. 1 atguigu atguigu 15429 5月  22 2017 LICENSE.txt
   -rw-r--r--. 1 atguigu atguigu   101 5月  22 2017 NOTICE.txt
   -rw-r--r--. 1 atguigu atguigu  1366 5月  22 2017 README.txt
   drwxr-xr-x. 2 atguigu atguigu  4096 5月  22 2017 sbin
   drwxr-xr-x. 4 atguigu atguigu  4096 5月  22 2017 share
   ```

2. 重要目录

   1. **bin目录**：存放对Hadoop相关服务（`hdfs`，`yarn`，`mapred`）进行操作的脚本。
   2. **etc目录**：Hadoop的配置文件目录，存放Hadoop的配置文件。
   3. **lib目录**：存放Hadoop的本地库（对数据进行压缩解压缩功能）。
   4. **sbin目录**：存放启动或停止Hadoop相关服务的脚本。
   5. **share目录**：存放Hadoop的依赖jar包、文档、和官方案例。

## 4、Hadoop运行模式

1. [Hadoop官方网站](http://hadoop.apache.org/)
2. Hadoop运行模式包括：**本地模式**、**伪分布式模式**以及**完全分布式模式**。
   - **本地模式**：单机运行，只是用来演示一下官方案例。**生产环境不用**。
   - **伪分布式模式：**也是单机运行，但是具备`Hadoop`集群的所有功能，一台服务器模拟一个分布式的环境。**个别缺钱的公司用来测试，生产环境不用。**
   - **完全分布式模式：**多台服务器组成分布式环境。生产环境使用。

### 4.1、本地运行模式（官方WordCount）

1. 创建在`hadoop-3.1.3`文件下面创建一个`wcinput`文件夹

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ mkdir wcinput
   ```

2. 在`wcinput`文件下创建一个`word.txt`文件

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ cd wcinput
   ```

3. 编辑`word.txt`文件

   ```shell
   [atguigu@hadoop102 wcinput]$ vim word.txt
   ```

   - 在文件中输入如下内容

     ```text
     hadoop yarn
     hadoop mapreduce
     atguigu
     atguigu
     ```

   - 保存退出：`:wq`

4. 回到`Hadoop`目录`/opt/module/hadoop-3.1.3`

5. 执行程序

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-3.1.3.jar wordcount wcinput wcoutput
   ```

6. 查看结果

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ cat wcoutput/part-r-00000
   ```

   看到如下结果：

   ```shell
   atguigu 2
   hadoop  2
   mapreduce       1
   yarn    1
   ```

### 4.2、完全分布式运行模式

分析：

1. 准备3台客户机（**关闭防火墙**、**静态IP**、**主机名称**）
2. 安装`JDK`
3. 配置环境变量
4. 安装`Hadoop`
5. 配置环境变量
6. **配置集群**
7. **单点启动**
8. **配置`ssh`**
9. **群起并测试集群**

#### 4.2.1、虚拟机准备

**详见3.1、3.2**

#### 4.2.2、编写集群分发脚本`xsync`

1. scp（secure copy）安全拷贝

   1. scp定义

      scp可以实现服务器与服务器之间的数据拷贝。（from server1 to server2）

   2. 基本语法

      scp  -r     $pdir/$fname       $user@$host:$pdir/$fname

      命令  递归   要拷贝的文件路径/名称  目的地用户@主机:目的地路径/名称

   3. 案例实操

      **前提：在hadoop102、hadoop103、hadoop104都已经创建好的`/opt/module`、`/opt/software`两个目录，并且已经把这两个目录修改为`atguigu:atguigu`**

      ```shell
      [atguigu@hadoop102 ~]$ sudo chown atguigu:atguigu -R /opt/module
      ```

      - 在**hadoop102**上，将hadoop102中`/opt/module/jdk1.8.0_212`目录拷贝到**hadoop103**上。

        ```shell
        [atguigu@hadoop102 ~]$ scp -r /opt/module/jdk1.8.0_212  atguigu@hadoop103:/opt/module
        ```

      - 在**hadoop103**上，将**hadoop102**中`/opt/module/hadoop-3.1.3`目录拷贝到**hadoop103**上。

        ```shell
        [atguigu@hadoop103 ~]$ scp -r atguigu@hadoop102:/opt/module/hadoop-3.1.3 /opt/module/
        ```

      - 在**hadoop103**上操作，将**hadoop102**中/opt/module目录下所有目录拷贝到**hadoop104**上。

        ```shell
        [atguigu@hadoop103 opt]$ scp -r atguigu@hadoop102:/opt/module/* atguigu@hadoop104:/opt/module
        ```

2. rsync远程同步工具

   rsync主要用于备份和镜像。具有速度快、避免复制相同内容和支持符号链接的优点。

   **rsync和scp区别**：用rsync做文件的复制要比scp的速度快，rsync只对差异文件做更新。scp是把所有文件都复制过去。

   1. 基本语法

      ```shell
      rsync    -av       $pdir/$fname             $user@$host:$pdir/$fname
      命令   选项参数   要拷贝的文件路径/名称   目的地用户@主机:目的地路径/名称
      ```

      选项参数说明

      | 选项 | 功能         |
      | :--- | ------------ |
      | -a   | 归档拷贝     |
      | -v   | 显示复制过程 |

      

   2. 案例实操

      - 删除`hadoop103`中`/opt/module/hadoop-3.1.3/wcinput`

        ```shell
        [atguigu@hadoop103 hadoop-3.1.3]$ rm -rf wcinput/
        ```

      - 同步`hadoop102`中的`/opt/module/hadoop-3.1.3`到`hadoop103`

        ```shell
        [atguigu@hadoop102 module]$ rsync -av hadoop-3.1.3/ atguigu@hadoop103:/opt/module/hadoop-3.1.3/
        ```

3. xsync集群分发脚本

   1. 需求：循环复制文件到所有节点的相同目录下

   2. 需求分析：

      - rsync命令原始拷贝：

        ```shell
        rsync -av /opt/module atguigu@hadoop103:/opt/
        ```

      - 期望脚本：

        `xsync`要同步的文件名称

      - 期望脚本在任何路径都能使用（脚本放在声明了全局环境变量的路径）

        ```shell
        [atguigu@hadoop102 ~]$ echo $PATH
        /usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/atguigu/.local/bin:/home/atguigu/bin:/opt/module/jdk1.8.0_212/bin
        ```

   3. 脚本实现

      - 在`/home/atguigu/bin`目录下创建`xsync`文件

        ```shell
        [atguigu@hadoop102 opt]$ cd /home/atguigu
        [atguigu@hadoop102 ~]$ mkdir bin
        [atguigu@hadoop102 ~]$ cd bin
        [atguigu@hadoop102 bin]$ vim xsync
        ```

        在该文件中编写如下代码

        ```shell
        #!/bin/bash
        
        #1. 判断参数个数
        if [ $# -lt 1 ]
        then
            echo Not Enough Arguement!
            exit;
        fi
        
        #2. 遍历集群所有机器
        for host in hadoop102 hadoop103 hadoop104
        do
            echo ====================  $host  ====================
            #3. 遍历所有目录，挨个发送
        
            for file in $@
            do
                #4. 判断文件是否存在
                if [ -e $file ]
                    then
                        #5. 获取父目录
                        pdir=$(cd -P $(dirname $file); pwd)
        
                        #6. 获取当前文件的名称
                        fname=$(basename $file)
                        ssh $host "mkdir -p $pdir"
                        rsync -av $pdir/$fname $host:$pdir
                    else
                        echo $file does not exists!
                fi
            done
        done
        ```

      - 修改脚本 xsync 具有执行权限

        ```shell
        [atguigu@hadoop102 bin]$ chmod +x xsync
        ```

      - 测试脚本

        ```shell
        [atguigu@hadoop102 ~]$ xsync /home/atguigu/bin
        ```

      - 将脚本复制到/bin中，以便全局调用

        ```shell
        [atguigu@hadoop102 bin]$ sudo cp xsync /bin/
        ```

      - 同步环境变量配置（root所有者）

        ```shell
        [atguigu@hadoop102 ~]$ sudo ./bin/xsync /etc/profile.d/my_env.sh
        ```

        **注意：如果用了sudo，那么xsync一定要给它的路径补全。**

        ```shell
        [atguigu@hadoop103 bin]$ source /etc/profile
        [atguigu@hadoop104 opt]$ source /etc/profile
        ```

#### 4.2.3、SSH无密登录配置

1. 配置ssh

   1. 基本语法

      ssh另一台电脑的IP地址

   2. ssh连接时出现Host key verification failed的解决方法

      ```shell
      [atguigu@hadoop102 ~]$ ssh hadoop103
      ```

      如果出现如下内容

      ```shell
      Are you sure you want to continue connecting (yes/no)? 
      ```

      输入yes，并回车

   3. 退回到`hadoop102`

      ```shell
      [atguigu@hadoop103 ~]$ exit
      ```

2. 无密钥配置

   1. 免密登录原理

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230214133151.png)

   2. 生成公钥和私钥

      ```shell
      [atguigu@hadoop102 .ssh]$ pwd
      /home/atguigu/.ssh
      
      [atguigu@hadoop102 .ssh]$ ssh-keygen -t rsa
      ```

      然后敲（三个回车），就会生成两个文件**id_rsa**（私钥）、**id_rsa.pub**（公钥）

   3. 将公钥拷贝到要免密登录的目标机器上

      ```shell
      [atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop102
      [atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop103
      [atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop104
      ```

      **注意：**

      - 还需要在`hadoop103`上采用`atguigu`账号配置一下无密登录到`hadoop102`、`hadoop103`、`hadoop104`服务器上。
      - 还需要在`hadoop104`上采用`atguigu`账号配置一下无密登录到`hadoop102`、`hadoop103`、`hadoop104`服务器上。
      - 还需要在`hadoop102`上采用root账号，配置一下无密登录到`hadoop102`、`hadoop103`、`hadoop104`。

3. `.ssh`文件夹下（~/.ssh）文件功能解释

   | known_hosts     | 记录ssh访问过计算机的公钥（public key） |
   | --------------- | --------------------------------------- |
   | id_rsa          | 生成的私钥                              |
   | id_rsa.pub      | 生成的公钥                              |
   | authorized_keys | 存放授权过的无密登录服务器公钥          |

#### 4.2.4、集群配置

1. 集群部署规划

   **注意：**

   - `NameNode`和`SecondaryNameNode`不要安装在同一台服务器
   - `ResourceManager`也很消耗内存，不要和`NameNode`、`SecondaryNameNode`配置在同一台机器上。

   |      | hadoop102                  | hadoop103                            | hadoop104                           |
   | ---- | -------------------------- | ------------------------------------ | ----------------------------------- |
   | HDFS | **NameNode**<br />DataNode | DataNode                             | **SecondaryNameNode**<br />DataNode |
   | YARN | NodeManager                | **ResourceManager**<br />NodeManager | NodeManager                         |

   

2. 配置文件说明

   Hadoop配置文件分两类：默认配置文件和自定义配置文件，只有用户想修改某一默认配置值时，才需要修改自定义配置文件，更改相应属性值。

   1. 默认配置文件：

      | 要获取的默认文件     | 文件存放在Hadoop的jar包中的位置                           |
      | -------------------- | --------------------------------------------------------- |
      | [core-default.xml]   | hadoop-common-3.1.3.jar/core-default.xml                  |
      | [hdfs-default.xml]   | hadoop-hdfs-3.1.3.jar/hdfs-default.xml                    |
      | [yarn-default.xml]   | hadoop-yarn-common-3.1.3.jar/yarn-default.xml             |
      | [mapred-default.xml] | hadoop-mapreduce-client-core-3.1.3.jar/mapred-default.xml |

   2. 自定义配置文件：

      `core-site.xml`、`hdfs-site.xml`、`yarn-site.xml`、`mapred-site.xml`四个配置文件存放在`$HADOOP_HOME/etc/hadoop`这个路径上，用户可以根据项目需求重新进行修改配置。

3. 配置集群

   1. 核心配置文件

      配置`core-site.xml`

      ```shell
      [atguigu@hadoop102 ~]$ cd $HADOOP_HOME/etc/hadoop
      [atguigu@hadoop102 hadoop]$ vim core-site.xml
      ```

      文件内容如下：

      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
      
      <configuration>
          <!-- 指定NameNode的地址 -->
          <property>
              <name>fs.defaultFS</name>
              <value>hdfs://hadoop102:8020</value>
          </property>
      
          <!-- 指定hadoop数据的存储目录 -->
          <property>
              <name>hadoop.tmp.dir</name>
              <value>/opt/module/hadoop-3.1.3/data</value>
          </property>
      
          <!-- 配置HDFS网页登录使用的静态用户为atguigu -->
          <property>
              <name>hadoop.http.staticuser.user</name>
              <value>atguigu</value>
          </property>
      </configuration>
      ```

   2. HDFS配置文件

      配置`hdfs-site.xml`

      ```shell
      [atguigu@hadoop102 hadoop]$ vim hdfs-site.xml
      ```

      文件内容如下：

      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
      
      <configuration>
      	<!-- nn web端访问地址-->
      	<property>
              <name>dfs.namenode.http-address</name>
              <value>hadoop102:9870</value>
          </property>
      	<!-- 2nn web端访问地址-->
          <property>
              <name>dfs.namenode.secondary.http-address</name>
              <value>hadoop104:9868</value>
          </property>
      </configuration>
      ```

   3. YARN配置文件

      配置`yarn-site.xml`

      ```shell
      [atguigu@hadoop102 hadoop]$ vim yarn-site.xml
      ```

      文件内容如下：

      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
      
      <configuration>
          <!-- 指定MR走shuffle -->
          <property>
              <name>yarn.nodemanager.aux-services</name>
              <value>mapreduce_shuffle</value>
          </property>
      
          <!-- 指定ResourceManager的地址-->
          <property>
              <name>yarn.resourcemanager.hostname</name>
              <value>hadoop103</value>
          </property>
      
          <!-- 环境变量的继承 -->
          <property>
              <name>yarn.nodemanager.env-whitelist</name>
              <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
          </property>
      </configuration>
      ```

   4. MapReduce配置文件

      配置`mapred-site.xml`

      ```shell
      [atguigu@hadoop102 hadoop]$ vim mapred-site.xml
      ```

      文件内容如下：

      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
      
      <configuration>
      	<!-- 指定MapReduce程序运行在Yarn上 -->
          <property>
              <name>mapreduce.framework.name</name>
              <value>yarn</value>
          </property>
      </configuration>
      ```

4. 在集群上分发配置好的Hadoop配置文件

   ```shell
   [atguigu@hadoop102 hadoop]$ xsync /opt/module/hadoop-3.1.3/etc/hadoop/
   ```

5. 去103和104上查看文件分发情况

   ```shell
   [atguigu@hadoop103 ~]$ cat /opt/module/hadoop-3.1.3/etc/hadoop/core-site.xml
   [atguigu@hadoop104 ~]$ cat /opt/module/hadoop-3.1.3/etc/hadoop/core-site.xml
   ```

#### 4.2.5、群起集群

1. 配置workers

   ```shell
   [atguigu@hadoop102 hadoop]$ vim /opt/module/hadoop-3.1.3/etc/hadoop/workers
   ```

   在该文件中增加如下内容：

   ```shell
   hadoop102
   hadoop103
   hadoop104
   ```

   **注意：该文件中添加的内容结尾不允许有空格，文件中不允许有空行。**

   同步所有节点配置文件

   ```shell
   [atguigu@hadoop102 hadoop]$ xsync /opt/module/hadoop-3.1.3/etc
   ```

2. 启动集群

   1. **如果集群是第一次启动**，需要在`hadoop102`节点格式化`NameNode`（注意：格式化`NameNode`，会产生新的集群id，导致`NameNode`和`DataNode`的集群id不一致，集群找不到已往数据。如果集群在运行过程中报错，需要重新格式化`NameNode`的话，一定要先停止`namenode`和`datanode`进程，并且要删除所有机器的`data`和`logs`目录，然后再进行格式化。）

      ```shell
      [atguigu@hadoop102 hadoop-3.1.3]$ hdfs namenode -format
      ```

   2. 启动HDFS

      ```shell
      [atguigu@hadoop102 hadoop-3.1.3]$ sbin/start-dfs.sh
      ```

   3. **在配置了ResourceManager的节点（hadoop103）**启动YARN

      ```shell
      [atguigu@hadoop103 hadoop-3.1.3]$ sbin/start-yarn.sh
      ```

   4. Web端查看HDFS的NameNode

      - 浏览器中输入：`http://hadoop102:9870`
      - 查看HDFS上存储的数据信息

   5. Web端查看YARN的ResourceManager

      - 浏览器中输入：`http://hadoop103:8088`
      - 查看YARN上运行的Job信息

3. 集群基本测试

   1. 上传文件到集群

      - 上传小文件

        ```shell
        [atguigu@hadoop102 ~]$ hadoop fs -mkdir /input
        [atguigu@hadoop102 ~]$ hadoop fs -put $HADOOP_HOME/wcinput/word.txt /input
        ```

      - 上传大文件

        ```shell
        [atguigu@hadoop102 ~]$ hadoop fs -put  /opt/software/jdk-8u212-linux-x64.tar.gz  /
        ```

   2. 上传文件后查看文件存放在什么位置

      - 查看HDFS文件存储路径

        ```shell
        [atguigu@hadoop102 subdir0]$ pwd
        /opt/module/hadoop-3.1.3/data/dfs/data/current/BP-1436128598-192.168.10.102-1610603650062/current/finalized/subdir0/subdir0
        ```

      - 查看HDFS在磁盘存储文件内容

        ```shell
        [atguigu@hadoop102 subdir0]$ cat blk_1073741825
        hadoop yarn
        hadoop mapreduce 
        atguigu
        atguigu
        ```

   3. 拼接

      ```shell
      -rw-rw-r--. 1 atguigu atguigu 134217728 5月  23 16:01 blk_1073741836
      -rw-rw-r--. 1 atguigu atguigu   1048583 5月  23 16:01 blk_1073741836_1012.meta
      -rw-rw-r--. 1 atguigu atguigu  63439959 5月  23 16:01 blk_1073741837
      -rw-rw-r--. 1 atguigu atguigu    495635 5月  23 16:01 blk_1073741837_1013.meta
      ```

      ```shell
      [atguigu@hadoop102 subdir0]$ cat blk_1073741836>>tmp.tar.gz
      [atguigu@hadoop102 subdir0]$ cat blk_1073741837>>tmp.tar.gz
      [atguigu@hadoop102 subdir0]$ tar -zxvf tmp.tar.gz
      ```

   4. 下载

      ```shell
      [atguigu@hadoop104 software]$ hadoop fs -get /jdk-8u212-linux-x64.tar.gz ./
      ```

   5. 执行`wordcount`程序

      ```shell
      [atguigu@hadoop102 hadoop-3.1.3]$ hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-3.1.3.jar wordcount /input /output
      ```

#### 4.2.6、配置历史服务器

**为了查看程序的历史运行情况，需要配置一下历史服务器。具体配置步骤如下：**

1. 配置`mapred-site.xml`

   ```shell
   [atguigu@hadoop102 hadoop]$ vim mapred-site.xml
   ```

   在该文件里面增加如下配置。

   ```xml
   <!-- 历史服务器端地址 -->
   <property>
       <name>mapreduce.jobhistory.address</name>
       <value>hadoop102:10020</value>
   </property>
   
   <!-- 历史服务器web端地址 -->
   <property>
       <name>mapreduce.jobhistory.webapp.address</name>
       <value>hadoop102:19888</value>
   </property>
   ```

2. 分发配置

   ```shell
   [atguigu@hadoop102 hadoop]$ xsync $HADOOP_HOME/etc/hadoop/mapred-site.xml
   ```

3. 在`hadoop102`启动历史服务器

   ```shell
   [atguigu@hadoop102 hadoop]$ mapred --daemon start historyserver
   ```

4. 查看历史服务器是否启动

   ```shell
   [atguigu@hadoop102 hadoop]$ jps
   ```

5. [查看JobHistory]

   `http://hadoop102:19888/jobhistory`

#### 4.2.7、配置日志的聚集

日志聚集概念：应用运行完成以后，将程序运行日志信息上传到HDFS系统上。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/1.png)

日志聚集功能好处：可以方便的查看到程序运行详情，方便开发调试。

**注意：开启日志聚集功能，需要重新启动NodeManager 、ResourceManager和HistoryServer。**

开启日志聚集功能具体步骤如下：

1. 配置`yarn-site.xml`

   ```shell
   [atguigu@hadoop102 hadoop]$ vim yarn-site.xml
   ```

   在该文件里面增加如下配置。

   ```xml
   <!-- 开启日志聚集功能 -->
   <property>
       <name>yarn.log-aggregation-enable</name>
       <value>true</value>
   </property>
   <!-- 设置日志聚集服务器地址 -->
   <property>  
       <name>yarn.log.server.url</name>  
       <value>http://hadoop102:19888/jobhistory/logs</value>
   </property>
   <!-- 设置日志保留时间为7天 -->
   <property>
       <name>yarn.log-aggregation.retain-seconds</name>
       <value>604800</value>
   </property>
   ```

2. 分发配置

   ```shell
   [atguigu@hadoop102 hadoop]$ xsync $HADOOP_HOME/etc/hadoop/yarn-site.xml
   ```

3. 关闭NodeManager 、ResourceManager和HistoryServer

   ```shell
   [atguigu@hadoop103 hadoop-3.1.3]$ sbin/stop-yarn.sh
   [atguigu@hadoop103 hadoop-3.1.3]$ mapred --daemon stop historyserver
   ```

4. 启动NodeManager 、ResourceManage和HistoryServer

   ```shell
   [atguigu@hadoop103 ~]$ start-yarn.sh
   [atguigu@hadoop102 ~]$ mapred --daemon start historyserver
   ```

5. 删除HDFS上已经存在的输出文件

   ```shell
   [atguigu@hadoop102 ~]$ hadoop fs -rm -r /output
   ```

6. 执行WordCount程序

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-3.1.3.jar wordcount /input /output
   ```

7. 查看日志

   1. 历史服务器地址

      `http://hadoop102:19888/jobhistory`

   2. 历史任务列表

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/150701.png)

   3. 查看任务运行日志

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/150702.png)

   4. 运行日志详情

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/150703.png)

#### 4.2.8、集群启动/停止方式总结

1. 各个模块分开启动/停止（配置ssh是前提）常用

   1. 整体启动/停止HDFS

      ```shell
      start-dfs.sh/stop-dfs.sh
      ```

   2. 整体启动/停止YARN

      ```shell
      start-yarn.sh/stop-yarn.sh
      ```

2. 各个服务组件逐一启动/停止

   1. 分别启动/停止HDFS组件

      ```shell
      hdfs --daemon start/stop namenode/datanode/secondarynamenode
      ```

   2. 启动/停止YARN

      ```shell
      yarn --daemon start/stop  resourcemanager/nodemanager
      ```

#### 4.2.9、编写Hadoop集群常用脚本

1. Hadoop集群启停脚本（包含`HDFS`，`Yarn`，`Historyserver`）：`myhadoop.sh`

   ```shell
   [atguigu@hadoop102 ~]$ cd /home/atguigu/bin
   [atguigu@hadoop102 bin]$ vim myhadoop.sh
   ```

   - 输入如下内容

     ```shell
     #!/bin/bash
     
     if [ $# -lt 1 ]
     then
         echo "No Args Input..."
         exit ;
     fi
     
     case $1 in
     "start")
             echo " =================== 启动 hadoop集群 ==================="
     
             echo " --------------- 启动 hdfs ---------------"
             ssh hadoop102 "/opt/module/hadoop-3.1.3/sbin/start-dfs.sh"
             echo " --------------- 启动 yarn ---------------"
             ssh hadoop103 "/opt/module/hadoop-3.1.3/sbin/start-yarn.sh"
             echo " --------------- 启动 historyserver ---------------"
             ssh hadoop102 "/opt/module/hadoop-3.1.3/bin/mapred --daemon start historyserver"
     ;;
     "stop")
             echo " =================== 关闭 hadoop集群 ==================="
     
             echo " --------------- 关闭 historyserver ---------------"
             ssh hadoop102 "/opt/module/hadoop-3.1.3/bin/mapred --daemon stop historyserver"
             echo " --------------- 关闭 yarn ---------------"
             ssh hadoop103 "/opt/module/hadoop-3.1.3/sbin/stop-yarn.sh"
             echo " --------------- 关闭 hdfs ---------------"
             ssh hadoop102 "/opt/module/hadoop-3.1.3/sbin/stop-dfs.sh"
     ;;
     *)
         echo "Input Args Error..."
     ;;
     esac
     ```

   - 保存后退出，然后赋予脚本执行权限

     ```shell
     [atguigu@hadoop102 bin]$ chmod +x myhadoop.sh
     ```

2. 查看三台服务器Java进程脚本：`jpsall`

   ```shell
   [atguigu@hadoop102 ~]$ cd /home/atguigu/bin
   [atguigu@hadoop102 bin]$ vim jpsall
   ```

   - 输入如下内容

     ```shell
     #!/bin/bash
     
     for host in hadoop102 hadoop103 hadoop104
     do
             echo =============== $host ===============
             ssh $host jps 
     done
     ```

   - 保存后退出，然后赋予脚本执行权限

     ```shell
     [atguigu@hadoop102 bin]$ chmod +x jpsall
     ```

3. 分发`/home/atguigu/bin`目录，保证自定义脚本在三台机器上都可以使用

   ```shell
   [atguigu@hadoop102 ~]$ xsync /home/atguigu/bin/
   ```

#### 4.2.10、常用端口说明

| 端口名称                  | Hadoop2.x   | Hadoop3.x              |
| ------------------------- | ----------- | ---------------------- |
| NameNode内部通信端口      | 8020 / 9000 | **8020** / 9000 / 9820 |
| NameNode HTTP UI          | **50070**   | **9870**               |
| MapReduce查看执行任务端口 | 8088        | 8088                   |
| 历史服务器通信端口        | 19888       | 19888                  |

#### 4.2.11、集群时间同步

- **如果服务器在公网环境（能连接外网），可以不采用集群时间同步**，因为服务器会定期和公网时间进行校准；
- 如果服务器在内网环境，必须要配置集群时间同步，否则时间久了，会产生时间偏差，导致集群执行任务时间不同步。

1. 需求

   找一个机器，作为时间服务器，所有的机器与这台集群时间进行定时的同步，生产环境根据任务对时间的准确程度要求周期同步。测试环境为了尽快看到效果，采用1分钟同步一次。

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/0346.png)

2. 时间服务器配置（必须root用户）

   1. **查看所有节点**`ntpd`服务状态和开机自启动状态

      ```shell
      [atguigu@hadoop102 ~]$ sudo systemctl status ntpd
      [atguigu@hadoop102 ~]$ sudo systemctl start ntpd
      [atguigu@hadoop102 ~]$ sudo systemctl is-enabled ntpd
      ```

   2. 修改`hadoop102`的`ntp.conf`配置文件

      ```shell
      [atguigu@hadoop102 ~]$ sudo vim /etc/ntp.conf
      ```

      修改内容如下

      - 修改1（授权192.168.**10.0**-192.168.**10.255**网段上的所有机器可以从这台机器上查询和同步时间）

        ```shell
        #restrict 192.168.10.0 mask 255.255.255.0 nomodify notrap
        
        修改为：
        restrict 192.168.10.0 mask 255.255.255.0 nomodify notrap
        ```

      - 修改2（集群在局域网中，不使用其他互联网上的时间）

        ```shell
        server 0.centos.pool.ntp.org iburst
        server 1.centos.pool.ntp.org iburst
        server 2.centos.pool.ntp.org iburst
        server 3.centos.pool.ntp.org iburst
        ```

        为

        ```shell
        #server 0.centos.pool.ntp.org iburst
        #server 1.centos.pool.ntp.org iburst
        #server 2.centos.pool.ntp.org iburst
        #server 3.centos.pool.ntp.org iburst
        ```

      - 添加3（当该节点丢失网络连接，依然可以采用本地时间作为时间服务器为集群中的其他节点提供时间同步）

        ```shell
        server 127.127.1.0
        fudge 127.127.1.0 stratum 10
        ```

   3. 修改`hadoop102`的`/etc/sysconfig/ntpd` 文件

      ```shell
      [atguigu@hadoop102 ~]$ sudo vim /etc/sysconfig/ntpd
      ```

      增加内容如下（让硬件时间与系统时间一起同步）

      ```shell
      SYNC_HWCLOCK=yes
      ```

   4. 重新启动`ntpd`服务

      ```shell
      [atguigu@hadoop102 ~]$ sudo systemctl start ntpd
      ```

   5. 设置ntpd服务开机启动

      ```shell
      [atguigu@hadoop102 ~]$ sudo systemctl enable ntpd
      ```

3. 其他机器配置（必须root用户）

   1. 关闭所有节点上ntp服务和自启动

      ```shell
      [atguigu@hadoop103 ~]$ sudo systemctl stop ntpd
      [atguigu@hadoop103 ~]$ sudo systemctl disable ntpd
      [atguigu@hadoop104 ~]$ sudo systemctl stop ntpd
      [atguigu@hadoop104 ~]$ sudo systemctl disable ntpd
      ```

   2. 在其他机器配置1分钟与时间服务器同步一次

      ```shell
      [atguigu@hadoop103 ~]$ sudo crontab -e
      ```

      编写定时任务如下：

      ```shell
      */1 * * * * /usr/sbin/ntpdate hadoop102

   3. 修改任意机器时间

      ```shell
      [atguigu@hadoop103 ~]$ sudo date -s "2021-9-11 11:11:11"

   4. 1分钟后查看机器是否与时间服务器同步

      ```shell
      [atguigu@hadoop103 ~]$ sudo date
      ```

## 5、常见错误及解决方案

1. 防火墙没关闭、或者没有启动YARN

   ```java
   INFO client.RMProxy: Connecting to ResourceManager at hadoop108/192.168.10.108:8032
   ```

2. 主机名称配置错误

3. IP地址配置错误

4. ssh没有配置好

5. root用户和atguigu两个用户启动集群不统一

6. 配置文件修改不细心

7. 不识别主机名称

   ```java
   java.net.UnknownHostException: hadoop102: hadoop102
           at java.net.InetAddress.getLocalHost(InetAddress.java:1475)
           at org.apache.hadoop.mapreduce.JobSubmitter.submitJobInternal(JobSubmitter.java:146)
           at org.apache.hadoop.mapreduce.Job$10.run(Job.java:1290)
           at org.apache.hadoop.mapreduce.Job$10.run(Job.java:1287)
           at java.security.AccessController.doPrivileged(Native Method)
   at javax.security.auth.Subject.doAs(Subject.java:415)
   ```

   解决办法：

   1. 在`/etc/hosts`文件中添加 **192.168.10.102hadoop102**
   2. 主机名称不要起hadoop  hadoop000等特殊名称

8. DataNode和NameNode进程同时只能工作一个。

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/1558.png)

9. 执行命令不生效，粘贴Word中命令时，遇到-和长–没区分开。导致命令失效

   解决办法：尽量不要粘贴Word中代码。

10. jps发现进程已经没有，但是重新启动集群，提示进程已经开启。

    原因是在Linux的根目录下`/tmp`目录中存在启动的进程临时文件，将集群相关进程删除掉，再重新启动集群。

11. jps不生效

    原因：全局变量`hadoop` `java`没有生效。解决办法：需要`source /etc/profile`文件。

12. 8088端口连接不上

    ```shell
    [atguigu@hadoop102 桌面]$ cat /etc/hosts
    ```

    注释掉如下代码

    ```shell
    #127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
    #::1         hadoop102
    ```


## 6、HDFS概述

### 6.1、HDFS产出背景及定义

1. HDFS产生背景

   随着数据量越来越大，在一个操作系统存不下所有的数据，那么就分配到更多的操作系统管理的磁盘中，但是不方便管理和维护，迫切**需要一种系统来管理多台机器上的文件**，这就是分布式文件管理系统。**HDFS 只是分布式文件管理系统中的一种。**

2. HDFS定义

   - **HDFS（Hadoop Distributed File System），它是一个文件系统**，用于存储文件，通过目录树来定位文件；**其次，它是分布式的**，由很多服务器联合起来实现其功能，集群中的服务器有各自的角色。
   - **HDFS 的使用场景：适合一次写入，多次读出的场景。**一个文件经过创建、写入和关闭之后就不需要改变。

### 6.2、HDFS优缺点

- HDFS优点
  1. 高容错性
     - 数据自动保存多个副本。它通过增加副本的形式，提高容错性。
     - 某一个副本丢失以后，它可以自动恢复。
  2. 适合处理大数据
     - 数据规模：能够处理数据规模达到GB、TB、甚至**PB级别的数据**；
     - 文件规模：能够处理**百万**规模以上的**文件数量**，数量相当之大。
  3. 可**构建在廉价机器上**，通过多副本机制，提高可靠性。
- HDFS缺点
  1. **不适合低延时数据访问**，比如毫秒级的存储数据，是做不到的。
  2. **无法高效的对大量小文件进行存储。**
     - 存储大量小文件的话，它会占用NameNode大量的内存来存储文件目录和块信息。这样是不可取的，因为NameNode的内存总是有限的；
     - 小文件存储的寻址时间会超过读取时间，它违反了HDFS的设计目标。
  3. 不支持并发写入、文件随机修改。
     - 一个文件只能有一个写，不允许多个线程同时写
     - 仅支持数据append（追加），不支持文件的随机修改

### 6.3、HDFS组成架构

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230216090221.png)

1. NameNode（nn）：就是Master，它是一个主管、管理者
   1. 管理HDFS的名称空间
   2. 配置副本策略
   3. 管理数据块（Block）映射信息
   4. 处理客户端读写请求
2. DataNode：就是Slave。NameNode下达命令，DataNode执行实际的操作
   1. 存储实际的数据块
   2. 执行数据块的读/写操作
3. Client：就是客户端
   1. 文件切分。文件上传HDFS的时候，Client将文件切分成一个一个的Block，然后进行上传
   2. 与NameNode交互，获取文件的位置信息
   3. 与DataNode交互，读取或者写入数据
   4. Client提供一些命令来管理HDFS，比如NameNode格式化
   5. Client可以通过一些命令来访问HDFS，比如对HDFS增删查改操作
4. Secondary NameNode：并非NameNode的热备。当NameNode挂掉的时候，它并不能马上替换NameNode并提供服务
   1. 辅助NameNode，分担其工作量，比如定期合并Fsimage和Edits，并推送给NameNode
   2. 在紧急情况下，可辅助恢复NameNode

### 6.4、HDFS文件块大小

HDFS中的文件在物理上是分块存储（Block），块的大小可以通过配置参数( dfs.blocksize）来规定，**默认大小在Hadoop2.x/3.x版本中是128M，1.x版本中是64M。**

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230216091154.png)

> 为什么块的大小不能设置太小，也不能设置太大

1. HDFS的块设置**太小，会增加寻址时间**，程序一直在找块的开始位置
2. 如果块设置的**太大**，从**磁盘传输数据的时间**会明显**大于定位这个块开始位置所需的时间**。导致程序在处理这块数据时，会非常慢。

**总结：HDFS块的大小设置主要取决于磁盘传输速率。**

## 7、HDFS的Shell操作

### 7.1、基本语法

hadoop fs 具体命令 OR hdfs dfs 具体命令

两个是完全相同的。

### 7.2、命令大全

```shell
[atguigu@hadoop102 hadoop-3.1.3]$ bin/hadoop fs
[-appendToFile <localsrc> ... <dst>]
 [-cat [-ignoreCrc] <src> ...]
 [-chgrp [-R] GROUP PATH...]
 [-chmod [-R] <MODE[,MODE]... | OCTALMODE> PATH...]
 [-chown [-R] [OWNER][:[GROUP]] PATH...]
 [-copyFromLocal [-f] [-p] <localsrc> ... <dst>]
 [-copyToLocal [-p] [-ignoreCrc] [-crc] <src> ... <localdst>]
 [-count [-q] <path> ...]
 [-cp [-f] [-p] <src> ... <dst>]
 [-df [-h] [<path> ...]]
 [-du [-s] [-h] <path> ...]
 [-get [-p] [-ignoreCrc] [-crc] <src> ... <localdst>]
 [-getmerge [-nl] <src> <localdst>]
 [-help [cmd ...]]
 [-ls [-d] [-h] [-R] [<path> ...]]
 [-mkdir [-p] <path> ...]
 [-moveFromLocal <localsrc> ... <dst>]
 [-moveToLocal <src> <localdst>]
 [-mv <src> ... <dst>]
 [-put [-f] [-p] <localsrc> ... <dst>]
 [-rm [-f] [-r|-R] [-skipTrash] <src> ...]
 [-rmdir [--ignore-fail-on-non-empty] <dir> ...]
<acl_spec> <path>]]
 [-setrep [-R] [-w] <rep> <path> ...]
 [-stat [format] <path> ...]
 [-tail [-f] <file>]
 [-test -[defsz] <path>]
 [-text [-ignoreCrc] <src> ...]
```

### 7.3、常用命令实操

#### 7.3.1、准备工作

1. 启动 Hadoop 集群（方便后续的测试）

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ sbin/start-dfs.sh
   [atguigu@hadoop103 hadoop-3.1.3]$ sbin/start-yarn.sh
   ```

2. -help：输出这个命令参数

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -help rm
   ```

3. 创建/sanguo 文件夹

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -mkdir /sangu
   ```

#### 7.3.2、上传

1. `-moveFromLocal`：从本地**剪切**粘贴到 HDFS

2. `-copyFromLocal`：从本地文件系统中拷贝文件到 HDFS 路径去

3. `-put`：等同于 copyFromLocal，生产环境更习惯用 put

4. `-appendToFile`：追加一个文件到已经存在的文件末尾

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ vim liubei.txt
   输入：
   liubei
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -appendToFile liubei.txt 
   /sanguo/shuguo.txt
   ```

#### 7.3.3、下载

1. `-copyToLocal`：从 HDFS 拷贝到本地

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -copyToLocal 
   /sanguo/shuguo.txt ./
   ```

2. `-get`：等同于 copyToLocal，生产环境更习惯用 get

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -get 
   /sanguo/shuguo.txt ./shuguo2.txt
   ```

#### 7.3.4、HDFS直接操作

1. `-ls`: 显示目录信息

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -ls /sangu
   ```

2. `-cat`：显示文件内容

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -cat /sanguo/shuguo.txt
   ```

3. `-chgrp`、`-chmod`、`-chown`：Linux 文件系统中的用法一样，修改文件所属权限

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -chmod 666 
   /sanguo/shuguo.txt
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -chown atguigu:atguigu 
   /sanguo/shuguo.txt
   ```

4. `-mkdir`：创建路径

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -mkdir /jingu
   ```

5. `-cp`：从 HDFS 的一个路径拷贝到 HDFS 的另一个路径

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -cp /sanguo/shuguo.txt 
   /jinguo
   ```

6. `-mv`：在 HDFS 目录中移动文件

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -mv /sanguo/wuguo.txt /jinguo
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -mv /sanguo/weiguo.txt 
   /jinguo
   ```

7. `-tail`：显示一个文件的末尾 1kb 的数据

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -tail /jinguo/shuguo.txt
   ```

8. `-rm`：删除文件或文件夹

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -rm /sanguo/shuguo.txt
   ```

9. `-rm -r`：递归删除目录及目录里面内容

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -rm -r /sanguo
   ```

10. `-du` 统计文件夹的大小信息

    ```shell
    [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -du -s -h /jinguo
    27 81 /jinguo
    [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -du -h /jinguo
    14 42 /jinguo/shuguo.txt
    7 21 /jinguo/weiguo.txt
    6 18 /jinguo/wuguo.tx
    ```

    **说明：27 表示文件大小；81 表示 27*3 个副本；/jinguo 表示查看的目录**

11. `-setrep`：设置 HDFS 中文件的副本数量

    ```shell
    [atguigu@hadoop102 hadoop-3.1.3]$ hadoop fs -setrep 10 /jinguo/shuguo.txt
    ```

    ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230216092413.png)

**这里设置的副本数只是记录在 NameNode 的元数据中，是否真的会有这么多副本，还得看 DataNode 的数量。因为目前只有 3 台设备，最多也就 3 个副本，只有节点数的增加到 10台时，副本数才能达到 10。**

## 8、HDSF的API操作

### 8.1、客户端环境准备

1. 找到资料包路径下的 Windows 依赖文件夹，拷贝 hadoop-3.1.0 到非中文路径（比如 d:\）。

2. 配置`HADOOP_HOME`

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230216134204.png)

3. 配置Path环境变量

   **注意：如果环境变量不起作用，可以重启电脑试试**

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230216134320.png)

   验证 Hadoop 环境变量是否正常。双击 winutils.exe，如果报如下错误。说明缺少微软运行库（正版系统往往有这个问题）。再资料包里面有对应的微软运行库安装包双击安装即可。

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230216134412.png)

4. 在`IDEA`中创建一个`Maven`工程`HdfsClientDemo`，并导入相关的依赖坐标+日志添加

   ```xml
   <dependencies>
   	<dependency>
   		<groupId>org.apache.hadoop</groupId>
   		<artifactId>hadoop-client</artifactId>
   		<version>3.1.3</version>
   	</dependency>
   	<dependency>
   		<groupId>junit</groupId>
   		<artifactId>junit</artifactId>
   		<version>4.12</version>
   	</dependency>
   	<dependency>
   		<groupId>org.slf4j</groupId>
   		<artifactId>slf4j-log4j12</artifactId>
   		<version>1.7.30</version>
   	</dependency>
   </dependencies>
   ```

   在项目的 src/main/resources 目录下，新建一个文件，命名为`log4j.properties`，在文件中填入

   ```properties
   log4j.rootLogger=INFO, stdout 
   log4j.appender.stdout=org.apache.log4j.ConsoleAppender 
   log4j.appender.stdout.layout=org.apache.log4j.PatternLayout 
   log4j.appender.stdout.layout.ConversionPattern=%d %p [%c] - %m%n 
   log4j.appender.logfile=org.apache.log4j.FileAppender 
   log4j.appender.logfile.File=target/spring.log 
   log4j.appender.logfile.layout=org.apache.log4j.PatternLayout 
   log4j.appender.logfile.layout.ConversionPattern=%d %p [%c] - %m%n
   ```

5. 创建包名：`com.atguigu.hdfs`

6. 创建HdfsClient类

   ```java
   public class HdfsClient {
   	@Test
   	public void testMkdirs() throws IOException, URISyntaxException, InterruptedException {
    		// 1 获取文件系统
       	Configuration configuration = new Configuration();
    		// FileSystem fs = FileSystem.get(new URI("hdfs://hadoop102:8020"), configuration);
   		FileSystem fs = FileSystem.get(new URI("hdfs://hadoop102:8020"), configuration, "atguigu");
    		// 2 创建目录
    		fs.mkdirs(new Path("/xiyou/huaguoshan/"));
    		// 3 关闭资源
    		fs.close();
    	}
   }
   ```

7. 执行程序

   客户端去操作 HDFS 时，是有一个用户身份的。默认情况下，HDFS 客户端 API 会从采用 Windows 默认用户访问 HDFS，会报权限异常错误。所以在访问 HDFS 时，一定要配置用户。

   ```shell
   org.apache.hadoop.security.AccessControlException: Permission denied: 
   user=56576, access=WRITE, 
   inode="/xiyou/huaguoshan":atguigu:supergroup:drwxr-xr-x
   ```

### 8.2、HDFS的API案例实操

#### 8.2.1、HDFS文件上传（测试参数优先级）

1. 编写源代码

   ```java
   @Test
   public void testCopyFromLocalFile() throws IOException, InterruptedException, URISyntaxException {
       // 1 获取文件系统
       Configuration configuration = new Configuration();
       configuration.set("dfs.replication", "2");
       FileSystem fs = FileSystem.get(new URI("hdfs://hadoop102:8020"), configuration, "atguigu");
   	
       //	2 上传文件
       //	boolean delSrc 表示删除原文件
       //	boolean overwrite 是否允许覆盖
       //	Path src 原数据路径参数
       //	Path dst 目的地路径
       fs.copyFromLocalFile(false, false, new Path("d:/sunwukong.txt"), new Path("/xiyou/huaguoshan"));
   
       // 3 关闭资源
       fs.close();
   ｝
   ```

2. 将`hdfs-site.xml`拷贝到项目的`resources`资源目录下

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
   
   <configuration>
   	<property>
   		<name>dfs.replication</name>
            <value>1</value>
   	</property>
   </configuration>
   ```

3. 参数优先级

   参数优先级排序：

   1. 客户端代码中设置的值 
   2. `ClassPath`下的用户自定义配置文件
   3. 然后是服务器的自定义配置（`xxx-site.xml`）
   4. 服务器的默认配置（`xxx-default.xml`）

#### 8.2.2、HDFS文件下载

```java
@Test
public void testCopyToLocalFile() throws IOException, InterruptedException, URISyntaxException{

    // 1 获取文件系统
    Configuration configuration = new Configuration();
    FileSystem fs = FileSystem.get(new URI("hdfs://hadoop102:8020"), configuration, "atguigu");
    
    // 2 执行下载操作
    // boolean delSrc 指是否将原文件删除
    // Path src 指要下载的文件路径
    // Path dst 指将文件下载到的路径
    // boolean useRawLocalFileSystem 是否开启文件校验
    fs.copyToLocalFile(false, new Path("/xiyou/huaguoshan/sunwukong.txt"), new Path("d:/sunwukong2.txt"), true);
    
    // 3 关闭资源
    fs.close();
}
```

注意：如果执行上面代码，下载不了文件，有可能是你电脑的微软支持的运行库少，需要安装一下微软运行库。

#### 8.2.3、HDFS文件更名和移动

```java
@Test
public void testRename() throws IOException, InterruptedException, URISyntaxException{
    
	// 1 获取文件系统
	Configuration configuration = new Configuration();
	FileSystem fs = FileSystem.get(new URI("hdfs://hadoop102:8020"), configuration, "atguigu"); 
		
	// 2 修改文件名称
    // Path path 原文件路径
    // Path path1 目标文件路径
	fs.rename(new Path("/xiyou/huaguoshan/sunwukong.txt"), new Path("/xiyou/huaguoshan/meihouwang.txt"));
		
	// 3 关闭资源
	fs.close();
}
```

#### 8.2.4、HDFS删除文件和目录

```java
@Test
public void testDelete() throws IOException, InterruptedException, URISyntaxException{

	// 1 获取文件系统
	Configuration configuration = new Configuration();
	FileSystem fs = FileSystem.get(new URI("hdfs://hadoop102:8020"), configuration, "atguigu");
		
	// 2 执行删除
    // Path f 要删除的路径
    // boolean recursive 是否递归删除
	fs.delete(new Path("/xiyou"), true);
		
	// 3 关闭资源
	fs.close();
}
```

#### 8.2.5、HDFS文件详情查看

查看文件名称、权限、长度、块信息

```java
@Test
public void testListFiles() throws IOException, InterruptedException, URISyntaxException {

	// 1获取文件系统
	Configuration configuration = new Configuration();
	FileSystem fs = FileSystem.get(new URI("hdfs://hadoop102:8020"), configuration, "atguigu");

	// 2 获取文件详情
	RemoteIterator<LocatedFileStatus> listFiles = fs.listFiles(new Path("/"), true);
	
    // 遍历文件
	while (listFiles.hasNext()) {
		LocatedFileStatus fileStatus = listFiles.next();

		System.out.println("========" + fileStatus.getPath() + "=========");
		System.out.println(fileStatus.getPermission());
		System.out.println(fileStatus.getOwner());
		System.out.println(fileStatus.getGroup());
		System.out.println(fileStatus.getLen());
		System.out.println(fileStatus.getModificationTime());
		System.out.println(fileStatus.getReplication());
		System.out.println(fileStatus.getBlockSize());
		System.out.println(fileStatus.getPath().getName());

		// 获取块信息
		BlockLocation[] blockLocations = fileStatus.getBlockLocations();
		System.out.println(Arrays.toString(blockLocations));
	}
	// 3 关闭资源
	fs.close();
}
```

#### 8.2.6、HDFS文件和文件夹判断

```java
@Test
public void testListStatus() throws IOException, InterruptedException, URISyntaxException{

    // 1 获取文件配置信息
    Configuration configuration = new Configuration();
    FileSystem fs = FileSystem.get(new URI("hdfs://hadoop102:8020"), configuration, "atguigu");

    // 2 判断是文件还是文件夹
    FileStatus[] listStatus = fs.listStatus(new Path("/"));

    for (FileStatus fileStatus : listStatus) {

        // 如果是文件
        if (fileStatus.isFile()) {
            System.out.println("f:"+fileStatus.getPath().getName());
        }else {
            System.out.println("d:"+fileStatus.getPath().getName());
        }
    }

    // 3 关闭资源
    fs.close();
}
```

## 9、HDFS的读写流程

### 9.1、HDFS写数据流程

#### 9.1.1、刨析文件写入

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217092947.png)

1. 客户端通过Distributed FileSystem模块向NameNode请求上传文件，NameNode检查目标文件是否已存在，父目录是否存在。
2. NameNode返回是否可以上传。
3. 客户端请求第一个 Block上传到哪几个DataNode服务器上。
4. NameNode返回3个DataNode节点，分别为dn1、dn2、dn3。
5. 客户端通过FSDataOutputStream模块请求dn1上传数据，dn1收到请求会继续调用dn2，然后dn2调用dn3，将这个通信管道建立完成。
6. dn1、dn2、dn3逐级应答客户端。
7. 客户端开始往dn1上传第一个Block（先从磁盘读取数据放到一个本地内存缓存），以Packet为单位，dn1收到一个Packet就会传给dn2，dn2传给dn3；dn1**每传一个packet会放入一个应答队列等待应答。**
8. 当一个Block传输完成之后，客户端再次请求NameNode上传第二个Block的服务器。（重复执行3-7步）。

#### 9.1.2、网络拓扑-节点距离计算

在HDFS写数据的过程中，NameNode会选择距离待上传数据最近距离的DataNode接收数据。那么这个最近距离怎么计算呢？

**节点距离：两个节点到达最近的共同祖先的距离总和。**

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217093209.png)

例如，假设有数据中心d1机架r1中的节点n1。该节点可以表示为/d1/r1/n1。利用这种标记，这里给出四种距离描述。

大家算一算每两个节点之间的距离。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217093247.png)

#### 9.1.3、机架感知（副本存储节点选择）

1. 机架感知说明

   1. [官方说明]([http://hadoop.apache.org/docs/r3.1.3/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Data_Replication](#Data_Replication))

      ```shell
      For the common case, when the replication factor is three, HDFS’s placement policy is to put one replica on the local machine if the writer is on a datanode, otherwise on a random datanode, another replica on a node in a different (remote) rack, and the last on a different node in the same remote rack. This policy cuts the inter-rack write traffic which generally improves write performance. The chance of rack failure is far less than that of node failure; this policy does not impact data reliability and availability guarantees. However, it does reduce the aggregate network bandwidth used when reading data since a block is placed in only two unique racks rather than three. With this policy, the replicas of a file do not evenly distribute across the racks. One third of replicas are on one node, two thirds of replicas are on one rack, and the other third are evenly distributed across the remaining racks. This policy improves write performance without compromising data reliability or read performance.
      ```

   2. 源码说明

      Crtl + n 查找BlockPlacementPolicyDefault，在该类中查找chooseTargetInOrder方法。

2. Hadoop3.1.3副本节点选择

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217093506.png)

### 9.2、HDFS读数据流程

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217093548.png)

1. 客户端通过DistributedFileSystem向NameNode请求下载文件，NameNode通过查询元数据，找到文件块所在的DataNode地址。
2. 挑选一台DataNode（就近原则，然后随机）服务器，请求读取数据。
3. DataNode开始传输数据给客户端（从磁盘里面读取数据输入流，以Packet为单位来做校验）。
4. 客户端以Packet为单位接收，先在本地缓存，然后写入目标文件。

## 10、NameNode和SecondaryNameNode

### 10.1、NN和2NN工作机制

> NameNode中的元数据是存储在哪里的？

- 首先，我们做个假设，如果存储在NameNode节点的磁盘中，因为经常需要进行随机访问，还有响应客户请求，必然是效率过低。因此，元数据需要存放在内存中。但如果只存在内存中，一旦断电，元数据丢失，整个集群就无法工作了。**因此产生在磁盘中备份元数据的FsImage。**
- 这样又会带来新的问题，当在内存中的元数据更新时，如果同时更新FsImage，就会导致效率过低，但如果不更新，就会发生一致性问题，一旦NameNode节点断电，就会产生数据丢失。**因此，引入Edits文件（只进行追加操作，效率很高）。每当元数据有更新或者添加元数据时，修改内存中的元数据并追加到Edits中。**这样，一旦NameNode节点断电，可以通过FsImage和Edits的合并，合成元数据。
- 但是，如果长时间添加数据到Edits中，会导致该文件数据过大，效率降低，而且一旦断电，恢复元数据需要的时间过长。因此，需要定期进行FsImage和Edits的合并，如果这个操作由NameNode节点完成，又会效率过低。**因此，引入一个新的节点SecondaryNamenode，专门用于FsImage和Edits的合并。**

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217093803.png)

1. 第一阶段：**NameNode**启动
   1. 第一次启动NameNode格式化后，创建Fsimage和Edits文件。如果不是第一次启动，直接加载编辑日志和镜像文件到内存。
   2. 客户端对元数据进行增删改的请求。
   3. NameNode记录操作日志，更新滚动日志。
   4. NameNode在内存中对元数据进行增删改。
2. 第二阶段：**Secondary NameNode**工作
   1. Secondary NameNode询问NameNode是否需要CheckPoint。直接带回NameNode是否检查结果。
   2. Secondary NameNode请求执行CheckPoint。
   3. NameNode滚动正在写的Edits日志。
   4. 将滚动前的编辑日志和镜像文件拷贝到Secondary NameNode。
   5. Secondary NameNode加载编辑日志和镜像文件到内存，并合并。
   6. 生成新的镜像文件fsimage.chkpoint。
   7. 拷贝fsimage.chkpoint到NameNode。
   8. NameNode将fsimage.chkpoint重新命名成fsimage。

### 10.2、Fsimage和Edits解析

> Fsimage和Edits概念

NameNode被格式化之后，将在`/opt/module/hadoop-3.1.3/data/tmp/dfs/name/current`目录中产生如下文件

```shell
fsimage_00000000000000000
fsimage_00ooooooooooooo0000.md5
seen_txid
VERSION
```

1. Fsimage文件：HDFS文件系统原数据的一个永久性的检查点，其中包含HDFS文件系统的所有目录和文件inode的序列化信息。
2. Edits文件：存放HDFS文件系统的所有更新操作的路径，文件系统客户端执行的所有写操作首先会被记录到Edits文件中。
3. seen_txid文件保存的是一个数字，就是最后一个edits_的数字
4. 每次NameNode启动的时候都会将Fsimage文件读入内存，加载Edits里面的更新操作，保证内存中的原数据信息是最新的、同步的，可以看到NameNode启动的时候就将Fsimage和Edits文件进行了合并。

1. oiv查看Fsimage文件

   1. 查看oiv和oev命令

      ```shell
      [atguigu@hadoop102 current]$ hdfs
      oiv            apply the offline fsimage viewer to an fsimage
      oev            apply the offline edits viewer to an edits file
      ```

   2. 基本语法

      ```shell
      hdfs oiv -p 文件类型 -i镜像文件 -o 转换后文件输出路径
      ```

   3. 案例实操

      ```shell
      [atguigu@hadoop102 current]$ pwd
      /opt/module/hadoop-3.1.3/data/dfs/name/current
      
      [atguigu@hadoop102 current]$ hdfs oiv -p XML -i fsimage_0000000000000000025 -o /opt/module/hadoop-3.1.3/fsimage.xml
      
      [atguigu@hadoop102 current]$ cat /opt/module/hadoop-3.1.3/fsimage.xml
      ```

      将显示的xml文件内容拷贝到Idea中创建的xml文件中，并格式化。部分显示结果如下。

      ```xml
      <inode>
      	<id>16386</id>
      	<type>DIRECTORY</type>
      	<name>user</name>
          <mtime>1512722284477</mtime>
      	<permission>atguigu:supergroup:rwxr-xr-x</permission>
      	<nsquota>-1</nsquota>
      	<dsquota>-1</dsquota>
      </inode>
      <inode>
      	<id>16387</id>
      	<type>DIRECTORY</type>
      	<name>atguigu</name>
      	<mtime>1512790549080</mtime>
      	<permission>atguigu:supergroup:rwxr-xr-x</permission>
      	<nsquota>-1</nsquota>
      	<dsquota>-1</dsquota>
      </inode>
      <inode>
      	<id>16389</id>
      	<type>FILE</type>
      	<name>wc.input</name>
      	<replication>3</replication>
      	<mtime>1512722322219</mtime>
      	<atime>1512722321610</atime>
      	<perferredBlockSize>134217728</perferredBlockSize>
      	<permission>atguigu:supergroup:rw-r--r--</permission>
      	<blocks>
      		<block>
      			<id>1073741825</id>
      			<genstamp>1001</genstamp>
      			<numBytes>59</numBytes>
      		</block>
      	</blocks>
      </inode >
      ```

      > 可以看出，Fsimage中没有记录块所对应DataNode，为什么？

      在集群启动后，要求DataNode上报数据块信息，并间隔一段时间后再次上报。

2. oev查看Edits文件

   1. 基本语法

      ```shell
      hdfs oev -p 文件类型 -i编辑日志 -o 转换后文件输出路径
      ```

   2. 案例实操

      ```shell
      [atguigu@hadoop102 current]$ hdfs oev -p XML -i edits_0000000000000000012-0000000000000000013 -o /opt/module/hadoop-3.1.3/edits.xml
      
      [atguigu@hadoop102 current]$ cat /opt/module/hadoop-3.1.3/edits.xml
      ```

      将显示的xml文件内容拷贝到Idea中创建的xml文件中，并格式化。显示结果如下。

      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <EDITS>
      	<EDITS_VERSION>-63</EDITS_VERSION>
      	<RECORD>
      		<OPCODE>OP_START_LOG_SEGMENT</OPCODE>
      		<DATA>
      			<TXID>129</TXID>
      		</DATA>
      	</RECORD>
          <RECORD>
      		<OPCODE>OP_ADD</OPCODE>
      		<DATA>
      			<TXID>130</TXID>
      			<LENGTH>0</LENGTH>
      			<INODEID>16407</INODEID>
      			<PATH>/hello7.txt</PATH>
      			<REPLICATION>2</REPLICATION>
      			<MTIME>1512943607866</MTIME>
      			<ATIME>1512943607866</ATIME>
      			<BLOCKSIZE>134217728</BLOCKSIZE>
      			<CLIENT_NAME>DFSClient_NONMAPREDUCE_-1544295051_1</CLIENT_NAME>
      			<CLIENT_MACHINE>192.168.10.102</CLIENT_MACHINE>
      			<OVERWRITE>true</OVERWRITE>
      			<PERMISSION_STATUS>
      				<USERNAME>atguigu</USERNAME>
      				<GROUPNAME>supergroup</GROUPNAME>
      				<MODE>420</MODE>
      			</PERMISSION_STATUS>
      			<RPC_CLIENTID>908eafd4-9aec-4288-96f1-e8011d181561</RPC_CLIENTID>
      			<RPC_CALLID>0</RPC_CALLID>
      		</DATA>
      	</RECORD>
      	<RECORD>
      		<OPCODE>OP_ALLOCATE_BLOCK_ID</OPCODE>
      		<DATA>
      			<TXID>131</TXID>
      			<BLOCK_ID>1073741839</BLOCK_ID>
      		</DATA>
      	</RECORD>
      	<RECORD>
      		<OPCODE>OP_SET_GENSTAMP_V2</OPCODE>
      		<DATA>
      			<TXID>132</TXID>
      			<GENSTAMPV2>1016</GENSTAMPV2>
      		</DATA>
      	</RECORD>
      	<RECORD>
      		<OPCODE>OP_ADD_BLOCK</OPCODE>
      		<DATA>
      			<TXID>133</TXID>
      			<PATH>/hello7.txt</PATH>
      			<BLOCK>
      				<BLOCK_ID>1073741839</BLOCK_ID>
      				<NUM_BYTES>0</NUM_BYTES>
      				<GENSTAMP>1016</GENSTAMP>
      			</BLOCK>
      			<RPC_CLIENTID></RPC_CLIENTID>
      			<RPC_CALLID>-2</RPC_CALLID>
      		</DATA>
      	</RECORD>
      	<RECORD>
      		<OPCODE>OP_CLOSE</OPCODE>
      		<DATA>
      			<TXID>134</TXID>
      			<LENGTH>0</LENGTH>
                  <INODEID>0</INODEID>
      			<PATH>/hello7.txt</PATH>
      			<REPLICATION>2</REPLICATION>
      			<MTIME>1512943608761</MTIME>
      			<ATIME>1512943607866</ATIME>
      			<BLOCKSIZE>134217728</BLOCKSIZE>
      			<CLIENT_NAME></CLIENT_NAME>
      			<CLIENT_MACHINE></CLIENT_MACHINE>
      			<OVERWRITE>false</OVERWRITE>
      			<BLOCK>
      				<BLOCK_ID>1073741839</BLOCK_ID>
      				<NUM_BYTES>25</NUM_BYTES>
      				<GENSTAMP>1016</GENSTAMP>
      			</BLOCK>
      			<PERMISSION_STATUS>
      				<USERNAME>atguigu</USERNAME>
      				<GROUPNAME>supergroup</GROUPNAME>
      				<MODE>420</MODE>
      			</PERMISSION_STATUS>
      		</DATA>
      	</RECORD>
      </EDITS >
      ```

      > NameNode如何确定下次开机启动的时候合并哪些Edits？

      ```shell
      [atguigu@hadoop102 current]$ cat seen_txid 
      429
      ```

      **将edits后缀大于429的全部合并（小于429已经合并完毕）**

### 10.3、CheckPoint时间设置

1. 通常情况下，SecondaryNameNode每隔一个小时执行一次

   **[hdfs-default.xml]**

   ```xml
   <property>
     <name>dfs.namenode.checkpoint.period</name>
     <value>3600s</value>
   </property>
   ```

2. 一分钟检查一次操作次数，当操作次数达到1百万时，SecondaryNameNode执行一次

   ```xml
   <property>
     	<name>dfs.namenode.checkpoint.txns</name>
     	<value>1000000</value>
   	<description>操作动作次数</description>
   </property>
   
   <property>
     	<name>dfs.namenode.checkpoint.check.period</name>
     	<value>60s</value>
   	<description> 1分钟检查一次操作次数</description>
   </property>
   ```

## 11、DataNode

### 11.1、DataNode工作机制

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217094945.png)

1. 一个数据块在DataNode上以文件形式存储在磁盘上，包括两个文件，一个是数据本身，一个是元数据包括数据块的长度，块数据的校验和，以及时间戳。

2. DataNode启动后向NameNode注册，通过后，周期性（6小时）的向NameNode上报所有的块信息。

   DN向NN汇报当前解读信息的时间间隔，默认6小时；

   ```xml
   <property>
   	<name>dfs.blockreport.intervalMsec</name>
   	<value>21600000</value>
   	<description>Determines block reporting interval in milliseconds.</description>
   </property>
   ```

   DN扫描自己节点块信息列表的时间，默认6小时

   ```xml
   <property>
   	<name>dfs.datanode.directoryscan.interval</name>
   	<value>21600s</value>
   	<description>Interval in seconds for Datanode to scan data directories and reconcile the difference between blocks in memory and on the disk.
   	Support multiple time unit suffix(case insensitive), as described
   	in dfs.heartbeat.interval.
   	</description>
   </property>
   ```

3. 心跳是每3秒一次，心跳返回结果带有NameNode给该DataNode的命令如复制块数据到另一台机器，或删除某个数据块。如果超过10分钟没有收到某个DataNode的心跳，则认为该节点不可用。

4. 集群运行中可以安全加入和退出一些机器。

### 11.2、数据完整性

> 如果电脑磁盘里面存储的数据是控制高铁信号灯的红灯信号（1）和绿灯信号（0），但是存储该数据的磁盘坏了，一直显示是绿灯，是否很危险？同理DataNode节点上的数据损坏了，却没有发现，是否也很危险，那么如何解决呢？

**如下是DataNode节点保证数据完整性的方法。**

1. 当DataNode读取Block的时候，它会计算CheckSum。

2. 如果计算后的CheckSum，与Block创建时值不一样，说明Block已经损坏。

3. Client读取其他DataNode上的Block。

4. 常见的校验算法crc（32），md5（128），sha1（160）

5. DataNode在其文件创建后周期验证CheckSum。

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217095242.png)

### 11.3、掉线时限参数设置

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217095332.png)

需要注意的是`hdfs-site.xml` 配置文件中的heartbeat.recheck.interval的单位为毫秒，dfs.heartbeat.interval的单位为**秒**。

```xml
<property>
    <name>dfs.namenode.heartbeat.recheck-interval</name>
    <value>300000</value>
</property>

<property>
    <name>dfs.heartbeat.interval</name>
    <value>3</value>
</property>
```

