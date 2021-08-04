# docker

1、概念：docker是一个开源的应用容器引擎，docker可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的Linux机器中

2、docker架构：镜像、容器（容器是镜像运行的实体）、仓库（代码控制中心的作用，用来保存镜像）

systemctl start docker 启动docker服务

systemctl stop docker 停止docker服务

systemctl restart docker 重启docker服务

systemctl status docker 查看docker服务状态

systemctl enable docker设置开机启动docker服务



3、docker命令：

查看镜像：查看本地所有镜像

```
docker images
# 查看所有镜像的ID
docker images -q 
```

搜索镜像

```
docker search 镜像名称
```

拉取镜像

```
docker pull 镜像名称
```

删除镜像：删除本地镜像

```
docker rmi 镜像id
docker rmi docker images -q 删除所有本地镜像
```

查看容器

```
查看正在运行的容器
docker PS 
docker PS -a 查看所有容器
```

创建并启动容器

```
docker run 参数
```

进入容器

```
docker exec 参数
```

停止容器

```
docker stop 容器名称
```

启动容器

```
docker start 容器名称
```

删除容器

```
docker rm 容器名称
```

查看容器信息

```
docker inspect 容器名称
```

查看日志

```
docker logs 参数 容器ID
```

4、dockerfile

dockerfile是一个文本文件，用于构建docker镜像