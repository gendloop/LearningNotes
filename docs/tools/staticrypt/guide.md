# Guide

## 安装

```bash
npm install -g staticrypt
```

## 基本命令

```bash
# 查看命令帮助
staticrypt --help
-d, --directory  # 指定输出目录
-p, --password   # 指定网页访问密码
-r, --recursive  # 是否递归加密目录
-t, --template   # 自定义网页模板
```

## 使用

```bash
# 使用指定密码对一个 html 文件加密并输出到默认目录 encrypted 下
staticrypt index.html -p 123
# 输出到指定目录下
staticrypt index.html -p 123 -d output
# 设置密码在本地存储的有效天数
staticrypt index.html -p 123 --remember 7
# 使用指定的模板
staticrypt index.html -p 123 -t password_template.html
# 使用指定模板和密码生成到指定目录下
staticrypt index.html -p 123 --remember 1 -t password_template.html -d output
```
