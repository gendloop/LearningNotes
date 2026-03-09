## 风格
+ 使用 Bash 作为 Shell 脚本语言
+ 应被用于小功能,  最好在百行内
+ 使用 `.sh` 作为扩展名
+ 缩进为两个空格

### 文件头
+ 以 `#!/bin/bash` 或 `#!/user/bin/env bash` 开头

```bash
#!/user/bin/env bash
# 
# @brief		Write your file description.
# @note			xxx
# @author		xxx
```

### 文件名 & 函数名 & 变量名
+ 文件名: <font style="color:rgb(38, 38, 38);">使用小写字母, 下划线分隔</font>
+ 函数名: 使用小写字母, 下划线分隔, 后跟圆括号
+ 变量名: <font style="color:rgb(38, 38, 38);">使用小写字母, 下划线分隔</font>

```bash
# Single Func
my_func() {
  ...
}

# Part of a pckage
mypackage::my_func() {
  ...
}

# Var
for zone in ${zones}; do
  something_with "${zone}"
done
```

### 其他变量
+ 常量和环境变量名: 全部大写, 下划线分隔, 声明在文件顶部
+ 只读变量: `readonly` 修饰
+ 局部变量: `local` 修饰, 只在函数内和子函数中可见; <u>声明和赋值需在不同行</u>

```bash
zip_version="$(dpkg --status zip | grep Version: | cut -d ' ' -f 2)"
if [[ -z "${zip_version}" ]]; then
  error_message
else
  readonly zip_version
fi

my_func2() {
  local name="$1"

  # Separate lines for declaration and assignment:
  local my_var
  my_var="$(my_func)" || return

  # DO NOT do this: $? contains the exit code of 'local', not my_func
  local my_var="$(my_func)"
  [[ $? -eq 0 ]] || return

  ...
}
```

### 主函数 main
+ 仅长脚本或非线性流时 使用
+ 放在最下面

### 内建命令
```bash
# Prefer this:
addition=$((${X} + ${Y}))
substitution="${string/#foo/bar}"

# Instead of this:
addition="$(expr ${X} + ${Y})"
substitution="$(echo "${string}" | sed -e 's/^foo/bar/')"
```

## 教程
### 样例
`$ vim test.sh`创建脚本

```bash
#!/bin/bash
echo "Hello World!"
```

运行脚本

```bash
$ chmod +x ./test.sh
$ ./test.sh
```

### 返回值
+ 每个命令都有一个返回值, 成功为 `0`, 失败为 1~255 之间的整数
+ `exit` 提前终止脚本, 并把返回值交给 shell; 当不带参数时, 返回上一个命令的返回值
+ `return` 提前终止函数
+ 程序结束后, shell 将返回值赋给环境变量 `$?`, 用来检测脚本执行成功与否

### 变量
```bash
# 创建变量, 无空格
my_link="https://www.yuque.com/gendloop"
readonly my_link
my_link="abc" # bash: my_link: readonly variable

# 删除变量
# unset <var>
user="gendloop"
unset user

# 字符串变量
my_str1="Hello"
my_str2=${my_str1}" World"
echo \"$my_str1\" \"$my_str2\" # "Hello" "Hello World"

# 整数变量

# 局部变量(函数内)
local local_var
local_var="local value"

# 环境变量
export GLOBAL_VAR="global value"
$HOME     	当前用户主目录
$PATH	    	查找命令的目录
$PWD	    	当前工作目录
$RANDOM   	0~32767 间的整数 
$UID				当前用户的ID
$PS1				主要系统输入提示符
$PS2				次要系统输入提示符

# 位置参数
$0						脚本名称
$1...$9				第 1~9 个参数列表
${10}...${N}	每 10~N 个参数列表
$* $@					除了 $0 外的所有位置参数
$FUNCNAME			函数名(仅函数内有值)
```

### 大括号拓展
```bash
# {start..end..increment}
echo beg{i,a,u}n # begin began begun
echo {0..9} # 0 1 2 3 4 5 6 7 8 9
echo {00..09..3} # 00 03 06 09
```

### 命令置换
```bash
# 用一组``或$()包裹命令
strs=($(echo beg{i,a,u}n))
echo ${strs[@]}

itvs=(`echo {0..9..3}`)
echo ${itvs[*]}

now=$(date +%T)
echo $now
```

### 算数扩展
```bash
# 算数表达式必须在$(())中
x=1
y=2
echo $(( x+y ))
echo $(( x++ + ++y ))
echo $(( x+y ))
```

### 双引号的使用
```bash
# 当变量中包含空格时, 注意加上双引号
fruits=" Apple  Pear    Peach"
echo $fruits # 会被分成单独的词
echo "$fruits"
```

### 数组




// todo: [https://www.runoob.com/linux/linux-shell-variable.html](https://www.runoob.com/linux/linux-shell-variable.html) 

// todo: [https://github.com/denysdovhan/bash-handbook/blob/master/translations/zh-CN/README.md#%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F](https://github.com/denysdovhan/bash-handbook/blob/master/translations/zh-CN/README.md#%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F) 

## References
1. [https://google.github.io/styleguide/shellguide.html](https://google.github.io/styleguide/shellguide.html) 
2. [https://zh-google-styleguide.readthedocs.io/en/latest/google-shell-styleguide/contents.html](https://zh-google-styleguide.readthedocs.io/en/latest/google-shell-styleguide/contents.html) 
3. [https://www.runoob.com/linux/linux-shell.html](https://www.runoob.com/linux/linux-shell.html) 
4. [https://github.com/denysdovhan/bash-handbook/blob/master/translations/zh-CN/README.md](https://github.com/denysdovhan/bash-handbook/blob/master/translations/zh-CN/README.md)
5. [https://tldp.org/LDP/Bash-Beginners-Guide/html/sect_03_02.html#sect_03_02_04](https://tldp.org/LDP/Bash-Beginners-Guide/html/sect_03_02.html#sect_03_02_04) 
6. [https://github.com/alebcay/awesome-shell?tab=readme-ov-file#guides](https://github.com/alebcay/awesome-shell?tab=readme-ov-file#guides)
7. [https://github.com/Idnan/bash-guide](https://github.com/Idnan/bash-guide)
8. [https://github.com/jlevy/the-art-of-command-line/blob/master/README-zh.md](https://github.com/jlevy/the-art-of-command-line/blob/master/README-zh.md) 

