## 命令
### ls
```bash
$ ls			 # 列出当前目录下文件夹和文件
$ ls -a		 # 列出当前目录下所有文件夹和文件, 包括隐藏文件
$ ls -A		 # 列出除 ., .. 外的
$ ls -lh	 # 列出详细信息
$ ls -lSh	 # 列出详细信息, 并按照文件大=>小排序
$ ls -d */ # 只列出当前目录下文件夹
$ ls -lt	 # 按创建时间排序(由新 => 旧)
$ ls -ltr	 # 按创建时间排序(由旧 => 新)
```

### xargs
```bash
$ xargs [option] command # 将输入数据(通常是多行文本) 转换为命令行参数
-I	定义参数占位符
-n	指定每个命令执行时传递的数量, 每次只传递 n 个参数给后面的命令
```

1. `-n`

```bash
# 创建文件 file.txt
$ echo -e "apple\nbanana\ncherry" > file.txt

# 逐行打印内容
$ cat file.txt | xargs -n 1 echo "Fruit:"
# Fruit: apple
# Fruit: banana
# Fruit: cherry
```

2. `-I`

```bash
# 查找当前目录下所有的 bat 文件, 复制到 test/ 目录下
mkdir -p test
find . -maxdepth 1 -name "*.bat" | xargs -I {} sh -c 'cp -f {} test/'
```

### grep
```bash
$ grep [option] pattern [file...] # 匹配指定模式的行
-i	忽略大小写
-n	显示匹配行的行号
-r	递归搜索
-v	反转匹配, 显示不匹配的行
```

1. `-i`, `-n`

```bash
$ echo -e "A1\na2\na3\nA4" | grep "a"
# a2
# a3

$ echo -e "A1\na2\na3\nA4" | grep -n "a"
# 2:a2
# 3:a3

$ echo -e "A1\na2\na3\nA4" | grep -i "a"
# A1
# a2
# a3
# A4

$ echo -e "A1\na2\na3\nA4" | grep -in "a"
# 1:A1
# 2:a2
# 3:a3
# 4:A4
```

2. `-r`

```bash
# 创建测试数据
$ mkdir -p test
$ echo -e "hello world\n hello today" > ./test/1.txt
$ echo "hello boy" > ./test/2.txt

# 搜索文件内容包含 hello 的文件
$ grep -rn "hello" ./test
# ./test/1.txt:1:hello world
# ./test/1.txt:2: hello today
# ./test/2.txt:1:hello boy

$ grep -rn --include='*.md' '-' .
$ grep -rn --include='*.md' --include='*.txt' 'pattern' .
```

3. `-v`

```bash
$ echo -e "A1\na2\na3\nA4" | grep -v "a"
# A1
# A4
```

### sed
<font style="background-color:#FBDE28;">// hack</font>

流编辑器, 用于文本的替换, 删除, 插入等

语法: `sed [option] 'command' [file...]`

+ option
    - `-i` 原地修改文件
    - `-n` 不输出匹配行

e.g.

1. `sed 's/pattern/replace/g' file.txt`
2. `sed '/pattern/d' file.txt`
3. `sed '1i\  
 Inserted text' file.txt`
4. `sed '1s/.*/New Line1/' file.txt`
5. `sed -e 's/pattern/replace/g' -e '/pattern/d' file.txt`
6. `sed -e ':a' -e 'N' -e '$!ba' -e 's/Line 2\nLine 3\nLine 4/New Line/g' example.txt`
7. `sed '3,5c\  
New Line 1\  
New Line 2' file.txt`

### find
```bash
# 列出当前目录下文件
# Tip: -maxdepth 是全局选项, 需放在开头
$ find . -maxdepth 1 -type f

# 列出当前目录下文件夹
$ find . -maxdepth 1 -mindepth 1 -type d

# 列出当前目录下文件夹名, 不含路径
$ find . -maxdepth 1 -mindepth 1 -type d -exec basename {} \;

# 列出当前目录及其子目录下的 .md 和 .html 文件
$ find . -type f \( -name "*.md" -o -name "*.html" \)
```

### tee
```bash
// todo
```

### fg, bg
```bash
$ Ctrl+Z     # 挂起当前程序
$ fg         # 最近挂起的程序
$ jobs       # 所有挂起的程序
$ fg %2      # 进入第二个挂起的程序
$ bg         # 最近挂起的程序放到后台运行
$ bg %2      # 将第二个挂起程序放到后台运行
$ kill %1    # 关闭第一个程序
$ kill -9 %1 # 强制关闭第一个程序
```

