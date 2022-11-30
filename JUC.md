## JUC

### 1、JUC是什么

> java.util.concurrent包在并发编程中使用的工具包

### 2、线程基础知识复习

- 为什么要使用多线程

  - 硬件方面

    - 摩尔定律失效

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221129152632.png)

  - 软件方面

    - 充分利用多核处理器
    - 提高程序性能，高并发系统
    - 提高程序吞吐量，异步+回调等生产需求

  - 弊端及问题

    - 线程安全性问题
      - i++
      - 集合类安全否
    - 线程锁问题
    - 线程性能问题

- 从start一个线程说起

  - Java线程理解以及openjdk中的实现

    - `private native void start0();`
    - Java语言本身底层就是C++语言
    - OpenJDK源码网址
      - `http://openjdk.java.net/`
      - `openjdk8\hotspot\src\share\vm\runtime`

  - 更加底层的C++源码解读

    1. openjdk8\jdk\src\share\native\java\lang：**thread.c**

       ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221117110032.png)

    2. openjdk8\hotspot\src\share\vm\prims：**jvm.cpp**

       ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221117110344.png)

       ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221117110423.png)

    3. openjdk8\hotspot\src\share\vm\runtime：**thread.cpp**

       ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221117110541.png)

- Java多线程相关概念

  - 一把锁

    - **synchronized**

  - 两个并

    - 并发(concurrent)
      - 是在同一实体上的多个事件

      - 是在一台处理器上"同时"处理多个任务

      - 同一时刻，其实是只有一个事件在发生

    - 并行(parallel)
      - 是在不同实体上的多个事件

      - 是在多台处理器上同时处理多个任务

      - 同一时刻，大家真的都在做事情，你做你的，我做我的

  - 三个程

    - 进程：简单的说，在系统中运行的一个应用程序就是一个进程，每一个进程都有它自己的内存空间和系统资源。

    - 线程：也被称为**轻量级进程**，在同一个进程内会有1个或多个线程，是大多数操作系统进行时序调度的基本单元。

    - 管程

      - Monitor(监视器)：也就是我们平时所说的锁

        ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221117122157.png)

      - JVM第3版

        ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221129175517.png)

- 用户线程和守护线程

  - Java线程分为用户线程和守护线程

    - 一般情况下不做特别说明配置，**默认就是用户线程**
    - 用户线程(User Thread)
      - 是系统的工作线程，它会完成这个程序需要完成的业务操作。

    - 守护线程(Daemon Thread)
      - 是一种特殊的线程**为其他线程服务的**，在后台默默地完成一些系统性的服务，比如垃圾回收线程就是最典型的例子
      - 守护线程作为一个服务线程，没有服务对象就没有必要继续运行了，如果用户线程全部结束了，意味着程序需要完成的业务操作已经结束了，系统可以退出了。所以加入当系统只剩下守护线程的时候，java虚拟机会自动退出。

  - 线程的daemon属性

    - ```java
          /**
           * Tests if this thread is a daemon thread.
           *
           * @return  <code>true</code> if this thread is a daemon thread;
           *          <code>false</code> otherwise.
           * @see     #setDaemon(boolean)
           */
          public final boolean isDaemon() {
              return daemon;
          }
      ```

    - true表示是守护线程

    - false表示是用户线程

  - 总结

    - 如果用户线程全部结束意味着程序需要完成的业务操作已经结束了，守护线程随着JVM一同结束工作
    - setDaemon(true)方法必须在start()之前设置，否则报IllegalThreadStateException异常


### 3、CompletableFuture

- Future接口理论知识复习

  ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221130132520.png)

- Future接口常用实现类FutureTask异步任务

  - Future接口能干什么

    ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221130135036.png)

  - Future编码实战和优缺点分析

    - 优点
      1. Future+线程池异步多线程任务配合，能显著提高程序的执行效率。
    - 缺点
      1. get()阻塞
         - 一旦调用get()方法求结果，如果计算没有完成容易导致程序阻塞
      2. isDone()轮询
         - 轮询的方式会消耗无谓的CPU资源，而且也不见得能及时地得到计算结果
         - 如果想要异步获取结果，通常都会以轮询的方式去获取结果，尽量不要阻塞

  - 想完成一些复杂的任务

    - 对于简单的业务场景使用Future完全OK
    - 回调通知
      - 应对Future的完成时间，完成了可以告诉我，也就是我们的回调通知
      - 通过轮询的方式去判断任务是否完成这样非常占CPU并且代码也不优雅
    - 创建异步任务
      - Future+线程池配合
    - 多个任务前后依赖可以组合处理
      - 想将多个异步任务的计算结果组合起来，后一个异步任务的计算结果需要前一个异步任务的值
      - 将两个或多个一部计算合成一个异步计算，这几个异步计算互相独立，同时后面这个又依赖前一个处理的结果
    - 对计算速度选最快
      - 当Future集合中某个任务最快结束时，返回结果，返回第一名处理结果

