# Guide

## 安装

```bash
scoop install qpdf
```

## 截取部分页面

```bash
# 打开 source.pdf, 从 source.pdf 中截取 1-5 页, 输出到 ouput.pdf 中
$ qpdf souce.pdf --pages souce.pdf 1-5 -- output.pdf
```

## References

1. [https://qpdf.readthedocs.io/en/stable/cli.html](https://qpdf.readthedocs.io/en/stable/cli.html)
