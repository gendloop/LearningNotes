# Guide

## 安装及运行

1. 下载
    1. 方式一: scoop install main/perl@5.32.1.1
    2. 方式二: <https://www.perl.org/get.html>
2. 测试
    1. `perl -v`
3. 运行方式
    1. `perl -we <perl code>`(-e, execute)
    2. `perl -w script.pl`(-w, warning)

## 基础语法

### 注释

1. 单行注释: `#`
2. 多行注释: 以`=pod`开头, `=cut`结尾

```perl
# 单行注释
=pod 多行注释
print "Hello World!\n";
print "Hello World!\n";
print "Hello World!\n";
print "Hellod World!\n";
=cut
```

### 单, 双引号

1. `''`单引号: 解析
2. `""`双引号: 不解析

```perl
print "Hello\n"; # 双引号
print 'Hello\n'; # 单引号
```

### Here 文档

格式

```perl
$var = << FLAG;
...
FLAG
```

示例

```perl
$str1 = << "eof";
this is a note \n
haha ha .
eof
print $str1;

$str2 = << 'eof';
this is a note \n
haha ha .
eof
print $str2;
```

### 转义字符

`\n`

```perl
$str = "http:// \\  \n";
print $str;

$str = "http:// \\\\  \n";
print $str;
```

## 数据类型

### 标量

`$var = 1;`

```perl
# 标量
$num = 12; # 数字
$str = "12"; # 字符串
```

### 数组

`@array = (1, 2);`

```perl
# 数组
@array = (1,2,3);
print @array;
print "\n";
print "$array[0] $array[1] $array[2]";
print "\n";
```

### 哈希

`%hash = ('a' => 1, 'b' => 2);`

```perl
# 哈希
%hash = (
    'a' => 1,
    'b' => 2,
);
print %hash;
print "\n";
print "$hash{'a'}";
print "\n";
```

### 整型

`$x = 1`

```perl
# 整型
$x = 12;
if ($x + 1 == 13) {
    print "$x + 1 == 13 \n";
}
$x = 011;
print "$x = 011 \n";
$x = 0x11;
print "$x = 0x11 \n";
```

### 浮点型

`$x = 1.0`

```perl
# 浮点数
$x1 = 0.1;
$x2 = -0.2;
$x3 = 1.1e3;
$x4 = -1.1e4;
print "$x1 $x2 $x3 $x4 \n";
```

### 字符串

`$x = '1'`

```perl
# 字符串
$v1 = "字符串";
$v2 = '字符串2';
print "$v1 \n $v2 \n";
```

### 转义字符

| **转义字符** | **含义** |
| --- | --- |
| \\ | 反斜线 |
| \' | 单引号 |
| \" | 双引号 |
| \a | 系统响铃 |
| \b | 退格 |
| \f | 换页符 |
| \n | 换行 |
| \r | 回车 |
| \t | 水平制表符 |
| \v | 垂直制表符 |
| \0nn | 创建八进制格式的数字 |
| \xnn | 创建十六进制格式的数字 |
| \cX | 控制字符, X可以是任何字符 |
| \u | 强制下一个字符为大写 |
| \l | 强制下一个字符为小写 |
| \U | 强制将所有字符转换为大写 |
| \L | 强制将所有字符转换为小写 |
| \Q | 将到\E为止的非单词字符加上反斜线 |
| \E | 结束\L, \U, \Q |

## 变量

* 不同变量可使用相同的变量
* 不需要显示声明
* 数组
    * `@var`
    * `$var[index]`
* 哈希
    * `%var`
    * `$var{'key'}`

```perl
# 数组
@ages = (23, 24, 25);
print "$ages[0], $ages[1], $ages[2] \n";

# 哈希
%names = (
    'a' => "var: a",
    'b' => "var: b",
    'c' => "var: c",
);
print "$names{'a'}, $names{'b'}, $names{'c'} \n";

# 复制数组
@copy = @ages;
print "@ages \n";
print "@copy \n";

# 数组个数
$size = @ages;
print "$size \n";
```

## 标量

### 字符串连接

`$str3 = $str1 . $str2`

```perl
# 字符串连接
$str1 = "hello";
$str2 = "world";
$str3 = $str1.$str2;
$str4 = $str3 . 3;
print "$str3 \n";
print "$str4 \n";
print "hello"."world"."\n";
```

### 数字运算

`$sum = $x + $y`

```perl
# 数字运算
$n1 = 1;
$n2 = 2;
$n3 = $n1 + $n2;
print "$n3 \n";
```

### 打印多行字符串

```perl
# 多行字符串
print << "eof";
line 1, ..  ..
line2 , .. ??
eof
print "LF";
```

### 特殊字符

`__FILE__` `__LINE__` `__PACKAGE__`

```perl
# 特殊字符
print "File name: " . __FILE__ . "\n";
print "Line number: " . __LINE__ . "\n";
print "Package name: " . __PACKAGE__ . "\n";
print "__FILE__ __LINE__ __PACKAGE__\n"; # unable to parse
```

### ASCII字符

`$gendloop = v103.101.110.100.108.111.111.112;`

```perl
# ASCII字符
# 48(0), 65(A), 97(a)
$str1 = v102.111.111.108;
$str2 = v103.101.110.100.108.111.111.112;
print "$str1 \n";
print "$str2 \n";
```

## 数组

### 创建数组

