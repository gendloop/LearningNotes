# Summary

## 习惯

* 在`.pl`文件开头加上
  * `use strict;`
  * `use warnings;`

## 用于变量的关键字

* `my` 局部变量
* `local` 局部全局变量
* `our` 全局变量
* `state` 静态变量, 需要加上`use feature 'state';`

### `my` VS `local`

```perl
# `my` vs `local`

use strict;
use warnings;

$a = 1;

sub printA {
    print($a, "\n");
}

sub funcMy {
    my $a = 2;
    printA();
}

sub funcLocal{
    local $a = 3;
    printA();
}

printA();
funcMy();
funcLocal();
printA();
```

## sort

```perl
use strict;
use warnings;

# sort 排序
=pod
sort LIST
sort SUBROUTINE LIST
=cut

sub printL {
    my $str = join(' -> ', @_);
    print($str, "\n");
}

sub f_bigger {
    return $a lt $b;
}

my @a = ('b', 'd', 'c', 'a');

my @b = sort(@a);

my @c = sort(f_bigger, @a);

printL(@a);
printL(@b);
printL(@c);
```
