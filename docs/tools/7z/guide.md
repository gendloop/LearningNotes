# Guide

## Add

1. 添加当前目录和子目录

    `7z a <archive>`

2. 包含目录前缀

    `7z a <archive> folder/`
    or `7z a <archive> folder/*`

3. 不包含目录前缀

    `7z a <archive> ./folder/*`

4. 添加文件

    `7z a <archive> file.txt`

5. 添加匹配的目录和文件

    `7z a <archive> folder/* file.txt`

6. 添加匹配的目录并覆盖已有文件

    `7z a <archive> folder/* -aoa`

7. 指定分卷大小

    `7z a -v<volume_size> <archive> folder`

8. 指定压缩线程数

    `7z a <archive> -v5g -mmt14 folder`

9. 指定压缩类型

    `7z a <archive> -tzip folder`

## Extract

1. 解压到当前目录

    `7z x <archive>`

2. 解压到指定目录

    `7z x <archive> -o<output_folder>`

3. 解压并覆盖已有文件

    `7z x <archive> -aoa`
