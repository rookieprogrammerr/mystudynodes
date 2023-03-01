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
      ```

   3. 修改任意机器时间

      ```shell
      [atguigu@hadoop103 ~]$ sudo date -s "2021-9-11 11:11:11"
      ```

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

5. oiv查看Fsimage文件

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

6. oev查看Edits文件

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



## 12、MapReduce概述

### 12.1、MapReduce定义

- MapReduce是一个**分布式运算程序**的编程框架，是用户开发"**基于Hadoop的数据分析应用**"的核心框架。
- MapReduce核心功能是将**用户编写的业务逻辑代码**和**自带默认组件**整合成一个完整的**分布式运算程序**，并发运行在一个Hadoop集群上。

### 12.2、MapReduce优缺点

#### 12.2.1、优点

1. MapReduct易于编程

   **它简单的实现一些接口，就可以完成一个分布式程序，**这个分布式程序可以分布到大量廉价的PC机器上运行。也就是说你写一个分布式程序，跟写一个简单的串行程序是一模一样的。就是因为这个特点使得MapReduce编程变得非常流行。

2. 良好的扩展性

   当你的计算资源不能得到满足的时候，你可以通过**简单的增加机器**来扩展它的计算能力。

3. 高容错性

   MapReduce设计的初衷就是使程序能够部署在廉价的PC机器上，这就要求它具有很高的容错性。比如**其中一台机器挂了，它可以把上面的计算任务转移到另外一个节点上运行，不至于这个任务运行失败，**而且这个过程不需要人工参与，而完全是由Hadoop内部完成的。

4. 适合PB级以上海量数据的离线处理

   可以实现上千台服务器集群并发工作，提供数据处理能力。

#### 12.2.2、缺点

1. 不擅长实时计算

   MapReduce无法像MySQL一样，在毫秒或者秒级内返回结果。

2. 不擅长流式计算

   流式计算的输入数据是动态的，而MapReduce的**输入数据集是静态的**，不能动态变化。这是因为MapReduce自身的设计特点决定了数据源必须是静态的。

3. 不擅长DAG（有向无环图）计算

   多个应用程序存在依赖关系，后一个应用程序的输入为前一个的输出。在这种情况下，MapReduce并不是不能做，而是使用后，**每个MapReduce作业的输出结果都会写入到磁盘，会造成大量的磁盘IO，导致性能非常的低下。**

### 12.3、MapReduct核心思想

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217130839.png)

1. 分布式的运算程序往往需要分成至少2个阶段。
2. 第一个阶段的MapTask并发实例，完全并行运行，互不相干。
3. 第二个阶段的ReduceTask并发实例互不相干，但是他们的数据依赖于上一个阶段的所有MapTask并发实例的输出。
4. MapReduce编程模型只能包含一个Map阶段和一个Reduce阶段，如果用户的业务逻辑非常复杂，那就只能多个MapReduce程序，串行运行。

**总结：分析WordCount数据流走向深入理解MapReduce核心思想。**

### 12.4、MapReduce进程

一个完整的MapReduce程序在分布式运行时有三类实例进程：

1. **MrAppMaster**：负责整个程序的过程调度及状态协调。
2. **MapTask**：负责Map阶段的整个数据处理流程。
3. **ReductTask**：负责Reduce阶段的整个数据处理流程。

### 12.5、官方WordCount源码

采用反编译工具反编译源码，发现WordCount案例有Map类、Reduce类和驱动类。且数据的类型是Hadoop自身封装的序列化类型。

### 12.6、常用数据序列化类型

| **Java类型** | **Hadoop Writable类型** |
| ------------ | ----------------------- |
| Boolean      | BooleanWritable         |
| Byte         | ByteWritable            |
| Int          | IntWritable             |
| Float        | FloatWritable           |
| Long         | LongWritable            |
| Double       | DoubleWritable          |
| String       | Text                    |
| Map          | MapWritable             |
| Array        | ArrayWritable           |
| Null         | NullWritable            |

### 12.7、MapReduce编程规范

用户编写的程序分成三个部分：Mapper、Reducer和Driver。

1. Mapper阶段

    1. 用户自定义的Mapper要继承自己的父类
    2. Mapper的输入数据是KV对的形式（KV的类型可自定义）
    3. Mapper中的业务逻辑写在`map()`方法中
    4. Mapper的输出数据是KV对的形式（KV的类型可自定义）
    5. **map()方法（MapTask进程）对每一个<K,V>调用一次**

2. Reducer阶段

    1. 用户自定义的Reducer要继承自己的父类
    2. Reducer的输入数据类型对应Mapper的输出数据类型，也是KV
    3. Reducer的业务逻辑写在`reduce()`方法中
    4. **ReduceTask进程对每一组相同K的<K,V>组调用一次reduce()方法**

3. Driver阶段

   相当于YARN集群的客户端，用于提交我整个程序到YARN集群，提交的是封装了MapReduce程序相关运行参数的job对象

### 12.8、WordCount案例实操

#### 12.8.1、本地测试

1. 需求

   在给定的文本文件中统计输出每一个单词出现的总次数

    1. 输入数据（hello.txt）

    2. 期望输出数据

       ```shell
       atguigu	2
       banzhang	1
       cls	2
       hadoop	1
       jiao	1
       ss	2
       xue	1

2. 需求分析

   按照MapReduce编程规范，分别编写Mapper，Reducer，Driver。

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217135630.png)

3. 环境准备

    1. 创建maven工程，MapReduceDemo

    2. 在pom.xml文件中添加如下依赖

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

    3. 在项目的src/main/resources目录下，新建一个文件，命名为“log4j.properties”，在文件中填入。

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

    4. 创建包名：com.atguigu.mapreduce.wordcount

4. 编写程序本地测试

    1. 编写Mapper类

       ```java
       package com.atguigu.mapreduce.wordcount;
       
       import java.io.IOException;
       import org.apache.hadoop.io.IntWritable;
       import org.apache.hadoop.io.LongWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Mapper;
       
       /**
        * KEYIN：map阶段输入的key类型：LongWritable
        * VALUEIN：map阶段输入的value类型：Text
        * KEYOUT：map阶段输出的key类型：Text
        * VALUEOUT：map阶段输出的value类型：IntWritable
        */
       public class WordCountMapper extends Mapper<LongWritable, Text, Text, IntWritable>{
           
           Text k = new Text();
           IntWritable v = new IntWritable(1);
           
           @Override
           protected void map(LongWritable key, Text value, Context context)	throws IOException, InterruptedException {
               
               // 1 获取一行
               String line = value.toString();
               
               // 2 切割
               String[] words = line.split(" ");
               
               // 3 输出
               for (String word : words) {
                   k.set(word);
                   context.write(k, v);
               }
           }
       }
       ```

    2. 编写Reducer类

       ```java
       package com.atguigu.mapreduce.wordcount;
       
       import java.io.IOException;
       import org.apache.hadoop.io.IntWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Reducer;
       
       /**
        * KEYIN：reduce阶段输入的key类型：Text
        * VALUEIN：reduce阶段输入的value类型：IntWritable
        * KEYOUT：reduce阶段输出的key类型：Text
        * VALUEOUT：reduce阶段输出的value类型：IntWritable
        */
       public class WordCountReducer extends Reducer<Text, IntWritable, Text, IntWritable>{
       
           int sum;
           IntWritable v = new IntWritable();
       
           @Override
           protected void reduce(Text key, Iterable<IntWritable> values,Context context) throws IOException, InterruptedException {
               // 1 累加求和
               sum = 0;
               for (IntWritable count : values) {
                   sum += count.get();
               }
               
               // 2 输出
                v.set(sum);
               context.write(key,v);
           }
       }
       ```

    3. 编写Driver驱动类

       ```java
       package com.atguigu.mapreduce.wordcount;
       import java.io.IOException;
       import org.apache.hadoop.conf.Configuration;
       import org.apache.hadoop.fs.Path;
       import org.apache.hadoop.io.IntWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Job;
       import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
       import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
       
       public class WordCountDriver {
       
           public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
               // 1 获取配置信息以及获取job对象
               Configuration conf = new Configuration();
               Job job = Job.getInstance(conf);
       
               // 2 关联本Driver程序的jar
               job.setJarByClass(WordCountDriver.class);
       
               // 3 关联Mapper和Reducer的jar
               job.setMapperClass(WordCountMapper.class);
               job.setReducerClass(WordCountReducer.class);
       
               // 4 设置Mapper输出的kv类型
               job.setMapOutputKeyClass(Text.class);
               job.setMapOutputValueClass(IntWritable.class);
       
               // 5 设置最终输出kv类型
               job.setOutputKeyClass(Text.class);
               job.setOutputValueClass(IntWritable.class);
               
               // 6 设置输入和输出路径
               FileInputFormat.setInputPaths(job, new Path(args[0]));
               FileOutputFormat.setOutputPath(job, new Path(args[1]));
       
               // 7 提交job
               boolean result = job.waitForCompletion(true);
               System.exit(result ? 0 : 1);
           }
       }
       ```

5. 本地测试

    1. 需要首先配置好HADOOP_HOME变量以及Windows运行依赖
    2. 在IDEA/Eclipse上运行程序

#### 12.8.2、提交到集群测试

集群上测试

1. 用Maven打jar包，需要添加的打包插件依赖

   ```xml
   <build>
       <plugins>
           <plugin>
               <artifactId>maven-compiler-plugin</artifactId>
               <version>3.6.1</version>
               <configuration>
                   <source>1.8</source>
                   <target>1.8</target>
               </configuration>
           </plugin>
           <plugin>
               <artifactId>maven-assembly-plugin</artifactId>
               <configuration>
                   <descriptorRefs>
                       <descriptorRef>jar-with-dependencies</descriptorRef>
                   </descriptorRefs>
               </configuration>
               <executions>
                   <execution>
                       <id>make-assembly</id>
                       <phase>package</phase>
                       <goals>
                           <goal>single</goal>
                       </goals>
                   </execution>
               </executions>
           </plugin>
       </plugins>
   </build>
   ```

   **注意：如果工程上显示红叉。在项目上右键->maven->Reimport刷新即可。**

2. 将程序打成jar包

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217151204.png)

3. 修改不带依赖的jar包名称为wc.jar，并拷贝该jar包到Hadoop集群的/opt/module/hadoop-3.1.3路径。

4. 启动Hadoop集群

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]sbin/start-dfs.sh
   [atguigu@hadoop103 hadoop-3.1.3]$ sbin/start-yarn.sh
   ```

5. 执行WordCount程序

   ```shell
   [atguigu@hadoop102 hadoop-3.1.3]$ hadoop jar  wc.jar
    com.atguigu.mapreduce.wordcount.WordCountDriver /user/atguigu/input /user/atguigu/output
   ```

## 13、Hadoop序列化

### 13.1、序列化概述

1. 什么是序列化

    - 序列化就是把内存中的对象，转换成字节序列（或其他数据传输协议）以便于存储到磁盘（持久化）和网络传输。
    - 反序列化就是将收到字节序列（或其他数据传输协议）或者是磁盘的持久化数据，转换成内存中的对象。

2. 为什么要序列化

   一般来说，“活的”对象只生存在内存里，关机断电就没有了。而且“活的”对象只能由本地的进程使用，不能被发送到网络上的另外一台计算机。 然而**序列化可以存储“活的”对象，可以将“活的”对象发送到远程计算机。**

3. 为什么不用Java的序列化

   Java的序列化是一个重量级序列化框架（Serializable），一个对象被序列化后，会附带很多额外的信息（各种校验信息，Header，继承体系等），不便于在网络中高效传输。所以，Hadoop自己开发了一套序列化机制（Writable）。

4. Hadoop序列化特点：

    1. 紧凑：高效使用存储空间
    2. 快速：读写数据的额外开销小
    3. 互操作：支持多语言的交互

### 13.2、自定义bean对象实现序列化接口（Writable）

在企业开发中往往常用的基本序列化类型不能满足所有需求，比如在Hadoop框架内部传递一个bean对象，那么该对象就需要实现序列化接口。

**具体实现bean对象序列化步骤如下7步。**

1. 必须实现Writable接口

2. 反序列化时，需要反射调用空参构造函数，所以必须有空参构造

   ```java
   public FlowBean() {
   	super();
   }
   ```

3. 重写序列化方法

   ```java
   @Override
   public void write(DataOutput out) throws IOException {
   	out.writeLong(upFlow);
   	out.writeLong(downFlow);
   	out.writeLong(sumFlow);
   }
   ```

4. 重写反序列化方法

   ```java
   @Override
   public void readFields(DataInput in) throws IOException {
   	upFlow = in.readLong();
   	downFlow = in.readLong();
   	sumFlow = in.readLong();
   }
   ```

5. **注意反序列化的顺序和序列化的顺序完全一致**

6. 要想把结果显示在文件中，需要重写toString()，可用"\t"分开，方便后续用。

7. 如果需要将自定义的bean放在key中传输，则还需要实现Comparable接口，因为MapReduce框中的Shuffle过程要求对key必须能排序。**详见后面排序案例。**

   ```java
   @Override
   public int compareTo(FlowBean o) {
   	// 倒序排列，从大到小
   	return this.sumFlow > o.getSumFlow() ? -1 : 1;
   }
   ```


### 13.3、序列化案例实操

1. 需求

   统计每一个手机号耗费的总上行流量、总下行流量、总流量

    1. 输入数据

       ```txt
       1	13736230513	192.196.100.1	www.atguigu.com	2481	24681	200
       2	13846544121	192.196.100.2			264	0	200
       3 	13956435636	192.196.100.3			132	1512	200
       4 	13966251146	192.168.100.1			240	0	404
       5 	18271575951	192.168.100.2	www.atguigu.com	1527	2106	200
       6 	84188413	192.168.100.3	www.atguigu.com	4116	1432	200
       7 	13590439668	192.168.100.4			1116	954	200
       8 	15910133277	192.168.100.5	www.hao123.com	3156	2936	200
       9 	13729199489	192.168.100.6			240	0	200
       10 	13630577991	192.168.100.7	www.shouhu.com	6960	690	200
       11 	15043685818	192.168.100.8	www.baidu.com	3659	3538	200
       12 	15959002129	192.168.100.9	www.atguigu.com	1938	180	500
       13 	13560439638	192.168.100.10			918	4938	200
       14 	13470253144	192.168.100.11			180	180	200
       15 	13682846555	192.168.100.12	www.qq.com	1938	2910	200
       16 	13992314666	192.168.100.13	www.gaga.com	3008	3720	200
       17 	13509468723	192.168.100.14	www.qinghua.com	7335	110349	404
       18 	18390173782	192.168.100.15	www.sogou.com	9531	2412	200
       19 	13975057813	192.168.100.16	www.baidu.com	11058	48243	200
       20 	13768778790	192.168.100.17			120	120	200
       21 	13568436656	192.168.100.18	www.alibaba.com	2481	24681	200
       22 	13568436656	192.168.100.19			1116	954	200

    2. 输入数据格式

       ```txt
       7 	13560436666	120.196.100.99		1116		 954			200
       id	手机号码		网络ip			上行流量  下行流量     网络状态码
       ```

    3. 期望输出数据格式

       ```txt
       13560436666 		1116		      954 			2070
       手机号码		    上行流量        下行流量		总流量
       ```

2. 需求分析

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230220104916.png)