`@array = (1, 2, 3);`

```perl
# 创建
@array1 = (1, 2, "s");
print @array1;
print "\n";

@array2 = qw/2 3 "ss"/;
print @array2;
print "\n";

@array3 = qw/
1
2
3
/;
print @array3;
print "\n";

$array4[0] = 'Monday';
$array4[6] = 'Sunday';
print @array4;
print "\n";
print "$array4[0] $array4[1] $array4[6]";
print "\n";
$size = @array4;
print $size;
print "\n";
```

### 访问数组元素

`$array[index]`

```perl
# 访问数组元素
@sites = qw/abc def ghi/;
print "$sites[0]\n";
print "$sites[2]\n";
print "$sites[-1]\n";
```

### 数组序列号

`@seq  = (1..10);`

```perl
# 数组序列号
@seq1 = (1..10);
print "@seq1\n";

@seq2 = (-3..3);
print "@seq2\n";

@seq3 = ('a'..'z');
print "@seq3\n";

@seq4 = ('A' .. 'Z');
print "@seq4\n";

@seq5 = ('a' .. 'Z');
print "@seq5\n";

@seq6 = ('A' .. 'z');
print "@seq6\n";
```

### 数组大小

`$size = @array`

```perl
# 数组大小
@array5 = (1,2,3);
print "size: ", scalar @array5, "\n";

$array5[10] = 10;
$size = @array5;
$max_index = $#array5;
print "real size: 4 \n";
print "size: $size \n";
print "max index: $max_index \n";
```

### 添加和删除元素

`$size = push(@array, new_end_element);`

`$end_element = pop(@array);`

`$size = unshift(@array, new_begin_element);`

`$begin_element = shift(@array);`

```perl
# 添加和删除数组元素
@seq7 = (1..4);
$size = @seq7;
print "original: \@seq7 = @seq7\n"."size: $size \n";

# add one at the end
$size = push(@seq7, 100);
print "push: \@seq7 = @seq7\n"."size: $size \n";

# delete the end
$var = pop(@seq7);
print "pop: \@seq7 = @seq7\n" . "var: $var \n";

# add one at the begin
$size = unshift(@seq7, "23");
print "unshift: \@seq7 = @seq7\n" . "size: $size \n";

# delete the begin
$var = shift(@seq7);
print "shift: \@seq7 = @seq7\n" . "var: $var \n";
```

### 切割数组

`@sub = @array[3..5];`

```perl
# 切割数组
@seq8 = (1..9);
@seq8_sub = @seq8[3..5];
print "@seq8\n";
print "@seq8_sub\n";
```

### 替换元素

`@new_array = splice(@array, offset, length, @to_replace);`

```perl
# 替换元素
# splice (@array, offset, length, list)
@seq9 = (1..9);
print "@seq9\n";
@seq9_2 = splice(@seq9, 3, 3, (0,0,0));
print "@seq9_2\n";
print "@seq9\n";
```

### 字符串转数组

`@array = split(separator, $str);`

```perl
# 将字符串转换为数组
# split (separator, $string [, number])
$str1 = "1 2 3";
@str1_array = split(' ', $str1);
$size = @str1_array;
print "@str1_array\n" . "size: $size\n";

$str2 = "1-2-3";
@str2_array = split('-', $str2);
$size = @str2_array;
print "@str2_array\n" . "size: $size\n";

$str3 = "1-2-3";
@str3_array = split('-', $str3, 2);
$size = @str3_array;
print "@str3_array\n" . "size: $size\n";
```

### 数组转字符串

`$str = join(connector, @array);`

```perl
# 将数组转换为字符串
# join (connect, @array)
@array = (1..5);
$str = join(' -> ', @array);
print "$str\n";
```

### 数组排序

`@sorted_array = sort(@array);`

```perl
# 数组排序
# sort (@array)
# sort by ASCII
@array = ('b', 'c', 'a', 'e', 'd');
@sort1 = sort(@array);
print "@sort1\n";
```

### 合并数组

`@array3 = (@array1, @array2);`

```perl
# 合并数组
@numbers = (1, 3, (4,5,6));
print "@numbers\n";

@nums2 = (1,3,5);
@nums3 = (2,4,6);
@nums4 = (@nums2, @nums3);
print "@nums4\n";
```

### 从列表中选择元素

`$var = @array[index];`

```perl
# 从列表中选择元素
@list = (1..5);
$var = $list[2];
$var2 = (1..5)[2];
print "$var\n$var2\n";
```

## 哈希

格式: `%var`

### 创建哈希

`%hash = ('a' => 'A', 'b' => 'B');`

```perl
# 1. 创建哈希
# method 1
%h1 = ('Person1', 'Maria', 'Person2', 'Jane');
print %h1, "\n";
print $h1{'Person2'}, "\n";

# method 2
$data{'P1'} = 'You';
$data{'P2'} = 'Me';
print %data, "\n";

# method 3
%data = (
    'g: ' => 'google',
    'bd: ' => 'baidu'
);
print %data, "\n";
```

### 访问哈希元素

单个:   `$value = $hash{key}`

多个(数组):  `$values = @hash{'key1', 'key2'}`

```perl
# 2. 访问哈希元素
# 单个
print "$data{'g'}", "\n";
print "$data{'bd'}", "\n";
# 多个
@array = @data{'g', 'bd'};
print @array, "\n";
```

### 读取哈希的 key 和 value

