# Backup

数据的备份和迁移包含三部分:
* `docker-compose.yml`
* PostgreSQL 数据库
* 本地数据目录 `data` 和 `logs`

## 备份

### 备份 `docker-compose.yml`

```bash
# 创建备份目录
dir="backup/$(date +%Y-%m-%d)" && echo $dir
mkdir -p "$dir"

# 备份 docker-compose.yml
cp docker-compose.yml "$dir/"
```

### 备份本地数据目录

```bash
# 停止服务以保证本地文件一致性
docker compose stop new-api

# 打包本地数据
tar -czvf "$dir/data.tar.gz" ./data ./logs
```

### 备份 PostgreSQL 数据库

```bash
docker compose exec -T postgres pg_dump -U root -d new-api > "$dir/postgres.sql"
```

## 迁移

```bash
# 替换 docker-compose.yml

# 启动基础环境
docker compose up -d postgres redis

# 解压本地数据
tar -xzvf data.tar.gz

# 导入数据库数据
docker compose exec -T postgres psql -U root -d new-api < postgres.sql

# 启动完整服务
docker compose up -d
```