3. 编写MapReduce程序

    1. 编写流量统计的Bean对象

       ```java
       package com.atguigu.mapreduce.writable;
       
       import org.apache.hadoop.io.Writable;
       import java.io.DataInput;
       import java.io.DataOutput;
       import java.io.IOException;
       
       //1 继承Writable接口
       public class FlowBean implements Writable {
       
           private long upFlow; //上行流量
           private long downFlow; //下行流量
           private long sumFlow; //总流量
       
           //2 提供无参构造
           public FlowBean() {
           }
       
           //3 提供三个参数的getter和setter方法
           public long getUpFlow() {
               return upFlow;
           }
       
           public void setUpFlow(long upFlow) {
               this.upFlow = upFlow;
           }
       
           public long getDownFlow() {
               return downFlow;
           }
       
           public void setDownFlow(long downFlow) {
               this.downFlow = downFlow;
           }
       
           public long getSumFlow() {
               return sumFlow;
           }
       
           public void setSumFlow(long sumFlow) {
               this.sumFlow = sumFlow;
           }
       
           public void setSumFlow() {
               this.sumFlow = this.upFlow + this.downFlow;
           }
       
           //4 实现序列化和反序列化方法,注意顺序一定要保持一致
           @Override
           public void write(DataOutput dataOutput) throws IOException {
               dataOutput.writeLong(upFlow);
               dataOutput.writeLong(downFlow);
               dataOutput.writeLong(sumFlow);
           }
       
           @Override
           public void readFields(DataInput dataInput) throws IOException {
               this.upFlow = dataInput.readLong();
               this.downFlow = dataInput.readLong();
               this.sumFlow = dataInput.readLong();
           }
       
           //5 重写ToString
           @Override
           public String toString() {
               return upFlow + "\t" + downFlow + "\t" + sumFlow;
           }
       }
       ```

    2. 编写Mapper类

       ```java
       package com.atguigu.mapreduce.writable;
       
       import org.apache.hadoop.io.LongWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Mapper;
       import java.io.IOException;
       
       public class FlowMapper extends Mapper<LongWritable, Text, Text, FlowBean> {
           private Text outK = new Text();
           private FlowBean outV = new FlowBean();
       
           @Override
           protected void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
       
               //1 获取一行数据,转成字符串
               String line = value.toString();
       
               //2 切割数据
               String[] split = line.split("\t");
       
               //3 抓取我们需要的数据:手机号,上行流量,下行流量
               String phone = split[1];
               String up = split[split.length - 3];
               String down = split[split.length - 2];
               //4 封装outK outV
               outK.set(phone);
               outV.setUpFlow(Long.parseLong(up));
               outV.setDownFlow(Long.parseLong(down));
               outV.setSumFlow();
       
               //5 写出outK outV
               context.write(outK, outV);
           }
       }
       ```

    3. 编写Reducer类

       ```java
       package com.atguigu.mapreduce.writable;
       
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Reducer;
       import java.io.IOException;
       
       public class FlowReducer extends Reducer<Text, FlowBean, Text, FlowBean> {
           private FlowBean outV = new FlowBean();
           @Override
           protected void reduce(Text key, Iterable<FlowBean> values, Context context) throws IOException, InterruptedException {
       
               long totalUp = 0;
               long totalDown = 0;
       
               //1 遍历values,将其中的上行流量,下行流量分别累加
               for (FlowBean flowBean : values) {
                   totalUp += flowBean.getUpFlow();
                   totalDown += flowBean.getDownFlow();
               }
       
               //2 封装outKV
               outV.setUpFlow(totalUp);
               outV.setDownFlow(totalDown);
               outV.setSumFlow();
       
               //3 写出outK outV
               context.write(key,outV);
           }
       }
       ```

    4. 编写Driver驱动类

       ```java
       package com.atguigu.mapreduce.writable;
       
       import org.apache.hadoop.conf.Configuration;
       import org.apache.hadoop.fs.Path;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Job;
       import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
       import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
       import java.io.IOException;
       
       public class FlowDriver {
           public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
       
               //1 获取job对象
               Configuration conf = new Configuration();
               Job job = Job.getInstance(conf);
               //2 关联本Driver类
               job.setJarByClass(FlowDriver.class);
       
               //3 关联Mapper和Reducer
               job.setMapperClass(FlowMapper.class);
               job.setReducerClass(FlowReducer.class);
               
               //4 设置Map端输出KV类型
               job.setMapOutputKeyClass(Text.class);
               job.setMapOutputValueClass(FlowBean.class);
               
               //5 设置程序最终输出的KV类型
               job.setOutputKeyClass(Text.class);
               job.setOutputValueClass(FlowBean.class);
               
               //6 设置程序的输入输出路径
               FileInputFormat.setInputPaths(job, new Path("D:\\inputflow"));
               FileOutputFormat.setOutputPath(job, new Path("D:\\flowoutput"));
               
               //7 提交Job
               boolean b = job.waitForCompletion(true);
               System.exit(b ? 0 : 1);
           }
       }
       ```

## 14、MapReduce框架原理

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230220105218.png)

### 14.1、InputFormat数据输入

#### 14.1.1、切片与MapTask并行度决定机制

1. 问题引出

   MapTask的并行度决定Map阶段的任务处理并发度，进而影响到整个Job的处理速度。

   > 1G的数据，启动8个MapTask，可以提高集群的并发处理能力。那么1K的数据，也启动8个MapTask，会提高集群性能吗？MapTask并行任务是否越多越好呢？哪些因素影响了MapTask并行度？

2. MapTask并行度决定机制

    - 数据块：Block是HDFS物理上把数据分成一块一块。数据块是HDFS存储数据单位。

    - 数据切片：数据切片只是在逻辑上对输入进行分片，并不会在磁盘上将其切分成片进行存储。数据切片是MapReduce程序计算输入数据的单位，一个切片会对应启动一个MapTask。

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230220132624.png)

#### 14.1.2、Job提交流程源码和切片源码详解

1. Job提交流程源码详解

   ```java
   waitForCompletion()
   
   submit();
   
   // 1建立连接
   	connect();	
           // 1）创建提交Job的代理
           new Cluster(getConfiguration());
           // （1）判断是本地运行环境还是yarn集群运行环境
           initialize(jobTrackAddr, conf); 
   
   	// 2 提交job
   	submitter.submitJobInternal(Job.this, cluster)
   
   	// 1）创建给集群提交数据的Stag路径
   	Path jobStagingArea = JobSubmissionFiles.getStagingDir(cluster, conf);
   
   	// 2）获取jobid ，并创建Job路径
   	JobID jobId = submitClient.getNewJobID();
   
   	// 3）拷贝jar包到集群
   	copyAndConfigureFiles(job, submitJobDir);	
   	rUploader.uploadFiles(job, jobSubmitDir);
   
   	// 4）计算切片，生成切片规划文件
   	writeSplits(job, submitJobDir);
   	maps = writeNewSplits(job, jobSubmitDir);
   	input.getSplits(job);
   
   	// 5）向Stag路径写XML配置文件
   	writeConf(conf, submitJobFile);
   	conf.writeXml(out);
   
   	// 6）提交Job,返回提交状态
   	status = submitClient.submitJob(jobId, submitJobDir.toString(), job.getCredentials());
   ```

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230220132844.png)

2. FileInputFormat切片源码解析（input.getSplits(job)）

    1. 程序先找到你数据存储的目录

    2. 开始遍历处理（规划切片）目录下的每一个文件

    3.  遍历第一个文件`ss.txt`

    - 获取文件大小`fs.sizeOf(ss.txt)`

    - 计算切片大小

    - **默认情况下，切片大小=blocksize**

    - 开始切，形成第1个切片：ss.txt——0:128M 第2个切片ss.txt——128:256M 第3个切片ss.txt——256:300M

      **（每次切片时，都要判断切完省下的部分是否大于块的1.1倍，不大于1.1倍就划分一块切片）**

    - 将切片信息写到一个切片规划文件中

    - 整个切片的核心过程在`getSplit()`方法中完成

    - **InputSplit只记录了切片的元数据信息**，比如起始位置、长度以及所在的节点列表等。

    4. **提交切片规划文件到YARN上，YARN上的MrAppMaster就可以根据切片规划文件计算开启MapTask个数。**

#### 14.1.3、FileInputFormat切片机制

1. 切片机制

    1. 简单地按照文件的内容长度进行切片
    2. 切片大小，默认等于Block大小
    3. **切片时不考虑数据集整体，而是逐个针对每一个文件单独切片**

2. 案例分析

    1. 输入数据有两个文件

       ```txt
       file1.txt	320M
       file2.txt	10M
       ```

    2. 经过FileInputFormat的切片机制运算后，形成的切片信息如下

       ```txt
       file1.txt.split1--	0~128
       file1.txt.split2--	128~256
       file1.txt.split3--	256~320
       file2.txt.split1--	0~10
       ```

3. FileInputFormat切片大小的参数配置

    1. 源码中计算切片大小的公式

       ```java
       Math.max(minSize,Math.min(maxSize,blockSize));
       mapreduce.input.fileinputformat.split.minsize=1	//默认值为1
       mapreduce.input.fileinputformat.split.maxsize=Long.MAXValue	//默认值Long.MAXValue
       ```

       **因此，默认情况下，切片大小=blocksize**

    2. 切片大小设置

        - maxsize（切片最大值）：参数如果调得比blockSize小，则会让切片变小，而且就等于配置的这个参数的值。
        - minsize（切片最小值）：参数调的比blockSize大，则可以让切片变得比blockSize还大。

    3. 获取切片信息API

       ```java
       //	获取切片的文件名称
       String name = inputSplit.getPath().getName();
       //	根据文件类型获取切片信息
       FileSplit inputSplit = (FileSplit) context.getInputSplit();
       ```

#### 14.1.4、TextInputFormat

1. FileInputFormat实现类

   > 在运行MapReduce程序时，输入的文件格式包括：基于行的日志文件、二进制格式文件、数据库表等。那么，针对不同的数据类型，MapReduce是如何读取这些数据的呢？

   FileInputFormat常见的接口实现类包括：**TextInputFormat、KeyValueTextInputFormat、NLineInputFormat、CombineTextInputFormat和自定义InputFormat**等。

2. TextInputFormat

   TextInputFormat是默认的FileInputFormat实现类。按行读取每条记录。**键是存储该行在整个文件中的起始字节偏移量， LongWritable类型。值是这行的内容，不包括任何行终止符（换行符和回车符），Text类型。**

   以下时一个示例，比如，一个分片包含了如下4条文本记录。

   ```txt
   Rich learning form
   Intelligent learning engine
   Learning more convenient
   From the real demand for more close to the enterprise
   ```

   每条记录表示为以下键/值对：

   ```txt
   (0,Rich learning form)
   (20,Intelligent learning engine)
   (49,Learning more convenient)
   (74,From the real demand for more close to the enterprise)
   ```

#### 14.1.5、CombineTextInputFormat切片机制

框架默认的TextInputFormat切片机制是对任务按文件规划切片，不管文件多小，都会是一个单独的切片，都会交给一个MapTask，这样如果有大量小文件，就会产生大量的MapTask，处理效率极其低下。

1. 应用场景

   CombineTextInputFormat用于小文件过多的场景，它可以将多个小文件从逻辑上规划到一个切片中，这样，多个小文件就可以交给一个MapTask处理。

2. 虚拟存储切片最大值设置

   ```java
   CombineTextInputFormat.setMaxInputSplitSize(job, 4194304);// 4m
   ```

   注意：虚拟存储切片最大值设置最好根据实际的小文件大小情况来设置具体的值。

3. 切片机制

   生成切片过程包括：虚拟存储过程和切片过程二部分。

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230220141125.png)

    1. 虚拟存储过程
        - 将输入目录下所有文件大小，依次和设置的setMaxInputSplitSize值比较，如果不大于设置的最大值，逻辑上划分一个块。如果输入文件大于设置的最大值且大于两倍，那么以最大值切割一块；**当剩余数据大小超过设置的最大值且不大于最大值2倍，此时将文件均分成2个虚拟存储块（防止出现太小切片）。**
        - 例如setMaxInputSplitSize值为4M，输入文件大小为8.02M，则先逻辑上分成一个4M。剩余的大小为4.02M，如果按照4M逻辑划分，就会出现0.02M的小的虚拟存储文件，所以将剩余的4.02M文件切分成（2.01M和2.01M）两个文件。
    2. 切片过程
        - 判断虚拟存储的文件大小是否大于setMaxInputSplitSize值，大于等于则单独形成一个切片。
        - 如果不大于则跟下一个虚拟存储文件进行合并，共同形成一个切片。
        - **测试举例：有4个小文件大小分别为1.7M、5.1M、3.4M以及6.8M这四个小文件，则虚拟存储之后形成6个文件块，大小分别为：**
            - **1.7M，（2.55M、2.55M），3.4M以及（3.4M、3.4M）**
            - **最终会形成3个切片，大小分别为：**
            - **（1.7+2.55）M，（2.55+3.4）M，（3.4+3.4）M**

#### 14.1.6、CombineTextInputFormat案例实操

1. 需求

   将输入的大量小文件合并成一个切片统一处理。

    1. 输入数据

       准备4个小文件（4个txt文件）

    2. 期望

       期望一个切片处理4个文件

2. 实现过程

    1. 不做任何处理，运行1.8节的WordCount案例程序，观察切片个数为4。

       ```java
       number of splits:4
       ```

    2. 在WordcountDriver中增加如下代码，运行程序，并观察运行的切片个数为3。

        - 驱动类中添加代码如下：

          ```java
          // 如果不设置InputFormat，它默认用的是TextInputFormat.class
          job.setInputFormatClass(CombineTextInputFormat.class);
          
          //虚拟存储切片最大值设置4m
          CombineTextInputFormat.setMaxInputSplitSize(job, 4194304);
          ```

        - 运行如果为3个切片

          ```java
          number of splits:3
          ```

    3. 在WordcountDriver中增加如下代码，运行程序，并观察运行的切片个数为1。

        - 驱动中添加代码如下：

          ```java
          // 如果不设置InputFormat，它默认用的是TextInputFormat.class
          job.setInputFormatClass(CombineTextInputFormat.class);
          
          //虚拟存储切片最大值设置20m
          CombineTextInputFormat.setMaxInputSplitSize(job, 20971520);
          ```

        - 运行如果为1个切片

          ```java
          number of splits:1
          ```

### 14.2、MapReduce工作流程

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230222134557.png)

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230222134609.png)

上面的流程是整个MapReduce最全工作流程，但是Shuffle过程只是从第7步开始到第16步结束，具体Shuffle过程详解，如下：

1. MapTask收集我们的map()方法输出的kv对，放到内存缓冲区中
2. 从内存缓冲区不断溢出本地磁盘文件，可能会溢出多个文件
3. 多个溢出文件会被合并成大的溢出文件
4. 在溢出过程及合并的过程中，都要调用Partitioner进行分区和针对key进行排序
5. ReduceTask根据自己的分区号，去各个MapTask机器上取相应的结果分区数据
6. ReduceTask会抓取到同一个分区的来自不同MapTask的结果文件，ReduceTask会将这些文件再进行合并（归并排序）
7. 合并成大文件后，Shuffle的过程也就结束了，后面进入ReduceTask的逻辑运算过程（从文件中取出一个一个的键值对Group，调用用户自定义的reduce()方法）

**注意：**

1. Shuffle中的缓冲区大小会影响到MapReduce程序的执行效率，原则上说，缓冲区越大，磁盘io的次数越少，执行速度就越快。
2. 缓冲区的大小可以通过参数调整，参数：mapreduce.task.io.sort.mb默认100M。

### 14.3、Shuffle机制

#### 14.3.1、Shuffle机制

Map方法之后，Reduce方法之前的数据处理过程称之为Shuffle。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230222134903.png)

#### 14.3.2、Partition分区

1. 问题引出

   > 要求将统计结果按照条件输出到不同文件中（分区）。比如：将统计结果按照手机归属地不同省份输出到不同文件中（分区）

2. 默认Partition分区

   ```java
   public class HashPartitioner<K,V> extends Partitioner<K, V> {
   	public int getPartition(K key, V value, int numReduceTasks) {
   		return(key.hashCode() & Integer.MAX VALUE) * numReduceTasks,
   	}
   }
   ```

   **默认分区时根据key的hashCode对ReduceTasks个数取模得到的。用户没法控制哪个key存储到哪个分区。**

3. 自定义Partition步骤

    1. 自定义类继承`Partitioner`，重写`getPartition()`方法

       ```java
       public class CustomPartitioner extends Partitioner<Text, FlowBean> {
           @Override
           public int getpartition(Text key, FlowBean value, int numPartitions) {
               // 控制分区代码逻辑
               … …
               return partition,
           }
       }
       ```

    2. 在Job驱动中，设置自定义`Partitioner`

       ```java
       job.setPartitionerClass(CustomPartitioner.class);
       ```

    3. 自定义Partition后，要根据自定义Partitioner的逻辑设置相应数量的ReduceTask

       ```java
       job.setNumReduceTasks(5);
       ```

4. 分区总结

    1. **如果ReduceTask的数量 > getPartition的结果数，则会多生产几个空的输出文件`part-r-000xx`;**
    2. **如果1 < ReductTask的数量 < getPartition 的结果数，则有一部分分区数据无处安放，会Exception;**
    3. **如果ReductTask的数量 = 1，则不管MapTask端输出多少个分区文件，最终结果都交给这一个ReductTask，最终也就只会产生一个结果文件`part-r-00000`;**
    4. **分区号必须从零开始，逐一累加。**

5. 案例分析

   例如：假设自定义分区数为5，则：

    1. job.setNumReduceTasks(1)：会正常运行，只不过会产生一个输出文件
    2. job.setNumReduceTasks(2)：会报错
    3. job.setNumReduceTasks(6)：大于5，程序会正常运行，会产生空文件

#### 14.3.3、Partition分区案例实操

1. 需求

   将统计结果按照手机归属地不同省份输出到不同文件中（分区）

    1. 输入数据

       ```txt
       1	13736230513	192.196.100.1	www.atguigu.com	2481	24681	200
       2	13846544121	192.196.100.2			264	0	200
       3 	13956435636	192.196.100.3			132	1512	200
       4 	13966251146	192.168.100.1			240	0	404
       5 	18271575951	192.168.100.2	www.atguigu.com	1527	2106	200
       6 	84188413	192.168.100.3	www.atguigu.com	4116	1432	200
       7 	13590439668	192.168.100.4			1116	954	200
       8 	15910133277	192.168.100.5	www.hao123.com	3156	2936	200
       9 	13729199489	192.168.100.6			240	0	200
       10 	13630577991	192.168.100.7	www.shouhu.com	6960	690	200
       11 	15043685818	192.168.100.8	www.baidu.com	3659	3538	200
       12 	15959002129	192.168.100.9	www.atguigu.com	1938	180	500
       13 	13560439638	192.168.100.10			918	4938	200
       14 	13470253144	192.168.100.11			180	180	200
       15 	13682846555	192.168.100.12	www.qq.com	1938	2910	200
       16 	13992314666	192.168.100.13	www.gaga.com	3008	3720	200
       17 	13509468723	192.168.100.14	www.qinghua.com	7335	110349	404
       18 	18390173782	192.168.100.15	www.sogou.com	9531	2412	200
       19 	13975057813	192.168.100.16	www.baidu.com	11058	48243	200
       20 	13768778790	192.168.100.17			120	120	200
       21 	13568436656	192.168.100.18	www.alibaba.com	2481	24681	200
       22 	13568436656	192.168.100.19			1116	954	200
       ```

    2. 期望输出数据

       手机号136、137、138、139开头都分别放到一个独立的4个文件中，其他开头的放到一个文件中。