`keys(%hash)` `values(%hash)`

```perl
# 3. 读取哈希的 key 和 value
%data = (
    'a' => 1,
    'b' => 2
);
print %data, "\n";

# keys
@names = keys(%data);
print @names, "\n";

# values
@nums = values(%data);
print @nums, "\n";
```

### 检测元素是否存在

`exist($hash{key})`

```perl
# 4. 检测元素是否存在
%data = (
 'a' => 'apple',
    'b' => 'banana',
    'c' => 'Exist C'
);
if(exists($data{'c'})) {
 print("$data{'c'}, "\n");
}
else {
 print("doesn't exist", "\n");
}
```

### 获取哈希大小

`@keys = keys(%hash); $size = @keys;`

```perl
# 5. 获取哈希大小
$data = (
 'a' => 'A',
 'b' => 'B',
 'c' => 'C',
);
@keys = keys(%data);
$size = @keys;
print("$size", "\n");
```

### 添加或删除元素

`$hash{'new_key'} = 'new_value';`

`$del_value = delete($hash{'del_key'});`

```perl
# 6. 添加或删除元素
%data = (
 'a' = 'A',
 'b' = 'B',
 'c' = 'C',
);
print(%data, "\n");
$data{'d'} = 'D';
print(%data, "\n");
if(exist($data{'a'})) {
 $del_value = delete($data{'a'});
    print("\$ret = $ret\n");
}
print(%data, "\n");
```

### 迭代哈希

`foreach $key (keys(%hash))`

`while(($key, $value) = each(%hash))`

```perl
%data = (
    'a' => 'A',
    'b' => 'B',
    'c' => 'C'
);
foreach $key (keys(%data)) {
 print("$key\n");
}
while(($key, $value) = each(%data)) {
 print("$data{$key}\n");
}
```

## 条件语句

### true 和 false

`false`: `0` `'0'` `"0"` `()` `undef`

`true`: 其他

```perl
# true 和 false
if(0) { print(0 . " is " . "true", "\n"); }
else { print(0 . " is " . "false", "\n"); }

if('0') { print('\'0\'' . " is " . "true", "\n"); }
else { print('\'0\'' . " is " . "false", "\n"); }

if("0") { print('"0"' . " is " . "true", "\n"); }
else { print('"0"' . " is " . "false", "\n"); }

@a = ();
if($a) { print('@()' . " is " . "true", "\n"); }
else { print('@()' . " is " . "false", "\n"); }

%a = ();
if($a) { print('%()' . " is " . "true", "\n"); }
else { print('%()' . " is " . "false", "\n"); }

if(undef) { print('undef' . " is " . "true", "\n"); }
else { print('undef' . " is " . "false", "\n"); }

if(!undef) { print('!undef' . " is " . "true", "\n"); }
else { print('!undef' . " is " . "false", "\n"); }

if('undef') { print('\'undef\'' . " is " . "true", "\n"); }
else { print('\'undef\'' . " is " . "false", "\n"); }

if("undef") { print('"undef"' . " is " . "true", "\n"); }
else { print('"undef"' . " is " . "false", "\n"); }

```

### 条件语句 if

* `if(<true expr>)`
* `if...else...`
* `if...elsif...else...`

```perl
# 条件语句
# if
if(1) {
    print('if', "\n");
}

# if.. else...
if(0) {
    print('if', "\n");
}
else {
    print('if else', "\n");
}

# if...elsif...else...
if(0) {
    print('if', "\n");
}
elsif(1) {
    print('if...elsif...else...', "\n");
}
else {
    print('else', "\n");
}
```

### 条件语句 unless

* `unless(<false expr>)`
* `unless...else...`
* `unless...elsif...else...`

```perl
# unless
@array = ();
unless(@array) {
    if(!$array[-1]) {
        push(@array, 'false will be executed');
    }
    else{
        push(@array, $array[-1]+1);
    }
}
print(@array, "\n");

# unless...else...
unless(1) {
    print("false", "\n");
}
else{
    print("true", "\n");
}

# unless...elsif...else
$a = 0;
unless($a < 1) {
    print("false to execute", "\n");
}
elsif($a < 2) {
    print("true to execute", "\n");
}
else{
    print('others', "\n");
}
```

### 条件语句

* `switch`

* 需安装
    * `cpan`
    * `install Switch`
* 使用要求
    * 代码前加上`use Switch;`

```perl
# switch
=pod 需要安装Switch.pm模块
cpan
install Switch
=cut
use Switch;
$var = 10;
@array = (10, 20, 30);
%hash = ('key1' => 10, 'key2' => 20);
switch(1) {
    case 1            { print "数字 1"; next } # next 继续向下执行
    case "a"          { print "字符串 a" }
    case [1..10,42]   { print "数字在列表中"; next }
    case [1..10,42]   { print "数字在列表中";  }
    case (\@array)    { print "数字在数组中" }
    case /\w+/        { print "正则匹配模式" }
    case qr/\w+/      { print "正则匹配模式" }
    case (\%hash)     { print "哈希" }
    case (\&sub)      { print "子进程" }
    else              { print "不匹配之前的条件" }
}
print("\n");
```

### 三元运算符

`<expr> ? <true expr> : <false expr>`

```perl
# 三元运算符
$ret = "Name" == "gendloop" ? "gendloop" : "guest";
print("$ret\n");
```

