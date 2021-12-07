# Docker  :dancer:

## download

sudo apt install docker.io

## 常用命令

**需要在管理员模式下进行**

镜像会放到容器中执行

* 拉镜像：docker pull  镜像名称
* 查看镜像：docker images
* 删除镜像：docker rmi 镜像名称:版本号/ID
* 查看进程: docker ps

 -a 会显示已经停止的运行的

* 停止运行进行进程:docker stop 容器名称/ID
* 开始已经存在的容器进程:docker start 容器名称/ID
* 删除容器:docker rm 容器名称/ID
* 进入容器:docker exec -it  /bin/bash 容器名称



### 现在一般配置都用docker-compose