2. 需求分析

    1. 需求：将统计结果按照手机归属地不同省份输出到不同文件中（分区）

    2. 数据输入

       ```txt
       13630577991		6960	690
       13736230513		2481	24681
       13846544121		264		0
       13956435636		132		1512
       13560439638		918		4938
       ```

    3. 期望数据输出

       ```txt
       文件1
       文件2
       文件3
       文件4
       文件5
       ```

    4. 增加一个`ProvincePartitioner`分区

       ```txt
       136		分区0
       137		分区1
       138		分区2
       139		分区3
       其他	   分区4
       ```

    5. Driver驱动类

       ```java
       //指定自定义数据分区
       job.setPartitionerClass(ProvincePartitioner.class);
       //同时指定相应数量的reduceTask
       job.setNumReduceTasks(5);
       ```

3. 在案例13.3的基础上，增加一个分区类

   ```java
   package com.atguigu.mapreduce.partitioner;
   
   import org.apache.hadoop.io.Text;
   import org.apache.hadoop.mapreduce.Partitioner;
   
   public class ProvincePartitioner extends Partitioner<Text, FlowBean> {
   
       @Override
       public int getPartition(Text text, FlowBean flowBean, int numPartitions) {
           //获取手机号前三位prePhone
           String phone = text.toString();
           String prePhone = phone.substring(0, 3);
   
           //定义一个分区号变量partition,根据prePhone设置分区号
           int partition;
   
           if("136".equals(prePhone)){
               partition = 0;
           }else if("137".equals(prePhone)){
               partition = 1;
           }else if("138".equals(prePhone)){
               partition = 2;
           }else if("139".equals(prePhone)){
               partition = 3;
           }else {
               partition = 4;
           }
   
           //最后返回分区号partition
           return partition;
       }
   }
   ```

4. 在驱动函数中增加自定义数据分区设置和ReduceTask设置

   ```java
   package com.atguigu.mapreduce.partitioner;
   
   import org.apache.hadoop.conf.Configuration;
   import org.apache.hadoop.fs.Path;
   import org.apache.hadoop.io.Text;
   import org.apache.hadoop.mapreduce.Job;
   import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
   import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
   import java.io.IOException;
   
   public class FlowDriver {
   
       public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
   
           //1 获取job对象
           Configuration conf = new Configuration();
           Job job = Job.getInstance(conf);
   
           //2 关联本Driver类
           job.setJarByClass(FlowDriver.class);
   
           //3 关联Mapper和Reducer
           job.setMapperClass(FlowMapper.class);
           job.setReducerClass(FlowReducer.class);
   
           //4 设置Map端输出数据的KV类型
           job.setMapOutputKeyClass(Text.class);
           job.setMapOutputValueClass(FlowBean.class);
   
           //5 设置程序最终输出的KV类型
           job.setOutputKeyClass(Text.class);
           job.setOutputValueClass(FlowBean.class);
   
           //8 指定自定义分区器
           job.setPartitionerClass(ProvincePartitioner.class);
   
           //9 同时指定相应数量的ReduceTask
           job.setNumReduceTasks(5);
   
           //6 设置输入输出路径
           FileInputFormat.setInputPaths(job, new Path("D:\\inputflow"));
           FileOutputFormat.setOutputPath(job, new Path("D\\partitionout"));
   
           //7 提交Job
           boolean b = job.waitForCompletion(true);
           System.exit(b ? 0 : 1);
       }
   }
   ```

#### 14.3.4、WritableComparable排序

排序是MapReduce框架中最重要的操作之一

- MapTask和ReduceTask均会对数据**按照key**进行排序。该操作属于Hadoop的默认行为。**任何应用程序中的数据均会被排序，而不管逻辑上是否需要。**
- 默认排序是按照**字典顺序排序，**且实现该排序的方法是**快速排序。**
- 对于MapTask，它会将处理的结果暂时放到环形缓冲区，**当环形缓冲区使用率达到一定阈值后，再对缓冲区的数据进行一次快速排序**，并将这些有序数据溢写到磁盘上，而当数据处理完毕后，它会**对磁盘上所有文件进行并归排序。**
- 对于ReduceTask，它从每个MapTask上远程拷贝相应的数据文件，如果文件大小超过一定阈值，则溢写磁盘上，否则存储在内存中。如果磁盘上文件数目达到一定阈值，则进行一次归并排序以生成一个更大文件；如果内存中文件大小或者数目超过一定阈值，则进行一次合并后将数据溢写到磁盘上。当所有数据拷贝完毕后，**ReduceTask统一对内存和磁盘上的所有数据进行一次归并排序。**

1. 部分排序

   MapReduce根据输入记录的键对数据集排序。保证输出的每个文件内部有序。

2. 全排序

   最终输出结果只有一个文件，则文件内部有序。实现方式是只设置一个ReduceTask。但该方法在处理大型文件时效率极低，因为一台机器处理所有文件，完全丧失了MapReduce锁提供的并行架构。

3. 辅助排序：（GroupingComparator分组）

   在Reduce端对key进行分组。应用于：在接收的key为bean对象时，想让一个或几个字段相同（全部字段比较不相同）的key进入到同一个reduce方法时，可以采用分组排序。

4. 二次排序

   在自定义排序过程中，如果compareTo中的判断条件为两个即二次排序。

##### 14.3.4.1、自定义排序WritableComparable原理分析

bean对象做为key传输，需要实现**WritableComparable**接口重写compareTo方法，就可以实现排序。

```java
@Override
public int compareTo(FlowBean bean) {

	int result;
		
	// 按照总流量大小，倒序排列
	if (this.sumFlow > bean.getSumFlow()) {
		result = -1;
	}else if (this.sumFlow < bean.getSumFlow()) {
		result = 1;
	}else {
		result = 0;
	}

	return result;
}
```

#### 14.3.5、WritableComparable排序案例实操（全排序）

1. 需求

   根据案例13.3序列化案例产生的结果再次对总流量进行倒序排序。

    1. 输入数据

       原始数据

       ```
       1	13736230513	192.196.100.1	www.atguigu.com	2481	24681	200
       2	13846544121	192.196.100.2			264	0	200
       3 	13956435636	192.196.100.3			132	1512	200
       4 	13966251146	192.168.100.1			240	0	404
       5 	18271575951	192.168.100.2	www.atguigu.com	1527	2106	200
       6 	84188413	192.168.100.3	www.atguigu.com	4116	1432	200
       7 	13590439668	192.168.100.4			1116	954	200
       8 	15910133277	192.168.100.5	www.hao123.com	3156	2936	200
       9 	13729199489	192.168.100.6			240	0	200
       10 	13630577991	192.168.100.7	www.shouhu.com	6960	690	200
       11 	15043685818	192.168.100.8	www.baidu.com	3659	3538	200
       12 	15959002129	192.168.100.9	www.atguigu.com	1938	180	500
       13 	13560439638	192.168.100.10			918	4938	200
       14 	13470253144	192.168.100.11			180	180	200
       15 	13682846555	192.168.100.12	www.qq.com	1938	2910	200
       16 	13992314666	192.168.100.13	www.gaga.com	3008	3720	200
       17 	13509468723	192.168.100.14	www.qinghua.com	7335	110349	404
       18 	18390173782	192.168.100.15	www.sogou.com	9531	2412	200
       19 	13975057813	192.168.100.16	www.baidu.com	11058	48243	200
       20 	13768778790	192.168.100.17			120	120	200
       21 	13568436656	192.168.100.18	www.alibaba.com	2481	24681	200
       22 	13568436656	192.168.100.19			1116	954	200
       ```

       第一次处理后的数据

       ```
       part-r-00000
       ```

    2. 期望输出数据

       ```txt
       13509468723	7335	110349	117684
       13736230513	2481	24681	27162
       13956435636	132		1512	1644
       13846544121	264		0		264
       。。。 。。。
       ```

2. 需求分析

    1. 需求

    2. 输入数据

       ```
       13736230513		2481	24681	27162
       13846544121		264		0		264
       13956435636		132		1512	1644
       13509468723		7335	110349	117684
       。。。 。。。
       ```

    3. 输出数据

       ```
       13509468723		7335	110349	117684
       13736230513		2481	24681	27162
       13846544121		264		0		264
       13956435636		132		1512	1644
       。。。 。。。
       ```

    4. FlowBean实现WritableComparable接口重写compareTo方法

       ```java
       @Override
       public int compareTo(FlowBean o) {
           //	倒序排序，按照总流量从大到小
           return this.sumFlow > o.getSumFlow() ? -1 : 1;
       }
       ```

    5. Mapper类

       ```java
       context.write(bean, 手机号);
       ```

    6. Reducer类

       ```java
       //	循环输出，避免总流量相同情况
       for(Text text : values) {
           context.wirte(text, key);
       }
       ```

3. 代码实现

    1. FlowBean对象在需求1基础上增加了比较功能

       ```java
       package com.atguigu.mapreduce.writablecompable;
       
       import org.apache.hadoop.io.WritableComparable;
       import java.io.DataInput;
       import java.io.DataOutput;
       import java.io.IOException;
       
       public class FlowBean implements WritableComparable<FlowBean> {
       
           private long upFlow; //上行流量
           private long downFlow; //下行流量
           private long sumFlow; //总流量
       
           //提供无参构造
           public FlowBean() {
           }
       
           //生成三个属性的getter和setter方法
           public long getUpFlow() {
               return upFlow;
           }
       
           public void setUpFlow(long upFlow) {
               this.upFlow = upFlow;
           }
       
           public long getDownFlow() {
               return downFlow;
           }
       
           public void setDownFlow(long downFlow) {
               this.downFlow = downFlow;
           }
       
           public long getSumFlow() {
               return sumFlow;
           }
       
           public void setSumFlow(long sumFlow) {
               this.sumFlow = sumFlow;
           }
       
           public void setSumFlow() {
               this.sumFlow = this.upFlow + this.downFlow;
           }
       
           //实现序列化和反序列化方法,注意顺序一定要一致
           @Override
           public void write(DataOutput out) throws IOException {
               out.writeLong(this.upFlow);
               out.writeLong(this.downFlow);
               out.writeLong(this.sumFlow);
       
           }
       
           @Override
           public void readFields(DataInput in) throws IOException {
               this.upFlow = in.readLong();
               this.downFlow = in.readLong();
               this.sumFlow = in.readLong();
           }
       
           //重写ToString,最后要输出FlowBean
           @Override
           public String toString() {
               return upFlow + "\t" + downFlow + "\t" + sumFlow;
           }
       
           @Override
           public int compareTo(FlowBean o) {
               //按照总流量比较,倒序排列
               if(this.sumFlow > o.sumFlow){
                   return -1;
               }else if(this.sumFlow < o.sumFlow){
                   return 1;
               }else {
                   return 0;
               }
           }
       }
       ```

    2. 编写Mapper类

       ```java
       package com.atguigu.mapreduce.writablecompable;
       
       import org.apache.hadoop.io.LongWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Mapper;
       import java.io.IOException;
       
       public class FlowMapper extends Mapper<LongWritable, Text, FlowBean, Text> {
           private FlowBean outK = new FlowBean();
           private Text outV = new Text();
       
           @Override
           protected void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
       
               //1 获取一行数据
               String line = value.toString();
       
               //2 按照"\t",切割数据
               String[] split = line.split("\t");
       
               //3 封装outK outV
               outK.setUpFlow(Long.parseLong(split[1]));
               outK.setDownFlow(Long.parseLong(split[2]));
               outK.setSumFlow();
               outV.set(split[0]);
       
               //4 写出outK outV
               context.write(outK,outV);
           }
       }
       ```

    3. 编写Reducer类

       ```java
       package com.atguigu.mapreduce.writablecompable;
       
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Reducer;
       import java.io.IOException;
       
       public class FlowReducer extends Reducer<FlowBean, Text, Text, FlowBean> {
           @Override
           protected void reduce(FlowBean key, Iterable<Text> values, Context context) throws IOException, InterruptedException {
       
               //遍历values集合,循环写出,避免总流量相同的情况
               for (Text value : values) {
                   //调换KV位置,反向写出
                   context.write(value,key);
               }
           }
       }
       ```

    4. 编写Driver类

       ```java
       package com.atguigu.mapreduce.writablecompable;
       
       import org.apache.hadoop.conf.Configuration;
       import org.apache.hadoop.fs.Path;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Job;
       import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
       import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
       import java.io.IOException;
       
       public class FlowDriver {
       
           public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
       
               //1 获取job对象
               Configuration conf = new Configuration();
               Job job = Job.getInstance(conf);
       
               //2 关联本Driver类
               job.setJarByClass(FlowDriver.class);
       
               //3 关联Mapper和Reducer
               job.setMapperClass(FlowMapper.class);
               job.setReducerClass(FlowReducer.class);
       
               //4 设置Map端输出数据的KV类型
               job.setMapOutputKeyClass(FlowBean.class);
               job.setMapOutputValueClass(Text.class);
       
               //5 设置程序最终输出的KV类型
               job.setOutputKeyClass(Text.class);
               job.setOutputValueClass(FlowBean.class);
       
               //6 设置输入输出路径
               FileInputFormat.setInputPaths(job, new Path("D:\\inputflow2"));
               FileOutputFormat.setOutputPath(job, new Path("D:\\comparout"));
       
               //7 提交Job
               boolean b = job.waitForCompletion(true);
               System.exit(b ? 0 : 1);
           }
       }
       ```

#### 14.3.6、WritableComparable排序案例实操（区内排序）

1. 需求

   要求每个省份手机号输出的文件中按照总流量内部排序。

2. 需求分析

   基于前一个需求，增加自定义分区类，分区按照省份手机号设置。

    1. 数据输入

       ```
       13509468723		7335	110349	117684
       13975057813		11058	48243	59301
       13568436656		3597	25635	29232
       13736230513		2481	24681	27162
       18390173782		9531	2412	11943
       13630577991		6960	690		7650
       15043685818		3659	3538	7197
       13992314666		3008	3720	6728
       15910133277		3156	2936	6092
       13560439638		918		4938	5856
       84188413		4116	1432	5548
       13682846555		1938	2910	4848
       18271575951		1527	2106	3633
       15959002129		1938	180		2118
       13590439668		1116	954		2070
       13956435636		132		1512	1644
       13470253144		180		180		360
       13846544121		264		0		264
       13966251146		240		0		240
       13768778790		120		120		240
       13729199489 	240		0		240
       。。。 。。。
       ```

    2. 期望数据输出

       `part-r-00000`

       ```
       13630577991		6960	690		7650
       13682846555		1938	2910	4848
       ```

       `part-r-00001`

       ```
       13736230513		2481	24681	27162
       13768778790		120		120		240
       13729199489 	240		0		240
       ```

       `part-r-00002`

       ```
       13846544121		264		0		264
       ```

       `part-r-00003`

       ```
       13975057813		11058	48243	59301
       13992314666		3008	3720	6728
       13956435636		132		1512	1644
       13966251146		240		0		240
       ```

       `part-r-00004`

       ```
       13509468723		7335	110349	117684
       13568436656		3597	25635	29232
       18390173782		9531	2412	11943
       15043685818		3659	3538	7197
       15959002129		1938	180		2118
       。。。 。。。
       ```

3. 案例实操

    1. 增加自定义分区类

       ```java
       package com.atguigu.mapreduce.partitionercompable;
       
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Partitioner;
       
       public class ProvincePartitioner2 extends Partitioner<FlowBean, Text> {
       
           @Override
           public int getPartition(FlowBean flowBean, Text text, int numPartitions) {
               //获取手机号前三位
               String phone = text.toString();
               String prePhone = phone.substring(0, 3);
       
               //定义一个分区号变量partition,根据prePhone设置分区号
               int partition;
               if("136".equals(prePhone)){
                   partition = 0;
               }else if("137".equals(prePhone)){
                   partition = 1;
               }else if("138".equals(prePhone)){
                   partition = 2;
               }else if("139".equals(prePhone)){
                   partition = 3;
               }else {
                   partition = 4;
               }
       
               //最后返回分区号partition
               return partition;
           }
       }
       ```

    2. 在驱动类中增加分区类

       ```java
       // 设置自定义分区器
       job.setPartitionerClass(ProvincePartitioner2.class);
       // 设置对应的ReduceTask的个数
       job.setNumReduceTasks(5);
       ```

#### 14.3.7、Combiner合并

1. Combiner是MR程序中Mapper和Reducer之外的一种组件。

2. Combiner组件的父类就是Reducer。

3. Combiner和Reducer的区别在于运行的位置

    - **Combiner是在每一个MapTask所在的节点运行；**
    - **Reducer是接收全局所有Mapper的输出结果；**

4. Combiner的意义就是对每一个MapTask的输出进行局部汇总，以减小网络传输量。

5. **Combiner能够应用的前提是不能影响最终的业务逻辑**，而且，Combiner的输出kv应该跟Reducer的输入kv类型要对应起来

   **Mapper**

   ```
   3 5 7 -> (3+5+7)/3=5
   2 6 -> (2+6)/2=4
   ```

   **Reducer**

   ```
   (3+5+7+2+6)/5=23/5
   不等于
   (5+4)/2=9/2
   ```

