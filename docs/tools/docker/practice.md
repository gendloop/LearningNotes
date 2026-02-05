# Practice

## Basic Command

1. 查看 docker 信息

    `docker info`

2. 查看已有镜像

    `docker image ls`

3. 运行容器1

    `docker run -itd --name c1 ubuntu:latest`

4. 运行容器2

    `docker run -itd --name c2 ubuntu:latest`

5. 进入容器1, 执行一条命令

    `docker exec c1 echo $SHELL`

6. 查看当前运行的容器

    `docker container ls`

7. 停止容器2

    `docker container stop c2`

8. 查看所有的容器

    `docker container ls -a`

9. 查看容器1的日志信息

    `docker logs c1`

10. 删除停止状态的容器

    `docker container prune -f`

11. 删除指定容器1

    `docker container stop c1 && docker container rm c1`

12. 查看 docker 资源使用情况

    `docker system df`

13. 列出镜像的摘要

    `docker image ls --digests`

14. 列出悬空镜像

    `docker image ls -f dangling=true`

15. 删除悬空镜像

    `docker image prune -f`

16. 获取镜像的ID列表

    `docker image ls -q`

## Dockerfile

### 1-CMD

```bash
FROM alpine:latest
CMD ["echo", "Hello, I'm your first dockerfile"]
```

```bash
docker build -t gendloop/cmd:v0.0.1 .
docker run --rm gendloop/cmd:v0.0.1
docker run --rm gendloop/cmd:v0.0.1 /bin/sh -c "echo Default is covered."
```

### 2-RUN

```bash
FROM alpine:latest
RUN apk update && apk add curl
CMD ["echo", "Hello, I'm your second dockerfile"]
```

```bash
docker build -t gendloop/run:v0.0.1 .
docker run --rm gendloop/run:v0.0.1
```

### 3-COPY

```bash
FROM alpine:latest
COPY file.txt /app/file.txt
CMD ["cat", "/app/file.txt"]
```

```bash
docker build -t gendloop/copy:v0.0.1 .
docker run --rm gendloop/copy:v0.0.1
```

### 4-ENV

```bash
FROM alpine:latest
ENV MY_NAME="gendloop" NUMBER="third"
CMD echo "Hello, $MY_NAME, I'm your $NUMBER dockerfile."
```

```bash
docker build -t gendloop/env:v0.0.1 .
docker run --rm gendloop/env:v0.0.1
docker run --rm -e MY_NAME="momo" -e NUMBER="fourth" gendloop/env:v0.0.1
```

### 5-ENTRYPOINT

```bash
FROM alpine:latest
ENTRYPOINT ["echo", "Hello,"]
CMD ["youth"]
```

```bash
docker build -t gendloop/entrypoint:v0.0.1 .
docker run --rm gendloop/entrypoint:v0.0.1
docker run --rm gendloop/entrypoint:v0.0.1 newcomer
```

### 6-WORKDIR

```bash
FROM alpine:latest
WORKDIR /usr
WORKDIR src
CMD ["pwd"]
```

```bash
docker build -t gendloop/workdir:v0.0.1 .
docker run --rm gendloop/workdir:v0.0.1
```

### 7-ARG

```bash
FROM alpine:latest
ARG VERSION="0.0.0"
ENV USER="who"
RUN echo -e "version=$VERSION\nuser=$USER" > ~/file.txt
CMD cat ~/file.txt
```

```bash
docker build -t gendloop/arg:v0.0.1 .
docker run --rm gendloop/arg:v0.0.1

docker build --build-arg VERSION="1.2.3" -t gendloop:v0.0.1 .
docker run --rm gendloop:v0.0.1
```

### 8-VOLUME

```bash
FROM alpine:latest
VOLUME /app
RUN mdir -p /app \
  && echo "This is a file" > /app/file1.txt \
  && echo "This is another file" > /app/file2.txt
CMD ["echo", "Hello, I'm your eighth dockerfile."]
```

```bash
docker build -t guide:v0.0.8 .
docker run -v 8-volume-data:/app --rm guide:v0.0.8
```

### 9-ONBUILD

```bash
FROM alpine
ONBUILD COPY . /app
CMD ["echo", "Basic image is ready."]
```

```bash
docker build -t guide-base:v0.0.9 -f Dockerfile.base .
```

```bash
FROM guide-base:v0.0.9
CMD ["ls", "/app"]
```

```bash
docker build -t guide:v0.0.9 .
docker run --rm guide:v0.0.9

mkdir test && cp Dockerfile test
docker build -t guide:v0.0.9 .
docker run --rm guide:v0.0.9

cd ..
docker build -t guide:v0.0.9 .
docker run --rm guide:v0.0.9

rm -rf test
docker build -t guide:v0.0.9 .
docker run --rm guide:v0.0.9
docker image prune -f

docker image inspect guide:v0.0.9
docker image inspect guide-base:v0.0.9
```

### 10-USER

```bash
FROM alpine:latest
RUN adduser -D gendloop
USER gendloop
CMD ["whoami"]
```

```bash
docker build -t guide:v0.0.10 .
docker run --rm guide:v0.0.10
docker inspect guide:v0.0.10
```

### 11-LABEL

```bash
FROM alpine:latest
LABEL \
  author="gendloop"
  date="2025-03-27"
CMD ["echo", "Hello, I'm a sample about LABEL"]
```

```bash
docker build -t guide:v0.0.11 .
docker run --rm guide:v0.0.11
docker image inspect guide:v0.0.11
```

### 12-SHELL

```bash
FROM ubuntu:15.10
SHELL ["/bin/bash" "-c"]
```

```bash
docker build -t guide:v0.0.12 .
docker run --rm guide:v0.0.12 dirs # an error
docker run --rm guide:v0.0.12 /bin/bash -c dirs
```

### 13-AS

```bash
FROM alpine:latest AS stage1
RUN echo "I'm the first stage." > stage1.txt
CMD echo "Stage1 is ready." && pwd

FROM alpine:latest AS stage2
RUN echo "I'm the second stage." > stage2.txt
CMD echo "Stage2 is ready." && pwd

FROM alpine:latest AS final
COPY --from=stage1 /stage1.txt /app/stage1.txt
COPY --from=stage2 /stage2.txt /app/stage2.txt
WORKDIR /app
RUN cat stage1.txt | tee -a stage.txt && \
  cat stage2.txt | tee -a stage.txt
CMD echo "Final stage is OK." && cat stage.txt
```

```bash
docker build --target stage1 -t guide:v0.0.13.stage1 .
docker run --rm guide:v0.0.13.stage1

docker build --target stage2 -t guide:v0.0.13.stage2 .
docker run --rm guide:v0.0.13.stage2

docker build -t guide:v0.0.13 .
docker run --rm guide:v0.0.13
```

## Network

1. 构建 alpine-with-ping 镜像

    ```bash
    FROM alpine:latest
    RUN apk add iputils-ping
    CMD ping -n 4 baidu.com
    ```

    ```bash
    docker build -t alpine-with-ping .
    ```

2. 创建网络

    ```bash
    docker network ls
    docker network create -d bridge my-net
    ```

3. 创建互联容器

    ```bash
    # Terminal 1
    docker run -it --rm --name c1 --network my-net alpine-with-ping sh
    # Terminal 2
    docker run -it --rm --name c2 --network my-net alpine-with-ping sh
    ```

4. 测试容器是否互联

    ```bash
    # Terminal 1
    ping -c 3 c2
    # Terminal 2
    ping -c 3 c1
    ```

## Compose

// todo
