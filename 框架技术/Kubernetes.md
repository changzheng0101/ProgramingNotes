# kubernetes

## 是啥，有啥用

用来管理容器的开源工具，谷歌开发的

## 特点

1. high availability   --- no downtime
2. scalability -- high performance
3. disaster recover -- backup and restore

## 重要概念

### node

一台机器，可能是服务器或者虚拟机等。

### pod

kubernetes的最小单元

可以看成是容器的一个抽象

通常每个pod中跑一个程序

每个pod有一个对应的ip，虚拟ip，用于在node中仿真不同的pod

当container死亡重启之后，ip会发生变化

### service

永久的ip地址

生命周期和pod无关，这样不用每次pod死亡之后就更改地址了

* external service 外部可以访问
* internal service 只有内部可以访问 例如数据库等

### Ingress

地址一般为：`地址：端口号`  这种方式，只可以用于测试，不能用于开发

需要用域名完成映射，这时候再访问的时候，需要先经过Ingress，再去访问service

### Config map

完成配置工作，主要是外部配置

### Secret

也是用于配置，放置密码等敏感信息

### volume

每次pod重启，就会丢失所有数据

volume可以将存储映射到硬件存储，达到持久化存储的目的

### deployment

当其中一个pod需要重启升级的时候，系统会有一段时间无法访问，所以需要一个pod的复制品，当升级的时候访问另一个pod

创建时候创建多少个复制品通过deployment指定

### StatefulSet

当数据库创建多个副本的时候，无法保证数据同步，所以要通过statefulset来完成数据的同步，但过程较为繁琐，所以通常的选择是将无状态的服务放在kubernetes中，数据库等放在外部进行维护。

![image-20211222103422361](Kubernetes.assets/image-20211222103422361.png)

## node中跑的进程

### container runtime

就是docker 可以运行容器的，保证容器正常运行

### kublete

同时和容器和机器进行交互，通过container启动pod

### kube proxy

重定向，保证访问的时候的路由，例如访问某个node，就访问这个node上的数据库，省去访问另一台机器的时间

## 模式

### master - salve 模式

#### master

master和其他的slave从结构上是不同的

很重要，一般有多个master

虽然重要，但是承担的工作其实不多，所以相对于node，其配置一般要求比较低

一般运行着四个进程：

* API server    
  * 和客户端交互
  * 
* scheduler
  * 决定访问哪个node
* controller manage 
  * 检测pod情况，是否有崩溃的需要重启
* etcd
  * 整个master核心
  * 用key : value 来保存数据
  * 数据记录着状态