6. **自定义Combiner实现步骤**

    1. 自定义一个Combiner继承Reducer，重写Reduce方法

       ```java
       public class WordCountCombiner extends Reducer<Text, IntWritable, Text, IntWritable> {
       
           private IntWritable outV = new IntWritable();
       
           @Override
           protected void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
       
               int sum = 0;
               for (IntWritable value : values) {
                   sum += value.get();
               }
            
               outV.set(sum);
            
               context.write(key,outV);
           }
       }
       ```

    2. 在Job驱动类中设置：

       ```java
       job.setCombinerClass(WordCountCombiner.class);
       ```

#### 14.3.8、Combiner合并案例实操

1. 需求

   统计过程中对每一个MapTask的输出进行局部汇总，以减小网络传输量即采用Combiner功能。

    1. 数据输入（hello.txt）

       ```
       banzhang ni hao
       xihuan hadoop banzhang
       banzhang ni hao
       xihuan hadoop banzhang
       ```

    2. 期望输出数据

       期望：Combine输入数据多，输出时经过合并，输出数据降低。

2. 需求分析

    1. 数据输入

       ```
       banzhang ni hao				    <banzhang, 4>
       xihuan hadoop banzhang			<ni, 2>
       banzhang ni hao					<xihuan, 2>
       xihuan hadoop banzhang			<Hadoop, 2>
       ```

    2. 期望输出

       ```shell
       Map-Reduce	Framework
               Map input records=4
               Map output records=12
               Map output bytes=126
               Map output materialized bytes=66
               Combine input records=12
               Combine output record=5
               Reduce input groups=5
               Reduce shuffle bytes=66
       ```

    3. 方案一

        1. 增加一个WordcountCombiner类继承Reducer
        2. 在WordcountCombiner中
            1. 统计单词汇总
            2. 将统计结果输出

    4. 方案二

        1. 将WordcountReducer作为Combiner在WordcountDriver驱动类中指定

           ```java
           job.setCombinerClass(WordcountReducer.class);
           ```

3. 案例实操（方案一）

    1. 增加一个WordCountCombiner类继承Reducer

       ```java
       package com.atguigu.mapreduce.combiner;
       
       import org.apache.hadoop.io.IntWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Reducer;
       import java.io.IOException;
       
       public class WordCountCombiner extends Reducer<Text, IntWritable, Text, IntWritable> {
       
       private IntWritable outV = new IntWritable();
       
           @Override
           protected void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
               int sum = 0;
               for (IntWritable value : values) {
                   sum += value.get();
               }
       
               //封装outKV
               outV.set(sum);
       
               //写出outKV
               context.write(key,outV);
           }
       }
       ```

    2. 在WordcountDriver驱动类中指定Combiner

       ```java
       // 指定需要使用combiner，以及用哪个类作为combiner的逻辑
       job.setCombinerClass(WordCountCombiner.class);
       ```

4. 案例实操（方案二）

    1. 将WordcountReducer作为Combiner在WordcountDriver驱动类中指定

       ```java
       // 指定需要使用Combiner，以及用哪个类作为Combiner的逻辑
       job.setCombinerClass(WordCountReducer.class);
       ```

       运行程序，如下图所示

       ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224095933.png)

### 14.4、OutputFormat数据输出

#### 14.4.1、OutputFormat接口实现类

> OutputFormat是MapReduce输出的基类，所有实现MapReduce输出都实现了OutputFormat接口。

1. **OutputFormat实现类**

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224100302.png)

2. **默认输出格式TextOutputFormat**

3. **自定义OutputFormat**

    1. 应用场景：

       例如：输出数据到MySQL/HBase+

    2. 自定义OutputFormat步骤

        - 自定义一个类继承FileOutputFormat
        - 改写RecordWriter，具体改写输出数据的方法write()。

#### 14.4.2、自定义OutputFormat案例实操

1. 需求

   过滤输入的log日志，包含`atguigu`的网站输出到`e:/atguigu.log`，不包含`atguigu`的网站输出到`e:/other.log`。

    1. 输入数据

       log.txt

       ```txt
       http://www.baidu.com
       http://www.google.com
       http://cn.bing.com
       http://www.atguigu.com
       http://www.sohu.com
       http://www.sina.com
       http://www.sin2a.com
       http://www.sin2desa.com
       http://www.sindsafa.com
       ```

    2. 期望输出数据

       atguigu.log

       ```txt
       http://www.atguigu.com
       ```

       other.log

       ```txt
       http://cn.bing.com
       http://www.baidu.com
       http://www.google.com
       http://www.sin2a.com
       http://www.sin2desa.com
       http://www.sina.com
       http://www.sindsafa.com
       http://www.sohu.com
       ```

2. 需求分析

    1. 需求

       过滤输入的log日志，包含`atguigu`的网站输出到`e:/atguigu.log`，不包含`atguigu`的网站输出到`e:/other.log`

    2. 输入数据

       ```txt
       http://www.baidu.com
       http://www.google.com
       http://cn.bing.com
       http://www.atguigu.com
       http://www.sohu.com
       http://www.sina.com
       http://www.sin2a.com
       http://www.sin2desa.com
       http://www.sindsafa.com
       ```

    3. 输出数据

       atguigu.log

       ```txt
       http://www.atguigu.com
       ```

       other.log

       ```txt
       http://cn.bing.com
       http://www.baidu.com
       http://www.google.com
       http://www.sin2a.com
       http://www.sin2desa.com
       http://www.sina.com
       http://www.sindsafa.com
       http://www.sohu.com
       ```

    4. 自定义一个OutputFormat类

        1. 创建一个类`LogRecordWriter`继承`RecordWriter`
            1. 创建两个文件的输出流：`atguiguOut`，`otherOut`
            2. 如果输入数据包含`atguigu`，输出到`atguiguOut`流。如果不包含`atguigu`，输出到`otherOut`流

    5. 驱动类



      ```java
      //	将自定义的输出格式组件设置到Job中
      job.setOutputFormatClass(LogOutputFormat.class);
      ```

3. 案例实操

    1. 编写LogMapper类

       ```java
       package com.atguigu.mapreduce.outputformat;
       
       import org.apache.hadoop.io.LongWritable;
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Mapper;
       
       import java.io.IOException;
       
       public class LogMapper extends Mapper<LongWritable, Text,Text, NullWritable> {
           @Override
           protected void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
               //不做任何处理,直接写出一行log数据
               context.write(value,NullWritable.get());
           }
       }
       ```

    2. 编写LogReducer类

       ```java
       package com.atguigu.mapreduce.outputformat;
       
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Reducer;
       
       import java.io.IOException;
       
       public class LogReducer extends Reducer<Text, NullWritable,Text, NullWritable> {
           @Override
           protected void reduce(Text key, Iterable<NullWritable> values, Context context) throws IOException, InterruptedException {
               // 防止有相同的数据,迭代写出
               for (NullWritable value : values) {
                   context.write(key,NullWritable.get());
               }
           }
       }
       ```

    3. 自定义一个LogOutputFormat

       ```java
       package com.atguigu.mapreduce.outputformat;
       
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.RecordWriter;
       import org.apache.hadoop.mapreduce.TaskAttemptContext;
       import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
       
       import java.io.IOException;
       
       public class LogOutputFormat extends FileOutputFormat<Text, NullWritable> {
           @Override
           public RecordWriter<Text, NullWritable> getRecordWriter(TaskAttemptContext job) throws IOException, InterruptedException {
               //创建一个自定义的RecordWriter返回
               LogRecordWriter logRecordWriter = new LogRecordWriter(job);
               return logRecordWriter;
           }
       }
       ```

    4. 编写LogRecordWriter

       ```java
       package com.atguigu.mapreduce.outputformat;
       
       import org.apache.hadoop.fs.FSDataOutputStream;
       import org.apache.hadoop.fs.FileSystem;
       import org.apache.hadoop.fs.Path;
       import org.apache.hadoop.io.IOUtils;
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.RecordWriter;
       import org.apache.hadoop.mapreduce.TaskAttemptContext;
       
       import java.io.IOException;
       
       public class LogRecordWriter extends RecordWriter<Text, NullWritable> {
       
           private FSDataOutputStream atguiguOut;
           private FSDataOutputStream otherOut;
       
           public LogRecordWriter(TaskAttemptContext job) {
               try {
                   //获取文件系统对象
                   FileSystem fs = FileSystem.get(job.getConfiguration());
                   //用文件系统对象创建两个输出流对应不同的目录
                   atguiguOut = fs.create(new Path("d:/hadoop/atguigu.log"));
                   otherOut = fs.create(new Path("d:/hadoop/other.log"));
               } catch (IOException e) {
                   e.printStackTrace();
               }
           }
       
           @Override
           public void write(Text key, NullWritable value) throws IOException, InterruptedException {
               String log = key.toString();
               //根据一行的log数据是否包含atguigu,判断两条输出流输出的内容
               if (log.contains("atguigu")) {
                   atguiguOut.writeBytes(log + "\n");
               } else {
                   otherOut.writeBytes(log + "\n");
               }
           }
       
           @Override
           public void close(TaskAttemptContext context) throws IOException, InterruptedException {
               //关流
               IOUtils.closeStream(atguiguOut);
               IOUtils.closeStream(otherOut);
           }
       }
       ```

    5. 编写LogDriver类

       ```java
       package com.atguigu.mapreduce.outputformat;
       
       import org.apache.hadoop.conf.Configuration;
       import org.apache.hadoop.fs.Path;
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Job;
       import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
       import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
       
       import java.io.IOException;
       
       public class LogDriver {
           public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
       
               Configuration conf = new Configuration();
               Job job = Job.getInstance(conf);
       
               job.setJarByClass(LogDriver.class);
               job.setMapperClass(LogMapper.class);
               job.setReducerClass(LogReducer.class);
       
               job.setMapOutputKeyClass(Text.class);
               job.setMapOutputValueClass(NullWritable.class);
       
               job.setOutputKeyClass(Text.class);
               job.setOutputValueClass(NullWritable.class);
       
               //设置自定义的outputformat
               job.setOutputFormatClass(LogOutputFormat.class);
       
               FileInputFormat.setInputPaths(job, new Path("D:\\input"));
               //虽然我们自定义了outputformat，但是因为我们的outputformat继承自fileoutputformat
               //而fileoutputformat要输出一个_SUCCESS文件，所以在这还得指定一个输出目录
               FileOutputFormat.setOutputPath(job, new Path("D:\\logoutput"));
       
               boolean b = job.waitForCompletion(true);
               System.exit(b ? 0 : 1);
           }
       }
       ```

### 14.5、MapReduce内核源码解析

#### 14.5.1、MapTask工作机制

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230227150035.png)

1. Read阶段：MapTask通过InputFormat获得的RecordReader，从输入InputSplit中解析出一个个key/value。
2. Map阶段：该节点主要是将解析出的key/value交给用户编写map()函数处理，并产生一系列新的key/value。
3. Collect收集阶段：在用户编写map()函数中，当数据处理完成后，一般会调用OutputCollector.collect()输出结果。在该函数内部，它会将生成的key/value分区（调用Partitioner），并写入一个环形内存缓冲区中。
4. Spill阶段：即“溢写”，当环形缓冲区满后，MapReduce会将数据写到本地磁盘上，生成一个临时文件。需要注意的是，将数据写入本地磁盘之前，先要对数据进行一次本地排序，并在必要时对数据进行合并、压缩等操作。
    - 利用快速排序算法对缓存区内的数据进行排序，排序方式是，先按照分区编号Partition进行排序，然后按照key进行排序。这样，经过排序后，数据以分区为单位聚集在一起，且同一分区内所有数据按照key有序。
    - 按照分区编号由小到大依次将每个分区中的数据写入任务工作目录下的临时文件output/spillN.out（N表示当前溢写次数）中。如果用户设置了Combiner，则写入文件之前，对每个分区中的数据进行一次聚集操作。
    - 将分区数据的元信息写到内存索引数据结构SpillRecord中，其中每个分区的元信息包括在临时文件中的偏移量、压缩前数据大小和压缩后数据大小。如果当前内存索引大小超过1MB，则将内存索引写到文件output/spillN.out.index中。
5. Merge阶段：当所有数据处理完成后，MapTask对所有临时文件进行一次合并，以确保最终只会生成一个数据文件。
    - 当所有数据处理完后，MapTask会将所有临时文件合并成一个大文件，并保存到文件output/file.out中，同时生成相应的索引文件output/file.out.index。
    - 在进行文件合并过程中，MapTask以分区为单位进行合并。对于某个分区，它将采用多轮递归合并的方式。每轮合并mapreduce.task.io.sort.factor（默认10）个文件，并将产生的文件重新加入待合并列表中，对文件排序后，重复以上过程，直到最终得到一个大文件。
    - 让每个MapTask最终只生成一个数据文件，可避免同时打开大量文件和同时读取大量小文件产生的随机读取带来的开销。

#### 14.5.2、ReduceTask工作机制

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230227150441.png)

1. Copy阶段：ReduceTask从各个MapTask上远程拷贝一片数据，并针对某一片数据，如果其大小超过一定阈值，则写到磁盘上，否则直接放到内存中。
2. Sort阶段：在远程拷贝数据的同时，ReduceTask启动了两个后台线程对内存和磁盘上的文件进行合并，以防止内存使用过多或磁盘上文件过多。按照MapReduce语义，用户编写reduce()函数输入数据是按key进行聚集的一组数据。为了将key相同的数据聚在一起，Hadoop采用了基于排序的策略。由于各个MapTask已经实现对自己的处理结果进行了局部排序，因此，ReduceTask只需对所有数据进行一次归并排序即可。
3. Reduce阶段：reduce()函数将计算结果写到HDFS上。

#### 14.5.3、ReduceTask并行度决定机制

> MapTask并行度由切片个数决定，切片个数由输入文件和切片规则决定。

> ReduceTask并行度由谁决定？

1. 设置ReduceTask并行度（个数）

   ReduceTask的并行度同样影响整个Job的执行并发度和执行效率，但与MapTask的并发数由切片数决定不同，ReduceTask数量的决定是可以直接手动设置：

   ```java
   // 默认值是1，手动设置为4
   job.setNumReduceTasks(4);
   ```

2. 实验：测试ReduceTask多少合适

    1. 实验环境：1个Master节点，16个Slave节点：CPU:8GHZ，内存: 2G

    2. 实验结论：

       ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230227150709.png)

3. 注意事项

    1. ReduceTask=0，表示没有Reduce阶段，输出文件个数和Map个数一致。
    2. ReduceTask默认值就是1，所以输出文件个数为一个。
    3. 如果数据分布不均匀，就有可能在Reduce阶段产生数据倾斜。
    4. ReduceTask数量并不是任意设置，还要考虑业务逻辑需求，有些情况下，需要计算全局汇总结果，就只能有1个ReduceTask
    5. 具体多少个ReduceTask，需要根据集群性能而定
    6. 如果分区数不是1，但是ReduceTask为1，是否执行分区过程。答案是：不执行分区过程。因为在MapTask的源码中，执行分区的前提是先判断ReduceNum个数是否大于1.不大于1肯定不执行。

#### 14.5.4、MapTask&ReduceTask源码解析

1. MapTask源码解析流程

   ```java
   =================== MapTask ===================
   context.write(k, NullWritable.get());   //自定义的map方法的写出，进入
   	output.write(key, value);  
   		//MapTask727行，收集方法，进入两次 
   		collector.collect(key, value,partitioner.getPartition(key, value, partitions));
   			HashPartitioner(); //默认分区器
   		collect()  //MapTask1082行 map端所有的kv全部写出后会走下面的close方法
   			close() //MapTask732行
   				collector.flush() // 溢出刷写方法，MapTask735行，提前打个断点，进入
   				sortAndSpill() //溢写排序，MapTask1505行，进入
   					sorter.sort()   QuickSort //溢写排序方法，MapTask1625行，进入
   				mergeParts(); //合并文件，MapTask1527行，进入
   				//file.out、file.out.index
   			collector.close(); //MapTask739行,收集器关闭,即将进入ReduceTask
   ```

2. ReduceTask源码解析流程

   ```java
   =================== ReduceTask ===================
   if (isMapOrReduce())  //reduceTask324行，提前打断点
   initialize()   // reduceTask333行,进入
   init(shuffleContext);  // reduceTask375行,走到这需要先给下面的打断点
   	totalMaps = job.getNumMapTasks(); // ShuffleSchedulerImpl第120行，提前打断点
   	merger = createMergeManager(context); //合并方法，Shuffle第80行
   		// MergeManagerImpl第232 235行，提前打断点
   		this.inMemoryMerger = createInMemoryMerger(); //内存合并
   		this.onDiskMerger = new OnDiskMerger(this); //磁盘合并
   rIter = shuffleConsumerPlugin.run();
   	eventFetcher.start();  //开始抓取数据，Shuffle第107行，提前打断点
   	eventFetcher.shutDown();  //抓取结束，Shuffle第141行，提前打断点
   	copyPhase.complete();   //copy阶段完成，Shuffle第151行
   	taskStatus.setPhase(TaskStatus.Phase.SORT);  //开始排序阶段，Shuffle第152行
   sortPhase.complete();   //排序阶段完成，即将进入reduce阶段 reduceTask382行
   reduce();  //reduce阶段调用的就是我们自定义的reduce方法，会被调用多次
   	cleanup(context); //reduce完成之前，会最后调用一次Reducer里面的cleanup方法
   ```

