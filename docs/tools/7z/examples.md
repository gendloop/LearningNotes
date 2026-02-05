# Examples

## a-Add

1. 添加目录, 包含`subdir\`前缀

    `7z a archive1.zip subdir\` or `7z a archive1.zip subdir\*`

    ```plain
    subdir/
    ├── 1-2/
    │   └── 1.txt
    ├── 1.txt
    └── 2.txt
    ```

    <img src="res/1.png" alt="1.png" style="zoom:50%;"/>

2. 添加目录, 不包含`subdir\`前缀

    `7z a archive2.zip .\subdir\*`

    ```plain
    subdir/
    ├── 1-2/
    │   └── 1.txt
    ├── 1.txt
    └── 2.txt
    ```

    <img src="res/2.png" alt="2.png" style="zoom:50%;"/>

3. 添加文件

    `7z a subdir.7z new.txt`

    <img src="res/3.png" alt="3.png" style="zoom:50%;"/>
    <img src="res/4.png" alt="4.png" style="zoom:50%;"/>

## x-Extract

1. 解压到当前目录

    `7z x archive2.zip`

    <img src="res/5.png" alt="5.png" style="zoom:50%;"/>

    ```plain
    folder/
    └── archive2.zip
    ```

    ```plain
    ├── 1-2/
    │   └── 1.txt
    ├── 1.txt
    ├── 2.txt
    ├── new.txt
    └── archive2.zip
    ```

2. 解压到指定目录下

    `7z x archive2.zip -oarchive2`

    <img src="res/6.png" alt="6.png" style="zoom:50%;"/>

    ```plain
    folder/
    └── archive2.zip
    ```

    ```plain
    folder/
    ├── archive2/
    │   ├── 1-2/
    │   │   └── 1.txt
    │   ├── 1.txt
    │   ├── 2.txt
    │   └── new.txt
    └── archive2.zip
    ```
