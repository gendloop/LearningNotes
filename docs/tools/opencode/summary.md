# OpenCode

## 安装

### Windows

```bash
scoop install main/opencode           # 安装OpenCode
echo 'export EDITOR=vim' >> ~/.bashrc # 设置外部编辑器
```

### Linux

```bash
npm install -g opencode-ai            # 安装OpenCode
echo 'export EDITOR=vim' >> ~/.bashrc # 设置外部编辑器
```

## 基础

* OpenCode将所有会话数据保存到同一个SQLite数据库中, 通常位于`~/.local/share/opencode/opencode.db`(Linux)或`%USERPROFILE%\.local\share\opencode\opencode.db`(Windows)
* OpenCode用不同的目录来隔离不同的项目, 每个目录内仅保存该项目关联的会话(/sessions, 目录感知)
* OpenCode包括Plan模式和Build模式, Plan模式不会进行任何修改, 只提供建议, Build模式会根据Plan模式的建议进行修改
* OpenCode的操作权限包括:
  * `allow`: 直接执行, 不询问
  * `ask`: 询问后执行
  * `deny`: 拒绝执行
* 操作权限的设置可通过配置文件实现, 配置文件位于`%USERPROFILE%\.config\opencode\`下的`opencode.json`或`opencode.jsonc`(带注释)

## 使用

一般使用tui(Terminal User Interface)模式, 进入项目目录后, 直接运行`opencode`即可

## 常用命令

### `/models`

列出当前可用模型, 进行切换模型

### `/connect`

添加新的提供商, 设置密钥

### `/init`

OpenCode会分析项目结构和编码规范, 在根目录下生成一个`AGENTS.md`文件

### `/compact`

压缩当前项目的会话数据, 减少上下文长度, 减少token消耗

### `/exit`

退出OpenCode

### `/session`

列出当前项目的所有会话

### `/new`

创建一个新的会话

### `/rename`

重命名当前会话标题

### `/fork`

从当前会话中任一历史结点创建一个新的会话分支, 该会话分支将继承该结点之前的所有上下文, 避免污染当前会话

### `/timeline`

显示当前会话的所有历史结点, 选择一个结点, 用于还原到任一历史结点, 或复制提交消息到粘贴板, 或进行fork操作

### `/undo`, `/redo`

撤销/重做当前会话的操作, 仅在Build模式下有效

### `/editor`

调用外部编辑器来输入
* `export EDITOR=vim`                     临时设置
* `echo 'export EDITOR=vim' >> ~/.bashrc` 永久设置

## 辅助功能

### `Ctrl+P`

显示所有命令和快捷键

### `Esc`

打断当前思考或执行操作

### `@`

引用文件或目录, 将其内容作为上下文传递给模型