## 循环

### while

`while(<true expr>)`

```perl
# while
$a = 1;
while($a < 4) {
    print("$a", "\n");
    $a = $a + 1;
}
print("\n");
```

### until

`until(<false expr>)`

```perl
# until
$a = 4;
until($a < 1) {
    print("$a", "\n");
    $a = $a - 1;
}
print("\n");
```

### for

`for(init; <true expr>; increment)`

```perl
1; # for
for($a = 0; $a < 3; $a = $a + 1) {
    print($a, "\n");
}
print("\n");
```

### foreach

`foreach $var ($list)`

```perl
# foreach
@array = (6..9);
foreach $e (@array) {
 print($e, "\n");
}
print("\n");

%hash = (
 'a' => 1,
    'b' => 2
);
foreach $e (keys(%hash)) {
 print($e, "\n");
}
print("\n");
```

### do...while

`do { ... } while(<true expr>);`

```perl
# do...while
@a = (0..2);
do {
 $size = @a;
    $size = push(@a, $size);
    print("size = $size, \@a = ", @a, "\n");
}while($size < 6);
print("\n");
```

### next

停止执行从next语句的下一语句开始到循环体结束标识符之间的语句，转去执行continue语句块，然后再返回到循环体的起始处开始执行下一次循环

`next`

`next LABEL`

```perl
# next
@array1 = (1..5);
foreach $a1 (@array1) {
 if($a1 == 3) {
        next;
    }
    print("$a1");
}
print("\n");
print("\n");

@array2 = ('a'..'e');
OUTER: foreach $a1 (@array1) {
 print("$a1: ");
    INNER: foreach $a2 (@array2) {
        if($a1 == 2) {
         print("\n");
            next OUTER;
        }
        elsif($a1 == 4 && $a2 eq 'c') {
            next INNER;
        }
        print("$a2");
    }
    print("\n");
}
print("\n");
```

### last

退出循环语句块，从而结束循环，last语句之后的语句不再执行，continue语句块也不再执行

* 相当于`break`

```perl
# last
for($i = 1; $i < 5; ++$i) {
 if($i == 3) {
        last;
    }
    print($i);
}
print("\n");
print("\n");
```

### continue

在条件语句再次判断前执行

* 只能用于 `while` 和 `foreach` 循环中

```perl
# continue
$i = 1;
while($i < 5) {
    $i++;
}continue{
    print("$i ");
}
print("\n");

foreach $e ((1..5)) {

}continue{
    print("$e ");
}
print("\n");
print("\n");
```

### redo

直接转到循环体的第一行开始重复执行本次循环，redo语句之后的语句不再执行，continue语句块也不再执行。

`redo`

`redo LABEL`

```perl
# redo
$i = 1;
while($i < 5) {
    if($i == 3) {
        $i++;
        redo;
    }
    $i++;
}continue{
    print("$i ");
}
print("\n");

foreach $e ((1..5)) {
    if($e == 4) {
        $e  = $e + 100;
        redo;
    }
}continue{
    print("$e ");
}
print("\n");
print("\n");
```

### goto

允许您将程序的执行跳转到指定的标签处

`goto LABEL`

`goto <expr>`

`goto &NAME` 把正在运行着的子进程替换为一个已命名子进程的调用

* 应尽量避免使用 `goto`

```perl
# goto
# goto LABEL
$a = 1;
LOOP: do {
    if($a == 3) {
        $a = $a + 1;
        print('break', "\n");
        goto LOOP;
        print('won\'t be execute', "\n");
    }
    print("\$a = $a", "\n");
    $a = $a + 1;
}while($a < 8);
print("\n");

# goto <expr>
$a = 1;
LOOP2: do {
    if($a == 3) {
        $a = $a + 1;
        goto 'LOOP' . '2';
        print('won\'t be execute', "\n");
    }
    print("\$a = $a", "\n");
    $a = $a + 1;
}while($a < 8);
print("\n");
```

## 运算符

### 算术运算符

`+` `-` `*` `/` `%`  `**`

```perl
# 算术运算符
$a = 2;
$b = 4;
print("$a + $b = ", $a+$b, "\n");
print("$a - $b = ", $a-$b, "\n");
print("$a * $b = ", $a*$b, "\n");
print("$a / $b = ", $a/$b, "\n");
print("$a % $b = ", $a%$b, "\n");
print("$a ** $b = ", $a**$b, "\n");
```

### 比较运算符

`==` `!=` `<=>` `>` `<` `>=` `<=`

字符串: `eq` `ne` `cmp` `gt` `lt` `ge` `le`

```perl
# 比较运算符
$a = 2;
$b = 4;
print("\"$a == $b\" => ", ($a == $b ? "true" : "false"), "\n");
print("\"$a != $b\" => ", ($a != $b ? "true" : "false"), "\n");
print("\"2 <=> 4\" => ", 2 <=> 4 , "\n");
print("\"3 <=> 3\" => ", 3 <=> 3 , "\n");
print("\"4 <=> 2\" => ", 4 <=> 2 , "\n");
print("\"$a > $b\" => ", ($a > $b ? "true" : "false"), "\n");
print("\"$a < $b\" => ", ($a < $b ? "true" : "false"), "\n");
print("\"$a >= $b\" => ", ($a >= $b ? "true" : "false"), "\n");
print("\"$a <= $b\" => ", ($a <= $b ? "true" : "false"), "\n");
```

