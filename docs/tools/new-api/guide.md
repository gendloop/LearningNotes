# new-api

New API 是 AI API 网关与用量管理系统, 支持私有化部署, 采用 GNU AGPLv3 开源协议.

## 安装部署

先进行部署, 部署完成启动服务后, 访问`http://服务器IP:3000`将自动引导到初始化页面. 按指引手动设置管理员账号和密码(仅首次安装需要).

### Docker Compose 部署

#### 部署

```bash
# 进入安装目录
cd /opt

# 下载项目源码
git clone https://github.com/QuantumNous/new-api.git

# 进入项目目录
cd new-api

# 根据需要编辑 docker-compose.yml 文件
# vim docker-compose.yml
# 修改项包括
# - SQL_DSN
# - REDIS_CONN_STRING
# - REDIS_PASSWORD
# - POSTGRES_PASSWORD

# 启动服务
docker compose up -d

# 停止服务
# docker compose down
```

#### 更新

```bash
# 进入安装目录
cd /opt

# 进入项目目录
cd new-api

# 拉取最新镜像
docker compose pull

# 停止并重启服务
docker compose down
docker compose up -d
```

### Docker 部署

使用PostgreSQL数据库部署.

#### 部署

```bash
docker run --name new-api -d --restart always \
  -p 3000:3000 \
  -e SQL_DSN="postgresql://用户名:密码@数据库地址:5432/数据库名" \
  -e TZ=Asia/Shanghai \
  -v /本地路径:/data \
  calciumion/new-api:latest
```

#### 更新

```bash
# 拉取最新镜像
docker pull calciumion/new-api:latest

# 停止并移除旧容器
docker stop new-api
docker rm new-api

# 使用相同的参数重新运行容器
docker run --name new-api -d --restart always \
  -p 3000:3000 \
  -e TZ=Asia/Shanghai \
  -v /YOUR_DATA_PATH:/data \
  calciumion/new-api:latest
```

## References

1. [new-api](https://github.com/QuantumNous/new-api)
2. [New API 项目介绍](https://docs.newapi.ai/zh/docs/guide/wiki/basic-concepts/project-introduction)
