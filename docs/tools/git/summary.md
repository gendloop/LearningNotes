# Git

`git help <command>`

## 命令

### git stash

```bash
# 暂存所有更改
git stash
# 暂存特定文件
git stash push <path>
# 暂存特定文件以外的文件
git stash push -- ":(exclude)<path>"
# 应用上一暂存
git stash apply
# 应用并删除上一暂存
git stash pop
# 删除上一暂存
git stash drop
# 删除指定暂存
git stash drop stash@{<index>}
# 应用指定暂存
git stash apply stash@{<index>}
# 列出所有暂存
git stash list
# 显示上一暂存修改的文件
git stash show
# 显示上一暂存修改的文件内容
git stash show -p
# 清空所有暂存
git stash clear
# 查看特定 stash 内容
git stash show -p stash@{0}
# 应用特定文件
git checkout stash@{0} -- <file>
```

### git diff

```bash
# 1. 比较工作目录中文件和暂存区中文件的差异
git diff
# 2. 比较暂存区中文件和最新提交(HEAD)中文件的差异
git diff --cached
# 3. 比较工作目录中文件和最新提交(HEAD)中文件的差异
git diff HEAD
# 4. 比较指定文件的差异
git diff <file>
# 5. 比较两次提交间的差异
git diff <commit1> <commit2>
# 6. 比较当前分支与另一个分支的差异
git diff <branch1>..<branch2>
# 7. 显示具体的文件差异, 包括新增, 修改, 删除
git diff --stat
# 8. 比较两次提交间特定文件的差异
git diff <commit1> <commit2> -- <file>
```

### git clone

```bash
# 克隆完成后, 不执行HEAD检出操作. 适用于需要获取历史记录但不需要在本地修改文件的情况
git clone --no-checkout <repo_url>
# 克隆裸仓库，不包含工作目录，适用于作为中央仓库或共享仓库使用
git clone --bare <repo_url>
# 克隆特定分支
git clone -b <branch> <repo_url>
# 克隆特定分支且只获取指定分支的信息
git clone --single-branch -b <branch> <repo_url>
```

### git archive

```bash
# git archive --format=<format> [--output=<file>] <commit> [<path>...]
#   --format=<format>：指定输出的归档文件格式，常见的格式包括tar、zip等。
#   --output=<file>：指定输出的归档文件名，如果未指定则输出到标准输出流。
#   <commit>：要打包的提交（可以是提交哈希、分支名、或标签名）。
#   <path>...：可选参数，指定要包含在归档中的文件或目录路径
git archive --format=tar --output=archive.tar HEAD

git archive --format=tar HEAD | tar -x -C .
#  下面是命令tar -x -C .的解释：
#  tar：表示调用tar命令。
#  -x：表示解压缩（或提取）操作。-x选项告诉tar命令要执行解压缩操作。
#  -C .：-C选项用于指定解压缩后文件的输出目录。在这里，.表示当前目录，即解压缩后的文件将被提取到当前目录中。
```

### git tag

```bash
# 按日期降序
git tag --sort=-creatordate
# 最近的5个
git tag --sort=-creatordate | head -n 5
git tag --sort=creatordate | tail -n 5
# 匹配的tag降序
git tag --sort=-creatordate | grep "v0.3.*"
```

### git cherry-pick

```bash
# 应用某次提交
git cherry-pick <commit-hash>
```

### git log

```bash
# 最近三次提交记录的注释信息
git log -3 --format="%s"
# %s:  提交信息标题
# %H:  完整提交哈希
# %h:  简短提交哈希(前 7 位)
# %an:  作者名
# %ar: 相对时间
# %ad: 具体日期时间
```

## 示例

### 通过ssh克隆项目