### 赋值运算符

`=` `+=` `-=` `*=` `/=` `%=` `**=`

```perl
# 赋值运算符
$a = 2;
$b = 4;
$c = $a + $b;
print($c, "\n");
$c += $a;
print($c, "\n");
$c -= $a;
print($c, "\n");
$c *= $a + $b;
print($c, "\n");
$c /= $a + $b;
print($c, "\n");
$c %= 5;
print($c, "\n");
$c **= 100;
print($c, "\n");
```

### 位运算

`&` `|` `^` `~` `<<` `>>`

```perl
# 位运算
$x = 5;
$y = 6;
$x = $x ^ $y;
$y = $x ^ $y;
$x = $x ^ $y;
print($x . " " . "$y", "\n");

{
    $x = 8;
    $y = ~$x;
    print("$y", "\n");
}

{
    use integer;
    $x = 8;
    $y = ~$x;
    print("$y", "\n");
}

print(1 << 3, " ", 8 >> 1, "\n");
```

### 逻辑运算符

`and &&` `or ||` `not !`

```perl
print(((1 < 2) and (2 < 3)) ? "true" : "false", "\n");
print(((1 < 2) && (2 < 3)) ? "true" : "false", "\n");

print(((1 < 2) or (2 > 3)) ? "true" : "false", "\n");
print(((1 < 2) || (2 > 3)) ? "true" : "false", "\n");

print(not(1 > 2) ? "true" : "false", "\n");
```

### 引号运算符

* `q{}` 为字符串添加单引号
* `qq{}`  为字符串添加双引号

```perl
$a = 10;
$b = q{ a = $a };
print($b, "\n");
$b = qq{ a = $a };
print($b, "\n");
```

### 其他运算符

* `.` 连接两个字符串
* `x` 对字符串重复指定次数
* `..` 序列范围
* `++`, `--`
* `->` 类似指针作用, 用于引用

```perl
# 其他运算符
# .
$a = "a";
$b = "b";
print($a . $b, "\n");

# x
$c = ('acxb ' x 2);
print($c, "\n");

# ..
@a = (1..5);
@b = ('a'..'f');
print(@a, "\n");
print(@b, "\n");

# ++, --
$a = 3;
print($a++, "\n");
print(++$a, "\n");
print($a--, "\n");
print(--$a, "\n");

# ->
$a = ['a'..'f'];
$c = $a->[2];
print($a, "\n");
print($c, "\n");
```

## 时间和日期

/

## 子程序(函数)

### 定义和调用

```perl
# 定义和调用
sub hello {
    print("Subroutine", "\n");
}

hello();
```

### 传参

* `@_` 子程序参数
* `$_[i]` 子程序第$i$个参数
* 传入的是引用

```perl
# 传参
sub average {
    $sum = 0;
    $count = 0;

    foreach $e (@_) {
        $sum += $e;
        $count++;
    }

    $mean = $sum / $count;

    print("@_", "\n");
    print("$_[0]", "\n");
    print("$_[-1]", "\n");
    print("$mean", "\n");
}

average(1, 2, 3, 4, 5);
```

```perl
# 传递列表
sub transferList {
    print("@_", "\n");
    $_[0] = 2;
}

my $a = 1;
my @b = ('a'..'d');
my %c = (
    'A' => 'g',
    'B' => 'e'
);
transferList($a, @b, %c);
print("\n");
print("\n");
```

### 返回值

```perl
# 子程序返回值
sub add_x_y {
    my $sum = $_[0] + $_[1];
    return $sum;
}
print('1 + 2 = ', add_x_y(1, 2), "\n");
print("\n");
print("\n");
```

### 作用域

* `my` 局部变量
* `local` 局部全局变量
* `state` 静态变量(需要加上`use feature 'state'`)

## 引用

* 引用
    * 在变量前加上一个右斜杠`\`
    * `my $scalar_ref = \my $foo;`  # 标量
    * `my $array_ref = \my @array;` # 列表
    * `my $hash_ref = \my %hash;`   # 哈希
    * `my $func_ref = \&func;`      # 函数
    * `my $global_ref = \*global;`  # GLOB句柄
* 解引用
    * 已知类型 `$$VAR` `@$ARRAY` `%$HASH`
    * 不知类型 `@{VAR}`
* 判断类型
    * `ref VAR` 存在返回以下值, 不存在返回false
        * `SCALAR`
        * `ARRAY`
        * `HASH`
        * `CODE`
        * `GLOB`
        * `REF`

```perl
# 引用

use strict;
use warnings;

my $scalar_ref = \my $foo;    # 标量
my $array_ref = \my @array;   # 列表
my $hash_ref = \my %hash;     # 哈希
my $func_ref = \&func;        # 函数
# my $global_ref = \*global;    # GLOB句柄

# 解引用
# 已知类型 $$var @$ARRAY %$HASH
# 不知类型 @{VAR}

# @{VAR}
my $a = [1, "str", 3, 13];
print(@{$a}, "\n");

my $b = [1, "str", ['a'..'f'], 13];
foreach my $e (@{$b}) {

    my $ee = \$e;

    if(ref $ee eq 'REF') {
        print(ref($ee), ": @{$e}", "\n");
    }
    else {
        print(ref($ee), ": $e", "\n");
    }
}
print("\n");

