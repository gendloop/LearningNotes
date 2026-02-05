# Guide

## 简介

* Docker 是一个简单的应用容器引擎, 可以让开发者打包应用以及依赖包到一个轻量级, 可移植的容器中

### 应用场景

* Web 应用的自动化打包和发布
* 自动化测试和持续集成, 发布

## Docker架构

* 镜像, Image, 相当于一个 root 文件系统 (把应用程序运行所需的环境, 打包为镜像文件)
* 容器, Container, 镜像运行时的实体, 可以被创建, 启动, 停止, 删除, 暂停
* 仓库, Repository, 保存镜像, 提供上传, 下载镜像的功能, 比如 DockerHub

## Docker安装

### Ubuntu

```bash
#curl -fsSL https://test.docker.com -o test-docker.sh
#sudo sh test-docker.sh

sudo apt-get remove docker \
               docker-engine \
               docker.io

sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
# $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://mirrors.aliyun.com/docker-ce/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null


# 官方源
# $ echo \
#   "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
#   $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

启动

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

配置

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": [
    "阿里云: https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors"
    "华为云: https://console.huaweicloud.com/swr/?region=cn-east-3#/swr/mirror"
  ]
}
EOF

sudo systemctl daemon-reload
sudo systemctl restart docker
```

### Docker Desktop

