# JavaScript

## 基础使用

1. 在HTML中引用

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <script src="my_script.js"></script>
    </head>
    </html>
    ```

2. 脚本编写和运行

    ```bash
    # 安装运行环境 Node.js
    $ scoop install nodejs

    # 编写 test.js 文件
    console.log("Hello World);

    # 使用 node 运行脚本
    $ node test.js

    # 使用谷歌浏览器
    # 方式 1
    右键 "检查" => 控制台 => 编写命令 => 回车执行
    # 方式 2
    右键 "检查" => 源代码 => 片段 => 编写新脚本片段 => 右键执行
    ```

3. 注释

    ```javascript
    // 行注释
    console.log("Comment");

    /**
    * @brief 块注释
    */
    console.log("Comment");
    ```

## 输出

```javascript
// 弹出警告框
window.alert(5 + 3);

// 替换 HTML 中元素内容
document.getElementById("content").innerHTML = "写入后内容";

// 写入控制台
console.log("output.js 已加载");
```

## 语法

* 优先使用 const, let 声明变量, 避免使用 var
* var
  * 函数级作用域
  * 初始化前访问为 undefined
  * 允许重复声明
* let
  * 块级作用域
  * 初始化前访问会报错
  * 不允许重复声明
* const
  * 块级作用域
  * 声明时必须初始化
* 变量拥有动态类型, 设不同值为不同类型: `number` `string` `boolean` `object` `undefined` `symbol`

## References

1. [https://www.runoob.com/js/js-tutorial.html](https://www.runoob.com/js/js-tutorial.html)
