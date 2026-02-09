# Guide

## 安装

### Windows

1. `scoop install main/nginx`
2. `nginx -p "$env:NGINX_HOME"`
3. 修改配置文件`$env:NGINX_HOME/conf/nginx.conf`中`server`属性中`listen`字段: 由80改为8080
4. 鼠标双击`$env:NGINX_HOME/nginx.exe`的方式来启动`nginx.exe`
5. 在`localhost:8080`可以查看启动后的网页
6. `nginx -s stop`关闭

### Ubuntu

1. `sudo apt update`
2. `sudo apt install -y nginx`
3. `systemctl status nginx`
4. `nginx -v`

## 新手指南

配置文件名`nginx.conf`

配置文件位置

* `/etc/nginx`
* `/usr/local/nginx/conf`
* `/usr/local/etc/nginx/`

### 配置文件命令相关

```bash
sudo systemctl start nginx  # 启动
sudo systemctl stop nginx   # 停止
sudo systemctl reload nginx  # 重载
sudo systemctl restart nginx # 重启

sudo nginx -t         # 测试配置文件语法

nginx
nginx -s stop
nginx -s quit
nginx -s reload
```

### 配置文件的结构

配置文件由简单指令`;`和块指令`{}`构成. `#`表示注释

```nginx
user www-data;

events {
  worker_connections 768;
  # multi_accept on;
}
```

**结构**

```nginx
main                # 全局上下文
 |--- events                # 事件驱动模块配置
 |--- http                  # HTTP服务器配置
 |    |--- server           # 虚拟主机
 |        |--- location     # URI路径配置
 |        |--- upstream     # HTTP负载无衡后端组
 |--- stream                # TCP/UDP代理配置(Nginx 1.9.0+)
 |    |--- server           # 流虚拟主机
 |    |--- upstream         # TCP/UDP负载均衡后端组
```

**server**

配置文件中定义多个服务器, 即server块, 通过端口和服务器名来区分.

**location**

输入的URL请求通过location按最长前缀进行匹配.

location后的路径要以`/`结尾.

当URL路径与文件路径有层级关系时, 使用root

```markdown
/data/
├── www/
│   ├── index.html
│   └── about.html
└── images/
    ├── logo.png
    └── bg.jpg
```

```nginx
server {
  location / {
    root /data/www; # 处理根路径'/'的请求
  }
  location /images/ {
    root /data;     # 处理'/images/'路径的请求
  }
}
```

* 访问 `/index.html` => `/data/www/index.html`
* 访问 `/images/logo.png` => `/data/images/logo.png`

当URL路径与文件路径无层级关系时, 使用alias

```nginx
location /images/ {
  alias /opt/media/;     # 处理 '/images/' 路径的请求
}
```

* 访问 `/images/logo.png` => `/opt/media/logo.png`, 不存在则返回 404 error.

### 设置一个简单的代理服务器

```nginx
server {
  listen 80;
  root   /data/upload;
  location / {
    proxy_pass http://localhost:8080;
  }
  location ~ \.(gif|jpg|png)$ {
    root /data/images;
  }
}
```

## References

1. [https://nginx.org/en/docs/beginners_guide.html](https://nginx.org/en/docs/beginners_guide.html)