- CompletableFuture对Future的改进

  - CompletableFuture为什么出现

    ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221130154724.png)

  - CompletableFuture和CompletionStage源码分别介绍

    - 接口CompletionStage

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221130161803.png)

    - 类CompletableFuture

      ![](https://zc-node.oss-cn-beijing.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221130163112.png)

  - 核心的四个静态方法，来创建一个异步任务

    - runAsync：无返回值

      - public static CompletableFuture<Void> runAsync(Runnable runnable)
      - public static CompletableFuture<Void> runAsync(Runnable runnable, **Executor executor**)

    - supplyAsync：有返回值

      - public static <U> CompletableFuture<U> supplyAsync(Supplier<U> supplier)
      - public static <U> CompletableFuture<U> supplyAsync(Supplier<U> supplier, **Executor executor**)

    - 上述Executor executor参数说明

      - 没有指定Executor的方法，直接使用默认的ForkJoinPool.commonPool()作为它的线程池执行异步代码
      - 如果指定线程池，则使用我们自定义的或特别指定的线程池执行异步代码

    - Code

      - 无返回值

        ```java
        /**
        * 不指定线程池
        */
        public static void main(String[] args) throws ExecutionException, InterruptedException {
            CompletableFuture<Void> completableFuture = CompletableFuture.runAsync(() -> {
                System.out.println(Thread.currentThread().getName());
                //暂停几秒钟线程
                try {
                    TimeUnit.SECONDS.sleep(1);
                } catch(InterruptedException e) {
                    e.printStackTrace();
                }
            })
                
            System.out.println(completableFuture.get());
        }
        ```

        ```java
        /**
        * 指定线程池
        */
        public static void main(String[] args) throws ExecutionException, InterruptedException {
            ExecutorService threadPool = Executors.newFixedThreadPool(3);
            
            CompletableFuture<Void> completableFuture = CompletableFuture.runAsync(() -> {
                System.out.println(Thread.currentThread().getName());
                //暂停几秒钟线程
                try {
                    TimeUnit.SECONDS.sleep(1);
                } catch(InterruptedException e) {
                    e.printStackTrace();
                }
            }, threadPool)
                
            System.out.println(completableFuture.get());
        }
        ```

      - 有返回值

        ```java
        /**
        * 不指定线程池
        */
        public static void main(String[] args) throws ExecutionException, InterruptedException {
            CompletableFuture<String> completableFuture = CompletableFuture.supplyAsync(() -> {
                System.out.println(Thread.currentThread().getName());
                //暂停几秒钟线程
                try {
                    TimeUnit.SECONDS.sleep(1);
                } catch(InterruptedException e) {
                    e.printStackTrace();
                }
                
           		return "hello supplyAsync";
            })
                
            System.out.println(completableFuture.get());
        }
        ```

        ```java
        /**
        * 指定线程池
        */
        public static void main(String[] args) throws ExecutionException, InterruptedException {
            ExecutorService threadPool = Executors.newFixedThreadPool(3);
            
            CompletableFuture<String> completableFuture = CompletableFuture.supplyAsync(() -> {
                System.out.println(Thread.currentThread().getName());
                //暂停几秒钟线程
                try {
                    TimeUnit.SECONDS.sleep(1);
                } catch(InterruptedException e) {
                    e.printStackTrace();
                }
                
                return "hello supplyAsync";
            }, threadPool)
                
            System.out.println(completableFuture.get());
        }
        ```

    - Code之通用演示，减少阻塞和轮询

      - 从Java8开始引入了CompletableFuture，**它是Future的功能增强版，减少阻塞和轮询**可以传入回调对象，当异步任务完成或者发生异常时，自动调用回调对象的回调方法

      - ```java
        public static void main(String[] args) throws ExecutionException, InterruptedException {
            ExecutorService threadPool = Executors.newFixedThreadPool(3);
            
            try {
                CompletableFuture.supplyAsync(() -{
                    System.out.println(Thread.currentThread().getName() + "----come in");
                    int result = ThreadLocal.Random.current().nextInt(10);
                    //暂停几秒钟线程
                    try {
                        TimeUnit.SECONDS.sleep(1);
                    } catch(InterruptedException e) {
                        e.printStackTrace();
                    }
        
                    System.out.println("------1秒钟后出结果：" + result);
                    return result;
                }, threadPool).whenComplete((v,e) -> {
                    if(e == null) {
                        System.out.println("------计算完成，更新系统UpdateValue：" + v);
                    }
                }).exceptionally(e -> {
                    e.printStackTrace();
                    System.out.println("异常情况：" + e.getCause() + "\t" + e.getMessage());
                    return null;
                });
        
                System.out.println(Thread.currentThread().getName() + "线程先去忙其他任务");
            } catch(Exception e) {
                e.printStackTrace();
            } finally {
                threadPool.shutdown();
            }
        }
        ```

    - CompletableFuture的优点

      - 异步任务结束时，会自动回调某个对象的方法
      - 主线程设置好回调后，不再关心异步任务的执行，异步任务之间可以顺序执行
      - 异步任务出错时，会自动回调某个对象的方法

- **join和get对比**

  - join不会出现检查时异常
  - get会出现检查时异常

- CompletableFuture常用方法
