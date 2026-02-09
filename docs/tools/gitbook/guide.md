# Guide

## 安装

```bash
# 卸载之前的Node.js版本
scoop uninstall nodejs -p
# 安装Node.js
scoop install main/nodejs@22.9.0
# 设置npm代理
npm config set proxy http://localhost:10809
npm config set https-proxy http://localhost:10809
# 法一: 使用默认镜像源
npm config set registry https://registry.npmjs.org
# 法二: 默认镜像源不能用则使用淘宝镜像源
# npm config delete registry
npm config set registry https://registry.npmmirror.com
# 安装gitbook-cli
npm install -g gitbook-cli
# 找到出错文件, 注释第62-64行
# E:\UserApps\persist\nodejs\bin\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js
  # // fs.stat = statFix(fs.stat)
  # // fs.fstat = statFix(fs.fstat)
  # // fs.lstat = statFix(fs.lstat)
# 安装GitBook
scoop install gendloopBucket/gitbook
# 查看当前版本
gitbook -V
# 安装calibre(用于生成电子书, 可选)
scoop install extras/calibre
```

## gitbook 常用命令

```bash
Command       Description
gitbook help                  # 列出gitbook所有命令
gitbook --help                # 列出gitbook-cli所有命令
gitbook init                  # 生成初始化目录文件
gitbook build                 # 生成静态网页
gitbook serve                 # 生成静态网页并运行服务器
gitbook build --gitbook=2.6.5 # 生成时指定gitbook 版本
gitbook ls                    # 列出本地gitbook版本
gitbook ls-remote             # 列出远程gitbook版本
gitbook fetch 2.6.5           # 安装远程gitbook版本
gitbook update                # 更新到gitbook最新版本
gitbook uninstall 2.6.5       # 卸载指定gitbook版本
```

## 创建新项目

### 项目结构

```bash
.
├── book.json
├── README.md
├── INTRO.md
├── SUMMARY.md
├── GLOSSARY.md
├── styles/
├── res/
└── chapters/
    ├── chapter1/
    |   ├── README.md
    |   └── something.md
    └── chapter2/
        ├── README.md
        └── something.md
```

### 基本流程

```bash
# 创建项目目录
mkdir TestGitBook
cd TestGitBook
gitbook init  # => README.md, SUMMARY.md
# 生成静态网页并运行服务器 http://localhost:4000
gitbook serve # 默认使用 35729 端口给 4000 端口提供服务
# 或自定义端口 gitbook serve --lrport 35728 --port 4001
# 仅生成网页
gitbook build
# 仅生成pdf
gitbook pdf
# 仅生成epub
gitbook epub
# 仅生成mobi
gitbook mobi
```

## 封面

在根目录添加`cover.jpg`文件, `cover_small.jpg`可作为小版本封面存在

| **最佳尺寸** | 大 | 小 |
| :---: | :---: | :---: |
| **文件** | `cover.jpg` | `cover_small.jpg` |
| **大小(像素)** | 1800 x 2360 | 200 x 262 |

## 多语言

在根目录下添加`LANGS.md`, 每种语言需作为一个子目录