### 14.6、Join应用

#### 14.6.1、Reduce Join

- Map端的主要工作：为来自不同表或文件的key/value对，**打标签以区别不同来源的记录**。然后**用连接字段作为key**，其余部分和新加的标志作为value，最后进行输出。
- Reduce端的主要工作：在Reduce端**以连接字段作为key的分组已经完成**，我们只需要在每一个分组当中将那些来源于不同文件的记录（在Map阶段已经打标志）分开，最后进行合并就ok了。

#### 14.6.2、Reduce Join案例实操

1. 需求

   order.txt

   ```txt
   id		pid		amount
   1001	01		1
   1002	02		2
   1003	03		3
   1004	04		4
   1005	05		5
   1006	06		6
   ```

   pd.txt

   ```txt
   pid		pname
   01		小米
   02		华为
   03		格力
   ```

   将商品信息表中数据根据商品pid合并到订单数据表中

   ```txt
   id		pname	amount
   1001	小米		1
   1004	小米		4
   1002	华为		2
   1005	华为		5
   1003	格力		3
   1006	格力		6
   ```

2. 需求分析

   通过将关联条件作为Map输出的key，将两表满足Join条件的数据并携带数据所来源的文件信息，发往同一个ReduceTask，在Reduce中进行数据的串联。

    1. 输入数据

       order.txt

       ```txt
       订单id	pid		数量
       1001	01		1
       1002	02		2
       1003	03		3
       1004	01		4
       1005	02		5
       1006	03		6
       ```

       pd.txt

       ```txt
       pid		产品名称
       01		小米
       02		华为
       03		格力
       ```

    2. 预期输出数据

       ```txt
       订单id	产品名称	数量
       1001		小米		1
       1004		小米		4
       1002		华为		2
       1005		华为		5
       1003		格力		3
       1006		格力		6
       ```

    3. MapTask

        1. Map中处理的事情

           ```txt
           01		1001	1	order
           02		1002	2	order
           03		1003	3	order
           01		1004	4	order
           02		1005	5	order
           03		1006	6	order
           01		小米			pd
           02		华为			pd
           03		格力			pd
           ```

            1. 获取输入文件类型
            2. 获取输入数据
            3. 不同文件分别处理
            4. 封装Bean对象输出

        2. 默认对产品id排序

           ```txt
           01		1001	1	order
           01		1004	4	order
           01		小米			pd
           
           02		1002	2	order
           02		1005	5	order
           02		华为			pd
           
           03		1003	3	order
           03		1006	6	order
           03		格力			pd
           ```

    4. ReduceTask

        1. Reduce方法缓存订单数据集合和产品表，然后合并

           ```txt
           订单id	产品名称	数量
           1001		小米		1
           1004		小米		4
           
           1002		华为		2
           1005		华为		5
           
           1003		格力		3
           1006		格力		6
           ```

3. 代码实现

    1. 创建商品和订单合并后的TableBean类

       ```java
       package com.atguigu.mapreduce.reducejoin;
       
       import org.apache.hadoop.io.Writable;
       
       import java.io.DataInput;
       import java.io.DataOutput;
       import java.io.IOException;
       
       public class TableBean implements Writable {
       
           private String id; //订单id
           private String pid; //产品id
           private int amount; //产品数量
           private String pname; //产品名称
           private String flag; //判断是order表还是pd表的标志字段
       
           public TableBean() {
           }
       
           public String getId() {
               return id;
           }
       
           public void setId(String id) {
               this.id = id;
           }
       
           public String getPid() {
               return pid;
           }
       
           public void setPid(String pid) {
               this.pid = pid;
           }
       
           public int getAmount() {
               return amount;
           }
       
           public void setAmount(int amount) {
               this.amount = amount;
           }
       
           public String getPname() {
               return pname;
           }
       
           public void setPname(String pname) {
               this.pname = pname;
           }
       
           public String getFlag() {
               return flag;
           }
       
           public void setFlag(String flag) {
               this.flag = flag;
           }
       
           @Override
           public String toString() {
               return id + "\t" + pname + "\t" + amount;
           }
       
           @Override
           public void write(DataOutput out) throws IOException {
               out.writeUTF(id);
               out.writeUTF(pid);
               out.writeInt(amount);
               out.writeUTF(pname);
               out.writeUTF(flag);
           }
       
           @Override
           public void readFields(DataInput in) throws IOException {
               this.id = in.readUTF();
               this.pid = in.readUTF();
               this.amount = in.readInt();
               this.pname = in.readUTF();
               this.flag = in.readUTF();
           }
       }
       ```

    2. 编写TableMapper类

       ```java
       package com.atguigu.mapreduce.reducejoin;
       
       import org.apache.hadoop.io.LongWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.InputSplit;
       import org.apache.hadoop.mapreduce.Mapper;
       import org.apache.hadoop.mapreduce.lib.input.FileSplit;
       
       import java.io.IOException;
       
       public class TableMapper extends Mapper<LongWritable,Text,Text,TableBean> {
       
           private String filename;
           private Text outK = new Text();
           private TableBean outV = new TableBean();
       
           @Override
           protected void setup(Context context) throws IOException, InterruptedException {
               //获取对应文件名称
               InputSplit split = context.getInputSplit();
               FileSplit fileSplit = (FileSplit) split;
               filename = fileSplit.getPath().getName();
           }
       
           @Override
           protected void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
       
               //获取一行
               String line = value.toString();
       
               //判断是哪个文件,然后针对文件进行不同的操作
               if(filename.contains("order")){  //订单表的处理
                   String[] split = line.split("\t");
                   //封装outK
                   outK.set(split[1]);
                   //封装outV
                   outV.setId(split[0]);
                   outV.setPid(split[1]);
                   outV.setAmount(Integer.parseInt(split[2]));
                   outV.setPname("");
                   outV.setFlag("order");
               }else {                             //商品表的处理
                   String[] split = line.split("\t");
                   //封装outK
                   outK.set(split[0]);
                   //封装outV
                   outV.setId("");
                   outV.setPid(split[0]);
                   outV.setAmount(0);
                   outV.setPname(split[1]);
                   outV.setFlag("pd");
               }
       
               //写出KV
               context.write(outK,outV);
           }
       }
       ```

    3. 编写TableReducer类

       ```java
       package com.atguigu.mapreduce.reducejoin;
       
       import org.apache.commons.beanutils.BeanUtils;
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Reducer;
       
       import java.io.IOException;
       import java.lang.reflect.InvocationTargetException;
       import java.util.ArrayList;
       
       public class TableReducer extends Reducer<Text,TableBean,TableBean, NullWritable> {
       
           @Override
           protected void reduce(Text key, Iterable<TableBean> values, Context context) throws IOException, InterruptedException {
       
               ArrayList<TableBean> orderBeans = new ArrayList<>();
               TableBean pdBean = new TableBean();
       
               for (TableBean value : values) {
       
                   //判断数据来自哪个表
                   if("order".equals(value.getFlag())){   //订单表
       
                     //创建一个临时TableBean对象接收value
                       TableBean tmpOrderBean = new TableBean();
       
                       try {
                           BeanUtils.copyProperties(tmpOrderBean,value);
                       } catch (IllegalAccessException e) {
                           e.printStackTrace();
                       } catch (InvocationTargetException e) {
                           e.printStackTrace();
                       }
       
                     //将临时TableBean对象添加到集合orderBeans
                       orderBeans.add(tmpOrderBean);
                   }else {                                    //商品表
                       try {
                           BeanUtils.copyProperties(pdBean,value);
                       } catch (IllegalAccessException e) {
                           e.printStackTrace();
                       } catch (InvocationTargetException e) {
                           e.printStackTrace();
                       }
                   }
               }
       
               //遍历集合orderBeans,替换掉每个orderBean的pid为pname,然后写出
               for (TableBean orderBean : orderBeans) {
       
                   orderBean.setPname(pdBean.getPname());
       
                  //写出修改后的orderBean对象
                   context.write(orderBean,NullWritable.get());
               }
           }
       }
       ```

    4. 编写TableDriver类

       ```java
       package com.atguigu.mapreduce.reducejoin;
       
       import org.apache.hadoop.conf.Configuration;
       import org.apache.hadoop.fs.Path;
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Job;
       import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
       import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
       
       import java.io.IOException;
       
       public class TableDriver {
           public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
               Job job = Job.getInstance(new Configuration());
       
               job.setJarByClass(TableDriver.class);
               job.setMapperClass(TableMapper.class);
               job.setReducerClass(TableReducer.class);
       
               job.setMapOutputKeyClass(Text.class);
               job.setMapOutputValueClass(TableBean.class);
       
               job.setOutputKeyClass(TableBean.class);
               job.setOutputValueClass(NullWritable.class);
       
               FileInputFormat.setInputPaths(job, new Path("D:\\input"));
               FileOutputFormat.setOutputPath(job, new Path("D:\\output"));
       
               boolean b = job.waitForCompletion(true);
               System.exit(b ? 0 : 1);
           }
       }
       ```

4. 测试

   运行程序查看结果

   ```txt
   1004	小米	4
   1001	小米	1
   1005	华为	5
   1002	华为	2
   1006	格力	6
   1003	格力	3
   ```

5. 总结

    - 缺点：这种方式中，合并的操作是在Reduce阶段完成，Reduce端的处理压力太大，Map节点的运算负载则很低，资源利用率不高，且在Reduce阶段极易产生数据倾斜。
    - **解决方案：Map端实现数据合并。**

#### 14.6.3、Map Join

1. 使用场景

   Map Join适用于一张表十分小、一张表很大的场景。

2. 优点

   > 在Reduce端处理过多的表，非常容易产生数据倾斜。怎么办？

   在Map端缓存多张表，提前处理业务逻辑，这样增加Map端业务，减少Reduce端数据的压力，尽可能的减少数据倾斜。

3. 具体方法：采用**DistributedCache**

    1. 在Mapper的setup阶段，将文件读取到缓存集合中。

    2. 在Driver驱动类中加载缓存。

       ```java
       //缓存普通文件到Task运行节点。
       job.addCacheFile(new URI("file:///e:/cache/pd.txt"));
       //如果是集群运行,需要设置HDFS路径
       job.addCacheFile(new URI("hdfs://hadoop102:8020/cache/pd.txt"));
       ```

#### 14.6.4、Map Join案例实操

1. 需求

   order.txt

   ```txt
   id		pid		amount
   1001	01		1
   1002	02		2
   1003	03		3
   1004	01		4
   1005	02		5
   1006	03		6
   ```

   pd.txt

   ```txt
   pid		pname
   01		小米
   02		华为
   03		格力
   ```

   将商品信息表中数据根据商品pid合并到订单数据表中。

   最终数据形式：

   ```txt
   id			pname	amount
   1001		小米		1
   1004		小米		4
   
   1002		华为		2
   1005		华为		5
   
   1003		格力		3
   1006		格力		6
   ```

2. 需求分析

   MapJoin适用于关联表中有小表的情形。

   ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230227160242.png)

3. 实现代码

    1. 先在MapJoinDriver驱动类中添加缓存文件

       ```java
       package com.atguigu.mapreduce.mapjoin;
       
       import org.apache.hadoop.conf.Configuration;
       import org.apache.hadoop.fs.Path;
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Job;
       import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
       import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
       
       import java.io.IOException;
       import java.net.URI;
       import java.net.URISyntaxException;
       
       public class MapJoinDriver {
       
           public static void main(String[] args) throws IOException, URISyntaxException, ClassNotFoundException, InterruptedException {
       
               // 1 获取job信息
               Configuration conf = new Configuration();
               Job job = Job.getInstance(conf);
               // 2 设置加载jar包路径
               job.setJarByClass(MapJoinDriver.class);
               // 3 关联mapper
               job.setMapperClass(MapJoinMapper.class);
               // 4 设置Map输出KV类型
               job.setMapOutputKeyClass(Text.class);
               job.setMapOutputValueClass(NullWritable.class);
               // 5 设置最终输出KV类型
               job.setOutputKeyClass(Text.class);
               job.setOutputValueClass(NullWritable.class);
       
               // 加载缓存数据
               job.addCacheFile(new URI("file:///D:/input/tablecache/pd.txt"));
               // Map端Join的逻辑不需要Reduce阶段，设置reduceTask数量为0
               job.setNumReduceTasks(0);
       
               // 6 设置输入输出路径
               FileInputFormat.setInputPaths(job, new Path("D:\\input"));
               FileOutputFormat.setOutputPath(job, new Path("D:\\output"));
               // 7 提交
               boolean b = job.waitForCompletion(true);
               System.exit(b ? 0 : 1);
           }
       }
       ```

    2. 在MapJoinMapper类中的setup方法中读取缓存文件

       ```java
       package com.atguigu.mapreduce.mapjoin;
       
       import org.apache.commons.lang.StringUtils;
       import org.apache.hadoop.fs.FSDataInputStream;
       import org.apache.hadoop.fs.FileSystem;
       import org.apache.hadoop.fs.Path;
       import org.apache.hadoop.io.IOUtils;
       import org.apache.hadoop.io.LongWritable;
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Mapper;
       
       import java.io.BufferedReader;
       import java.io.IOException;
       import java.io.InputStreamReader;
       import java.net.URI;
       import java.util.HashMap;
       import java.util.Map;
       
       public class MapJoinMapper extends Mapper<LongWritable, Text, Text, NullWritable> {
       
           private Map<String, String> pdMap = new HashMap<>();
           private Text text = new Text();
       
           //任务开始前将pd数据缓存进pdMap
           @Override
           protected void setup(Context context) throws IOException, InterruptedException {
       
               //通过缓存文件得到小表数据pd.txt
               URI[] cacheFiles = context.getCacheFiles();
               Path path = new Path(cacheFiles[0]);
       
               //获取文件系统对象,并开流
               FileSystem fs = FileSystem.get(context.getConfiguration());
               FSDataInputStream fis = fs.open(path);
       
               //通过包装流转换为reader,方便按行读取
               BufferedReader reader = new BufferedReader(new InputStreamReader(fis, "UTF-8"));
       
               //逐行读取，按行处理
               String line;
               while (StringUtils.isNotEmpty(line = reader.readLine())) {
                   //切割一行    
       //01	小米
                   String[] split = line.split("\t");
                   pdMap.put(split[0], split[1]);
               }
       
               //关流
               IOUtils.closeStream(reader);
           }
       
           @Override
           protected void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
       
               //读取大表数据    
       //1001	01	1
               String[] fields = value.toString().split("\t");
       
               //通过大表每行数据的pid,去pdMap里面取出pname
               String pname = pdMap.get(fields[1]);
       
               //将大表每行数据的pid替换为pname
               text.set(fields[0] + "\t" + pname + "\t" + fields[2]);
       
               //写出
               context.write(text,NullWritable.get());
           }
       }
       ```


### 14.7、数据清洗（ETL）

- ETL，是英文Extract-Transform-Load的缩写，用来描述将数据从来源端经过抽取（Extract）、转换（Transform）、加载（Load）至目的端的过程。ETL一词较常用在数据仓库，但其对象并不限于数据仓库
- 在运行核心业务MapReduce程序之前，往往要先对数据进行清洗，清理掉不符合用户要求的数据。**清理的过程往往只需要运行Mapper程序，不需要运行Reduce程序。**

1. 需求

   去除日志中字段个数小于等于11的日志。

    1. 输入数据

       web.log
       
    2. 期望输出数据

       每行字段长度都大于11。

2. 需求分析

   需要在Map阶段对输入的数据根据规则进行过滤清洗。

3. 实现代码

    1. 编写WebLogMapper类

       ```java
       package com.atguigu.mapreduce.weblog;
       import java.io.IOException;
       import org.apache.hadoop.io.LongWritable;
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Mapper;
       
       public class WebLogMapper extends Mapper<LongWritable, Text, Text, NullWritable>{
           
           @Override
           protected void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
               
               // 1 获取1行数据
               String line = value.toString();
               
               // 2 解析日志
               boolean result = parseLog(line,context);
               
               // 3 日志不合法退出
               if (!result) {
                   return;
               }
               
               // 4 日志合法就直接写出
               context.write(value, NullWritable.get());
           }
       
           // 2 封装解析日志的方法
           private boolean parseLog(String line, Context context) {
       
               // 1 截取
               String[] fields = line.split(" ");
               
               // 2 日志长度大于11的为合法
               if (fields.length > 11) {
                   return true;
               }else {
                   return false;
               }
           }
       }
       ```

    2. 编写WebLogDriver类

       ```java
       package com.atguigu.mapreduce.weblog;
       import org.apache.hadoop.conf.Configuration;
       import org.apache.hadoop.fs.Path;
       import org.apache.hadoop.io.NullWritable;
       import org.apache.hadoop.io.Text;
       import org.apache.hadoop.mapreduce.Job;
       import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
       import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
       
       public class WebLogDriver {
           public static void main(String[] args) throws Exception {
       
       // 输入输出路径需要根据自己电脑上实际的输入输出路径设置
               args = new String[] { "D:/input/inputlog", "D:/output1" };
       
               // 1 获取job信息
               Configuration conf = new Configuration();
               Job job = Job.getInstance(conf);
       
               // 2 加载jar包
               job.setJarByClass(LogDriver.class);
       
               // 3 关联map
               job.setMapperClass(WebLogMapper.class);
       
               // 4 设置最终输出类型
               job.setOutputKeyClass(Text.class);
               job.setOutputValueClass(NullWritable.class);
       
               // 设置reducetask个数为0
               job.setNumReduceTasks(0);
       
               // 5 设置输入和输出路径
               FileInputFormat.setInputPaths(job, new Path(args[0]));
               FileOutputFormat.setOutputPath(job, new Path(args[1]));
       
               // 6 提交
                boolean b = job.waitForCompletion(true);
                System.exit(b ? 0 : 1);
           }
       }
       ```

