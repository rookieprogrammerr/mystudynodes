# Docker概念

### 什么是Docker

Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的镜像中，然后发布到任何流行的 Linux或Windows 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。

### 为什么要使用Docker?

企业使用一项技术是为了解决当前企业环境中存在的某个痛点。目前整个软件行业存在着以下几个痛点

1. 软件更新发布及部署低效，过程烦琐且需要人工介入。
2. 环境一致性难以保证。 
3. 不同环境之间迁移成本太高。

### Docker的思想

隔离：Docker的核心思想，将所有的项目打包装箱，每个箱子都是相互隔离的



### 关于Docker

1. Docker通过隔离机制，可以将服务器利用到机制
2. 虚拟机属于虚拟化技术，Docker容器技术也是一种虚拟化技术
3. Docker是基于Go语言开发的开源项目，是内核级别的虚拟化，可以在一个物理机上运行很多的容器实例。服务器的性能可以运行到极致

**[Docker官方网站](https://www.docker.com)：https://www.docker.com**
**[Docker文档地址](https://docs.docker.com/)：https://docs.docker.com/**
**[仓库地址](https://hub.docker.com/)：https://hub.docker.com/**

### Docker能干嘛
##### 虚拟机技术缺点

1. 资源占用十分多
2. 冗余步骤多
3. 启动速度慢

##### Docker的好处

1. 应用更快速的交付和部署，即打包镜像发布测试，一键部署
2. 更便捷的升级和扩缩容
3. 更简单的系统运维，开发和测试环境都是高度一致的
4. 更高效的计算资源利用
5. 

##### Docker和虚拟机的区别

* 传统虚拟机，虚拟出一条硬件，运行出一个完整的操作系统，然后在这个系统上安装并运行软件
* 容器内的应用直接运行在 **宿主机** 的内容，容器是没有自己的内核的，也没有虚拟我们的硬件，更加轻量级
* 每个容器间是互相隔离，每个容器内都有一个属于自己的文件系统，互不影响

# Docker安装
### Docker的基本组成!

![img](http://zhaocan.fym233.cn/20210121100822.png)

**镜像（image）：**

  * Docker镜像就好比一个模板，可以通过这个模板来创建容器服务。通过这个镜像可以创建多个容器（最终服务运行或者项目运行就是在容器中的）

**容器（container）：**

  * Docker利用容器技术，独立运行一个或一组应用，通过镜像创建的。
  * 容器的基本操作：启动，停止，删除

    

**仓库（repository）：**
  * 仓库就是存放镜像的地方（类似于git），仓库分为公有仓库和私有仓库
  * DockerHub（默认是国外的）

  ### 安装Docker

##### windows安装

![](https://i.loli.net/2021/01/05/NRLxHnQveW6J3tT.png)


* docker desktop 基于windows hyper-v，必须确保hyper-v组件已经开启。可通过如下PowerShell （管理员身份）命令启动。
  ````powershell
    C:\Users\Administrator>dism.exe /Online /Enable-Feature:Microsoft-Hyper-V /All
  ````
* hyper-v组件开启后，需确保其守护进程自动运行（我问题出在这里，守护进程没有运行），可通过如下PowerShell（管理员身份） 命令启动：
````powershell
C:\Users\Administrator>bcdedit /set hypervisorlaunchtype auto
````

##### Linux安装
##### 环境准备

1.   需要会一点点的Linux的基础
2.   Centos
3.   使用Xshell连接远程服务器进行操作

##### 环境查看
````shell
   # 系统内核查看
   # uname -r
   
   #系统版本查看
   # cat /etc/os-release
````

````shell
#1、卸载旧的版本
[root@VM-8-3-centos /] $ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine 
                  
 #2、需要的安装包
 [root@VM-8-3-centos /] yum install -y yum-utils
 
 #3、设置镜像的仓库
 [root@VM-8-3-centos /] yum -config -manager \
    --add-repo \
  https://download.docker.com/linux/centos/docker-ce.repo  #默认是国外的

 [root@VM-8-3-centos /] yum -config -manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo  #阿里云镜像
    
 #更新yum软件包索引
[root@VM-8-3-centos /]# yum makecache fast
 
 #4 安装Docker引擎
 // docker-ce社区版
[root@VM-8-3-centos /]# yum install docker-ce docker-ce-cli containerd.io

#5、启动docker
[root@VM-8-3-centos /]# systemctl start docker

#6、查看是否安装成功
[root@VM-8-3-centos /]# docker version

#7、测试hello world
[root@VM-8-3-centos /]# docker run hello-world

#8、查看下载的hello world镜像
[root@VM-8-3-centos /]# docker images
`````
![](http://zhaocan.fym233.cn/20210121093358.png)

##### 卸载Docker

`````shell
#1、卸载依赖
[root@VM-8-3-centos /]# yum remove docker-ce-cli contaionerd.io

#2、删除资源
[root@VM-8-3-centos /]# rm -rf /var/lib/docker

#/var/lib/docker       docker的默认工作路径
`````

##### 阿里云镜像加速

1. 登录阿里云
2. 找到容器镜像服务
3. 配置使用
``````shell
[root@VM-8-3-centos /]# sudo mkdir -p /etc/docker 

[root@VM-8-3-centos /]# sudo tee /etc/docker/daemon.json <<-'EOF' { "registry-mirrors": ["https://c792n0vc.mirror.aliyuncs.com"] } 
EOF 

[root@VM-8-3-centos /]# sudo systemctl daemon-reload 

[root@VM-8-3-centos /]# sudo systemctl restart docker
```````

##### 回顾HelloWorld流程

![](http://zhaocan.fym233.cn/20210121093359.png)

![](http://zhaocan.fym233.cn/20210121093400.png)


### Docker的底层原理

##### Docker是怎么工作的？
Docker是一个Client-Server结构的系统，Docker的守护进程运行在**宿主机**上，通过Socket从客户端访问。Docker-Server接收到Docker-Client的指令，就会执行这个命令

![](http://zhaocan.fym233.cn/20210121093401.png)

##### Docker为什么比虚拟机快？

1. Docker有着比虚拟机更少的抽象层
2. Docker利用的是宿主机的内核，虚拟机需要是GuestOS

![](http://zhaocan.fym233.cn/20210121093402.png)

**所以，新建一个容器的时候，Docker不需要像虚拟机一样重新加载一个操作系统内核，避免引导。虚拟机是加载GuestOS，是分钟级别的；而Docker是利用宿主机的操作系统，省略了这个复杂的过程，是秒级别的。**
![](http://zhaocan.fym233.cn/20210121093403.png)

### Docker的常用命令
##### 帮助命令
``````shell
docker version      # 显示docker的版本信息
docker info         # 显示docker的系统信息，包括镜像和容器的数量
docker --help       # 帮助命令
``````

[帮助文档](https://docs.docker.com/reference/)：https://docs.docker.com/reference/

##### 镜像命令
**docker images** 查看所有本地的主机上的镜像

`````shell
[root@VM-8-3-centos /]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    bf756fb1ae65   11 months ago   13.3kB

#解释
REPOSITORY：镜像的仓库源
TAG：镜像的标签
IMAGE ID ：镜像的id
CREATED：镜像的创建时间
SIZE：镜像的大小

#可选项
Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs

-a，--all：列出所有镜像
-q，--quiet：只显示镜像的id
`````
**docker search  搜索镜像**
`````shell
[root@VM-8-3-centos /]# docker search mysql

#可选项，通过搜索来过滤
--filter=STARS=3000     搜索出来的镜像STARS大于3000

[root@VM-8-3-centos /]# docker search mysql --filter=STARS=3000
NAME      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql     MySQL is a widely used, open-source relation…   10247     [OK]       
mariadb   MariaDB is a community-developed fork of MyS…   3785      [OK]  

`````

**docker pull 下载镜像**

`````shell
#下载镜像 docker pull 镜像名[：tag
]

[root@VM-8-3-centos /]# docker pull mysql
Using default tag: latest           #如果不写tag默认拉取最新版本
latest: Pulling from library/mysql
852e50cd189d: Pull complete    #分层下载，docker images的核心
29969ddb0ffb: Pull complete 
a43f41a44c48: Pull complete 
5cdd802543a3: Pull complete 
b79b040de953: Pull complete 
938c64119969: Pull complete 
7689ec51a0d9: Pull complete 
a880ba7c411f: Pull complete 
984f656ec6ca: Pull complete 
9f497bce458a: Pull complete 
b9940f97694b: Pull complete 
2f069358dc96: Pull complete 
Digest: sha256:4bb2e81a40e9d0d59bd8e3dc2ba5e1f2197696f6de39a91e90798dd27299b093
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest      #真实地址，即
docker pull mysql = docker pull docker.io/library/mysql:latest 

#指定版本下载
[root@VM-8-3-centos /]# docker pull mysql:5.7
5.7: Pulling from library/mysql
852e50cd189d: Already exists 
29969ddb0ffb: Already exists 
a43f41a44c48: Already exists 
5cdd802543a3: Already exists 
b79b040de953: Already exists 
938c64119969: Already exists 
7689ec51a0d9: Already exists 
36bd6224d58f: Pull complete 
cab9d3fa4c8c: Pull complete 
1b741e1c47de: Pull complete 
aac9d11987ac: Pull complete 
Digest: sha256:8e2004f9fe43df06c3030090f593021a5f283d028b5ed5765cc24236c2c4d88e
Status: Downloaded newer image for mysql:5.7
docker.io/library/mysql:5.7


`````
![](http://zhaocan.fym233.cn/20210121093404.png)

**docker rmi 删除镜像**
rm：删除
i：images

`````shell
[root@VM-8-3-centos /]# docker rmi -f 镜像id #删除指定的镜像
[root@VM-8-3-centos /]# docker rmi -f 镜像id1 镜像id2 镜像id3。。。 #删除多个的镜像

[root@VM-8-3-centos /]# docker rmi -f $(docker images -aq)   #删除全部镜像
`````

##### 容器命令
**说明：有了镜像才能创建容器，Linux，下载一个CentOS镜像测试学习**

`````shell
[root@VM-8-3-centos /]# docker pull centos

#新建容器并启动
[root@VM-8-3-centos /]# docker run [可选参数] images

#参数说明
--name='Name'   # 容器名字，例如tomcat1，tomcat2。。。用于区分容器
-d      # 后台方式运行
-it     # 进入容器
-p      # 指定容器端口 -p  8080:8080
        -p ip:主机端口:容器端口
        -p 主机端口:容器端口 （常用的）
        -p 容器端口
        容器端口
-P      #随机指定端口（大写的P）


#测试，启动容器并进入容器
[root@VM-8-3-centos /]# docker run -it centos /bin/bash
[root@dfd49a746e15 /]# 

#查看容器内的centos，基础版本，很多命令不完善
[root@dfd49a746e15 /]# ls
bin  etc   lib	  lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr

#从容器退回到主机
[root@dfd49a746e15 /]# exit
exit
[root@VM-8-3-centos /]# ls
bin   data  etc   lib    lost+found  mnt  proc  run   srv  tmp  var
boot  dev   home  lib64  media       opt  root  sbin  sys  usr

`````

##### 列出所有的运行的容器
`````shell
# docker ps 命令
         	# 列出当前正在运行的容器
-a      	# 列出当前正在运行的容器+带出历史运行过的容器
-n=？	   # 显示最近创建的容器 ？：跟数字，代表最近创建的多少个容器
-q     		# 只显示容器的编号
-aq    		# 显示所有容器的编号

[root@VM-8-3-centos /]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@VM-8-3-centos /]# docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED         STATUS                     PORTS     NAMES
dfd49a746e15   centos        "/bin/bash"   7 minutes ago   Exited (0) 4 minutes ago             focused_germain
df18a0e46849   hello-world   "/hello"      2 hours ago     Exited (0) 2 hours ago               serene_chaplygin
2ec419a77230   hello-world   "/hello"      4 hours ago     Exited (0) 4 hours ago               magical_brown

`````

**退出容器**
`````shell
exit    			# 退出容器
快捷键Ctrl+P+Q    	  # 容器不停止退出
`````

**删除容器**

`````shell
docker rm 容器id      			   # 删除指定容器，不能删除正在运行的容器，如果要强制删除 rm -f   
docker rm -f $(docker ps -aq)   	# 删除所有容器
docker ps -a -q|xargs docker rm 	# 删除所有容器
`````

**启动和停止容器的操作**
`````shell
docker start 容器id       	# 启动容器
docker restart 容器id   		# 重启容器
docker stop 容器id       		# 停止当前正在运行的容器
docker kill 容器id         	# 强制停止当前容器
`````



### 常用其他命令

##### 后台启动容器

```shell
# 命令 docker -run -d 镜像名
[root@VM-8-3-centos /]# docker run -d centos

# 问题：  使用docker ps命令后发现 centos停止了

# docker容器使用后台运行，就必须要有一个前台进程，docker发现没有应用，就会自动停止
# 容器启动后，发现自己没有提供服务，就会立刻停止
```

##### 查看日志

```shell
docker logs -f -t --tail 容器，没有日志

# 自己编写一段shell脚本
[root@VM-8-3-centos /]# docker run -d centos /bin/sh -c "while true;do echo kuangshen;sleep 1;done"

# [root@VM-8-3-centos /]# docker ps
CONTAINER ID   IMAGE
2ec419a77230   centos

# 显示日志
-tf						# 显示日志
--tail number 			# number：要显示多少条日志
[root@VM-8-3-centos /]# docker logs -tf --tail 10 2ec419a77230
```

##### 查看容器中进程信息

```shell
# 命令 docker top 容器id
[root@VM-8-3-centos /]# docker top 2ec419a77230
UID			PID			PPID		C		STIME		TTY	
root		22891		22875		0		16:15		?
root		23351		22891		0		16:15		?
```

##### 查看元数据

```shell
# 命令 
docker inspect 容器id

#测试
[root@VM-8-3-centos /]# docker inspect 8d9d08163c44
[
    {
        "Id": "8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9",
        "Created": "2020-12-11T07:58:08.862929488Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "exited",
            "Running": false,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 0,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-12-11T07:58:09.1334543Z",
            "FinishedAt": "2020-12-11T07:58:09.141032725Z"
        },
        "Image": "sha256:300e315adb2f96afe5f0b2780b87f28ae95231fe3bdd1e16b9ba606307728f55",
        "ResolvConfPath": "/var/lib/docker/containers/8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9/hostname",
        "HostsPath": "/var/lib/docker/containers/8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9/hosts",
        "LogPath": "/var/lib/docker/containers/8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9/8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9-json.log",
        "Name": "/affectionate_johnson",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/a3271183f6b309fb4c8871fd4cfd178cf76d797aabbd0ae8bba5f6a3792d60ff-init/diff:/var/lib/docker/overlay2/aa70f6c8cd9cb9213220f2d3e86a0c090115826ba090240ac9fa46ec52885c57/diff",
                "MergedDir": "/var/lib/docker/overlay2/a3271183f6b309fb4c8871fd4cfd178cf76d797aabbd0ae8bba5f6a3792d60ff/merged",
                "UpperDir": "/var/lib/docker/overlay2/a3271183f6b309fb4c8871fd4cfd178cf76d797aabbd0ae8bba5f6a3792d60ff/diff",
                "WorkDir": "/var/lib/docker/overlay2/a3271183f6b309fb4c8871fd4cfd178cf76d797aabbd0ae8bba5f6a3792d60ff/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "8d9d08163c44",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20201204",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "27d7a59577638cbc74b1b4a574ed36dbf1d06f50599e94b3c4dc8288d78a2628",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/27d7a5957763",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "5778ac1918700bfb934d3da1c2184bc27c7f2147bda769850d82f68b83d434ae",
                    "EndpointID": "",
                    "Gateway": "",
                    "IPAddress": "",
                    "IPPrefixLen": 0,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "",
                    "DriverOpts": null
                }
            }
        }
    }
]

```

##### 进入当前正在运行的容器

```shell
# 通常容器都是使用后台方式运行的，需要进入容器，修改一些配置

# 命令
docker exec -it 容器id bashShell

# 测试

# 方式二
docker attach 容器id
# 测试
[root@VM-8-3-centos /]# docker attach 8d9d08163c44
正在执行当前的代码...


# docker exec			# 进入容器后开启一个新的终端，可以在里面操作
# docker attach			# 进入容器正在执行的终端，不会启动新的进程
```

##### 从容器内拷贝文件到主机上

```shell
docker cp 容器id:容器内路径 目的的主机路径
```

![](http://zhaocan.fym233.cn/20210121094303.png)



#### 练习1

> Docker安装Nginx

```shell
# 1、 搜索镜像 docker search

# 2、 下载镜像 docker pull

# 3、 运行测试
[root@VM-8-3-centos ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
nginx         latest    7baf28ea91eb   2 days ago      133MB
centos        latest    300e315adb2f   6 days ago      209MB
mysql         latest    dd7265748b5d   3 weeks ago     545MB
hello-world   latest    bf756fb1ae65   11 months ago   13.3kB
	# -d					后台运行
	# --name				给容器命名
	# -p 宿主机端口:容器内部端口

[root@VM-8-3-centos ~]# docker run -d --name nginx01 -p 3344:80 nginx
775f90c4b06e3dba777afd6bfd85b9ce863cad5a28ab7cc1bb3960725ac41347
[root@VM-8-3-centos ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS         PORTS                  NAMES
775f90c4b06e   nginx     "/docker-entrypoint.…"   10 seconds ago   Up 9 seconds   0.0.0.0:3344->80/tcp   nginx01
[root@VM-8-3-centos ~]# curl localhost:3344

# 4、进入容器
[root@VM-8-3-centos ~]# docker exec -it nginx01 /bin/bash
root@775f90c4b06e:/# whereis nginx
nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx
root@775f90c4b06e:/# cd /etc/nginx
root@775f90c4b06e:/etc/nginx# ls
conf.d		koi-utf  mime.types  nginx.conf   uwsgi_params
fastcgi_params	koi-win  modules     scgi_params  win-utf


```

##### 端口暴露

![](http://zhaocan.fym233.cn/20210121094304.png)

#### 练习2

> Docker安装一个tomcat

```shell
# 官方的使用
docker run -it --rm tomcat:9.0

# 之前启动方式都是后台启动，停止容器后，容器还是可以查到的。
# 而docker run -it --rm tomcat:9.0，一般用来测试，用完即删除

# 下载后启动
docker pull tomat:9.0

# 启动运行
[root@VM-8-3-centos ~]# docker run -d -p 8080:8080 --name tomcat01 tomcat

# 测试访问没有问题
[root@VM-8-3-centos ~]# docker exec -it tomcat01 /bin/bash

# 发现问题：1、linux命令少了 2、没有webapps
# 原因：阿里云镜像的原因。默认是最小的镜像，所以不必要的都剔除掉，保证最小可运行的环境

```

#### 练习3

> 部署es+kibana

```shell
# es：Elasticsearch
# es 暴露的端口最多！
# es 十分耗内存
# es 数据一般需要放置到安全目录！挂载

# --net somenetwork ： 网络配置
# -e "discovery.type-single-node" 	:集群，默认单个节点

# 启动 elasticsearch
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2

# docker stats	查看cpu的状态

CONTAINER ID   NAME       CPU %     MEM USAGE / LIMIT     MEM %     NET I/O           BLOCK I/O         PIDS
1128f18ee77c   tomcat01   0.09%     128.9MiB / 990.9MiB   13.00%    118kB / 1.21MB    180MB / 0B        29
775f90c4b06e   nginx01    0.00%     1.512MiB / 990.9MiB   0.15%     9.69kB / 5.01kB   9.06MB / 8.19kB   2



# 增加内存限制，修改配置文件 -e 环境配置修改
# -e ES_JAVA_OPTS=“-Xms64m -Xmx512m” :最小64m~最大512m
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e ES_JAVA_OPTS=“-Xms64m -Xmx512m” -e "discovery.type=single-node" elasticsearch:7.6.2


```

### 可视化

- portainer

- Rancher

  

##### 什么是portainer？

Docker图形化界面管理工具。提供一个后台面板供我们操作	

```shell
docker run -d -p 8088:9000 \
--restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer

```

##### 访问测试

http://81.70.39.205:8088/

![](http://zhaocan.fym233.cn/20210121094305.png)

选择local本地

![](http://zhaocan.fym233.cn/20210121094306.png)

进去之后的面板

![](http://zhaocan.fym233.cn/20210121094618.png)

# Docker镜像

### 什么是镜像

镜像是一种轻量级，可执行的独立软件包。用来打包软件运行环境和基于运行环境开发的软件，它包含运行某个软件所需的所有内容，包括代码、运行时、库、环境变量和配置文件。

**所有的应用，直接打包dkcer镜像，就可以直接跑起来****

如何得到镜像：

- 从远程仓库下载
- 朋友拷贝
- 自己制作一个镜像 DockerFile

### Docker镜像加载原理

> UnionFS（联合文件系统）

UnionFS（联合文件新系统）：Union文件系统（UnionFS）是一种分层、轻量级并且高性能的文件系统，它支持对文件系统的修改作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统下(unite several directories into a single virtual filesystem)。Union文件系统是Docker镜像的基础，镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。

**特性：一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录**



> Docker镜像加载原理

docker的镜像实际上是由一层一层的文件系统组成，这种层级的文件系统UnionFS。

bootfs(boot file system)主要包含bootloader和kernel，bootloader主要是引导加载kernel，Linux刚启动时会加载bootfs

文件系统，在Docker镜像的最底层时bootfs。这一层与我们镜像的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中了，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。

rootfs(root file system)，在bootfs之上。包含的就是经典Linux系统中的/dev，/proc，/bin ，/etc等标准目录和文件。rootfs就是各种不同的操作系统发行版，比如Ubuntu，Centos等等。

![](http://zhaocan.fym233.cn/20210121094619.png)

**平时安装到虚拟机的CentOS都是好几个G，为什么在Docker里才200M？**

![](http://zhaocan.fym233.cn/20210121094620.png)

对于一个精简的OS，rootfs可以很小，只需要包含最基本的命令、工具和程序库就可以了，因为底层直接用Host的kernel，自己只需要提供rootfs就可以了，由此可见对于不同的Linux发行版，bootfs基本是一致的，rootfs会有差别，因此不同的发行版可以公用bootfs。

### 分层原理

>分层的镜像

下载镜像时，主要观察下载的日志输出，可以看到是一层一层的在下载

![](http://zhaocan.fym233.cn/20210121094621.png)**为什么Docker镜像要采用这种分层的结构？**

资源共享，比如有多个镜像都从相同的Base镜像构建而来，那么宿主机只需要在磁盘上保留一份base镜像，同时内存中也只需要加载一份base镜像，这样就可以为所有的容器服务了，而且镜像的每一层都可以被共享。



查看镜像分层的方式可以通过 **docker image inspect** 命令

```shell
[root@VM-8-3-centos /]# docker inspect 8d9d08163c44
[
    {
        "Id": "8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9",
        "Created": "2020-12-11T07:58:08.862929488Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "exited",
            "Running": false,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 0,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-12-11T07:58:09.1334543Z",
            "FinishedAt": "2020-12-11T07:58:09.141032725Z"
        },
        "Image": "sha256:300e315adb2f96afe5f0b2780b87f28ae95231fe3bdd1e16b9ba606307728f55",
        "ResolvConfPath": "/var/lib/docker/containers/8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9/hostname",
        "HostsPath": "/var/lib/docker/containers/8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9/hosts",
        "LogPath": "/var/lib/docker/containers/8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9/8d9d08163c44becf5bd66b1aa41ec007cd6985c8bb0c13be41584f22564156c9-json.log",
        "Name": "/affectionate_johnson",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/a3271183f6b309fb4c8871fd4cfd178cf76d797aabbd0ae8bba5f6a3792d60ff-init/diff:/var/lib/docker/overlay2/aa70f6c8cd9cb9213220f2d3e86a0c090115826ba090240ac9fa46ec52885c57/diff",
                "MergedDir": "/var/lib/docker/overlay2/a3271183f6b309fb4c8871fd4cfd178cf76d797aabbd0ae8bba5f6a3792d60ff/merged",
                "UpperDir": "/var/lib/docker/overlay2/a3271183f6b309fb4c8871fd4cfd178cf76d797aabbd0ae8bba5f6a3792d60ff/diff",
                "WorkDir": "/var/lib/docker/overlay2/a3271183f6b309fb4c8871fd4cfd178cf76d797aabbd0ae8bba5f6a3792d60ff/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "8d9d08163c44",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20201204",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "27d7a59577638cbc74b1b4a574ed36dbf1d06f50599e94b3c4dc8288d78a2628",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/27d7a5957763",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "5778ac1918700bfb934d3da1c2184bc27c7f2147bda769850d82f68b83d434ae",
                    "EndpointID": "",
                    "Gateway": "",
                    "IPAddress": "",
                    "IPPrefixLen": 0,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "",
                    "DriverOpts": null
                }
            }
        }
    }
]
```

##### 理解：

所有的Docker镜像都起始于一个基础镜像层，当进行修改或增加新内容时，就会在当前镜像层之上，创建新的镜像层。



例如基于Ubuntu Linux 16.04创建一个新的镜像，这就是新景象的第一层；如果在该镜像中添加Python包，就会在基础镜像层之上创建第二个镜像层；如果继续添加一个安全补丁，就会创建第三个镜像层。

该镜像当前已经包含3个镜像层，如下图所示（只是一个用于演示的很简单的例子）。

![](http://zhaocan.fym233.cn/20210121094622.png)

在添加额外的镜像层的同时，镜像始终保持时当前所有镜像的组合。下图举一个简单的例子，每一个镜像层都包含3个文件，而镜像包含了来自两个镜像层的6个文件。

![](http://zhaocan.fym233.cn/20210121094623.png)

上图中的镜像层跟之前途中的略有区别，主要目的时便于展示文件。

下图中展示了一个稍微复杂的三层镜像，在外部看来整个镜像只有6个文件，这是因为最上层的文件7时文件5的一个更新版本。

![](http://zhaocan.fym233.cn/20210121094624.png)

这种情况下，上层镜像层中的文件覆盖了底层镜像层中的文件。这样就使得文件的更新版本作为一个新镜像层添加到镜像当中。Docker通过存储引擎（新版本采用快照机制）的方式来实现镜像层堆栈，并保证多镜像层对外展示为统一的文件系统。

Linux上可用的存储引擎有AUFS、Overlay2、Device Mapper、Btrfs以及ZFS。顾名思义，每种存储引擎都基于Linux中对应的文件系统或者快设备技术，并且每种存储引擎都有其独有的性能特点。

Docker在Windows上仅支持windowsfilter一种存储引擎，该引擎基于NTFS文件系统之上实现了分层和CoW[1]。

下图展示了与系统显示相同的三层镜像。所有镜像层堆叠并合并，对外提供统一的视图。

![](http://zhaocan.fym233.cn/20210121094625.png)



> 特点

Docker镜像都是只读的，当容器启动时，一个新的可写层被加载到镜像的顶部。

这一层就是我们通常说的容器层，容器之下的都叫镜像层。

![](http://zhaocan.fym233.cn/20210121094626.png)



### Commit镜像

```shell
docker commit 提交容器成为一个新的副本

# 命令与git原理类似
docker commit -m="提交的描述信息" -a="作者" 容器id 目标镜像名:[tag]
```

##### 实战测试

```shell
# 1、启动一个默认的tomcat

# 2、发现默认的tomcat 时没有webapps应用，镜像的原因，官方的镜像默认webapps下时没有文件的

# 3、自己拷贝基本文件

# 4、将操作过的容器通过commit提交为一个新的镜像。以后就使用修改过的镜像即可，这就是一个修改过的镜像。
```

![](http://zhaocan.fym233.cn/20210121094627.png)



> 使用场景

如果想要保存当前容器的状态，就可以通过commit来提交，获得一个镜像。好比VM中的快照



# 容器数据卷



### 什么时容器数据卷？

##### Docker的理念

将应用的环境打包成一个镜像

**如果将数据都放到容器中，那么如果容器被删除，数据就会丢失**

需求：

1. ​	数据可以持久化
2. ​	MySQL数据可以存储在本地或者其他地方

容器之间可以有一个数据共享的技术。Docker容器中产生的数据同步到本地

**这就是卷技术。目录挂载，将我们容器内的目录挂载到Linux上**

![image-20201215152812411](http://zhaocan.fym233.cn/20210121095117.png)

**总结：容器的持久化和同步操作。容器间也是可以数据共享的**



### 使用数据卷

> 方式一：直接使用命令挂载  -v

```shell
docker run -it -v 主机目录:容器内目录

# 测试
[root@VM-8-3-centos ~]# docker run -it -v /home/test:/home centos /bin/bash

# 启动起来后可以通过 docker inspect 容器id 
```

![image-20201215153834022](http://zhaocan.fym233.cn/20210121095118.png)

测试文件同步后的具体效果

![image-20201215154204487](http://zhaocan.fym233.cn/20210121095119.png)

```shell
# 测试2

1、停止容器
2、宿主机上修改文件
3、重新启动容器
4、容器内的数据依旧是同步的
```

![image-20201215154637164](http://zhaocan.fym233.cn/20210121095120.png)

**好处：以后修改只需要在本地修改即可，容器内会自动同步**

### 实战：安装MySQL

需要注意的问题：MySQL的数据持久化问题

```shell
# 获取镜像
[root@VM-8-3-centos /]# docker pull mysql:5.7

# 运行容器，需要做数据挂载
# 安装启动mysql时，需要配置密码！

# 官方测试： docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

# 启动容器
-d		后台运行
-p		端口映射
-v		数据卷挂载
-e		环境配置
--name	容器名字

[root@VM-8-3-centos /]# docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v/home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=3306 --name mysql01 mysql:5.7
1351cb48a033cdfa6f49eb672668acae4cb6ee2145f39f09dd3365abd92fc888

# 启动成功后，在本地可以使用sqlyog/navicat来测试一下
# sqlyog连接到服务器的3310端口，服务器的3310端口与容器内的3306端口映射，这样就可以连接上了。

# 在本地测试创建一个数据库，查看一下映射的路径是否ok
```

假设将容器删除

![image-20201216092031191](http://zhaocan.fym233.cn/20210121095121.png)

发现挂载到本地的数据卷依旧没有丢失，这就实现了容器数据持久化功能

### 具名挂载和匿名挂载

```shell
# 匿名挂载
-v 容器内路径
docker run -d -P --name nginx01 -v /etc/nginx nginx

# 查看所有 volume的情况
[root@VM-8-3-centos /]# docker volume ls
DRIVER    VOLUME NAME
local     b8d50520514210b0bcc96b3d85b8be07220666427828c571a4cf247e53f43918
local     c34af132fb8f6429d2e86ac6e9f788c838fb767db3fdda8eaf2724aebfee9e42

# 这里发现，这种就是匿名挂载，我们在 -v 只写了容器内的路径，没有写容器外的路径

# 具名挂载
[root@VM-8-3-centos /]#  docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx nginx
0ea448f320e143afa55322aedd0acb1520a951154141b682c7e9810b7fd37dfd
[root@VM-8-3-centos /]# docker volume ls
DRIVER    VOLUME NAME
local     b8d50520514210b0bcc96b3d85b8be07220666427828c571a4cf247e53f43918
local     c34af132fb8f6429d2e86ac6e9f788c838fb767db3fdda8eaf2724aebfee9e42
local     juming-nginx
# 通过 -v 卷名：容器内路径  来查看这个卷
[root@VM-8-3-centos /]# docker volume inspect juming-nginx

[
    {
        "CreatedAt": "2020-12-16T09:29:23+08:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/juming-nginx/_data",
        "Name": "juming-nginx",
        "Options": null,
        "Scope": "local"
    }
]

# Mountpoint：卷的存储地址
# 所有的coker容器内的卷，没有指定目录的情况下都是在 /var/lib/docker/volumes/xxxxx/_data 

# 我们通过具名挂载可以方便的找到我们的一个卷，大多数情况在使用的都是“具名挂载”。
```

```shell
# 如何确定是具名挂载还是匿名挂载，还是指定路径挂载
-v 容器内路径			 # 匿名挂载
-v 卷名:容器内路径	   	    # 具名挂载	
-v /宿主机路径:容器内路径	  # 指定路径挂载

```

拓展：

```shell
# 通过 -v 容器内路径:ro/rw 改变读写权限
# ro：readonly	只读
# rw：readwrite	可读写

# 一旦设置了容器权限，容器对我们挂载出来的内容就有限定了
docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx:ro nginx
docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx:rw nginx

# ro 只要看到ro就说明这个路径只能通过宿主机来操作，容器内部是无法操作的
```

### 初识Dockerfile

Dockerfile就是用来构建 docker 镜像的构建文件，一段命令脚本

**通过这个脚本可以生成镜像，镜像是一层一层的，脚本一个一个的命令，每个命令都是一层**

```shell
# 创建一个dockerfile文件，名字可以自定义 建议Dockerfile
# 文件中的内容
# 格式：指令(大写) 参数
FROM centos

VOLUME ["volume01","volume02"]

CMD echo "----end----"
CMD /bin/bash

# 这里的每个命令，都是镜像的一层
[root@VM-8-3-centos docker-test-volume]# docker build -f dockerfile -t zhaocan/centos .
```



![image-20201216095905720](http://zhaocan.fym233.cn/20210121095122.png)

```shell
# 启动自己写的容器
```

![image-20201216100605366](http://zhaocan.fym233.cn/20210121095123.png)

这个卷和外部一定有一个同步的目录

![image-20201216100700346](http://zhaocan.fym233.cn/20210121095124.png)

查看一下卷挂载的路径

![image-20201216101247996](http://zhaocan.fym233.cn/20210121095125.png)

测试一下刚才的文件是否同步出去

这种方式我们未来使用的十分多，因为通常会构建自己的镜像

假设构建镜像的时候没有挂载卷，要收动镜像挂载 -v 卷名:容器内路径



### 数据卷容器

![image-20201216112943459](http://zhaocan.fym233.cn/20210121095618.png)

```shell
# 启动3个容器，通过刚才自己写的镜像启动
```

![image-20201218131922861](http://zhaocan.fym233.cn/20210121095619.png)

![image-20201218133939078](http://zhaocan.fym233.cn/20210121095620.png)

![image-20201218134353986](http://zhaocan.fym233.cn/20210121095621.png)

**关键词：--volume-from 只要通过他我们就可以实现容器间的数据共享了**

```shell
# 测试：删除docker01，查看docker02和docker03是否还可以访问这个文件
# 测试结果：依旧可以访问

# 使用的是拷贝概念，即双向同步。只要还有至少一个容器还在使用该数据，数据就不会丢失
```

![image-20201218134828803](http://zhaocan.fym233.cn/20210121095622.png)

> 使用场景：

**当多个mysql需要实现数据共享时使用**

```shell
[root@VM-8-3-centos /]# docker run -d -p 3310:3306 -v /etc/mysql/conf.d -v /var/lib/mysql -e MYSQL_ROOT_PASSWORD=3306 --name mysql01 mysql:5.7

[root@VM-8-3-centos /]# docker run -d -p 3310:3306 -e MYSQL_ROOT_PASSWORD=3306 --name mysql02 --volume-from mysql01 mysql:5.7
```

**结论：**

容器之间配置信息的传递，数据卷容器的生命周期一直持续到没有容器使用为止。

但是一旦持久化到了本地，本地的数据时不会被删除的！

# DockerFile

### DockerFile介绍

>概念

dockerfile是用来构建docker镜像的文件，是一段命令参数脚本

**构建步骤：**

1. 编写一个dockerfile文件
2. docker build 构建成为一个镜像
3. docker run 运行镜像
4. docker push 发布镜像（DockerHub，阿里云镜像仓库）

查看官方文档操作

![image-20201218140515322](http://zhaocan.fym233.cn/20210121095623.png)

![image-20201218143247842](http://zhaocan.fym233.cn/20210121095624.png)

很多官方镜像都是基础包，很多功能都没有。我们通常会自己搭建自己的镜像

### DockerFile构建过程

**基础知识：**

1. 每个保留关键字（指令）都必须是大写字母
2. 执行从上到下顺序执行
3. “#” 表示注释
4. 每一个指令都会创建提交一个新的镜像层，并提交

![](https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1982640279,3003728739&fm=26&gp=0.jpg)

dockerfile是面向开发的，我们以后要发布项目、做镜像，就需要编写dockerfile文件，非常简单

**步骤：开发，部署，运维  缺一不可**

Docker镜像逐渐成为企业交付的标准，必须要掌握

- DockerFile：构建文件，定义了一切的步骤
- DockerImages：通过 DockerFile 构建生成的镜像，最终发布和运行产品，原来是jar/war
- Docker容器：容器就是镜像运行起来提供服务的



### DockerFile指令

```shell
# FROM			# 基础镜像，就是一切从这里开始构建
# MAINTAINER	# 镜像是谁写的，一般写姓名+邮箱
# RUN			# 镜像构建的时候需要运行的命令
# ADD			# 添加内容
# WORKDIR		# 镜像的工作目录
# VOLUME		# 挂载的目录
# EXPOSE		# 指定暴露端口配置
# CMD			# 指定这个容器启动的时候要运行的命令
# ENTRYPOINT	# 指定这个容器启动的时候要运行的命令
# ONBUILD		# 当构建一个被继承的 DockerFile 的时候就会运行 ONBUILD 指令，触发指令
# COPY			# 类似 ADD 命令，将文件拷贝到镜像中
# ENV			# 构建的时候设置环境变量

# CMD与ENTRYPOINT的区别：
# CMD：只有最后一个会生效，可被替代
# ENTRYPOINT：可以追加命令
```



![](https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=149583840,2981326221&fm=26&gp=0.jpg)

**实战测试：**

Docker Hub 中99%镜像都是从这个基础镜像过来的：**FROM scratch**，然后配置需要的软件和配置来进行构建

![image-20201218143511023](http://zhaocan.fym233.cn/20210121095625.png)

> 创建一个自己的CentOS

```shell
# 1、编写Dockerfile的文件

[root@VM-8-3-centos dockerfile]# cat mydockerfile-centos
FROM centos
MAINTAINER zhaocan<1872751113@qq.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yum -y install vim
RUN yum -y install net-tools
RUN yum -y install clear

EXPOSE 80

CMD echo $MYPATH
CMD echo "-----end-----"
CMD /bin/bash 

# 2、通过这个文件构建镜像
# 命令 docker build -f dockerfile 文件路径 -t 镜像名:[tag]

Successfully built 09460bfb7651
Successfully tagged mycentos:0.1

# 3、测试运行
对比：之前的原生的centos
```

![image-20201218145152007](http://zhaocan.fym233.cn/20210121095626.png)

增加后的镜像

![image-20201218145410093](http://zhaocan.fym233.cn/20210121095627.png)

列出本地进行的变更历史

```shell
docker history imageID
```



![image-20201218145559378](http://zhaocan.fym233.cn/20210121095628.png)



> CMD 和 ENTRYPOINT 的区别

```shell
# CMD			# 指定这个容器启动的时候要运行的命令
# ENTRYPOINT	# 指定这个容器启动的时候要运行的命令
```

测试cmd

```shell
# 编写 dockerfile 文件
[root@VM-8-3-centos dockerfile]# vim dockerfile-cmd-test
FROM centos
CMD["ls","-a"]

# 构建镜像
[root@VM-8-3-centos dockerfile]# docker build -f dockerfile-cmd-test -t cmdtest .

# run 运行，发现ls -a命令生效
[root@VM-8-3-centos dockerfile]# docker run b9f4086389e1
.
..
.dockerenv
bin
dev
etc
home
lib
lib64

# 想追加一个命令 -l
[root@VM-8-3-centos dockerfile]# docker run b9f4086389e1 -l
docker: Error response from daemon: OCI runtime create failed: container_linux.go:370: starting container process caused: exec: "-l": executable file not found in $PATH: unknown.

# cmd的情况下 -l 替换了 CMD["ls","-a"] 命令，-l 不是命令，所以报错
```

测试 ENTRYPOINT

```shell
# 编写 dockerfile 文件
[root@VM-8-3-centos dockerfile]# vim dockerfile-entrypoint-test
FROM centos
ENTRYPOINT ["ls","-a"]

# 构建镜像
[root@VM-8-3-centos dockerfile]# docker build -f dockerfile-entrypoint-test -t entrypoint .

# run 运行，发现ls -a命令生效
[root@VM-8-3-centos dockerfile]# docker run 451aa73a6b76
.
..
.dockerenv
bin
dev
etc
home
lib
lib64

# 测试追加命令，是直接拼接在 ENTRYPOINT ["ls","-a"] 命令的后面！
[root@VM-8-3-centos dockerfile]# docker run 451aa73a6b76 -l
total 56
drwxr-xr-x   1 root root 4096 Dec 18 07:12 .
drwxr-xr-x   1 root root 4096 Dec 18 07:12 ..
-rwxr-xr-x   1 root root    0 Dec 18 07:12 .dockerenv
lrwxrwxrwx   1 root root    7 Nov  3 15:22 bin -> usr/bin
drwxr-xr-x   5 root root  340 Dec 18 07:12 dev
drwxr-xr-x   1 root root 4096 Dec 18 07:12 etc
drwxr-xr-x   2 root root 4096 Nov  3 15:22 home
lrwxrwxrwx   1 root root    7 Nov  3 15:22 lib -> usr/lib
lrwxrwxrwx   1 root root    9 Nov  3 15:22 lib64 -> usr/lib64
drwx------   2 root root 4096 Dec  4 17:37 lost+found
drwxr-xr-x   2 root root 4096 Nov  3 15:22 media
drwxr-xr-x   2 root root 4096 Nov  3 15:22 mnt
drwxr-xr-x   2 root root 4096 Nov  3 15:22 opt
dr-xr-xr-x 115 root root    0 Dec 18 07:12 proc
dr-xr-x---   2 root root 4096 Dec  4 17:37 root
drwxr-xr-x  11 root root 4096 Dec  4 17:37 run
lrwxrwxrwx   1 root root    8 Nov  3 15:22 sbin -> usr/sbin
drwxr-xr-x   2 root root 4096 Nov  3 15:22 srv
dr-xr-xr-x  13 root root    0 Dec 16 02:02 sys
drwxrwxrwt   7 root root 4096 Dec  4 17:37 tmp
drwxr-xr-x  12 root root 4096 Dec  4 17:37 usr
drwxr-xr-x  20 root root 4096 Dec  4 17:37 var
```

**Dockerfile中很多命令都十分的相似，我们需要了解它们的区别**



实战测试：Tomcat镜像

1、准备镜像文件  tomcat的压缩包，jdk的压缩包

![image-20201218162059388](http://zhaocan.fym233.cn/20210121095629.png)

2、编写dockerfile文件，官方命名 **Dockerfile** ，build会自动寻找这个文件，就不需要 -f 指定了

```shell
FROM centos
MAINTAINER <zhaocan1872751113@qq.com>

COPY readme.txt /home/dockerfile/dockerfile-test/readme.txt

ADD jdk-8u271-linux-i586.tar.gz /usr/local/
ADD apache-tomcat-9.0.41.tar.gz /usr/local/

RUN yum -y install vim

ENV MYPATH /usr/local
WORKDIR $MYPATH

ENV JAVA_HOME /usr/local/jdk1.8.0_271
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.41
ENV CATALINA_BASH /usr/local/apache-tomcat-9.0.41
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin

EXPOSE 8080
 
CMD /usr/local/apache-tomcat-9.0.41/bin/startup.sh && tail -F /usr/local/apache-tomcat-9.0.41/bin/logs/catalina.out
```

3、构建镜像

```shell
# docker build -t testtomcat .
```

4、启动镜像

```shell
# docker run -d -p 9090:8080 --name testtomcat -v /fym/docker/testtomcat/test:/usr/local/apache-tomcat-9.0.41/webapps/test -v /fym/docker/testtomcat/tomcatlogs:/usr/local/apache-tomcat-9.0.41/bin/logs testtomcat
```

5、访问测试

```shell
# curl localhost:9090
# 或者在外部访问ip:9090(http://47.98.47.51:9090)
```

6、发布项目（由于做了卷挂载，我们直接在本地编写项目就可以发布了）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
                 			 http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" 
         version="2.5">
         
</web-app>
```

```jsp
<html>
<head><title>Hello zhaocan</title></head>
<body>
Hello World!<br/>
<%
System.out.println("-----my test web logs-----");
%>
</body>
</html>
```

项目部署成功，可以直接访问



### 发布镜像

> Docker Hub

1、地址：https://hub.docker.com/ 注册账号

2、确定账号可以正常登录使用

```shell
[root@iZbp194xjjt5ig1q0i39f8Z tomcatlogs]# docker login --help

Usage:	docker login [OPTIONS] [SERVER]

Log in to a Docker registry.
If no server is specified, the default is defined by the daemon.

Options:
  -p, --password string   Password
      --password-stdin    Take the password from stdin
  -u, --username string   Username
```

3、在服务器上提交自己的镜像

```shell
[root@iZbp194xjjt5ig1q0i39f8Z tomcatlogs]# docker login -u crownqqq
Password: 
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```

4、登录完毕后就可以提交镜像了，就是 **Docker push**

```shell
# push镜像到服务器上
[root@iZbp194xjjt5ig1q0i39f8Z tomcatlogs]# docker push testtomcat

# 拒绝
denied: requested access to the resource is denied

# push镜像的问题
[root@iZbp194xjjt5ig1q0i39f8Z tomcatlogs]# docker push testtomcat
The push refers to repository [docker.io/testtomcat]
An images does not exist locally with the tag:testtomcat

# 解决方案：增加tag  
# 语法：docker tag imagesid 容器命名:tag
[root@iZbp194xjjt5ig1q0i39f8Z tomcatlogs]#docker tag 18bc6c031e70 crownqqq/testtomcat:1.0

# 注意：上传镜像名一定要 docker push 注册用户名/镜像名[:tag]
```

### 拉取镜像

```shell
docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]
```