# @$ARRAY
my @arr = (1..5);
my $temp = \@arr;
my @temp2 = @$temp;
push(@$temp, 6);
print(@$temp, "\n");
print(@arr, "\n");
print(@temp2, "\n");

# \&sub
sub add{
    my %temp_hash = @_;
    foreach my $item (%temp_hash) {
        print("item: $item", "\n");
    }
}
my %hash2 = (
    'name' => 'gendloop',
    'age' => '(50+49)/2'
);
my $add_ref = \&add;
&$add_ref(%hash2);


```

## 格式化输出

/

## 文件操作

### open & print & close

open 三步曲: `open`=>`print`=>`close`

`open(my $fh, '<', $file) or die "$file: $! \n"`

`print($fh $content)`

`close $fh`

* `<`  读
* `>`   写
* `+>`  读写
* `+>>`  追加

```perl
sub getContent {
    local $/;
    my $content = $_[0];
    return <$content>;
}

## read
my $file = 'files/file.txt';
open(my $fh, '<', $file) or die "$file: $! \n";
my $content = getContent($fh);
close $fh;

## write
my $file_out = 'files/file_out.txt';
open($fh, '>', $file_out) or die "$file_out: $! \n";
print($fh $content);
close $fh;

## readwrite
my $file_rw = 'files/file_rw.txt';
open($fh, '+>', $file_rw) or die "file: $! \n";
my $temp = $content."\nnew line\n";
print($fh $temp);
close $fh;

## readwrite_app
my $file_rw_app = 'files/file_rw_app.txt';
open($fh, '+>>', $file_rw_app) or die "file: $! \n";
$temp = $content."\nnew line\n";
print($fh $temp);
close $fh;
```

### 文件拷贝

```perl
# 文件拷贝

my $file_to_copy = "files/file.txt";
my $file_copy_to = "files/file_copy.txt";
open(my $hd_to_copy, '<', $file_to_copy) or die "file to cp: $! \n";
open(my $hd_copy_to, '>', $file_copy_to) or die "file cp to: $! \n";
while(<$hd_to_copy>) {
    print $hd_copy_to $_;
}
close($hd_to_copy);
close($hd_copy_to);
```

### 文件重命名

`rename(<old_name>, <new_name>);`

```perl
# 文件重命名
rename("files/file_copy.txt", "files/file_renamed.txt") or die "fail to rename file: $! \n";
```

### 删除文件

`unlink(<file>);`

```perl
# 删除文件
unlink("files/file_rw_app.txt");
```

### 指定文件位置

* `tell($fh)` 返回当前光标位置; 类型: int, 单位: 字节
* `seek($fh, OFFSET, START_POSITION)`
    * START_POSITION: 起始位置
        * 0: 文件开头
        * 1: 当前
        * 2: 结尾
    * OFFSET: 偏移的字节数

```perl
# 指定文件位置
open($fh, '+>>', "files/file_renamed.txt") or die "fail to open file: $! \n";

seek $fh, 7, 0; # 从文件开头位置开始移动7个字节
while(<$fh>) {
    print($_);
    my $pos = tell $fh; # 返回当前光标的位置
    print($pos, "\n");
}
print("\n");

seek $fh, 0, 0;
my $line = <$fh>;
print($line);
print(tell $fh, "\n");

seek $fh, 0, 1;
print(tell $fh, "\n");

seek($fh, 0, 2);
print(tell($fh), "\n");

close($fh);
```

### 获取文件信息

```perl
# 获取文件信息
$file = "files/file.txt";
my (@description, $is_B, $is_s, $is_c);
if(-e $file) {
    push(@description, ('文件上一次被访问的时间: ' . (-A _)));
    push(@description, ('是否是二进制文件: ' . ((-B _) ? 'T' : 'F'))) ;
    push(@description, ('文件索引修改时间: ' . (-C _)));
    push(@description, ('文件上一次修改时间: ' . (-M _)));
    push(@description, ('是否是一个socket(套接字): ' . ((-S _) ? 'T' : 'F'))) ;
    push(@description, ('是否是一个文本文件: ' . ((-T _) ? 'T' : 'F'))) ;
    push(@description, ('是否是block-special(特殊块)文件(如挂载磁盘): ' . ((-b _) ? 'T' : 'F'))) ;
    push(@description, ('是否是目录: ' . ((-d _) ? 'T' : 'F'))) ;
    push(@description, ('文件或目录名是否存在: ' . ((-e _) ? 'T' : 'F'))) ;
    push(@description, ('是否是普通文件: ' . ((-f _) ? 'T' : 'F'))) ;
    push(@description, ('是否是符号链接: ' . ((-l $file) ? 'T' : 'F'))) ;
    push(@description, ('文件或目录是否存在且不为0(返回字节数): ' . (-s $file)));
    push(@description, ('是否为空文件: ' . ((-z $file) ? 'T' : 'F'))) ;

    print(join("\n", @description), "\n");
}
```

## 目录操作

### glob

`glob`获取匹配的文件列表

```perl
my $fh;
my $file = "files/test.cpp";
open($fh, '>', $file) or die "$file: $! \n";
print($fh "Hello World!\n");
close $fh;

# 显示所有文件
print("\n", '# 显示所有文件', "\n");
my $dir = "files/*";
my @files = glob($dir);
foreach (@files) {
    print($_, "\n");
}

sub printArray {
    foreach (@_) {
        print($_, "\n");
    }
}