```bash
# 1. 检查是否已生成 ssh 密钥
ls ~/.ssh/id_ed25519 ~/.ssh/id_rsa
# 2. 若没有, 生成新的 ssh 密钥
ssh-keygen -t rsa -b 4096 -C "gendloop@163.com"
# ssh-keygen -t ed25519 -C "gendloop@163.com"
# 3. 添加到 ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
# ssh-add ~/.ssh/id_ed25519
# 4. 将公钥添加到 github 账户
cat ~/.ssh/id_rsa.pub
# cat ~/.ssh/id_ed25519.pub
# 登录 github => Settings => SSH and GPG keys => New SSH key => 粘贴
# 5. 测试 ssh 连接
ssh -T git@github.com
# Hi gendloop! You've successfully authenticated, but GitHub does not provide shell access.
# 6. 克隆仓库
git clone git@github.com:gendloop/Blog.git blog
```

### 使用ssh-agent管理密钥

```bash
# 启动 ssh-agent
eval "$(ssh-agent -s)"
# 列出密钥
ssh-add -l
# 添加密钥
ssh-add ~/.ssh/id_rsa
# 删除指定密钥
ssh-add -d ~/.ssh/id_rsa # 按路径
ssh-add -d SHA256:xxx/xxx # 按指纹
# 删除所有密钥
ssh-add -D
```

### 判断一个分支名是否存在

```bash
branch_name="branch_name"
if git show-ref --verify --quiet refs/heads/"$branch_name"; then
  branch_exists=true
 else
  branch_exists=false
fi
```

### 镜像某项目到另一项目

```bash
# git push --mirror <remote_repo_url>
git push --mirror https://github.com/gendloop/template-IndependentProject.git
```

### 拉取远程分支修改到本地分支

```bash
git fetch origin <remote_branch>:<local_branch>
```

### 删除所有历史提交记录

```bash
# Create a new empty branch
git checkout --orphan new_branch
# Add all files
git add .
git commit -m "chore: Initial commit"
# Force update the primary branch
git branch -D main
git branch -m main
# Force push to the remote repository
git push origin main --force
```

### 推送本地分支到远程分支

```bash
git push --force --quiet https://github.com/<user>/<remote_repo> <local_branch>:<remote_branch>
```

### 获取当前提交哈希值

```bash
git rev-parse HEAD
```

### 签出分支

```bash
git checkout <local_branch>
git checkout -b <local_banch>
git checkout <local_branch> <source_branch>
git checkout -b <local_branch> <source_branch>
git switch <local_branch>
git switch -c <local_branch>
git switch <local_branch> <source_branch>
git switch -c <local_branch> <source_branch>
```

### 获取提交日志

```bash
git log <commit_hash_prev>..<commit_hash_curr> --pretty=format:'%s'
```

### 推送某一子目录到分支

```bash
git subtree push --prefix docs origin gh-pages
```

### 判断是否是Git托管项目

```bash
if ! git rev-parse --is-inside-work-tree > /dev/null 2>&1; then
  echo "Error: no a git repo"
  exit 1
fi
```

### 获取仓库名

```bash
echo $(basename $(git rev-parse --show-toplevel))
```

### 获取分支名

```bash
echo $(git symbolic-ref --short HEAD)
```

### 获取仓库大小

```bash
git count-objects -vH
```

### 取消更改

```bash
git restore .
git restore file1 file2
git checkout -- .
git checkout -- file1 file2
```

### 取消上一次的提交

```bash
git reset HEAD^1
```

### 删除未跟踪的文件和目录

```bash
git clean -f    # files
git clean -fd   # files and folders
git clean -i    # interaction
```

### 重新应用.gitignore

```bash
git rm -r --cached .
git add .
```

### 清理历史记录中的大文件

```bash
# 查找历史中的大文件
git rev-list --objects --all | while read -r hash name; do
    size=$(git cat-file -s "$hash" 2>/dev/null || echo 0)
    if [ $size -gt 1000000 ]; then  # 大于1MB
        echo "$size $hash $name"
    fi
done | sort -nr
# 安装 git filter-repo
pip3 install git-filter-repo
# 删除大文件
git filter-repo --path "tools/1.zip" --invert-paths --force
git filter-repo --path "tools/2.zip" --invert-paths --force
# 检查文件是否还在历史中
git log --all --full-history -- "tools/1.zip"
git log --all --full-history -- "tools/2.zip"
# 查看仓库大小
git count-objects -vH
du -sh .git
```

### 删除远程不存在的本地分支

```bash
git fetch --prune
```
