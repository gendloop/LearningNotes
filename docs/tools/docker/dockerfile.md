# Dockerfile

## FROM 指定基础镜像

```docker
# 如服务类镜像
nginx, redis, mongo, mysql, httpd, php, tomcat
# 运行语方类镜像
node, openjdk, python, ruby, golang
# 基础操作系统镜像
ubuntu, debian, centos, fedora, alpine
# 空白镜像
scratch
```

## RUN 构建镜像时执行命令

```docker
# shell 格式
RUN echo '<h1>Hello, gendloop!</h1>' > /usr/share/nginx/html/index.html
# exec 格式
RUN ["sh", "-c", "echo '<h1>Hello, gendloop!</h1>' > /usr/share/nginx/html/index.html"]
# example
FROM debian:stretch
RUN set -x; buildDeps='gcc libc6-dev make wget' \
    && apt-get update \
    && apt-get install -y $buildDeps \
    && wget -O redis.tar.gz "http://download.redis.io/releases/redis-5.0.3.tar.gz" \
    && mkdir -p /usr/src/redis \
    && tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1 \
    && make -C /usr/src/redis \
    && make -C /usr/src/redis install \
    && rm -rf /var/lib/apt/lists/* \
    && rm redis.tar.gz \
    && rm -r /usr/src/redis \
    && apt-get purge -y --auto-remove $buildDeps
```

## COPY复制

```docker
COPY [--chown=<user>:<group>] <source>,... <destination>
COPY [--chown=<user>:<group>] "<source>",... "<destination>"
COPY package.json /usr/src/app/
COPY hom* /mydir/
COPY hom?.txt /mydir/
COPY --chown=gendloop:gendloop files* /mydir/
COPY --chown=gendloop files* /mydir/
COPY EmptyFolder/* /mydir/
```

## ADD更高级的复制

```docker
# 功能在 COPY 基础上 增加自动解压缩
# 仅当源路径为 tar 压缩文件 (格式: gzip, bzip2, xz) 时使用
```

## CMD指定容器默认启动命令

```docker
# 一个 Dockerfile 只能有一个 COM 指令
# 如
CMD ["sh", "-c", "echo $HOME"]
CMD ["nginx", "-g", "daemon off;"]
```

## ENTRYPOINT入口点

```docker
# 1. 使用了 ENTRYPOINT, 而没有指定 CMD, ENTRYPOINT 指定的命令即入口点
#    启动时传入的任何参数都会作为 ENTRYPOINT 命令的参数
FROM ubuntu:18.04
RUN apt-get update \
    && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/*
ENTRYPOINT [ "curl", "-s", "http://myip.ip.net" ]

docker run myip
docker run myip -i

# 2. 同时指定了 ENTRYPOINT 和 CMD, CMD 中的命令被作为参数传递给 ENTRYPOINT
#    指定的命令, 以提供默认命令
FROM ubuntu:18.04
ENTRYPOINT [ "echo" "Hello" ]
CMD [ "gendloop" ]

docker run myubuntu
docker run myubuntu "World"
```

## ENV环境变量

```docker
# ENV <key> <value>
# ENV <key1>=<value1> <key2>=<value2>...
# 支持 环境变量的指令有: ADD, COPY, ENV, EXPOSE, FROM
# LABEL, USER, WORKDIR, VOLUME, STOPSIGNAL, ONBUILD, RUN
ENV MY_NAME gendloop
ENV MY_HOME /app
RUN mkdir -p $MY_HOME
CMD echo "Hello, $MY_NAME! Welcome to $MY_HOME"
```

## ARG构建参数

```docker
# ARG 指令用于定义构建镜像时传递的参数
# ENV 指令用于容器运行时内部的环境变量
# ARG 指定生效范围: 如果在 FROM 指令前指定, 则只能用于 FROM 指令中
ARG <var>[=<default_value>]

docker build --build-arg <var>=<value>

ARG VERSION=v1.0.0
RUN echo "Building version $VERSION"

docker build --build-arg VERSION=v1.2.3 -t myapp .
```