### 14.8、MapReduce开发总结

1. **输入数据接口：InputFormat**

    1. 默认使用的实现类是：TextInputFormat
    2. TextInputFormat的功能逻辑是：一次读一行文本，然后将该行的起始偏移量作为key，行内容作为value返回。
    3. CombineTextInputFormat可以把多个小文件合并成一个切片处理，提高处理效率。

2. **逻辑处理接口：Mapper**

   用户根据业务需求实现其中三个方法：map()  setup()  cleanup ()

3. **Partitioner分区**

    1. 有默认实现 HashPartitioner，逻辑是根据key的哈希值和numReduces来返回一个分区号；key.hashCode()&Integer.MAXVALUE % numReduces
    2. 如果业务上有特别的需求，可以自定义分区。

4. **Comparable排序**

    1. 当我们用自定义的对象作为key来输出时，就必须要实现WritableComparable接口，重写其中的compareTo()方法。
    2. 部分排序：对最终输出的每一个文件进行内部排序。
    3. 全排序：对所有数据进行排序，通常只有一个Reduce。
    4. 二次排序：排序的条件有两个。

5. **Combiner合并**

   Combiner合并可以提高程序执行效率，减少IO传输。但是使用时必须不能影响原有的业务处理结果。

6. **逻辑处理接口：Reducer**

   用户根据业务需求实现其中三个方法：reduce()  setup()  cleanup ()

7. **输出数据接口：OutputFormat**

    1. 默认实现类是TextOutputFormat，功能逻辑是：将每一个KV对，向目标文本文件输出一行。
    2. 用户还可以自定义OutputFormat。

## 15、Hadoop数据压缩

### 15.1、概述

1. 压缩的好处和坏处
    - 压缩的优点：以减少磁盘IO、减少磁盘存储空间。
    - 压缩的缺点：增加CPU开销。
2. 压缩原则
    - 运算密集型的Job，少用压缩
    - IO密集型的Job，多用压缩

### 15.2、MR支持的压缩编码

1. 压缩算法对比介绍

   | 压缩格式 | Hadoop自带？     | 算法    | 文件扩展名 | 是否可切片 | 换成压缩格式后，原来的程序是否需要修改 |
      | -------- | ---------------- | ------- | ---------- | ---------- | -------------------------------------- |
   | DEFLATE  | 是，直接使用     | DEFLATE | .deflate   | 否         | 和文本处理一样，不需要修改             |
   | Gzip     | 是，直接使用     | DEFLATE | .gz        | 否         | 和文本处理一样，不需要修改             |
   | bzip2    | 是，直接使用     | bzip2   | .bz2       | **是**     | 和文本处理一样，不需要修改             |
   | LZ0      | **否，需要安装** | LZ0     | .lz0       | **是**     | **需要建索引，还需要指定输入格式**     |
   | Snappy   | 是，直接使用     | Snappy  | .snappy    | 否         | 和文本处理一样，不需要修改             |

2. 压缩性能的比较

   | 压缩算法 | 原始文件大小 | 压缩文件大小 | 压缩速度 | 解压速度 |
      | -------- | ------------ | ------------ | -------- | -------- |
   | gzip     | 8.3GB        | 1.8GB        | 17.5MB/s | 58MB/s   |
   | bzip2    | 8.3GB        | 1.1GB        | 2.4MB/s  | 9.5MB/s  |
   | LZ0      | 8.3GB        | 2.9GB        | 49.3MB/s | 74.6MB/s |

   http://google.github.io/snappy/

   Snappy is a compression/decompression library. It **does not aim for maximum compression**, or compatibility with any other compression library; instead, it **aims for very high speeds and reasonable compression**. For instance, compared to the fastest mode of zlib, Snappy is an order of magnitude faster for most inputs, but the resulting compressed files are anywhere from 20% to 100% bigger.On a single core of a Core i7 processor in 64-bit mode, Snappy **compresses** at about **250 MB**/sec or more and **decompresses** at about **500 MB**/sec or more.

### 15.3、压缩方式选择

压缩方式选择时重点考虑：**压缩/解压缩速度、压缩率（压缩后存储大小）、压缩后是否可以支持切片。**

#### 15.3.1、Gzip压缩

- 优点：压缩率比较高；
- 缺点：不支持Split；压缩/解压速度一般；

#### 15.3.2、Bzip2压缩

- 优点：压缩率高；支持Split
- 缺点：压缩/解压速度慢。

#### 15.3.3、Lzo压缩

- 优点：压缩/解压速度比较快；支持Split；
- 缺点：压缩率一般；想支持切片需要额外创建索引。

#### 15.3.4、Snappy压缩

- 优点：压缩和解压缩速度快；
- 缺点：不支持Split；压缩率一般；

#### 15.3.5、压缩位置选择

压缩可以在MapReduce作用的任意阶段启用！。

![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230227163128.png)

### 15.4、压缩参数配置

1. 为了支持多种压缩/解压缩算法，Hadoop引入了编码/解码器

   | 压缩格式 | 对应的编码/解码器                          |
   | -------- | ------------------------------------------ |
   | DEFLATE  | org.apache.hadoop.io.compress.DefaultCodec |
   | gzip     | org.apache.hadoop.io.compress.GzipCodec    |
   | bzip2    | org.apache.hadoop.io.compress.BZip2Codec   |
   | LZO      | com.hadoop.compression.lzo.LzopCodec       |
   | Snappy   | org.apache.hadoop.io.compress.SnappyCodec  |

2. 要在Hadoop中启用压缩，可以配置如下参数

   | 参数                                                         | 默认值                                         | 阶段        | 建议                                          |
   | ------------------------------------------------------------ | ---------------------------------------------- | ----------- | --------------------------------------------- |
   | io.compression.codecs  （在core-site.xml中配置）             | 无，这个需要在命令行输入hadoop checknative查看 | 输入压缩    | Hadoop使用文件扩展名判断是否支持某种编解码器  |
   | mapreduce.map.output.compress（在mapred-site.xml中配置）     | false                                          | mapper输出  | 这个参数设为true启用压缩                      |
   | mapreduce.map.output.compress.codec（在mapred-site.xml中配置） | org.apache.hadoop.io.compress.DefaultCodec     | mapper输出  | 企业多使用LZO或Snappy编解码器在此阶段压缩数据 |
   | mapreduce.output.fileoutputformat.compress（在mapred-site.xml中配置） | false                                          | reducer输出 | 这个参数设为true启用压缩                      |
   | mapreduce.output.fileoutputformat.compress.codec（在mapred-site.xml中配置） | org.apache.hadoop.io.compress.DefaultCodec     | reducer输出 | 使用标准工具或者编解码器，如gzip和bzip2       |

### 15.5、压缩实操案例

#### 15.5.1、Map输出端采用压缩

即使你的MapReduce的输入输出文件都是未压缩的文件，你仍然可以对Map任务的中间结果输出做压缩，因为它要写在硬盘并且通过网络传输到Reduce节点，对其压缩可以提高很多性能，这些工作只要设置两个属性即可，我们来看下代码怎么设置。