可参考[GitbookIO/git: ProGit Book Fork generated using GitBook (github.com)](https://github.com/GitbookIO/git)

## 术语表

在根目录下添加`GLOSSARY.md`, 格式为

```markdown
## Word1
不支持中文
## Word1 Word2
不支持中文
```

## 转义*

// todo

## 引用*

// todo

## 继承*

// todo

## 自定义配置

在根目录下创建`book.json`文件, 包含的字段如下

> 粘贴内容到[JSON Lint](https://jsonlint.com/)可验证JSON语法

### gitbook

探测用来生成书本的gitbook的版本

```json
{ "gitbook": "3.2.3" }
{ "gitbook": ">=3.2.3" }
```

### title

```json
{ "title" : "How To Use GitBook" }
```

### author

```json
{ "author": "gendloop" }
```

### description

定义书本的描述, 默认从 README (第一段) 中提取

```json
{ "description": "This is such a great book!" }
```

### language

可选语言

```markdown
en, ar, bn, cs, de, en, es, fa, fi, fr, he,
it, ja, ko, no, pl, pt, ro, ru, sv, uk, vi,
zh-hans, zh-tw
```

```json
{ "language" : "zh-hans", # 简体中文 }
```

### root

```json
{ "root": "." }
```

### links

### isbn

定义书本的 ISBN

```json
{ "isbn": "978-3-16-148410-0" }
```

### direction

设置语言的文字方向

```json
{ "direction": "rtl" }
```

### styles

自定义书本的 css

```json
{
  "styles": {
    "website": "styles/website.css",
    "ebook": "styles/ebook.css",
    "pdf": "styles/pdf.css",
    "mobi": "styles/mobi.css",
    "epub": "styles/epub.css"
  }
}
```

### plugins

```json
{ "plugins": ["mathjax"] }
```

### pluginsConfig

```json
{
  "plugins": ["myplugin"],
  "pluginsConfig": {
    "myPlugin": {
        "message": "Hello World"
    }
  }
}
```

### structure

用来覆盖GitBook使用的路径的。

例如你想要使用`INTRO.md`代替`README.md`：

```json
{
  "structure": {
    "readme": "INTRO.md"
  }
}
```

### variables

定义在模板中使用的变量值

```json
{
  "variables": {
    "myVariable": "Hello World"
  }
}
```

## 插件

### 查找插件

输入`npm search gitbook-plugin`可搜索部分插件, 更多在此搜索<https://www.npmjs.com/>

### 安装插件

1. 添加到 `book.json`

    ```json
    {
      "plugins": ["myPlugin@2.3.2", "anotherPlugin"]
    }
    ```

2. 执行`npm install`安装所有缺失的插件

    执行`npm install gitbook-plugin-myPlugnin@2.3.2`可安装特定的插件

### 部分插件说明

[https://gendloop.github.io/GitBookPlugins/](https://gendloop.github.io/GitBookPlugins/)

## 拓展网站和电子书样式

通过在`styles`目录中建立文件来扩展

```bash
Type          File
website       'styles/website.css'
pdf           'styles/pdf.css    '
epub          'styles/epub.css   '
mobi          'styles/mobi       '
pdf,epub,mobi 'styles/ebook.css  '
```

这些路径可以在`book.json`设置中改变，例如使用根文件夹中的文件：

```json
{
  "styles": {
    "website": "website.css",
    "ebook": "ebook.css",
    "pdf": "pdf.css",
    "mobi": "mobi.css",
    "epub": "epub.css"
  }
}
```

## 数学 & Tex

有两个官方的插件用来显示数学公式：[mathjax](https://github.com/GitbookIO/plugin-mathjax)和[katex](https://github.com/GitbookIO/plugin-katex)

## 构建*

// todo

## 可参考的GitBook项目

* [honkit/honkit: :book: HonKit is building beautiful books using Markdown - Fork of GitBook](https://github.com/honkit/honkit)

## References

1. [https://chrisniael.gitbooks.io/gitbook-documentation/content/index.html](https://chrisniael.gitbooks.io/gitbook-documentation/content/index.html)
2. [http://gitbook.zhangjikai.com/](http://gitbook.zhangjikai.com/)
3. [https://www.zhaowenyu.com/gitbook-doc/](https://www.zhaowenyu.com/gitbook-doc/)
4. [简介-GitBook 简明教程-码谱](https://www.mapull.com/gitbook/comscore/)
5. [http://gitbook.zhangjikai.com/plugins.html#gitbook](http://gitbook.zhangjikai.com/plugins.html#gitbook-%E6%8F%92%E4%BB%B6)
6. [https://www.cnblogs.com/jiangming-blogs/p/14643147.html (插件使用)](https://www.cnblogs.com/jiangming-blogs/p/14643147.html)
7. [gitbook serve后报错：_Error_ ENOENT_ no such file or directory……__book_gitbook_gitbook - 柳仙慧子 - 博客园.html](https://www.yuque.com/attachments/yuque/0/2024/html/22048361/1729236095582-763efb13-bcf6-4a9a-836c-1343f939ffb0.html)
8. [Gitbook的安装和部署 - 快乐的提千万 - 博客园.html](https://www.yuque.com/attachments/yuque/0/2024/html/22048361/1729237395153-5fa7cac2-9d1b-41f2-b0d6-d5eb7ce96804.html)
9. [node.js - Gitbook-cli install error TypeError_ cb.apply is not a function inside graceful-fs - Stack Overflow.html](https://www.yuque.com/attachments/yuque/0/2024/html/22048361/1729436395825-a08aa4e9-6704-462f-beeb-153916622f05.html)
10. [2021年gitbook的安装报错，一次解决方案！ - 握着玫瑰的屠夫 - 博客园.html](https://www.yuque.com/attachments/yuque/0/2024/html/22048361/1729436405148-cffb8177-06d9-4c83-99d6-eded39eb55a6.html)