## VOLUME定义匿名卷

```docker
# VOLUME ["<path1>", "<path2>"...]
VOLUME /data

docker run -d -v mydata:/data xxx
```

## EXPOSE声明端口

```docker
# EXPOSE <port1> [<port2>/<protocol>...]
# EXPOSE 指令仅是一个元数据, 用于声明容器内部服务运行的端口, 并不会实际打开或映射端口
# 推荐放在 CMD 或 ENTRYPOINT 之前
# 使用 docker run -P, Docker 会自动将声明的端口映射到主机的一个随机端口
EXPOSE 3000 8080
EXPOSE 443/tcp
EXPOSE 443/udp
```

## WORKDIR指定工作目录

```docker
# WORKDIR <path>
# 功能: 改变以后 各层 的工作目录和位置
# 相对路径是相对于前一个 WORDIR 指令或 Dockerfile 的当前目录
# 绝对路径是相对于容器的根目录
WORKDIR /a
WORKDIR b
WORKDIR c
RUN pwd # /a/b/c
```

## USER指定当前用户

```docker
# USER <user>[:<group>]
RUN groupadd -r redis && useradd -r -g redis redis
USER redis
RUN [ "redis-server" ]
```

## HEALTHCHECK健康检查

```docker
# HEALTHCHECK NONE # 屏蔽基础镜像的健康检查指令
# HEALTHCHECK [options] CMD <cmd>
# - options:
#   --interal=<itv> # 30s
#   --timeout=<time> # 30s
#   --retries=<count> # 3
# - CMD 的返回值: 0, 成功; 1, 失败;
# 功能: 告诉 Docker 应该如何判断容器的状态是否正常
# 状态: starting, healthy/unhealthy
RUN nginx
RUN apt-get update \
    && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/* \
    HEALTHCHECK --interval=5s --timeout=3s \
    CMD curl -fs http://localhost/ || exit 1

docker build -t myweb:v1
docker run -d --name web -p 80:80 myweb:v1
docker inspect --format '{{json .State.Health}}' web | python -m json.tool
```

## ONBUILD为他人做嫁衣

```docker
# ONBUILD <other_cmds>

# Stage1
FROM node:slim
RUN mkdir /app
WORKDIR /app
COPY ./package.json /app
RUN [ "npm", "install" ]
COPY . /app/
CMD [ "npm", "start" ]

# Stage2
FROM node:silm
RUN mkdir /app
WORKDIR /app
CMD [ "npm", "start" ]

FROM my-node
COPY ./package.json /app
RUN [ "npm", "install" ]
COPY . /app/

# Stage 3
FROM node:slim
RUN mkdir /app
WORKDIR /app
ONBUILD COPY ./package.json /app
ONBUILD RUN [ "npm", "install" ]
ONBUILD COPY . /app/
CMD [ "npm", "start" ]

FROM my-node
```

## LABEL指令

```docker
# LABEL <key1>=<value1> <key2>=<value2>...
# 功能: 用来给镜像以键值对的形式添加一些元数据
LABEL org.opencontainers.image.authors="gendloop"
LABEL org.opencontainers.image.documentation="https://yuque.com/gendloop"
LABEL org.opencontainers.image.references="https://github.com/opencontainers/image-spec/blob/master/annotations.md"
```

## SHELL指令

```docker
# SHELL [ "<exe>", "<params>"]
# 功能: 指定 RUN, ENTRYPOINT, CMD 指令中的 shell, 默认为 [ "/bin/sh", "-c" ]
SHELL ["/bin/sh", "-cex"]
# /bin/sh -cex "nginx"
ENTRYPOINT nginx

SHELL ["/bin/sh", "-cex"]
# /bin/sh -cex "nginx"
CMD nginx
```

## References

1. [https://yeasy.gitbook.io/docker_practice](https://yeasy.gitbook.io/docker_practice)
2. [https://docs.docker.com/build/building/best-practices/](https://docs.docker.com/build/building/best-practices/)
3. [https://github.com/docker-library/docs](https://github.com/docker-library/docs)