1. 给大家提供的Hadoop源码支持的压缩格式有：**BZip2Codec**、**DefaultCodec**

   ```java
   package com.atguigu.mapreduce.compress;
   
   import java.io.IOException;
   import org.apache.hadoop.conf.Configuration;
   import org.apache.hadoop.fs.Path;
   import org.apache.hadoop.io.IntWritable;
   import org.apache.hadoop.io.Text;
   import org.apache.hadoop.io.compress.BZip2Codec;	
   import org.apache.hadoop.io.compress.CompressionCodec;
   import org.apache.hadoop.io.compress.GzipCodec;
   import org.apache.hadoop.mapreduce.Job;
   import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
   import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
   
   public class WordCountDriver {
   
   	public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
   		Configuration conf = new Configuration();
   
   		// 开启map端输出压缩
   		conf.setBoolean("mapreduce.map.output.compress", true);
   
   		// 设置map端输出压缩方式
   		conf.setClass("mapreduce.map.output.compress.codec", BZip2Codec.class,CompressionCodec.class);
   
   		Job job = Job.getInstance(conf);
   
   		job.setJarByClass(WordCountDriver.class);
   
   		job.setMapperClass(WordCountMapper.class);
   		job.setReducerClass(WordCountReducer.class);
   
   		job.setMapOutputKeyClass(Text.class);
   		job.setMapOutputValueClass(IntWritable.class);
   
   		job.setOutputKeyClass(Text.class);
   		job.setOutputValueClass(IntWritable.class);
   
   		FileInputFormat.setInputPaths(job, new Path(args[0]));
   		FileOutputFormat.setOutputPath(job, new Path(args[1]));
   
   		boolean result = job.waitForCompletion(true);
   
   		System.exit(result ? 0 : 1);
   	}
   }

2. Mapper保持不变

   ```java
   package com.atguigu.mapreduce.compress;
   import java.io.IOException;
   import org.apache.hadoop.io.IntWritable;
   import org.apache.hadoop.io.LongWritable;
   import org.apache.hadoop.io.Text;
   import org.apache.hadoop.mapreduce.Mapper;
   
   public class WordCountMapper extends Mapper<LongWritable, Text, Text, IntWritable>{
   	Text k = new Text();
   	IntWritable v = new IntWritable(1);
   
   	@Override
   	protected void map(LongWritable key, Text value, Context context)throws IOException, InterruptedException {
   
   		// 1 获取一行
   		String line = value.toString();
   
   		// 2 切割
   		String[] words = line.split(" ");
   
   		// 3 循环写出
   		for(String word:words){
   			k.set(word);
   			context.write(k, v);
   		}
   	}
   }
   ```

3. Reducer保持不变

   ```java
   package com.atguigu.mapreduce.compress;
   import java.io.IOException;
   import org.apache.hadoop.io.IntWritable;
   import org.apache.hadoop.io.Text;
   import org.apache.hadoop.mapreduce.Reducer;
   
   public class WordCountReducer extends Reducer<Text, IntWritable, Text, IntWritable>{
   	IntWritable v = new IntWritable();
   
   	@Override
   	protected void reduce(Text key, Iterable<IntWritable> values,
   			Context context) throws IOException, InterruptedException {
   		
   		int sum = 0;
   
   		// 1 汇总
   		for(IntWritable value:values){
   			sum += value.get();
   		}
   		
            v.set(sum);
   
            // 2 输出
   		context.write(key, v);
   	}
   }
   ```

#### 15.5.2、Reduce输出端采用压缩

> 基于WordCount案例处理。

1. 修改驱动

   ```java
   package com.atguigu.mapreduce.compress;
   
   import java.io.IOException;
   import org.apache.hadoop.conf.Configuration;
   import org.apache.hadoop.fs.Path;
   import org.apache.hadoop.io.IntWritable;
   import org.apache.hadoop.io.Text;
   import org.apache.hadoop.io.compress.BZip2Codec;
   import org.apache.hadoop.io.compress.DefaultCodec;
   import org.apache.hadoop.io.compress.GzipCodec;
   import org.apache.hadoop.io.compress.Lz4Codec;
   import org.apache.hadoop.io.compress.SnappyCodec;
   import org.apache.hadoop.mapreduce.Job;
   import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
   import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
   
   public class WordCountDriver {
   
   	public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
   		
   		Configuration conf = new Configuration();
   		
   		Job job = Job.getInstance(conf);
   		
   		job.setJarByClass(WordCountDriver.class);
   		
   		job.setMapperClass(WordCountMapper.class);
   		job.setReducerClass(WordCountReducer.class);
   		
   		job.setMapOutputKeyClass(Text.class);
   		job.setMapOutputValueClass(IntWritable.class);
   		
   		job.setOutputKeyClass(Text.class);
   		job.setOutputValueClass(IntWritable.class);
   		
   		FileInputFormat.setInputPaths(job, new Path(args[0]));
   		FileOutputFormat.setOutputPath(job, new Path(args[1]));
   		
   		// 设置reduce端输出压缩开启
   		FileOutputFormat.setCompressOutput(job, true);
   
   		// 设置压缩的方式
   	    FileOutputFormat.setOutputCompressorClass(job, BZip2Codec.class); 
   //	    FileOutputFormat.setOutputCompressorClass(job, GzipCodec.class); 
   //	    FileOutputFormat.setOutputCompressorClass(job, DefaultCodec.class); 
   	    
   		boolean result = job.waitForCompletion(true);
   		
   		System.exit(result?0:1);
   	}
   }
   ```

2. Mapper和Reducer保持不变（详见15.5.1）

## 16、常见错误及解决方案

1. 导包容易出错。尤其Text和CombineTextInputFormat。

2. Mapper中第一个输入的参数必须是LongWritable或者NullWritable，不可以是IntWritable.  报的错误是类型转换异常。

3. java.lang.Exception: java.io.IOException: Illegal partition for 13926435656 (4)，说明Partition和ReduceTask个数没对上，调整ReduceTask个数。

4. 如果分区数不是1，但是reducetask为1，是否执行分区过程。答案是：不执行分区过程。因为在MapTask的源码中，执行分区的前提是先判断ReduceNum个数是否大于1。不大于1肯定不执行。

5. 在Windows环境编译的jar包导入到Linux环境中运行，

   ```shell
   hadoop jar wc.jar com.atguigu.mapreduce.wordcount.WordCountDriver /user/atguigu/ /user/atguigu/output
   ```

   报如下错误：

   ```shell
   Exception in thread "main" java.lang.UnsupportedClassVersionError: com/atguigu/mapreduce/wordcount/WordCountDriver : Unsupported major.minor version 52.0
   ```

   原因是Windows环境用的jdk1.7，Linux环境用的jdk1.8。

   解决方案：统一jdk版本。

6. 缓存pd.txt小文件案例中，报找不到pd.txt文件

   原因：大部分为路径书写错误。还有就是要检查pd.txt.txt的问题。还有个别电脑写相对路径找不到pd.txt，可以修改为绝对路径。

7. 报类型转换异常。

   通常都是在驱动函数中设置Map输出和最终输出时编写错误。

   Map输出的key如果没有排序，也会报类型转换异常。

8. 集群中运行wc.jar时出现了无法获得输入文件。

   原因：WordCount案例的输入文件不能放用HDFS集群的根目录。

9. 出现了如下相关异常

   ```shell
   Exception in thread "main" java.lang.UnsatisfiedLinkError: org.apache.hadoop.io.nativeio.NativeIO$Windows.access0(Ljava/lang/String;I)Z
   	at org.apache.hadoop.io.nativeio.NativeIO$Windows.access0(Native Method)
   	at org.apache.hadoop.io.nativeio.NativeIO$Windows.access(NativeIO.java:609)
   	at org.apache.hadoop.fs.FileUtil.canRead(FileUtil.java:977)
   java.io.IOException: Could not locate executable null\bin\winutils.exe in the Hadoop binaries.
   	at org.apache.hadoop.util.Shell.getQualifiedBinPath(Shell.java:356)
   	at org.apache.hadoop.util.Shell.getWinUtilsPath(Shell.java:371)
   	at org.apache.hadoop.util.Shell.<clinit>(Shell.java:364)
   ```

   解决方案：拷贝hadoop.dll文件到Windows目录C:\Windows\System32。个别同学电脑还需要修改Hadoop源码。

   方案二：创建如下包名，并将NativeIO.java拷贝到该包名下

   ```java
   /**
    * Licensed to the Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See the NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  The ASF licenses this file
    * to you under the Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with the License.  You may obtain a copy of the License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed to in writing, software
    * distributed under the License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See the License for the specific language governing permissions and
    * limitations under the License.
    */
   package org.apache.hadoop.io.nativeio;
   
   import java.io.File;
   import java.io.FileDescriptor;
   import java.io.FileInputStream;
   import java.io.FileOutputStream;
   import java.io.IOException;
   import java.io.RandomAccessFile;
   import java.lang.reflect.Field;
   import java.nio.ByteBuffer;
   import java.nio.MappedByteBuffer;
   import java.nio.channels.FileChannel;
   import java.util.Map;
   import java.util.concurrent.ConcurrentHashMap;
   
   import org.apache.hadoop.classification.InterfaceAudience;
   import org.apache.hadoop.classification.InterfaceStability;
   import org.apache.hadoop.conf.Configuration;
   import org.apache.hadoop.fs.CommonConfigurationKeys;
   import org.apache.hadoop.fs.HardLink;
   import org.apache.hadoop.io.IOUtils;
   import org.apache.hadoop.io.SecureIOUtils.AlreadyExistsException;
   import org.apache.hadoop.util.NativeCodeLoader;
   import org.apache.hadoop.util.Shell;
   import org.apache.hadoop.util.PerformanceAdvisory;
   import org.apache.commons.logging.Log;
   import org.apache.commons.logging.LogFactory;
   
   import sun.misc.Unsafe;
   
   import com.google.common.annotations.VisibleForTesting;
   
   /**
    * JNI wrappers for various native IO-related calls not available in Java. These
    * functions should generally be used alongside a fallback to another more
    * portable mechanism.
    */
   @InterfaceAudience.Private
   @InterfaceStability.Unstable
   public class NativeIO {
   	public static class POSIX {
   		// Flags for open() call from bits/fcntl.h
   		public static final int O_RDONLY = 00;
   		public static final int O_WRONLY = 01;
   		public static final int O_RDWR = 02;
   		public static final int O_CREAT = 0100;
   		public static final int O_EXCL = 0200;
   		public static final int O_NOCTTY = 0400;
   		public static final int O_TRUNC = 01000;
   		public static final int O_APPEND = 02000;
   		public static final int O_NONBLOCK = 04000;
   		public static final int O_SYNC = 010000;
   		public static final int O_ASYNC = 020000;
   		public static final int O_FSYNC = O_SYNC;
   		public static final int O_NDELAY = O_NONBLOCK;
   
   		// Flags for posix_fadvise() from bits/fcntl.h
   		/* No further special treatment. */
   		public static final int POSIX_FADV_NORMAL = 0;
   		/* Expect random page references. */
   		public static final int POSIX_FADV_RANDOM = 1;
   		/* Expect sequential page references. */
   		public static final int POSIX_FADV_SEQUENTIAL = 2;
   		/* Will need these pages. */
   		public static final int POSIX_FADV_WILLNEED = 3;
   		/* Don't need these pages. */
   		public static final int POSIX_FADV_DONTNEED = 4;
   		/* Data will be accessed once. */
   		public static final int POSIX_FADV_NOREUSE = 5;
   
   		/*
   		 * Wait upon writeout of all pages in the range before performing the write.
   		 */
   		public static final int SYNC_FILE_RANGE_WAIT_BEFORE = 1;
   		/*
   		 * Initiate writeout of all those dirty pages in the range which are not
   		 * presently under writeback.
   		 */
   		public static final int SYNC_FILE_RANGE_WRITE = 2;
   
   		/*
   		 * Wait upon writeout of all pages in the range after performing the write.
   		 */
   		public static final int SYNC_FILE_RANGE_WAIT_AFTER = 4;
   
   		private static final Log LOG = LogFactory.getLog(NativeIO.class);
   
   		private static boolean nativeLoaded = false;
   		private static boolean fadvisePossible = true;
   		private static boolean syncFileRangePossible = true;
   
   		static final String WORKAROUND_NON_THREADSAFE_CALLS_KEY = "hadoop.workaround.non.threadsafe.getpwuid";
   		static final boolean WORKAROUND_NON_THREADSAFE_CALLS_DEFAULT = true;
   
   		private static long cacheTimeout = -1;
   
   		private static CacheManipulator cacheManipulator = new CacheManipulator();
   
   		public static CacheManipulator getCacheManipulator() {
   			return cacheManipulator;
   		}
   
   		public static void setCacheManipulator(CacheManipulator cacheManipulator) {
   			POSIX.cacheManipulator = cacheManipulator;
   		}
   
   		/**
   		 * Used to manipulate the operating system cache.
   		 */
   		@VisibleForTesting
   		public static class CacheManipulator {
   			public void mlock(String identifier, ByteBuffer buffer, long len) throws IOException {
   				POSIX.mlock(buffer, len);
   			}
   
   			public long getMemlockLimit() {
   				return NativeIO.getMemlockLimit();
   			}
   
   			public long getOperatingSystemPageSize() {
   				return NativeIO.getOperatingSystemPageSize();
   			}
   
   			public void posixFadviseIfPossible(String identifier, FileDescriptor fd, long offset, long len, int flags)
   					throws NativeIOException {
   				NativeIO.POSIX.posixFadviseIfPossible(identifier, fd, offset, len, flags);
   			}
   
   			public boolean verifyCanMlock() {
   				return NativeIO.isAvailable();
   			}
   		}
   
   		/**
   		 * A CacheManipulator used for testing which does not actually call mlock. This
   		 * allows many tests to be run even when the operating system does not allow
   		 * mlock, or only allows limited mlocking.
   		 */
   		@VisibleForTesting
   		public static class NoMlockCacheManipulator extends CacheManipulator {
   			public void mlock(String identifier, ByteBuffer buffer, long len) throws IOException {
   				LOG.info("mlocking " + identifier);
   			}
   
   			public long getMemlockLimit() {
   				return 1125899906842624L;
   			}
   
   			public long getOperatingSystemPageSize() {
   				return 4096;
   			}
   
   			public boolean verifyCanMlock() {
   				return true;
   			}
   		}
   
   		static {
   			if (NativeCodeLoader.isNativeCodeLoaded()) {
   				try {
   					Configuration conf = new Configuration();
   					workaroundNonThreadSafePasswdCalls = conf.getBoolean(WORKAROUND_NON_THREADSAFE_CALLS_KEY,
   							WORKAROUND_NON_THREADSAFE_CALLS_DEFAULT);
   
   					initNative();
   					nativeLoaded = true;
   
   					cacheTimeout = conf.getLong(CommonConfigurationKeys.HADOOP_SECURITY_UID_NAME_CACHE_TIMEOUT_KEY,
   							CommonConfigurationKeys.HADOOP_SECURITY_UID_NAME_CACHE_TIMEOUT_DEFAULT) * 1000;
   					LOG.debug("Initialized cache for IDs to User/Group mapping with a " + " cache timeout of "
   							+ cacheTimeout / 1000 + " seconds.");
   
   				} catch (Throwable t) {
   					// This can happen if the user has an older version of libhadoop.so
   					// installed - in this case we can continue without native IO
   					// after warning
   					PerformanceAdvisory.LOG.debug("Unable to initialize NativeIO libraries", t);
   				}
   			}
   		}
   
   		/**
   		 * Return true if the JNI-based native IO extensions are available.
   		 */
   		public static boolean isAvailable() {
   			return NativeCodeLoader.isNativeCodeLoaded() && nativeLoaded;
   		}
   
   		private static void assertCodeLoaded() throws IOException {
   			if (!isAvailable()) {
   				throw new IOException("NativeIO was not loaded");
   			}
   		}
   
   		/** Wrapper around open(2) */
   		public static native FileDescriptor open(String path, int flags, int mode) throws IOException;
   
   		/** Wrapper around fstat(2) */
   		private static native Stat fstat(FileDescriptor fd) throws IOException;
   
   		/** Native chmod implementation. On UNIX, it is a wrapper around chmod(2) */
   		private static native void chmodImpl(String path, int mode) throws IOException;
   
   		public static void chmod(String path, int mode) throws IOException {
   			if (!Shell.WINDOWS) {
   				chmodImpl(path, mode);
   			} else {
   				try {
   					chmodImpl(path, mode);
   				} catch (NativeIOException nioe) {
   					if (nioe.getErrorCode() == 3) {
   						throw new NativeIOException("No such file or directory", Errno.ENOENT);
   					} else {
   						LOG.warn(
   								String.format("NativeIO.chmod error (%d): %s", nioe.getErrorCode(), nioe.getMessage()));
   						throw new NativeIOException("Unknown error", Errno.UNKNOWN);
   					}
   				}
   			}
   		}
   
   		/** Wrapper around posix_fadvise(2) */
   		static native void posix_fadvise(FileDescriptor fd, long offset, long len, int flags) throws NativeIOException;
   
   		/** Wrapper around sync_file_range(2) */
   		static native void sync_file_range(FileDescriptor fd, long offset, long nbytes, int flags)
   				throws NativeIOException;
   
   		/**
   		 * Call posix_fadvise on the given file descriptor. See the manpage for this
   		 * syscall for more information. On systems where this call is not available,
   		 * does nothing.
   		 *
   		 * @throws NativeIOException
   		 *             if there is an error with the syscall
   		 */
   		static void posixFadviseIfPossible(String identifier, FileDescriptor fd, long offset, long len, int flags)
   				throws NativeIOException {
   			if (nativeLoaded && fadvisePossible) {
   				try {
   					posix_fadvise(fd, offset, len, flags);
   				} catch (UnsupportedOperationException uoe) {
   					fadvisePossible = false;
   				} catch (UnsatisfiedLinkError ule) {
   					fadvisePossible = false;
   				}
   			}
   		}
   
   		/**
   		 * Call sync_file_range on the given file descriptor. See the manpage for this
   		 * syscall for more information. On systems where this call is not available,
   		 * does nothing.
   		 *
   		 * @throws NativeIOException
   		 *             if there is an error with the syscall
   		 */
   		public static void syncFileRangeIfPossible(FileDescriptor fd, long offset, long nbytes, int flags)
   				throws NativeIOException {
   			if (nativeLoaded && syncFileRangePossible) {
   				try {
   					sync_file_range(fd, offset, nbytes, flags);
   				} catch (UnsupportedOperationException uoe) {
   					syncFileRangePossible = false;
   				} catch (UnsatisfiedLinkError ule) {
   					syncFileRangePossible = false;
   				}
   			}
   		}
   
   		static native void mlock_native(ByteBuffer buffer, long len) throws NativeIOException;
   
   		/**
   		 * Locks the provided direct ByteBuffer into memory, preventing it from swapping
   		 * out. After a buffer is locked, future accesses will not incur a page fault.
   		 * 
   		 * See the mlock(2) man page for more information.
   		 * 
   		 * @throws NativeIOException
   		 */
   		static void mlock(ByteBuffer buffer, long len) throws IOException {
   			assertCodeLoaded();
   			if (!buffer.isDirect()) {
   				throw new IOException("Cannot mlock a non-direct ByteBuffer");
   			}
   			mlock_native(buffer, len);
   		}
   
   		/**
   		 * Unmaps the block from memory. See munmap(2).
   		 *
   		 * There isn't any portable way to unmap a memory region in Java. So we use the
   		 * sun.nio method here. Note that unmapping a memory region could cause crashes
   		 * if code continues to reference the unmapped code. However, if we don't
   		 * manually unmap the memory, we are dependent on the finalizer to do it, and we
   		 * have no idea when the finalizer will run.
   		 *
   		 * @param buffer
   		 *            The buffer to unmap.
   		 */
   		public static void munmap(MappedByteBuffer buffer) {
   			if (buffer instanceof sun.nio.ch.DirectBuffer) {
   				sun.misc.Cleaner cleaner = ((sun.nio.ch.DirectBuffer) buffer).cleaner();
   				cleaner.clean();
   			}
   		}
   
   		/** Linux only methods used for getOwner() implementation */
   		private static native long getUIDforFDOwnerforOwner(FileDescriptor fd) throws IOException;
   
   		private static native String getUserName(long uid) throws IOException;
   
   		/**
   		 * Result type of the fstat call
   		 */
   		public static class Stat {
   			private int ownerId, groupId;
   			private String owner, group;
   			private int mode;
   
   			// Mode constants
   			public static final int S_IFMT = 0170000; /* type of file */
   			public static final int S_IFIFO = 0010000; /* named pipe (fifo) */
   			public static final int S_IFCHR = 0020000; /* character special */
   			public static final int S_IFDIR = 0040000; /* directory */
   			public static final int S_IFBLK = 0060000; /* block special */
   			public static final int S_IFREG = 0100000; /* regular */
   			public static final int S_IFLNK = 0120000; /* symbolic link */
   			public static final int S_IFSOCK = 0140000; /* socket */
   			public static final int S_IFWHT = 0160000; /* whiteout */
   			public static final int S_ISUID = 0004000; /* set user id on execution */
   			public static final int S_ISGID = 0002000; /* set group id on execution */
   			public static final int S_ISVTX = 0001000; /* save swapped text even after use */
   			public static final int S_IRUSR = 0000400; /* read permission, owner */
   			public static final int S_IWUSR = 0000200; /* write permission, owner */
   			public static final int S_IXUSR = 0000100; /* execute/search permission, owner */
   
   			Stat(int ownerId, int groupId, int mode) {
   				this.ownerId = ownerId;
   				this.groupId = groupId;
   				this.mode = mode;
   			}
   
   			Stat(String owner, String group, int mode) {
   				if (!Shell.WINDOWS) {
   					this.owner = owner;
   				} else {
   					this.owner = stripDomain(owner);
   				}
   				if (!Shell.WINDOWS) {
   					this.group = group;
   				} else {
   					this.group = stripDomain(group);
   				}
   				this.mode = mode;
   			}
   
   			@Override
   			public String toString() {
   				return "Stat(owner='" + owner + "', group='" + group + "'" + ", mode=" + mode + ")";
   			}
   
   			public String getOwner() {
   				return owner;
   			}
   
   			public String getGroup() {
   				return group;
   			}
   
   			public int getMode() {
   				return mode;
   			}
   		}
   
   		/**
   		 * Returns the file stat for a file descriptor.
   		 *
   		 * @param fd
   		 *            file descriptor.
   		 * @return the file descriptor file stat.
   		 * @throws IOException
   		 *             thrown if there was an IO error while obtaining the file stat.
   		 */
   		public static Stat getFstat(FileDescriptor fd) throws IOException {
   			Stat stat = null;
   			if (!Shell.WINDOWS) {
   				stat = fstat(fd);
   				stat.owner = getName(IdCache.USER, stat.ownerId);
   				stat.group = getName(IdCache.GROUP, stat.groupId);
   			} else {
   				try {
   					stat = fstat(fd);
   				} catch (NativeIOException nioe) {
   					if (nioe.getErrorCode() == 6) {
   						throw new NativeIOException("The handle is invalid.", Errno.EBADF);
   					} else {
   						LOG.warn(String.format("NativeIO.getFstat error (%d): %s", nioe.getErrorCode(),
   								nioe.getMessage()));
   						throw new NativeIOException("Unknown error", Errno.UNKNOWN);
   					}
   				}
   			}
   			return stat;
   		}
   
   		private static String getName(IdCache domain, int id) throws IOException {
   			Map<Integer, CachedName> idNameCache = (domain == IdCache.USER) ? USER_ID_NAME_CACHE : GROUP_ID_NAME_CACHE;
   			String name;
   			CachedName cachedName = idNameCache.get(id);
   			long now = System.currentTimeMillis();
   			if (cachedName != null && (cachedName.timestamp + cacheTimeout) > now) {
   				name = cachedName.name;
   			} else {
   				name = (domain == IdCache.USER) ? getUserName(id) : getGroupName(id);
   				if (LOG.isDebugEnabled()) {
   					String type = (domain == IdCache.USER) ? "UserName" : "GroupName";
   					LOG.debug("Got " + type + " " + name + " for ID " + id + " from the native implementation");
   				}
   				cachedName = new CachedName(name, now);
   				idNameCache.put(id, cachedName);
   			}
   			return name;
   		}
   
   		static native String getUserName(int uid) throws IOException;
   
   		static native String getGroupName(int uid) throws IOException;
   
   		private static class CachedName {
   			final long timestamp;
   			final String name;
   
   			public CachedName(String name, long timestamp) {
   				this.name = name;
   				this.timestamp = timestamp;
   			}
   		}
   
   		private static final Map<Integer, CachedName> USER_ID_NAME_CACHE = new ConcurrentHashMap<Integer, CachedName>();
   
   		private static final Map<Integer, CachedName> GROUP_ID_NAME_CACHE = new ConcurrentHashMap<Integer, CachedName>();
   
   		private enum IdCache {
   			USER, GROUP
   		}
   
   		public final static int MMAP_PROT_READ = 0x1;
   		public final static int MMAP_PROT_WRITE = 0x2;
   		public final static int MMAP_PROT_EXEC = 0x4;
   
   		public static native long mmap(FileDescriptor fd, int prot, boolean shared, long length) throws IOException;
   
   		public static native void munmap(long addr, long length) throws IOException;
   	}
   
   	private static boolean workaroundNonThreadSafePasswdCalls = false;
   
   	public static class Windows {
   		// Flags for CreateFile() call on Windows
   		public static final long GENERIC_READ = 0x80000000L;
   		public static final long GENERIC_WRITE = 0x40000000L;
   
   		public static final long FILE_SHARE_READ = 0x00000001L;
   		public static final long FILE_SHARE_WRITE = 0x00000002L;
   		public static final long FILE_SHARE_DELETE = 0x00000004L;
   
   		public static final long CREATE_NEW = 1;
   		public static final long CREATE_ALWAYS = 2;
   		public static final long OPEN_EXISTING = 3;
   		public static final long OPEN_ALWAYS = 4;
   		public static final long TRUNCATE_EXISTING = 5;
   
   		public static final long FILE_BEGIN = 0;
   		public static final long FILE_CURRENT = 1;
   		public static final long FILE_END = 2;
   
   		public static final long FILE_ATTRIBUTE_NORMAL = 0x00000080L;
   
   		/**
   		 * Create a directory with permissions set to the specified mode. By setting
   		 * permissions at creation time, we avoid issues related to the user lacking
   		 * WRITE_DAC rights on subsequent chmod calls. One example where this can occur
   		 * is writing to an SMB share where the user does not have Full Control rights,
   		 * and therefore WRITE_DAC is denied.
   		 *
   		 * @param path
   		 *            directory to create
   		 * @param mode
   		 *            permissions of new directory
   		 * @throws IOException
   		 *             if there is an I/O error
   		 */
   		public static void createDirectoryWithMode(File path, int mode) throws IOException {
   			createDirectoryWithMode0(path.getAbsolutePath(), mode);
   		}
   
   		/** Wrapper around CreateDirectory() on Windows */
   		private static native void createDirectoryWithMode0(String path, int mode) throws NativeIOException;
   
   		/** Wrapper around CreateFile() on Windows */
   		public static native FileDescriptor createFile(String path, long desiredAccess, long shareMode,
   				long creationDisposition) throws IOException;
   
   		/**
   		 * Create a file for write with permissions set to the specified mode. By
   		 * setting permissions at creation time, we avoid issues related to the user
   		 * lacking WRITE_DAC rights on subsequent chmod calls. One example where this
   		 * can occur is writing to an SMB share where the user does not have Full
   		 * Control rights, and therefore WRITE_DAC is denied.
   		 *
   		 * This method mimics the semantics implemented by the JDK in
   		 * {@link java.io.FileOutputStream}. The file is opened for truncate or append,
   		 * the sharing mode allows other readers and writers, and paths longer than
   		 * MAX_PATH are supported. (See io_util_md.c in the JDK.)
   		 *
   		 * @param path
   		 *            file to create
   		 * @param append
   		 *            if true, then open file for append
   		 * @param mode
   		 *            permissions of new directory
   		 * @return FileOutputStream of opened file
   		 * @throws IOException
   		 *             if there is an I/O error
   		 */
   		public static FileOutputStream createFileOutputStreamWithMode(File path, boolean append, int mode)
   				throws IOException {
   			long desiredAccess = GENERIC_WRITE;
   			long shareMode = FILE_SHARE_READ | FILE_SHARE_WRITE;
   			long creationDisposition = append ? OPEN_ALWAYS : CREATE_ALWAYS;
   			return new FileOutputStream(
   					createFileWithMode0(path.getAbsolutePath(), desiredAccess, shareMode, creationDisposition, mode));
   		}
   
   		/** Wrapper around CreateFile() with security descriptor on Windows */
   		private static native FileDescriptor createFileWithMode0(String path, long desiredAccess, long shareMode,
   				long creationDisposition, int mode) throws NativeIOException;
   
   		/** Wrapper around SetFilePointer() on Windows */
   		public static native long setFilePointer(FileDescriptor fd, long distanceToMove, long moveMethod)
   				throws IOException;
   
   		/** Windows only methods used for getOwner() implementation */
   		private static native String getOwner(FileDescriptor fd) throws IOException;
   
   		/** Supported list of Windows access right flags */
   		public static enum AccessRight {
   			ACCESS_READ(0x0001), // FILE_READ_DATA
   			ACCESS_WRITE(0x0002), // FILE_WRITE_DATA
   			ACCESS_EXECUTE(0x0020); // FILE_EXECUTE
   
   			private final int accessRight;
   
   			AccessRight(int access) {
   				accessRight = access;
   			}
   
   			public int accessRight() {
   				return accessRight;
   			}
   		};
   
   		/**
   		 * Windows only method used to check if the current process has requested access
   		 * rights on the given path.
   		 */
   		private static native boolean access0(String path, int requestedAccess);
   
   		/**
   		 * Checks whether the current process has desired access rights on the given
   		 * path.
   		 * 
   		 * Longer term this native function can be substituted with JDK7 function
   		 * Files#isReadable, isWritable, isExecutable.
   		 *
   		 * @param path
   		 *            input path
   		 * @param desiredAccess
   		 *            ACCESS_READ, ACCESS_WRITE or ACCESS_EXECUTE
   		 * @return true if access is allowed
   		 * @throws IOException
   		 *             I/O exception on error
   		 */
   		public static boolean access(String path, AccessRight desiredAccess) throws IOException {
   			return true;
   			// return access0(path, desiredAccess.accessRight());
   		}
   
   		/**
   		 * Extends both the minimum and maximum working set size of the current process.
   		 * This method gets the current minimum and maximum working set size, adds the
   		 * requested amount to each and then sets the minimum and maximum working set
   		 * size to the new values. Controlling the working set size of the process also
   		 * controls the amount of memory it can lock.
   		 *
   		 * @param delta
   		 *            amount to increment minimum and maximum working set size
   		 * @throws IOException
   		 *             for any error
   		 * @see POSIX#mlock(ByteBuffer, long)
   		 */
   		public static native void extendWorkingSetSize(long delta) throws IOException;
   
   		static {
   			if (NativeCodeLoader.isNativeCodeLoaded()) {
   				try {
   					initNative();
   					nativeLoaded = true;
   				} catch (Throwable t) {
   					// This can happen if the user has an older version of libhadoop.so
   					// installed - in this case we can continue without native IO
   					// after warning
   					PerformanceAdvisory.LOG.debug("Unable to initialize NativeIO libraries", t);
   				}
   			}
   		}
   	}
   
   	private static final Log LOG = LogFactory.getLog(NativeIO.class);
   
   	private static boolean nativeLoaded = false;
   
   	static {
   		if (NativeCodeLoader.isNativeCodeLoaded()) {
   			try {
   				initNative();
   				nativeLoaded = true;
   			} catch (Throwable t) {
   				// This can happen if the user has an older version of libhadoop.so
   				// installed - in this case we can continue without native IO
   				// after warning
   				PerformanceAdvisory.LOG.debug("Unable to initialize NativeIO libraries", t);
   			}
   		}
   	}
   
   	/**
   	 * Return true if the JNI-based native IO extensions are available.
   	 */
   	public static boolean isAvailable() {
   		return NativeCodeLoader.isNativeCodeLoaded() && nativeLoaded;
   	}
   
   	/** Initialize the JNI method ID and class ID cache */
   	private static native void initNative();
   
   	/**
   	 * Get the maximum number of bytes that can be locked into memory at any given
   	 * point.
   	 *
   	 * @return 0 if no bytes can be locked into memory; Long.MAX_VALUE if there is
   	 *         no limit; The number of bytes that can be locked into memory
   	 *         otherwise.
   	 */
   	static long getMemlockLimit() {
   		return isAvailable() ? getMemlockLimit0() : 0;
   	}
   
   	private static native long getMemlockLimit0();
   
   	/**
   	 * @return the operating system's page size.
   	 */
   	static long getOperatingSystemPageSize() {
   		try {
   			Field f = Unsafe.class.getDeclaredField("theUnsafe");
   			f.setAccessible(true);
   			Unsafe unsafe = (Unsafe) f.get(null);
   			return unsafe.pageSize();
   		} catch (Throwable e) {
   			LOG.warn("Unable to get operating system page size.  Guessing 4096.", e);
   			return 4096;
   		}
   	}
   
   	private static class CachedUid {
   		final long timestamp;
   		final String username;
   
   		public CachedUid(String username, long timestamp) {
   			this.timestamp = timestamp;
   			this.username = username;
   		}
   	}
   
   	private static final Map<Long, CachedUid> uidCache = new ConcurrentHashMap<Long, CachedUid>();
   	private static long cacheTimeout;
   	private static boolean initialized = false;
   
   	/**
   	 * The Windows logon name has two part, NetBIOS domain name and user account
   	 * name, of the format DOMAIN\UserName. This method will remove the domain part
   	 * of the full logon name.
   	 *
   	 * @param Fthe
   	 *            full principal name containing the domain
   	 * @return name with domain removed
   	 */
   	private static String stripDomain(String name) {
   		int i = name.indexOf('\\');
   		if (i != -1)
   			name = name.substring(i + 1);
   		return name;
   	}
   
   	public static String getOwner(FileDescriptor fd) throws IOException {
   		ensureInitialized();
   		if (Shell.WINDOWS) {
   			String owner = Windows.getOwner(fd);
   			owner = stripDomain(owner);
   			return owner;
   		} else {
   			long uid = POSIX.getUIDforFDOwnerforOwner(fd);
   			CachedUid cUid = uidCache.get(uid);
   			long now = System.currentTimeMillis();
   			if (cUid != null && (cUid.timestamp + cacheTimeout) > now) {
   				return cUid.username;
   			}
   			String user = POSIX.getUserName(uid);
   			LOG.info("Got UserName " + user + " for UID " + uid + " from the native implementation");
   			cUid = new CachedUid(user, now);
   			uidCache.put(uid, cUid);
   			return user;
   		}
   	}
   
   	/**
   	 * Create a FileInputStream that shares delete permission on the file opened,
   	 * i.e. other process can delete the file the FileInputStream is reading. Only
   	 * Windows implementation uses the native interface.
   	 */
   	public static FileInputStream getShareDeleteFileInputStream(File f) throws IOException {
   		if (!Shell.WINDOWS) {
   			// On Linux the default FileInputStream shares delete permission
   			// on the file opened.
   			//
   			return new FileInputStream(f);
   		} else {
   			// Use Windows native interface to create a FileInputStream that
   			// shares delete permission on the file opened.
   			//
   			FileDescriptor fd = Windows.createFile(f.getAbsolutePath(), Windows.GENERIC_READ,
   					Windows.FILE_SHARE_READ | Windows.FILE_SHARE_WRITE | Windows.FILE_SHARE_DELETE,
   					Windows.OPEN_EXISTING);
   			return new FileInputStream(fd);
   		}
   	}
   
   	/**
   	 * Create a FileInputStream that shares delete permission on the file opened at
   	 * a given offset, i.e. other process can delete the file the FileInputStream is
   	 * reading. Only Windows implementation uses the native interface.
   	 */
   	public static FileInputStream getShareDeleteFileInputStream(File f, long seekOffset) throws IOException {
   		if (!Shell.WINDOWS) {
   			RandomAccessFile rf = new RandomAccessFile(f, "r");
   			if (seekOffset > 0) {
   				rf.seek(seekOffset);
   			}
   			return new FileInputStream(rf.getFD());
   		} else {
   			// Use Windows native interface to create a FileInputStream that
   			// shares delete permission on the file opened, and set it to the
   			// given offset.
   			//
   			FileDescriptor fd = NativeIO.Windows.createFile(
   					f.getAbsolutePath(), NativeIO.Windows.GENERIC_READ, NativeIO.Windows.FILE_SHARE_READ
   							| NativeIO.Windows.FILE_SHARE_WRITE | NativeIO.Windows.FILE_SHARE_DELETE,
   					NativeIO.Windows.OPEN_EXISTING);
   			if (seekOffset > 0)
   				NativeIO.Windows.setFilePointer(fd, seekOffset, NativeIO.Windows.FILE_BEGIN);
   			return new FileInputStream(fd);
   		}
   	}
   
   	/**
   	 * Create the specified File for write access, ensuring that it does not exist.
   	 * 
   	 * @param f
   	 *            the file that we want to create
   	 * @param permissions
   	 *            we want to have on the file (if security is enabled)
   	 *
   	 * @throws AlreadyExistsException
   	 *             if the file already exists
   	 * @throws IOException
   	 *             if any other error occurred
   	 */
   	public static FileOutputStream getCreateForWriteFileOutputStream(File f, int permissions) throws IOException {
   		if (!Shell.WINDOWS) {
   			// Use the native wrapper around open(2)
   			try {
   				FileDescriptor fd = NativeIO.POSIX.open(f.getAbsolutePath(),
   						NativeIO.POSIX.O_WRONLY | NativeIO.POSIX.O_CREAT | NativeIO.POSIX.O_EXCL, permissions);
   				return new FileOutputStream(fd);
   			} catch (NativeIOException nioe) {
   				if (nioe.getErrno() == Errno.EEXIST) {
   					throw new AlreadyExistsException(nioe);
   				}
   				throw nioe;
   			}
   		} else {
   			// Use the Windows native APIs to create equivalent FileOutputStream
   			try {
   				FileDescriptor fd = NativeIO.Windows.createFile(
   						f.getCanonicalPath(), NativeIO.Windows.GENERIC_WRITE, NativeIO.Windows.FILE_SHARE_DELETE
   								| NativeIO.Windows.FILE_SHARE_READ | NativeIO.Windows.FILE_SHARE_WRITE,
   						NativeIO.Windows.CREATE_NEW);
   				NativeIO.POSIX.chmod(f.getCanonicalPath(), permissions);
   				return new FileOutputStream(fd);
   			} catch (NativeIOException nioe) {
   				if (nioe.getErrorCode() == 80) {
   					// ERROR_FILE_EXISTS
   					// 80 (0x50)
   					// The file exists
   					throw new AlreadyExistsException(nioe);
   				}
   				throw nioe;
   			}
   		}
   	}
   
   	private synchronized static void ensureInitialized() {
   		if (!initialized) {
   			cacheTimeout = new Configuration().getLong("hadoop.security.uid.cache.secs", 4 * 60 * 60) * 1000;
   			LOG.info("Initialized cache for UID to User mapping with a cache" + " timeout of " + cacheTimeout / 1000
   					+ " seconds.");
   			initialized = true;
   		}
   	}
   
   	/**
   	 * A version of renameTo that throws a descriptive exception when it fails.
   	 *
   	 * @param src
   	 *            The source path
   	 * @param dst
   	 *            The destination path
   	 * 
   	 * @throws NativeIOException
   	 *             On failure.
   	 */
   	public static void renameTo(File src, File dst) throws IOException {
   		if (!nativeLoaded) {
   			if (!src.renameTo(dst)) {
   				throw new IOException("renameTo(src=" + src + ", dst=" + dst + ") failed.");
   			}
   		} else {
   			renameTo0(src.getAbsolutePath(), dst.getAbsolutePath());
   		}
   	}
   
   	public static void link(File src, File dst) throws IOException {
   		if (!nativeLoaded) {
   			HardLink.createHardLink(src, dst);
   		} else {
   			link0(src.getAbsolutePath(), dst.getAbsolutePath());
   		}
   	}
   
   	/**
   	 * A version of renameTo that throws a descriptive exception when it fails.
   	 *
   	 * @param src
   	 *            The source path
   	 * @param dst
   	 *            The destination path
   	 * 
   	 * @throws NativeIOException
   	 *             On failure.
   	 */
   	private static native void renameTo0(String src, String dst) throws NativeIOException;
   
   	private static native void link0(String src, String dst) throws NativeIOException;
   
   	/**
   	 * Unbuffered file copy from src to dst without tainting OS buffer cache
   	 *
   	 * In POSIX platform: It uses FileChannel#transferTo() which internally attempts
   	 * unbuffered IO on OS with native sendfile64() support and falls back to
   	 * buffered IO otherwise.
   	 *
   	 * It minimizes the number of FileChannel#transferTo call by passing the the src
   	 * file size directly instead of a smaller size as the 3rd parameter. This saves
   	 * the number of sendfile64() system call when native sendfile64() is supported.
   	 * In the two fall back cases where sendfile is not supported,
   	 * FileChannle#transferTo already has its own batching of size 8 MB and 8 KB,
   	 * respectively.
   	 *
   	 * In Windows Platform: It uses its own native wrapper of CopyFileEx with
   	 * COPY_FILE_NO_BUFFERING flag, which is supported on Windows Server 2008 and
   	 * above.
   	 *
   	 * Ideally, we should use FileChannel#transferTo() across both POSIX and Windows
   	 * platform. Unfortunately, the
   	 * wrapper(Java_sun_nio_ch_FileChannelImpl_transferTo0) used by
   	 * FileChannel#transferTo for unbuffered IO is not implemented on Windows. Based
   	 * on OpenJDK 6/7/8 source code, Java_sun_nio_ch_FileChannelImpl_transferTo0 on
   	 * Windows simply returns IOS_UNSUPPORTED.
   	 *
   	 * Note: This simple native wrapper does minimal parameter checking before copy
   	 * and consistency check (e.g., size) after copy. It is recommended to use
   	 * wrapper function like the Storage#nativeCopyFileUnbuffered() function in
   	 * hadoop-hdfs with pre/post copy checks.
   	 *
   	 * @param src
   	 *            The source path
   	 * @param dst
   	 *            The destination path
   	 * @throws IOException
   	 */
   	public static void copyFileUnbuffered(File src, File dst) throws IOException {
   		if (nativeLoaded && Shell.WINDOWS) {
   			copyFileUnbuffered0(src.getAbsolutePath(), dst.getAbsolutePath());
   		} else {
   			FileInputStream fis = null;
   			FileOutputStream fos = null;
   			FileChannel input = null;
   			FileChannel output = null;
   			try {
   				fis = new FileInputStream(src);
   				fos = new FileOutputStream(dst);
   				input = fis.getChannel();
   				output = fos.getChannel();
   				long remaining = input.size();
   				long position = 0;
   				long transferred = 0;
   				while (remaining > 0) {
   					transferred = input.transferTo(position, remaining, output);
   					remaining -= transferred;
   					position += transferred;
   				}
   			} finally {
   				IOUtils.cleanup(LOG, output);
   				IOUtils.cleanup(LOG, fos);
   				IOUtils.cleanup(LOG, input);
   				IOUtils.cleanup(LOG, fis);
   			}
   		}
   	}
   
   	private static native void copyFileUnbuffered0(String src, String dst) throws NativeIOException;
   }
   ```

10. 自定义Outputformat时，注意在RecordWirter中的close方法必须关闭流资源。否则输出的文件内容中数据为空。

    ```java
    @Override
    public void close(TaskAttemptContext context) throws IOException, InterruptedException {
    		if (atguigufos != null) {
    			atguigufos.close();
    		}
    		if (otherfos != null) {
    			otherfos.close();
    		}
    }
    ```

    