### history
```bash
$ history			# 查看历史命令
$ history 10	# 查看最近的 10 条命令
$ history -c	# 清空当前会话的历史命令	
```

### sort
```bash
$ sort -n		# 按数字排序
$ sort -r		# 逆序排序
$ sort -V		# 按版本号排序
```

### scp
```bash
# scp user@url:origin_path local_path
$ scp -r gendloop@gendloop.top:~/Others ./Tmp
```

### chage
```bash
$ sudo chage -d 0 user
```

### du
```bash
$ du -sh folder	# 查看文件夹大小
$ du -h --max-depth=1 | sort -hr | head -n 3
$ du -h --max-depth=1 --exclude="./2025-02-17"
```

### wc
```bash
$ wc -l	file.txt		# 统计行数
$ wc -w file.txt		# 统计单词数
$ wc -c file.txt		# 统计字节数
$ wc -m file.txt 		# 统计字符数
```

## 示例
### 添加管理员权限用户
```bash
$ sudo vim /etc/sudoers

# User privilege specification
root ALL=(ALL:ALL) ALL
gendloop ALL=(ALL:ALL) ALL
gendloop-test ALL=(ALL) NOPASSWD:ALL
```

### 执行上一次命令
```bash
!!
```

### 查看系统版本
```bash
$ lsb_release -a
$ cat /etc/lsb-release


$ cat /etc/os-release

$ uname -a
```

### <font style="color:rgb(51, 51, 51);">反向搜索历史记录命令</font>
```bash
Ctrl + R
```

### 查看和修改默认SHELL
```bash
# 查看当前使用的 shell
$ echo $SHELL

# 查看系统可用的 shell
$ cat /etc/shells

# 修改默认 shell
$ chsh -s $(which zsh)
```

### 初始化账户
```bash
# 1. 设置初始密码
$ sudo passwd username

# 2. 强制首次登录改密码
$ sudo chage -d 0 username
```

### 修改ssh登陆方式(公钥|密码)
```bash
$ sudo vim /etc/ssh/sshd_config

# sshd_config
PasswordAuthentication no  # 禁用密码登录
PubkeyAuthentication yes   # 启用公钥认证

$ sudo systemctl restart sshd
```

### ssh自动连接服务器配置
```bash
$ vim ~/.ssh/config

# config
Host gendloop.top
    HostName gendloop.top
    User gendloop
    IdentityFile ~/.ssh/gendloop.pem
    Port 2222  # 如果SSH端口非默认22
```

### 从子目录中提取指定类型文件到当前目录下
```bash
$ find . -mindepth 2 -type f \( -name "*.png" -o -name "*.jpg" -o -name "*.jpeg" \) \
-exec cp {} . \;
```

### 查看当前日期时间
```bash
$ date
$ date '+%Y-%m-%d'
$ date '+%H:%M:%S'
$ date '+%Y-%m-%d %H:%M:%S'
```

### 查找包含某内容的文件
```bash
# 显示具体匹配内容
find . -type f -name '*.ini' -exec grep -nH '\.png' {} \;

# 只显示包含匹配模式的文件名
find . -type f -name '*.ini' -exec grep -l '\.png' {} \;
```

### 替换文件内容
```bash
find . -type f -name '*.ini' -exec sed -i 's/\.png/\.bmp/g' {} \;
```

### 批量修改文件名
```bash
for file in *.svg+xml; do
    mv "$file" "${file%.svg+xml}.svg"
done
```

## 快捷键
### 光标移动
| Ctrl + A | 移动到行首 |
| :---: | :---: |
| Ctrl + E | 移动到行尾 |
| Ctrl + B | 向前移动一个字符 |
| Ctrl + F | 向后移动一个字符 |
| Alt + B | 向前移动一个单词 |
| Alt + F | 向后移动一个单词 |


### 编辑
| Ctrl + W | 删除前一个单词 |
| :---: | :---: |
| Ctrl + U | 删除到行首 |
| Ctrl + K | 删除到行尾 |
| Ctrl + Y | 粘贴刚才删除的内容 |
| Ctrl + H | 删除前一个字符 |
| Ctrl + T | 交换当前字符和前一个字符 |
| Alt + T | 交换当前单词和前一个单词 |
| Ctrl + Shift + - | 撤销上一次操作 |




