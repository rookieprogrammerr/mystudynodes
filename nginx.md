### 什么是Nginx

​	Nginx（engine x）是一个高性能的 HTTP 和反向代理 web服务器，同时也提供了 IMAP/POP3/SMTP 服务。Nginx 是由伊戈尔·塞索耶夫为俄罗斯访问量第二的 Rambler.ru 站点开发的，第一个公开版本 0.1.0发布于 2004年10月4日。2011年6月1日，nginx1.0.4 发布。

​	其特点是占有内存少，并发能力强，事实上 nginx 的并发能力在同类型的网页服务器中表现较好，中国大陆使用 nginx 网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。在全球活跃的网站中有 12.18% 的使用比率，大约为 2220万个网站。

​	Nginx 是一个安装非常简单、配置文件非常简洁（还能够支持 perl语法）、Bug非常少的服务。Nginx 启动特别容易，并且几乎可以做到 7*24 不间断运行，即便运行数个月也不需要重新启动。你还能够不间断服务的情况下进行软件版本的升级。

​	Nginx 代码完全用C语言从头写成。官方数据测试表明能够支持高达 50,000 个并发连接数的响应

### Nginx的作用

> Http代理，反向代理：作为 web 服务器最常用的功能之一，尤其是反向代理。

正向代理

![](http://zhaocan.fym233.cn/20210128132107.png)

反向代理

![](http://zhaocan.fym233.cn/20210128132108.png)

### 负载均衡

> Nginx 提供的负载均衡策略有2种：
>
> 1.内置策略和扩展策略。内置策略为轮询，加权轮询，Ip hash。
>
> 2.扩展策略，就天马行空，只有你想不到的没有他做不到的

**轮询：依次循环**

![](http://zhaocan.fym233.cn/20210128132729.png)



**加权轮询：大量的请求会请求权重最大的服务器**

![](http://zhaocan.fym233.cn/20210128132730.png)

​	iphash 对客户端请求的 ip 进行 hash 操作，然后根据 hash 结果将同一个客户端 ip 的请求分发给同一台服务器进行处理，可以解决 session 不共享的问题。

![](http://zhaocan.fym233.cn/20210128133710.png)

> 动静分离，在我们的软件开发中，有些请求是需要后台处理的，有些请求是不需要经过后台处理的（如：css、html、jpg、js等等文件），这些不需要经过后台处理的文件称为静态文件。让动态网站里的动态网页根据一定规则把不变的资源和经常变的资源区分开来，动静资源做好了拆分以后，我们就可以根据静态资源的特点将其做缓存操作。提高资源响应的速度。

![](http://zhaocan.fym233.cn/20210128133711.png)

​	目前，通过使用 Nginx 大大提高了我们网站的响应速度，优化了用户体验，让网站的健壮性更上一层楼！

### Nginx 的安装

##### Windows下安装

**1、下载nginx**

http://nginx.org/en/download.html 下载稳定版本

以nginx/Windows-1.16.1为例，直接下载 nginx-1.16.1.zip

下载后解压，解压后如下：

![](http://zhaocan.fym233.cn/20210128135431.png)

2、运行nginx.exe（也可以通过命令行运行）

![](http://zhaocan.fym233.cn/20210128135433.png)

3、访问 localhost:80 查看运行结果

![](http://zhaocan.fym233.cn/20210128135432.png)

##### Linux 下安装

1、http://nginx.org/en/download.html 下载稳定版本

2、将安装包上传到远程服务器上

3、解压nginx

![](http://zhaocan.fym233.cn/20210128140851.png)

4、自动配置 `configure`

```shell
./configure
```

5、进行编译

```shell
make
```

6、进入sbin目录下运行nginx

```shell
cd sbin
./nginx
```

### Nginx常用命令

```shell
cd /usr/local/nginx/sbin/
# 启动
./nginx	
# 停止
./nginx -s stop
# 安全退出
./nginx -s quit
# 重新加载配置文件
./nginx -s reload
# 查看nginx进程
ps aux|grep nginx
```

**注：如果连接不上，检查阿里云安全组是否开放端口，或者服务器防火墙是否开发端口**

相关命令：

```shell
# 开启
service firewalld start
# 重启
service firewalld restart
# 关闭
service firewalld stop
# 查看防火墙规则
firewall-cmd --list-all
# 查询端口是否开放
firewall-cmd --query-port=8080/tcp
# 开放80端口
firewall-cmd --permanent --add-port=80/tcp
# 移除端口
firewall-cmd --permanent --remove-port=8080/tcp

# 重启防火墙（修改配置后要重启防火墙）
firewall-cmd --reload
# 参数解释
firewall-cmd：是Linux提供的操作firewall的一个工具
--permanent：表示设置为持久
--add-port：标识添加的端口
```

