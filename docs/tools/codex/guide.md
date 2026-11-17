# Guide

## 安装

### Codex CLI

* Mac / Linux

    ```bash
    curl -fsSL https://chatgpt.com/codex/install.sh | sh
    ```

* Windows

  * 方式一

    ```bash
    scoop install codex
    ```

  * 方式二

    ```powershell
    powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
    ```

* Others

  * npm

    ```bash
    npm install -g @openai/codex
    ```

  * brew

    ```bash
    brew install --cask codex
    ```

## 常用配置

Codex的配置文件位于`~/.codex`目录下, 需要人工维护的有`config.toml`, `AGENTS.md`, `skills/`

* `config.toml`

  核心配置文件. 管理模型, 代理, API Key等配置

* `auth.json`

  认证凭据文件. 存储OpenAI API Key, 以及登录的ChatGPT账号信息

* `AGENTS.md`

  全局代理规则文件. 为每个会话注入行为约束, 如输出风格, 代码注释要求等

* `.codex-gloabl-state.json`

  全局状态文件. 存储设备指纹, 窗口位置, 最近工作区, 线程关联信息等

* `sessions/`

  会话目录. 按`YYYY/MM/DD`日期分层存储每次会话的完整日志, 文件格式为`rollout-*.jsonl`

* `session_index.jsonl`

  会话索引文件. 保存了所有对话线程的ID,标题和更新时间, 用于快速列出历史对话

* `history.jsonl`

  仅保存用户输入的提示词的历史记录, 用于快速检索和复用

* `*.sqlite`

  SQLite数据库文件. 存储运行时的各种状态

* `skills/`

  已安装技能目录. 每个技能为一个独立的目录, 包含一个`SKILL.md`定义文件

* `skills/.system/`

  系统技能目录. 存放Codex自带的系统技能

* `plugins/`

  插件缓存. 存放插件缓存和版本化文件

* `browser/`, `computer-use/`

  保存浏览器控制和计算机使用能力相关配置和白名单

* `tmp/`

  临时文件目录

* `version.json`

  版本记录文件. 用于自更新检查, 记录版本信息

* `generated_images/`

  图片产物目录. 存放Codex生成的图片的最终文件

* `ambient-suggestions/`

  环境建议缓存. 存放当前项目上下文生成的建议缓存

* `rules/`

  命令放行规则集. 定义了哪些命令可以安全执行, 如`default.rules`

## 使用

在工作目录下, 执行`codex`命令

### OpenAI API Key

首次使用时, 会提示三种方式登录
1. Sign in with ChatGPT
2. Sign in with Device Code
3. Provide your own API key

这三种方式都需要使用OpenAI API Key. 若已经登录, 需要切换登录方式或账号, 可以执行`codex login`命令或在CLI中执行`/logout`

### Custom API Key

自定义的OpenAI API Key, 在配置文件`config.toml`中进行设置

## 定制化

In Codex, customization comes from a few layers that work together:
* **Project guidance** (`AGENTS.md`) for persistent instructions
* **Memories** for useful context learned from prior work
* **Skills** for reusable workflows and domain expertise
* **MCP** for access to external tools and shared systems
* **Subagents** for delegating work to specialized subagents

These are complementary, not competing.

## References

1. <https://github.com/openai/codex>
2. [Customization](https://learn.chatgpt.com/docs/customization/overview)
