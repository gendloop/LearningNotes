# Command

## container

```bash
docker container ls
docker ps
docker container ls -a
docker container prune
docker container start <container>
docker container logs <container>
docker container stop <container>
docker container rm <container>
docker container rm -f <container>
```

## image

```bash
docker system df
docker image ls
docker image ls --digests
docker image ls -f dangling=true
docker image prune
docker image ls -a
docker image ls ubuntu
docker image ls ubuntu:18.04
docker image ls -f since=mongo:3.2
docker image ls -f before=mongo:3.2
docker image ls -f label=com.example.version=0.1
docker image ls -q
docker image ls --format "{{.ID}}: {{.Repository}}"
docker image ls --format "table {{.ID}}\t{{.Repository}}\t{{.Tag}}"
docker image ls --format "{{.Repository}}:{{.Tag}}" | grep 'guide*' | sort -t: -k2 -Vr
docker image rm [options] <img1> [<img2> ...]
docker image rm 501ad78535f0
docker image rm centos
docker image rm $(docker image ls -q redis)
docker image rm $(docker image ls -q -f before=mongo:3.2)
```

## pull

```bash
# docker pull [option] [docker_registry[:port]/]repo[:tag]
docker pull ubuntu:18.04
docker pull docker.io/library/ubuntu:18.04
```

## run

```bash
docker run -it --rm ubuntu:18.04 bash
docker run -d -p 80:80 --name blog nginx:latest
docker run -itd -p 80:80 --name blog nginx:latest /bin/bash
docker run -d ubuntu:18.04 /bin/sh -c "while true; do echo hello world; sleep 1; done"
docker run --rm -v mydata:/app guide:v0.0.8
```

## volume

```bash
docker volume ls
docker volume create myvolume
docker volume inspect myvolume
docker ls /var/lib/docker/volumes/myvolume/_data
docker volume prune -f
docker volume rm myvolume
```

## exec

```bash
docker exec -it <container> bash
```

## commit

```bash
docker commit \
  --author "gendloop <gendloop.cn@gmail.com>" \
  --message "chore: update contents" \
  webserver \
  nginx: v2
docker history nginx:v2
```

## build

```bash
# docker build [options] <context/URL/->
docker build -t nginx:v3 .
docker build -t hello-world https://github.com/docker-library/hello-world.git#master:amd64/hello-world
docker build http://server/context.tar.gz
docker build - < Dockerfile
cat Dockerfile | docker build -
docker build - < context.tar.gz
```

## export

```bash
docker export 7691 > ubuntu.tar
```

## import

```bash
# docker import [options] <file>|<URL>|- [<repo>[:<tag>]]
cat ubuntu.tar | docker import - test/ubuntu:v1.0.0
docker import http://download.openvz.org/template/precreated/ubuntu-16.04-x86_64.tar.gz opencz/ubuntu:16.04
```

## save

```bash
docker save alpine | gzip > alpine-latest.tar.gz
```

## load

```bash
docker load -i alpine-latest.tar.gz
docker save <img> | bzip2 | pv | ssh <usr>@<hostname> 'cat | docker load'
```

## cp

```bash
docker cp CONTAINER:/var/logs/ /tmp/app_logs
docker cp blog:/usr/share/nginx/html/index.html .
docker cp ./index.html blog:/usr/share/nginx/html
```

## network

```bash
sudo docker network create -d bridge my-net
sudo docker run --it --rm --name c1 --network my-net ubuntu:ping
sudo docker network ls
sudo docker network inspect my-net
sudo docker network connect my-net my-container
sudo docker network disconnect -f my-net my-container
sudo docker network rm my-net
sudo docker network prune -f
```

## tag

```bash
sudo docker tag old-image:latest new-image:latest
```

## References

1. [https://docs.docker.com/reference/cli/docker/](https://docs.docker.com/reference/cli/docker/)