# 显示指定文件
print("\n", '# 显示指定文件', "\n");
my $pattern2 = "files/*.cpp";
@files = glob($pattern2);
printArray(@files);

# 显示隐藏文件
print("\n", '# 显示隐藏文件', "\n");
my $pattern3 = "files/.*";
@files = glob($pattern3);
printArray(@files);

# 显示多个目录下文件
print("\n", '# 显示多个目录下文件', "\n");
my $pattern4 = "./* files/*";
@files = glob($pattern4);
printArray(@files);
```

### opendir & readdir & closedir

open 三步曲: `opendir`=>`readdir`=>`closedir`

* `opendir($hd, DIR)`
* `@files = readdir($hd)`
* `closedir($hd)`

```perl
# 当前目录下的文件
print("\n", '# 当前目录下的文件', "\n");
my $hd;
opendir($hd, '.') or die "不能打开目录 $! \n";
@files = readdir($hd);
foreach (@files) {
    print("$_ \n");
}
close($hd);
```

### mkdir & rmdir chdir

```perl
# 目录操作
print("\n", '# 目录操作', "\n");
=pod
创建: mkdir($dir)
删除: rmdir($dir)
切换: chdir($dir)
=cut
my $new_dir = './files/new';
my $new_dir2 = './files/new2';
mkdir('./files') or print "error: fail to mkdir './files' \n";
mkdir($new_dir) or print "error: fail to mkdir '$new_dir' \n";
mkdir($new_dir2) or print "error: fail to mkdir '$new_dir2' \n";

open($fh, '>', $new_dir . '/1.txt');
print($fh 'bingou☀\n');
close($fh);

rmdir($new_dir) or print "error: fail to rmdir '$new_dir' \n";
rmdir($new_dir2) or print "error: fail to rmdir '$new_dir2' \n";

chdir($new_dir) or print "error: fail to chdir '$new_dir' \n";
@files = glob("*");
printArray(@files);
```

## 错误处理

* 判断
  * `if`
  * `unless`
  * `STANDARD ? TRUE : FALSE`
* 打印
  * `warn`
  * `die`
  * `use Carp; carp, cluck; croak, confess;`

```perl
# 错误处理

# if
my $fh;
if(open($fh, '<', "17_none.pl")) {
    print("success to open", "\n");
}
else {
    print("fail to open, error: $!", "\n");
}

open($fh, '<', "17_none.pl") || print("error: $!", "\n");

# unless
unless(chdir("none")) {
    print("fail to change dir, error: $!", "\n");
}

# 三元
my %fruits = (
    'p' => 'Peach'
);
print((exists($fruits{'p'}) ? $fruits{'p'} : 'not found'), "\n");
print((exists($fruits{'q'}) ? $fruits{'q'} : 'not found'), "\n");

# warn, die
chdir('none') || warn('STDERR', "\n");

# Carp
=pod
use Carp;
carp, cluck
croak, confess
=cut
use Carp;
carp("warn", "\n");
croak("die", "\n");
```

## 特殊变量

> 待完善

### $_

`$_`默认输入和模式匹配内容

```perl
# $_
# 默认输入和模式匹配内容
print("\n", '# $_', "\n");
foreach ('a'..'f') {
    print($_, " -> ");
}
print("end\n");

foreach ('a'..'f') {
    print;
    print(" -> ");
}
print("end\n");
```

### $

`$.`获取当前句柄的行号

```perl
# $.
# 获取当前句柄的行号
print("\n", '# $.', "\n");
open(my $fh, '<', 'files/file.txt') or die "$! \n";
while(<$fh>) {
    print($_);
    print($., "\n");
}
close($fh);
```

### $/

`$/`定义输入操作符(如<STDIN>, <FILEHANDLE>)在读取文本时如何确定边界

* 默认值: `\n`

```perl
# $/
# 定义输入操作符(如<STDIN>, <FILEHANDLE>) 在读取文本时如何确定边界
print("\n", '# $/', "\n");
$/ = ";";
print("input multi-line text:\n");
my $input = <STDIN>;
my @lines = split("\n", $input);
print("lines: \n");
foreach (@lines) {
    print($_, "\n");
}

$/ = "\n";
open(my $fh, '<', 'files/file.txt') or die "$! \n";
my $contents = do { local $/ = undef; <$fh>; };
print($contents, "\n");
close($fh);
```

### $

`$,` 定义输出字段分隔符, 定义了在用print或say输入多个值间的分隔符

* 默认值`undef`

```perl
print("\n", '# $,', "\n");
$, = "->";
my @values = (1..5);
print(@values);
print("\n");
$, = undef;
print(@values);
print("\n");
```

### $\

`$\`定义输出记录分隔符, 定义了在用print或say输出时, 会在记录末尾添加分隔符

* 默认值`undef`

```perl
# $\
# 定义输出记录分隔符, 定义了在用print或say输出时, 会在记录末尾添加分隔符
print("\n", '# $\\', "\n");
$\ = "\n";
print("1");
print("2");
print("3");
$\ = undef;
print("1");
print("2");
print("3");
```

## 正则表达式

* 三种形式
  1. 匹配 `m/PATTERN/` 或 `/PATTERN/`
  2. 替换 `s/PATTERN/`
  3. 转化 `tr/PATTERN/`
* 操作符
  1. `=~` 匹配
  2. `!~` 不匹配

```perl
=pod
三种形式:
1. 匹配: m/PATTERN/ 或 /PATTERN/
2. 替换: s/PATTERN/REPLACEMENT/
3. 转化: tr///

