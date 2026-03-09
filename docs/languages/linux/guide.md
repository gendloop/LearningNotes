## Linux 系统启动过程
启动过程分5个阶段:

1. 内核的引导
2. 运行 init
3. 系统初始化
4. 建立终端
5. 用户登陆系统

### 内核引导
+ 过程

=> 打开电源   
=> 按BIOS中设置的启动程序(通常是硬盘)启动  
=> 操作系统读入 /boot 目录下的内核文件

### 运行init
init 进程是系统中所有进程的起点

+ 过程  
=> 读取配置文件 /etc/inittab
+ 运行级别  
许多程序需要开机启动. 在Windows中叫做"服务"(service), Linux中叫"守护进程"(daemon)  
Linux允许为不同的场合, 分配不同的开机启动程序, 这就是"运行级别"  
即启动时, 根据不同的运行级别
+ 7个运行级别(runlevel)
    - 0: 系统停机状态, 系统默认运行级别不能为0, 否则不能正常启动
    - 1: 单用户工作状态, root权限, 用于系统维护, 禁止远程登陆
    - 2: 多用户状态(没有NFS)

> NFS(Network File System) 网络文件系统, 是一种分布式文件系统协议, 允许计算机通过网络共享文件和目录
>

    - 3: 完全的多用户状态(有NFS), 登陆后进入控制台命令行模式
    - 4: 系统未使用, 保留
    - 5: X11控制台, 登陆后进入图形GUI模式
    - 6: 系统正常关闭并重启, 默认运行级别不能设为6, 否则不能正常启动

### 系统初始化
\

### 建立终端
\

### 用户登陆系统
\

### 图形模式与文字模式的切换方式
\

### Linux 关机
\

## Linux 系统目录结构
### 目录结构
查看系统目录 `ls /`

```bash
bin		dev	home	lib		lib64 	lost+found 	mnt proc 	run		snap	sys	usr
boot 	etc	init 	lib32 libx32	media 			opt root	sbin	srv		tmp	var
```

+ `/bin`  
Binary, 二进制文件的缩写, 存放经常使用的命令
+ `/dev`  
Device, 设备的缩写, 存放 Linux 的外部设备
+ `/home`  
用户的主目录, 每个用户有一个自己的目录, 目录名以用户的账号命名
+ `/lib`  
Library, 库的缩写, 存放系统最基本的动态链接共享库, 类似 Windows 里的Dll
+ `/lib32` `/lib64` `libx32`  
存放 32 位, 64 位, x32 ABI 系统运行时需要的共享库
+ `/lost+found`  
存放文件系统修复时找到的损坏文件
+ `/mnt`  
挂载临时文件系统
+ `/proc`  
Processes, 进程的缩写, 虚拟文件系统, 包含系统和进程信息
+ `/run`  
存放系统运行时需要的临时文件. 当重启时应被清除
+ `/snap`  
存放 Snap 软件包管理器安装的应用程序
+ `/sys`  
虚拟文件系统, 包含内核和硬件设备信息
+ `/boot`  
存放启动 Linux 时使用的一些核心文件, 包括一些连接文件以及镜像文件
+ `/usr`  
Unix shared resources, 共享资源的缩写, 存放用户安装的应用程序和数据文件
+ `/boot`  
存放系统启动时需要的引导文件
+ `/etc`  
Etcetera, 等等的缩写, 存放所有的系统管理所需要的配置文件和子目录
+ `/init`  
存放系统初始化过程中需要执行的脚本和程序
+ `/media`  
挂载可移动媒体设备, 如光盘, USB
+ `/opt`  
第三方软件包安装的目录
+ `/root`  
root 用户的主目录
+ `/sbin`  
存放系统管理员使用的系统命令
+ `/srv`  
存放服务数据目录
+ `/tmp`  
存放临时文件
+ `/var`  
存放系统运行时产生的变化数据, 如日志文件, 缓存文件等

