# Docker

## 下载安装

安装所需依赖软件。

```shell
sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

导入原仓库的`GPG key`。

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

> ##### :question: 什么是`GPG`
>
> `GPG`是一种加密软件，它是 `PGP` 加密软件的开源替代程序。`GnuPG` 是一个混合加密软件程序，可以使用多种非专利的算法。

将`Docker apt`软件源添加到系统。

```shell
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

安装最新版`Docker`。

```shell
sudo apt install docker-ce docker-ce-cli containerd.io
```

## 常用指令

```shell
# 进程管理指令

systemctl start docker       # 启动docker服务

systemctl stop docker        # 停止docker服务

systemctl restart docker     # 重启docker服务

systemctl status docker      # 查看docker服务状态

systemctl enable docker      # 设置开机启动服务

# 容器管理指令

docker run --name={your_name} --d {image_name}     # 运行容器

docker ps                    # 查看正在运行的容器

docker ps -s -a              # 查看当前所有容器

docker start 容器名称         # 启动容器

docker stop 容器名称           # 停止容器

docker restart 容器名称       # 重启容器

docker kill 容器名称          # 杀死容器

docker rm -f 镜像ID或者镜像名  # 删除已经停止的容器

docker images               # 查看当前机器的所有镜像

docker images –q            # 查看所用镜像的id

# 镜像管理指令

docker search 镜像名称           # 搜索镜像，网络中查找需要的镜像

docker pull 镜像名称             # 从Docker仓库拉取镜像，名称:版本号
  
docker push 镜像名称             # 推送镜像

docker rmi 镜像名称/镜像id       # 删除本地机器的镜像

docker rmi docker images -q    # 删除所有本地镜像

docker tag 镜像名称:tag 镜像名称:tag                   #为一个镜像打tag

docker save {image_name} > {new_image_name}.tar     #镜像打包成一个tar包

docker load < {image_name}.tar                      #解压一个镜像tar包

# 查看日志信息 

docker logs -f 容器名称    # 查看容器日志

docker info              # 查看docker服务的信息

docker inspect 容器名称   # 获取镜像的元信息，详细信息

# 退出容器

exit          #退出也关闭容器;

Ctrl+P+Q      #退出不关闭容器
```

## 创建一个`Ubuntu`容器

> ##### :hammer: `Docker`拉取镜像慢
>
> 进入`docker`本地的配置目录。
>
> ```shell
> cd /etc/docker
> ```
>
> 创建`daemon.json`文件，填入以下内容保存退出。
>
> ```json
> {
> 
>     "registry-mirrors":["https://almtd3fa.mirror.aliyuncs.com"]      
> 
> }
> ```
>
> 重启`docker`服务。
>
> ```shell
> service docker restart
> ```
>
> 

拉取一个`Ubuntu`镜像。

```shell
sudo docker pull ubuntu
```

创建`ubuntu`容器。

```shell
sudo docker run -it -d --name ubuntu-huang ubuntu /bin/bash
```

进入刚创建的容器。

```shell
sudo docker exec -it ubuntu-huang /bin/bash
```