直接安装 Docker Desktop 即可, 下载链接: [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

### Windows

```powershell
scoop install main/docker@24.0.6
sudo dockerd --register-service # 注册 docker 服务
# sudo dockerd --unregister-service
sudo net start docker # 启动 docker 服务

sudo Enable-WindowsOptionalFeature -Online -FeatureName containers –All # 启用容器功能
sudo Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V –All # 启用 Hyper-V
# 重启
```

配置

```shell
path='C:/ProgramData/docker'
cd $path
mkdir -p config
vim ./config/daemon.json

# daemon.json
{
  "registry-mirrors": [
    "阿里云: https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors"
    "华为云: https://console.huaweicloud.com/swr"
  ],
	"proxies": {
		"http-proxy": "localhost:10809",
		"https-proxy": "localhost:10809"
	}
}

```

验证是否成功

```powershell
sudo net stop docker
sudo net start docker
sudo docker info
sudo docker run hello-world
```

### snap

```bash
sudo snap install docker
sudo snap start docker
sudo snap stop docker
sudo snap restart docker
sudo snap services docker
snap info docker
ls /var/snap/docker/current/config/daemon.json
sudo snap restart docker
```

## Docker Hello World

### Docker 命令帮助

```bash
docker
docker --help
docker <command> --help
```

### 运行容器

```bash
# docker [command] [image] [commands]
sudo docker run ubuntu:15.10 /bin/echo "Hello, gendloop"
```

### 运行交互式的容器

```bash
# -t: 在新容器内指定一个伪终端
# -i: 允许对容器内的标准输入(STDIN)进行交互
# 使用 exit 来退出容器
docker run -i -t ubuntu:15.10 /bin/bash
```

### 启动容器(后台模式)

```bash
sudo docker run -d ubuntu:15.10 /bin/sh -c "while true; do echo hello gendloop; sleep 1; done"
# docker run -d
# docker run -itd --name detach-test ubuntu /bin/bash
```

### 查看容器

```bash
sudo docker ps    # 查看运行的容器
sudo docker ps -a # 查看所有的容器
sudo docker ps -l # 查看最后一次创建的容器
# CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS     NAMES
# 8cc7c997aedc   ubuntu:15.10   "/bin/sh -c 'while t…"   3 minutes ago    Up 3 minutes              sharp_pike

# STATUS 有 7 种状态
# Created    已创建
# Restarting 重启中
# Running|Up 运行中
# Removing   迁移中
# Paused     暂停
# Exited     停止
# Dead       死亡

# PORTS
# TCP
# UDP
```

### 查看容器内标准输出

```bash
# docker logs <container_id>
sudo docker logs 8cc7c997aedc
```

### 停止容器

```bash
# docker stop <container_id>
sudo docker stop 8cc7c997aedc
```

## Docker 容器使用

### 获取镜像

```bash
docker pull <image>
docker pull <image>:<tag>
# e.g.
docker pull ubuntu
docker pull ubuntu:15.10
```

### 启动已停止的容器

```bash
docker ps -a
docker start <container_id>
docker restart <container_id>
# e.g.
sudo docker start 8cc7c997aedc
sudo docker restart 8cc7c997aedc
```

### 进入后台容器

```bash
docker exec [OPTIONS] CONTAINER COMMAND
# e.g.
sudo docker exec -it detach-test /bin/bash
```

### 导出和导入容器快照

```bash
docker export CONTAINER > container.tar
docker import FILE|URL|- [REPOSITORY[:TAG]]
# e.g.
sudo docker export detach-test > detach-test.tar
# e.g.
cat detach-test.tar | docker import - gendloop/detach-test:v0.0.0
sudo docker images
sudo docker import detach-test.tar
sudo docker images
sudo docker tag 3d823535d136 gendloop/detach-test:v1.0.0
sudo docker import detach-test.tar gendloop/detach-test:v2.0.0
sudo docker images
```

### 删除容器

```bash
docker rm CONTAINER
docker rm -f CONTAINER
docker container prune
# 清理不再使用的容器、镜像、网络和卷
sudo docker system prune
# 清理所有未使用的数据，包括垃圾镜像、构建缓存、不再关联的数据
sudo docker system prune -a
# e.g.
sudo docker rm -f 44dc6ec3b7c4
sudo docker container prune
```

### 端口映射

```bash
docker port CONTAINER_ID
docker run -d -P training/webapp python app.py
docker run -d -p 5000:5000 training/webapp python app.py
docker run -d -p 127.0.0.1:5000:5000 training/webapp python app.py
docker run -d -p 127.0.0.1:5000:5000/udp training/webapp python app.py
# -P 容器内部端口 随机 映射到主机端口
# -p 容器内部端口 绑定 到指定的主机端口
# e.g.
docker pull training/webapp
sudo docker run -d -p 5000:5000 training/webapp python app.py
sudo docker port 7d3475f07e70
```

### 查看容器内部信息

```bash
docker top CONTAINER # 查看容器内部运行的进程
docker inspect detach-test # 查看 Docker 的底层信息
# e.g.
docker top detach-test
```

### 设置镜像标签

```bash
docker tag CONTAINER <repo>:<tag> # 为镜像添加一个新标签
```

## Docker 镜像使用

### 管理和使用本地Docker机镜像

```bash
# 列出镜像列表
docker images
# 查找镜像
docker search httpd
# NAME DESCRIPTION STARS OFFICIAL AUTOMATED
# 镜像名 镜像描述 点赞数 是否官方发布 是否自动构建
# 获取一个新镜像
docker pull httpd
# 使用镜像
docker run httpd
# 删除镜像
docker rmi feb5d9fea6a5
```

### 创建镜像

对镜像进行更改的方式:

1. 从已创建的容器中更新镜像

    ```bash
    sudo docker commit -m="update" -a="gendloop" 7d3475f07e70 gendloop/ubuntu:v2.0.0
    ```

2. 使用 Dockerfile 指令创建一个新的镜像

    ```docker
    FROM ubuntu
    MAINTAINER gendloop "gendloop@163.com"
    RUN /bin/echo 'gendloop:g' | chpasswd
    RUN useradd newer
    RUN /bin/echo 'gendloop:g' | chpasswd
    RUN /bin/echo -e "LANG=\"en_US.UTF-8\"" > /etc/default/local
    EXPOSE 22
    EXPOSE 80
    CMD /usr/sbin/sshd -D
    ```

每一条指令都会在镜像上创建一个新的层, 每一个指令的前缀都必须是大写的

## Docker 容器互联

### 多个容器互联

```bash
# 新建网络
docker network create -d bridge test-net
# 连接一个容器
docker run -itd --name test1 --network test-net ubuntu:15.10 /bin/bash
# 再连接一个容器
docker run -itd --name test2 --network test-net ubuntu:15.10 /bin/bash
# 进入 test2
docker exec -it test2 /bin/bash
apt-get update
apt install iputils-ping
ping --help

# 制作新镜像
docker commit -m="support cmd ping" -a="gendloop" test2 gendloop/ubuntu:ping
docker images
docker inspect ubuntu
docker inspect gendloop/ubuntu:ping

# 使用新镜像连接容器
docker run -itd --name test3 --network test-net gendloop/ubuntu:ping /bin/bash
docker ps

# 尝试 ping 命令
docker exec -it test3 /bin/bash
ping test2
exit

docker exec -it test2 /bin/bash
ping test3
exit
```

### 配置 DNS

```bash
# daemon.json 位置
## apt: /etc/docker/daemon.json
## snap: /var/snap/docker/current/config/daemon.json
## win: C:/ProgramData/docker/config/daemon.json

# daemon.json 文件添加以下内容来设置全部容器的 DNS
{
  "dns": [
    "114.114.114.114",
    "8.8.8.8"
  ]
}

# 重启 docker
snap stop docker
snap start docker
docker start test1
docker start test2
docker start test3

# 测试 DNS 是否生效
docker run -it --rm ubuntu cat /etc/resolv.conf
```

```bash
# 手动指定容器的配置
docker run -it --rm -h host_ubuntu --dns=114.114.114.114 --dns-search=test.com ubuntu

# -h HOSTNAME 或 --host==HOSTNAME: 设定容器的主机名, 它会被写入 /etc/hostname 和 /etc/hosts
#
# --dns=IP_ADDRESS: 添加 DNS 服务器到容器的 /etc/resolv.conf 中,
#                   让容器用此解析不在 /etc/hosts 中的主机名
#
# --dns-search=DOMAIN: 设定容器的搜索域, 当设定搜索域为 .example.com 时,
#                      在搜索一个名为 host 的主机时, DNS不仅搜索 host, 还会搜索 host.example.com

# 查看配置
cat /etc/hostname
cat /etc/hosts
cat /etc/resolv.conf
exit
```

## Docker 仓库管理

### Docker Hub

1. 在[https://hub.docker.com/](https://hub.docker.com/)注册账号
2. 登录和退出

    ```bash
    # login
    docker login
    Username: gendloop
    Password: PRIVATE_ACCESS_TOKEN
    # logout
    docker logout
    ```

3. 推送镜像

    ```bash
    docker tag gendloop/ubuntu:ping gendloop/ubuntu:v1.2.3
    docker images
    docker push gendloop/ubuntu:v1.2.3
    ```

## Docker Dockerfile

Dockerfile 是一个用来构建镜像的文本文件

### 使用 Dockerfile 定制镜像

1. 创建 Dockfile 文件

    ```docker
    FROM nginx
    RUN echo '一个本地构建的 nginx 镜像' > /usr/share/nginx/html/index.html
    ```

    * `FROM`
    指定基础镜像, 以此为基础构建和定制自己的镜像, 从而避免从头开始构建 (特殊: `FROM scratch`, 表示一个空白的镜像)
    * `RUN`
    在容器中执行的命令.

    Dockerfile 的指令每执行一次都会在 docker 上创建一层, 过多无意义的层, 会造成镜像过大, 如:

    ```docker
    FROM centos
    RUN yum -y install wget
    RUN wget -O redis.tar.gz "http://download.redis.io/releases/redis-5.0.3.tar.gz"
    RUN tar -xvf redis.tar.gz
    ```

    会创建 3 层镜像, 使用以下命令可简化为一层镜像

    ```docker
    FROM centos
    RUN yum -y install wget \
    && wget -O redis.tar.gz "http://download.redis.io/releases/redis-5.0.3.tar.gz"
    && tar -xvf redis.tar.gz
    ```

2. 构建镜像

    ```bash
    docker build -t nginx:v3 .
    ```

    * `.`
    表示上下文路径, 构建镜像，需使用到本机的文件, 会将路径下的所有内容打包, 提供给docker引擎使用;
    如果未说明最后一个参数，那么默认上下文路径就是Dockerfile所在的位置

### Dockerfile多阶段构建

```docker
FROM golang:alpine as builder
RUN apk --no-cache add git
WORKDIR /go/src/github.com/go/helloworld/
RUN go get -d -v github.com/go-sql-driver/mysql
COPY app.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .
FROM alpine:latest as prod
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=0 /go/src/github.com/go/helloworld/app .
CMD ["./app"]

docker build -t go/helloworld:3 .
```

### 只构建某一阶段的镜像

```docker
FROM golang:alpine as builder

docker build --target builder -t username/imagename:tag .
```

### 构建时从其它镜像复制文件

```docker
COPY --from=0 /go/src/github.com/go/helloworld/app . # 0 表示构建阶段的编号
COPY --from=nginx:latest /etc/nginx/nginx.conf /nginx.conf
```

## 构建多种系统架构支持的 Docker 镜像

[https://docker-practice.github.io/zh-cn/image/manifest.html](https://docker-practice.github.io/zh-cn/image/manifest.html)

// TODO

## Docker Compose

通过 `docker-compose.yml` 来定义和运行多个相关联的 docker 容器

* `service`: 一个应用的容器
* `project`: 一组关联容器组成的一个完整业务单元

### 安装Compose

```bash
docker_config=/usr/local/lib/docker
sudo mkdir -p $docker_config/cli-plugins
sudo curl -L "https://github.com/docker/compose/releases/download/v2.36.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/lib/docker/cli-plugins/docker-compose
# 或手动下载复制 (下载地址: https://github.com/docker/compose/releases)
# sudo cp /mnt/c/Users/gendloop/Desktop/docker-compose-linux-x86_64 /usr/local/lib/docker/cli-plugins/docker-compose # wsl
sudo chmod +x $docker_config/cli-plugins/docker-compose
docker compose version
```

### 常用命令

```bash
docker compose up # 启动
docker compose up -d # 后台启动
docker compose down # 停止 up 命令启动的容器, 并移除网络
```

## References

1. [https://www.runoob.com/docker/docker-tutorial.html](https://www.runoob.com/docker/docker-tutorial.html)
2. [https://docker-practice.github.io/zh-cn/install/ubuntu.html](https://docker-practice.github.io/zh-cn/install/ubuntu.html)
3. [https://docker-practice.github.io/zh-cn/appendix/best_practices.html](https://docker-practice.github.io/zh-cn/appendix/best_practices.html)
4. [https://github.com/docker-library/docs](https://github.com/docker-library/docs)