## WSL 忘记密码解决办法
1. 确定要修改的分发版  
`wsl -l`
2. 进入指定分发版  
`wsl -u root` or `wsl -d <distribution> -u root`
3. 指定要修改密码的用户  
`passwd <user_name>` => New password
4. `exit`

## Linux 远程登陆
### 查看当前ip
1. `ip addr`  
查看当前系统网络接口信息
2. `hostname -I`  
当前系统的 IP 地址
3. `curl ifconfig.me`  
当前系统所使用的公网 IP 地址

### 通过 Putty 远程登陆
1. 安装 openssh-server
    1. `sudo apt update`
    2. `sudo apt install openssh-server`
2. 启动 ssh 服务器
    1. `sudo service ssh start`
    2. `sudo service ssh status`
3. 允许远程
4. 下载 Putty
    1. 方式一 `scoop install extras/putty`
    2. 方式二: [https://www.putty.org/](https://www.putty.org/) 
5. 打开 Putty  
=> `Session`  
=> `<Host Name>` (Port: 22; Connection Type: SSH)  
=> `Open`  
=> login as: `<user>`  
=> password: `<pwd>`

### 使用密钥认证机制远程登陆 Linux
1. 生成公钥和私钥
    1. 打开 `PuTTYgen (PuTTY Key Generator)`
    2. `Key comment <key_comment>` 
    3. `Parameters`  
 => `Type of key to generate: <RSA>`  
 => `Number of bits in a generated key: <2048>`
    4. 点击`Generate`, 不断移动鼠标至生成
    5. 点击 `Save public key` `Save private key`, 保存为 public_key.pub 和 private_key.ppk
2. 添加公钥至 Linux 服务器
    1. `mkdir -p ~/.ssh`
    2. `vim ~/.ssh/authorized_keys`  
 输入 `ssh-rsa <public_key>`, `:wq`
    3. `chmod 700 ~/.ssh`  
`chmod 600 ~/.ssh/authorized_keys`
3. 保存 `<private key>` 到 PuTTY
    1. 打开 `PuTTY`
    2. `Category/Session`  
=> `Host Name(or IP address)`  
=> `Saved Sessions <user_session>`  
=> `Save`
    3. `Category/Connection/Data`  
=> `Auto-login username <user_name>`
    4. `Category/Connection/SSH/Auth/Credentials`  
=> `Private key file for authencation`   
=> `Browse...` `<private_key_file>`
    5. `Category/Session`  
=> 单击 `<user_session>`  
=> `Save`
4. 后续登陆   
=> `Category/Session`  
=> 双击 `<user_session>`

## Linux 文件基本属性
+ `chown` (change owner): 修改所属用户和组
+ `chmod` (change mode): 修改用户的权限

### 列出所属用户和组
`ls -l`

```bash
total 40
drwxr-x--- 4 gendloop gendloop 4096 Apr  6 16:54 ./
drwxr-xr-x 3 root     root     4096 Mar 20 00:20 ../
-rw------- 1 gendloop gendloop  625 Apr  2 23:49 .bash_history
-rw-r--r-- 1 gendloop gendloop  220 Mar 20 00:20 .bash_logout
-rw-r--r-- 1 gendloop gendloop 3771 Mar 20 00:20 .bashrc
drwx------ 2 gendloop gendloop 4096 Mar 20 00:21 .cache/
-rw------- 1 gendloop gendloop   20 Apr  2 23:35 .lesshst
-rw-r--r-- 1 gendloop gendloop    0 Apr  6 16:45 .motd_shown
-rw-r--r-- 1 gendloop gendloop  807 Mar 20 00:20 .profile
drwx------ 2 gendloop gendloop 4096 Apr  6 16:54 .ssh/
-rw-r--r-- 1 gendloop gendloop    0 Mar 24 23:00 .sudo_as_admin_successful
-rw------- 1 gendloop gendloop 1825 Apr  6 16:54 .viminfo
```

1. 第 1 列, 10 个字符, 记为0-9
    1. 第 1 个
        1. `d` 目录
        2. `-` 文件
        3. `l` 链接文档
        4. `b` 装置文件里的可供存储的接口设备(可随机存取装置)
        5. `c` 装置文件里的串行端口设备, 如键盘, 鼠标(一次性读取装置)
    2. 三个为一组(`r`可读; `w`可写; `x`可执行; `-`无权限), 共三组
        1. 123: 所有者权限
        2. 456: 组权限
        3. 789: 其他用户权限
2. 第 2 列: number of hard links
3. 第 3 列: owner name
4. 第 4 列: group name
5. 第 5 列: size
6. 第 6, 7, 8 列: date/time last modified
7. 第 9 列: file name

### chgrp 更改文件所属组
+ `chgrp <group> <file>`
+ `chgrp  [-R] <group> <dir>`

### chown 更改所有者, 也可更改所属组
+ `chown <owner> <file>`
+ `chown [-R] <owner> <dir>`
+ `chown <owner>:<group> <file>`
+ `chown [-R] <owner>:<group> <dir>`

### chmod 更改文件 9 个属性
#### 数字方式
三个身份: `owner` `group` `others`

三个权限: `r:4` `w:2` `x:1`

一个身份下的权限 = r + w + x = 4 + 2 + 1 = 7

+ `chmod <xyz> <file>`
+ `chmod [-R] <xyz> <dir>`

#### 符号方式
三个身份: `u` `g` `o`

全部身份: `a`

设定符号: `+` `-` `=`

权限: `r` `w` `x`

+ `chmod <u|g|o|a> <+|-|=> <rwx> <file>`
+ `chmod [-R] <u|g|o|a> <+|-|=> <rwx> <dir>`

e.g.

1. `chomd u=rwx,g=rx,o=r test1.txt`

## Linux 文件与目录管理
+ 根目录: `/`
+ 绝对路径: 如 `/usr/share/doc` 
+ 相对路径: 如 `../man`

### 处理目录的常用命令
+ `ls` list files  
列出目录及文件名
+ `cd` change directory  
切换目录
+ `pwd` print word directory  
显示目前的目录
+ `mkdir` make directory  
创建一个新的目录
+ `rmdir` remove directory  
删除一个空目录
+ `cp` copy file  
复制文件或目录
+ `rm` remove  
删除文件或目录
+ `mv` move file  
移动文件或目录 或 修改名称

> 使用 `man` 查看各命令的使用文档, 如 `man cp`
>

#### `ls`
+ `-a` 全部文件, 包括隐藏
+ `-d` 仅列出目录
+ `-l` 列出文件属性和权限等

#### `cd`
#### `pwd`
+ `pwd`
+ `pwd [-P]` 显示实际路径, 而非链接路径

#### `mkdir`
+ `-p`   
no error if existing, make parent directories as needed
+ `-m`  
 设置权限  
e.g.    
	`mkdir -m u=r,g=w,o=x -p t4`  
	`mkdir -m 111 -p t3`

#### `rmdir`
+ `rmdir <dir>`  
删除空目录
+ `rmdir -p <dir1/dir2/dir3>`  
删除多级空目录

#### `cp`
语法: `cp [optinos] source1 source2 ... destination`

+ `-a`   
相当于 `-pdr`
+ `-d`  
若来源档属性为链接(`l`开头), 则复制链接档而非文件
+ `-f`  
force
+ `-i`  
若已存在, 会询问
+ `-l`  
进行硬式链接的链接档创建, 而非复制文件本身
+ `-p`  
连同文件属性一起复制, 而非使用默认属性(备份常用)
+ `-r`  
递归复制, 用于目录
+ `-s`  
创建 symbolic link 软链接文件
+ `-u`  
若 destination 比 source 旧才升级 destination

> 硬链接: `ln <target> <link_name>`
>
> 软链接: `ln -s <target> <link_name>`
>
> e.g. 
>
> + raw_file: 1.txt;   
`-rwxr--r-- 2 gendloop-test gendloop-test 18 Apr  8 20:34 1.txt`
> + symbolic_link: 2.txt;   
`lrwxrwxrwx 1 gendloop-test gendloop-test  5 Apr  8 20:33 2.txt -> 1.txt`  
cp: `cp -d 2.txt 2_symbolic_link.txt`
> + hard link: 3.txt  
`-rwxr--r-- 2 gendloop-test gendloop-test 18 Apr  8 20:34 3.txt`  
cp: `cp -l 3.txt 3_hard_link.txt`
>

#### `rm`
语法: `rm [-fir] <file|dir>`

+ `-f`
+ `-i`
+ `-r`

#### `mv`
语法: `mv [-fiu] source1 source2 ... destination` 

+ `-f`
+ `-i`
+ `-u`

### Linux 文件内容查看
+ `cat`  
由一行开始显示文件内容
+ `tac`  
从最后一行开始显示文件内容, 是 cat 的倒写
+ `nl`  
显示的时候, 输出行号
+ `more`  
一页一页的显示内容
+ `less`  
与 more 类似, 但可向前翻页
+ `head`  
只看头几行
+ `tail`  
只看尾几行

#### `cat`
语法: `cat [-AbEnTv]`

+ `-A`  
相当于 `-vET`
+ `-b`  
列出行号, 仅针对非空白行
+ `-E`  
将结尾的断行符用 $ 显示
+ `-n`  
显示行号, 包括空白行
+ `-T`  
将 [Tab] 键以 ^| 显示
+ `-v`  
列出一些看不出来的特殊字符, 如中文

#### `more`
+ 空格:	向下翻一页
+ Enter:	向下翻一行
+ /字串:	向下搜寻 「字串」 这个关键字
+ `:f`:	立即显示当前文件名和目前显示的行数
+ q:		退出
+ b: 		往回翻页

#### `head`
语法: `head [-n number] <file>`

+ `-n`  
显示前 n 行 

#### `tail`
语法: `tail [-n number] <file>`

+ `-n`  
显示后 n 行

## Linux 用户和用户组的管理
Linux 系统是一个多用户多任务的分时操作系统, 任何一个要使用系统资源的用户, 都必须先向系统管理员申请一个账号.

每个账号都拥有一个唯一的用户名和口令

要实现用户的管理, 需要完成

+ 用户账户的添加, 删除和修改
+ 用户口令的管理
+ 用户组的管理

### Linux 系统用户账号的管理
#### 添加新用户 `useradd`
语法: `useradd [option] <user_name>`

+ `-c`  
comment, 指定一段注释性描述
+ `-d`  
指定用户主目录, 若此目录不存在, 可使用 -m, 创建
+ `-g`  
用户组, 指定用户所属的用户组
+ `-G`  
用户组, 指定用户所属的附加组
+ `-s`  
Shell 文件, 指定用户的登陆 Shell
+ `-u`  
用户号, 如果同时有 -o, 可重复使用其他用户的标识号

e.g.

1. `sudo useradd -d /home/gendloop -m gendloop`
2. `sudo useradd -s /bin/sh -g group -G adm,root gendloop2`

> 增加账号就是在 `/etc/passwd` 中为新用户增加一条记录, 同时更新文件如 /etc/shadow, /etc/group
>

#### 删除账号 `userdel`
语法: `userdel [option] <user_name>`

+ `-r`  
并删除用户的主目录

#### 修改账号 `usermod`
语法: `usermod [option] <user_name>`

+ `-c`
+ `-d`
+ `-g`
+ `-G`
+ `-s`
+ `-u`
+ `-l`

e.g.

1. `usermod -s /bin/ksh -d /home/z -g developer gendloop`
2. `usermod -l new_name gendloop`

#### 用户口令的管理
用户财号刚创建时没有口令, 被系统锁定, 无法使用, 必须指定后才可用

如 `$ tail /etc/shadow` => `gendloop:!:19821:0:99999:7:::`

指定和修改用户口令的命令: `passwd [option] [user_name]`

+ `-l`  
锁定口令, 即禁用账号
+ `-u`  
口令解锁
+ `-d`  
使账号无口令
+ `-e`  
强迫用户下次登录时修改口令

e.g.

1. 修改当前用户的口令  
`passwd`
2. 强迫用户下次登录时修改口令   
`sudo passwd -e gendloop`(需要输入原密码)  
or `sudo passwd -d gendloop` (不需要输入原密码)  
`su gendloop`

#### 查看用户
1. `users`
2. `cat /etc/passwd`
3. `getent passwd`
4. `cut -d: -f1 /etc/passwd`

#### 赋予 sudo 权限
1. `vim /etc/sudoers`  
或 `sudo visudo`
2. 添加 `<user> ALL=(ALL:ALL) ALL`   
或 `<user> ALL=(ALL) NOPASSWD:ALL` 

#### 切换用户
+ `su <user>`		使用当前用户环境
+ `su - <user>`	使用目标用户环境

### Linux 系统用户组的管理
每个用户都有一个用户组, 在创建用户时, 会自动创建一个与它同名的用户组

用户组的管理涉及用户组的添加, 删除, 修改, 实际是对 `/etc/group`的更新

#### 增加一个用户组 `groupadd`
语法: `groupadd [option] <group>`

+ `-g`  
GID, 指定新用户组的组标识号
+ `-o`  
一般与 -g 选项同时使用, 表示新用户组的 GID 可以与系统已有用户组的GID相同

e.g.

1. 添加一个新组, 即在当前最大组标识号基础上加1  
`sudo groupadd new group`  
=>

```plain
admin:x:115:
netdev:x:116:gendloop-test
gendloop-test:x:1000:
gendloop:x:1001:
newgroup:x:1002:
```

2. 指定新组的标识号  
`sudo groupadd -g 1003 newgroup2`
3. 指定新组的标识号, 与已有的相同  
`sudo groupadd -g 1003 -o newgroup3`  
=>

```plain
admin:x:115:
netdev:x:116:gendloop-test
gendloop-test:x:1000:
gendloop:x:1001:
newgroup:x:1002:
newgroup2:x:1003:
newgroup3:x:1003:
```

#### 删除一个已有用户组 `groupdel`
语法: `groupdel <group>`

#### 修改用户组的属性 `groupmod`
语法: `groupmod [option] <group>`

+ `-g`  
GID, 为用户组指定新的组标识号
+ `-go`  
新的GID可以与已有用户组的相同
+ `-n`  
修改用户组名

e.g.

1. 修改组号  
`sudo groupmod -g 1004 newgroup`
2. 修改组号为已有的  
`sudo groupmod -g 1003 -o newgroup`
3. 修改组号和组名  
`sudo groupmod -g 1004 -n gendloop2 gendloop`

#### 切换用户组 `newgrp`
语法: `newgrp <group>`

#### 查看用户组
1. `groups`
2. `cat /etc/group`
3. `getent group`
4. `cut -d: -f1 /etc/group`

### 与用户账号有关的系统文件
与用户相关的系统文件包括

+ /etc/passwd
+ /etc/shadow
+ /etc/group

#### /etc/passwd
每个用户都在 /etc/passwd 文件中有一个对应的记录行

这个文件对所有用户都是可读的

```bash
$ cat /etc/passwd
...
uuidd:x:106:112::/run/uuidd:/usr/sbin/nologin
tcpdump:x:107:113::/nonexistent:/usr/sbin/nologin
gendloop-test:x:1000:1000:,,,:/home/gendloop-test:/bin/bash
sshd:x:108:65534::/run/sshd:/usr/sbin/nologin
gendloop:x:1001:10004::/home/gendloop:/bin/bash
```

一行记录对应一个用户, 用冒号分隔为7个字段, 含义为

`用户名:口令:用户标识号:组标识号:注释性描述:主目录:登录Shell`

##### 用户名
表示用户账号的字符串

通常不超过8个字符, 由大小写字母或数字组成

##### 口令
存放用户口令的加密串, 但由于 /etc/passwd 均可读. 故将加密后的用户口令存放在 /etc/shadow 文件中, 而在 /etc/passwd 中的口令字段处 只存放一个特殊字符, 如 "x" 或 "*"

##### 用户标识号
一个整数, 系统内部用它来标识用户

一般与用户名一一对应

若多个用户名对应的用户标识号一样, 则系统视为同一个用户, 但它们可以有不同的口令, 主目录和登录Shell

用户标识号的取值范围是 0 ~ 65 535.

0 是超级用户 root 的标识号

1~99 由系统保留, 作为管理账号

普通用户的标识号从 100 开始

##### 组标识号
用户所属组, 对应 /etc/group 中的记录

查看组标识号方法:

1. `getent group | grep <group_name>:`
2. `id`

##### 注释性描述
记录用户的个人情况, 如真实姓名,电话,地址等, 无实际用途

##### 主目录
用户的起始目录

##### 登录Shell
用户登录后, 会启动一个进程, 负责将用户的操作传给内核, 即Shell

Shell是用户与Linux系统之间的接口. 常用的Shell有sh(Bourne Shell), csh(C Shell), ksh(Korn Shell) tcsh(TENEX/TOPS-20 type C Shell), bash(Bourne Again Shell)

默认使用 sh, 值为 /bin/sh.   
用户可指定某一特定程序, 利用这一特点, 可限制用户只能运行指定的应用程序, 程序运行完成后, 用户就自动退出

##### 伪用户
伪用户(pseudo users) 在 /etc/passwd 中也占有记录, 但是不能登录, 因为登录Shell为空

它们的存在主要是为了方便系统管理

常用的伪用户有

+ bin		拥有可执行的用户命令文件
+ sys		拥有系统文件
+ adm		拥有账户文件
+ uucp	UUCP使用
+ lp		lp或lpd子系统使用
+ nobody	NFS使用

#### /etc/shadow
`登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志`

#### /etc/group
`组名:口令:组标识号:组内用户列表`

#### 批量添加用户
1. 编辑一个用户文本文件 users.txt
    1. 一行表示一个用户
    2. 格式与 /etc/passwd 文件格式相同, 7个字段  
即: `用户名:口令:用户标识号:组标识号:注释性描述:主目录:用户登录Shell`
2. 用 root 身份通过 `/usr/sbin/newusers`, 从 users.txt 中导入用户  
`sudo newusers < users.txt`
3. 查看用户是否添加
    1. `tail /etc/passwd`
    2. `ls /home/`
4. 测试用户登录  
`su - <user_name>`

> + 密码转换
>     - `sudo pwunconv`, 将 /etc/shadow 中的密码解码, 并回写到 /etc/passwd 中
>     - `sudo pwconv`, 将密码重新编码
>

#### 批量修改用户密码
5. 编辑一个密码文件 passwd.txt. 
    1. 一行一个用户
    2. 格式: `<user>:<password>`
6. `sudo chpasswd < passwd.txt`
7. 测试用户登录  
`su - <user_name>`

## Linux 磁盘管理
磁盘管理常用的三个命令

+ `df`, disk free, 列出文件系统的整体磁盘使用量
+ `du`, disk used, 检查磁盘空间使用量
+ `fdisk`, 用于磁盘分区

### `df`
### `du`
### `fdisk`
## References
1. [Linux 教程 | 菜鸟教程](https://www.runoob.com/linux/linux-system-boot.html)  
[Linux教程_ 菜鸟教程.html](https://www.yuque.com/attachments/yuque/0/2024/html/22048361/1711291367979-3038344c-94cc-44e6-8a51-b5739e20f3eb.html)