操作符:
* =~ 相匹配
* !~ 不匹配
=cut

# 匹配操作符
print("\n", '# =~', "\n");
my $str1 = "name: gendloop";
if ($str1 =~ /name/) {
    print("match: 'gendloop'", "\n");
}
if($str1 !~ m/pooldneg/) {
    print("match: 'pooldneg'", "\n");
}
```

### `$`` `$&`  `$'`

* `$`` 匹配部分的前一部分
* `$&` 匹配部分
* `$'` 未匹配的剩余部分

```perl
# 三个特殊变量
=pod
$`  匹配部分的前一部分字符串
$&  匹配的字符串
$'  未匹配的剩余字符串
=cut
print("\n", '$` $& $\'', "\n");
$str1 = "A_B_C";
$str1 =~ "B";
print("$`", "\n");
print("$&", "\n");
print("$'", "\n");
```

### [m]/PATTERN/[MODIFIER]

* 修饰符
  * `i` 忽略模式中的大小写
  * `x` 忽略模式中的空白
  * `g` 全局匹配. 查找所有匹配的模式, 并在每次匹配后继续查找下一个匹配

```perl
# 模式匹配修饰符
=pod
i   忽略模式中的大小写
x   忽略模式中的空白
g   全局匹配. 查找所有匹配的模式，并在每次匹配后继续查找下一个匹配。
=cut

# i
print("\n", 'i', "\n");
$str1 = "Hello WoRlD, from a maniac";
if($str1 =~ m/world/i) {
    print("match: '$&'", "\n");
}
else {
    print("match nothing", "\n");
}

# x
print("\n", 'x', "\n");
$str1 = "Line123";
if($str1 =~ m/Line 1 2 3/x) {
    print("match: '$&'", "\n");
}
else {
    print("match nothing", "\n");
}

# g
print("\n", 'g', "\n");
$str1 = "Hi \tforeigner Hi\t gendloop";
while($str1 =~ m/Hi[\s]+[a-z]+/g) {
    print("match: '$&'", "\n");
}
```

### s/PATTERN/REPLACEMENT/[MODIFIER]

```perl
# 替换操作符
=pod
s/PATTERN/REPLACEMENT/[MODIFIER]
=cut
print("\n", '# substitute', "\n");
$str1 = "welcome to my notes";
my $str2 = $str1;
$str2 =~ s/my/gendloop's/;
print('\'', $str1, '\' => \'', $str2, "\'\n");

# i
print("\n", 'i', "\n");
$str1 = "hello, world";
$str2 = $str1;
$str2 =~ s/HELLO/Hi/i;
$str2 =~ s/WORLD/gendloop/i;
print('\'', $str1, '\' => \'', $str2, "\'\n");

# x
print("\n", 'x', "\n");
$str1 = "Blank";
$str2 = "B l a  n k ";
$str1 =~ s/$str2/NoBlank/x;
print('\'', "Blank", '\' => \'', $str1, "\'\n");

# g
print("\n", 'g', "\n");
$str1 = "1 2 3 \n 4 5 6 \n";
$str2 = '\d';
$str1 =~ s/$str2/D/;
print('\'', "1 2 3 \n 4 5 6 \n", '\' => \'', $str1, "\'\n");
$str1 =~ s/$str2/D/g;
print('\'', "1 2 3 \n 4 5 6 \n", '\' => \'', $str1, "\'\n");
```

### tr/PATTERN/REPLACEMENT/[MODIFIER]

* 修饰符
  * `s` 删除连续且相同的字符, 仅保留一个
  * `c` 转换所有未指定的字符
  * `d` 删除所有指定的字符

```perl
# 转化操作符
=pod
字符替换
tr/PARTTERN/REPLACEMENT/[MODIFIER]
s   删除连续且相同的字符, 仅保留一个
c   转换所有未指定的字符
d   删除所有指定字符
=cut

print("\n", '# transliteration', "\n");

$str1 = "world";
$str1 =~ tr/a-z/A-Z/;
print("world", ' => ', $str1, "\n");

# s
print("\n", 's', "\n");
$str1 = "gendloopgendloop";
$str1 =~ tr/a-z/A-Z/s;
print("gendloopgendloop", ' => ', $str1, "\n");

# c
print("\n", 'c', "\n");
$str1 = "animal";
$str1 =~ tr/a/A/c;
print("animal", ' => ', $str1, "\n");

# d
print("\n", 'd', "\n");
$str1 = "animal";
$str1 =~ tr/a//d;
print("\'animal", '\' => \'', $str1, "\'\n");
```

## 发送邮件

\

## Socket 编程

\

## 面向对象

## References

1. [Perl 教程 | 菜鸟教程](https://www.runoob.com/perl/perl-tutorial.html)
2. [https://perldoc.perl.org/perlre#Regular-Expressions](https://perldoc.perl.org/perlre#Regular-Expressions)
3. [Perl 教程](http://www.92csz.com/study/perl/index.htm)
4. [BeginnersBook Perl 教程 · BeginnersBook 中文系列教程 · 看云](https://www.kancloud.cn/apachecn/beginnersbook-zh/1955924)
5. [两个半小时学会Perl](https://qntm.org/perl_cn)
