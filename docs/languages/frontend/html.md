# HTML

HTML(HyperText Markup Language)超文本标记语言, 用于创建网页

## 实例

> 中文网页需要使用 <meta charset="utf-8"> 声明编码, 否则会乱码

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>第一个实例</title>
</head>

<body>
  <h1>第一个标题</h1>
  <p>第一个段落</p>
</body>

</html>
```

更多实例: [https://www.runoob.com/html/html-examples.html](https://www.runoob.com/html/html-examples.html)

## 标题

```html
<body>
  <h1>一级标题</h1>
  <h2>二级标题</h2>
  <h3>三级标题</h3>
  <h4>四级标题</h4>
  <h5>五级标题</h5>
  <h6>六级标题</h6>
</body>
```

## 段落

```html
<body>
  <p>这是一个段落, 内容是关于段落的</p>
  <p>这是另一个段落, 内容是关于另一个段落的</p>
</body>
```

## 链接

> href(hypertext reference)

```html
<body>
  <!-- 文本链接 -->
  <a href="https://www.yuque.com/gendloop/learningnotes/frontend-html">HTML</a>
  <hr>
  <!-- 在当前窗口或标签页中打开链接 -->
  <a href="https://www.yuque.com/gendloop/learningnotes/frontend-html" target="_self">_self</a>
  <hr>
  <!-- 在新窗中或新标签中打开链接 -->
  <a href="https://www.yuque.com/gendloop/learningnotes/frontend-html" target="_blank">_blank</a>
  <hr>
  <!-- 在父框架中打开链接 -->
  <a href="https://www.yuque.com/gendloop/learningnotes/frontend-html" target="_parent">_parent</a>
  <hr>
  <!-- 在整个窗口中打开链接 取消任何框架 -->
  <a href="https://www.yuque.com/gendloop/learningnotes/frontend-html" target="_top">_top</a>
  <hr>
  <!-- nofollow 表示搜索引擎不应跟踪该链接, 常用于外部链接 -->
  <a href="https://www.yuque.com/gendloop/learningnotes/frontend-html" target="_blank" rel="nofollow">rel="nofollow"</a>
  <hr>
  <!-- noopener 防止新的浏览上下文页面访问 window.opener 属性和 open 方法 -->
  <!-- noreferrer 不发送 referer header, 即不告诉目标网站你从哪里来的 -->
  <a href="https://www.yuque.com/gendloop/learningnotes/frontend-html" target="_blank" rel="noopener noreferrer">安全链接</a>
  <hr>
  <!-- download 提示浏览器下载链接目标而不是导航到该目标 -->
  <a href="file.pdf" download="example.pdf">下载文件</a>
  <hr>
  <!-- hreflang 指定链接的目标 URL 的语言 -->
  <a href="https://www.example.com/es" hreflang="es">访问西班牙语网站</a>
  <hr>
  <!-- type 指定链接资源的 MIME 类型 -->
  <a href="style.css" type="text/css">样式表</a>
  <hr>
  <!-- style 直接在元素上定义 CSS 样式 -->
  <a href="https://www.example.com" style="color: red;">红色链接</a>
  <hr>
  <!-- 锚点链接 -->
  <a href="#section1">跳转到第 1 部分</a>
  <div id="section1">这是第 1 部分</div>
  <hr>
  <!-- 图像链接 -->
  <a href="https://www.yuque.com/gendloop/learningnotes/frontend-html">
    <img src="res/favicon_32x32.ico" alt="Frontend">
  </a>
  <hr>
  <!-- id 用于创建一个 HTML 书签, 不显示 -->
  <a id="tips">这是提示</a>
  <a href="#tips">访问提示</a>
  <hr>
  <!-- 空链接  -->
  <a href="#">导航到页面顶部, 会跳转, 作为占位符, 捕获点击事件</a>
  <hr>
  <a href="javascript:void(0)">阻止默认行为, 不刷新页面, 不会跳转, 配合 JS 使用</a>
  <hr>
  <a href="">刷新当前页面, 会跳转</a>
  <hr>
  <a href="about:blank">在新窗口打开空白页面, 会跳转</a>
  <hr>
  <a role="button">链接表现为按钮, 无默认行为, 不会跳转, 配合 JS 实现按钮功能</a>
  <hr>
</body>
```

## 图像

```html
<body>
<img src="res/nature.png" width="380" height="250"/>
</body>
```

## 换行

```html
<body>
  <p>这是一段被换行符<br/>隔开的文字</p>
</body>
```

## 属性

| **属性名** | **适用元素** | **说明** |
| --- | --- | --- |
| `id` | 所有 | 为元素指定唯一标识符 |
| `class` | 所有 | 为元素指定一个或多个类名, 用于 CSS 或 JavaScript 选择 |
| `style` | 所有 | 直接在元素上应用 CSS 样式 |
| `title` | 所有 | 为元素提供提示信息, 在鼠标悬停时显示 |
| `date-*` | 所有 | 用于存储自定义数据, 通常通过 JavaScript 访问 |
| `href` | <a> <link> | 指定链接的目标 URL |
| `src` | <img> <script> <iframe> | 指定外部资源的 URL |
| `alt` | <img> | 为图像提供替代文本, 当图像无法显示时 |
| `type` | <input> <button> | 指定输入控件的类型 (如 text, password, checkbox 等) |
| `value` | <input> <button> <option> | 指定元素的初始值 |
| `disabled` | 表单元素 | 禁用元素, 使其不可交互 |
| `checked` | <input type="checkbox">   <input type="radio"> | 指定复选框或单选按钮是否被选中 |
| `placeholder` | <input> <textarea> | 在输入框中显示提示文本 |
| `target` | <a> <form> | 指定链接或表单提交的目标窗口或框架 (如 _blank) |
| `readonly` | 表单元素 | 使输入框只读 |
| `required` | 表单元素 | 指定输入字段为必填项 |
| `autoplay` | <audio> <video> | 自动播放媒体 |
| `onclick` | 所有 | 当用户点击元素时触发 JavaScript 事件 |
| `onmouseover` | 所有 | 当用户将鼠标悬停在元素上时触发 JavaScript 事件 |
| `onchange` | 表单元素 | 当元素的值发生变化时触发 JavaScript 事件 |

```html
<body>
  <div id="header">我的 id 是 header</div>
  <p class="text highlight">我属于高亮文本类 "text hightlight"</p>
  <p style="color: red; font-size: 14px;">这是一个用了 style 属性的文本</p>
  <p title="才没有提示哦">鼠标悬停在我上面会显示提示哟</p>
  <div data-user-id="123">用户 id (data-*)</div>
  <a href="https://github.com/gendloop/Frontend">上链接, 我要源码</a><br/>
  <img src="res/none.png" alt="没图时就显示我喽"/><br/>
  <input type="text" placeholder="提示文本: 请输入名字"><br/>
  <input type="text" value="默认值 gendloop"><br/>
  <input type="text" disabled placeholder="不可交互"><br/>
  <a href="https://github.com/gendloop/Frontend" target="_blank">在新窗口打开呗</a><br/>
  <input type="text" readonly placeholder="只读项"><br/>
  <input type="text" required placeholder="必填项">
</body>
```

## 水平线

```html
<body>
  <p>下面有一条水平线</p>
  <hr>
  <p>上下各有一条水平线</p>
  <hr>
  <p>上面有一条水平线</p>
</body>
```

## 注释

```html
<body>
  <!-- 这是一条注释 -->
  <p>上面是注释</p>
</body>
```

## 头部

```html
<body>
  <p>头部区域的元素标签有 title, style, meta, link, script, noscript, base</p>
  <hr>
  <p>title: 标题; 收藏夹显示的标题; 在搜索引擎页面的标题</p>
  <hr>
  <p>base: 所有链接地址的前缀</p>
  <hr>
  <p>link: 用于链接到样式表</p>
  <hr>
  <p>style: 定义样式文件引用地址</p>
  <hr>
  <p>meta: 描述一些元数据, 会被解析, 但不显示</p>
  <hr>
  <p>script: 加载脚本文件</p>
  <hr>
</body>
```

## 样式

```html
<body>
  <h1>红色标题</h1>
  <a href="url" style="text-decoration:none;">无下划线链接</a>
  <p style="color: rebeccapurple;margin-left: 20px;background-color: yellow;">段落</p>
</body>
```

## 表格

```html
<body>
  <ul>
    <li>tr: table row 的缩写, 表示表格的一行</li>
    <li>td: table data 的缩写, 表示表格的数据单元格</li>
    <li>th: table header 的缩写, 表示表格的表头单元格</li>
  </ul>
  <table border="1">
    <thead>
      <caption>表格标题</caption>
      <tr>
        <th>第一列标题</th>
        <th>第二列标题</th>
        <th>第三列标题</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td rowspan="2">行12, 列1</td>
        <td colspan="2">行1, 列23</td>
      </tr>
      <tr>
        <td>行2, 列2</td>
        <td>行2, 列3</td>
      </tr>
    </tbody>
  </table>
</body>
```

## 列表

```html
<body>
  <ul>
    <li>Apple</li>
    <li>Banana</li>
  </ul>
  <ol>
    <li>Apple</li>
    <li>Banana</li>
  </ol>
</body>
```

## 分区

```html
<body>
  <div id="container">

    <div id="header" style="background-color: antiquewhite;">
      <h1 style="margin-bottom: 0;">网页标题</h1>
    </div>

    <div id="menu" style="background-color: darkorange; width: 100px; float: left;">
      <b>菜单</b>
      <hr>
      <p>HTML</p>
      <p>CSS</p>
      <p>JavaScript</p>
    </div>

    <div id="content" style="background-color: aqua;">
      内容...
    </div>

    <div id="fotter" style="background-color: antiquewhite; clear: both; text-align: center;">
      版权
    </div>
  </div>
</body>
```

## 表单

```html
<body>
  <form action="" method="post">
    <!-- 文本输入框 -->
    <label for="name">用户名:</label>
    <input type="text" id="name" name="user" required>

    <br/>

    <!-- 密码输入框 -->
    <label for="password">密码:</label>
    <input type="password" id="password" name="password" required>

    <br/>

    <!-- 单选按钮 -->
    <label>性别:</label>
    <input type="radio" id="male" name="gender" value="male" checked>
    <label for="male">男</label>
    <input type="radio" id="female" name="gender" value="female">
    <label for="female">女</label>

    <br/>

    <!-- 复选框 -->
    <input type="checkbox" id="subscribe" name="subscribe" checked>
    <label for="subscribe">订阅</label>
    <input type="checkbox" id="send" name="send" checked>
    <label for="send">发送</label>

    <br/>

    <!-- 下拉列表 -->
    <label for="country">国家</label>
    <select id="country" name="country">
      <option value="cn">CN</option>
      <option value="uk">UK</option>
    </select>

    <br/>

    <!-- 提交按钮 -->
    <input type="submit" value="提交">
  </form>
</body>
```

## 框架

```html
<body>
  <iframe src="demo_iframe.htm" name="iframe_baidu"></iframe>
  <p><a href="https://baidu.com" target="iframe_baidu" rel="noopener">百度</a></p>
</body>
```

## 颜色

```html
<body>
  <p>颜色由一个十六进制符号定义, 由红, 绿, 蓝(RGB) 三个值组成</p>
  <p>每种颜色的范围是 0(#00) ~ 255(#ff)</p>
  <table border="1">
    <thead>
      <caption>常见颜色值</caption>
      <tr>
        <th style="width: 180px;">color</th>
        <th style="width: 100px;">hex</th>
        <th style="width: 100px;">rgb</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="background-color: black"></td>
        <td>#000000</td>
        <td>rgb(0,0,0)</td>
      </tr>
      <tr>
        <td style="background-color: #ff0000;"></td>
        <td>#ff0000</td>
        <td>rgb(255,0,0)</td>
      </tr>
      <tr>
        <td style="background-color: rgb(0,255,0);"></td>
        <td>#00ff00</td>
        <td>rgb(0,255,0)</td>
      </tr>
      <tr>
        <td style="background-color: blue;"></td>
        <td>#0000ff</td>
        <td>rgb(0,0,255)</td>
      </tr>
      <tr>
        <td style="background-color: white;"></td>
        <td>#ffffff</td>
        <td>rgb(255,255,255)</td>
      </tr>
    </tbody>
  </table>
</body>
```

## 脚本

```html
<body>
  <p>
    写入到 HTML
  </p>
  <script>document.write("Hello World")</script>
  <noscript>Sorry, not support JavaScript</noscript>
  <script>
    document.write("<h1>一级标题</h1>");
    document.write("<p>段落</p>");
  </script>

  <p id="click">
    触发事件
  </p>
  <script>
    function changeContent() {
      document.getElementById("click").innerHTML="我改变喽!";
    }
    function chageColor() {
      x = document.getElementById("click");
      x.style.color="#ff0000";
    }
  </script>
  <button type="button" onclick="changeContent()">点我</button>
  <br/>
  <button type="button" onclick="chageColor()">再点我</button>
</body>
```

## 实体

```html
<body>
  <table border="1" style="width: 100%;">
    <thead>
      <caption>字符实体</caption>
      <tr>
        <th>显示结果</th>
        <th>描述</th>
        <th>实体名称</th>
        <th>实体编号</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td> </td>
        <td>空格</td>
        <td>&amp;nbsp;</td>
        <td>&amp;#160;</td>
      </tr>
      <tr>
        <td>&lt;</td>
        <td>小于号</td>
        <td>&amp;lt;</td>
        <td>&amp;#60;</td>
      </tr>
    </tbody>
  </table>
</body>
```

## URL

```html
<body>
  <h2>URL - 统一资源定位器</h2>
  <code>scheme://host.domain:port/path/filename</code>

  <h2>常见的 URL Scheme</h2>
  <table border="1">
    <thead>
      <tr>
        <th>Scheme</th>
        <th>访问</th>
        <th>用于...</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>http</td>
        <td>超文本传输协议</td>
        <td>以 http:// 开头的普通网页, 不加密</td>
      </tr>
      <tr>
        <td>https</td>
        <td>安全超文本传输协议</td>
        <td>安全网页, 加密所有信息交换</td>
      </tr>
      <tr>
        <td>ftp</td>
        <td>文件传输协议</td>
        <td>用于将文件下载或上传至网站</td>
      </tr>
      <tr>
        <td>file</td>
        <td></td>
        <td>本机上的文件</td>
      </tr>
    </tbody>
  </table>

  <h2>URL 字符编码</h2>
  <p>只能使用 ASCII 字符集</p>
  <p>使用"%"其后跟两位的十六进制数来替换非 ASCII 字符</p>
  <p>不能包含空格. 使用 + 来替换空格</p>
</body>
```

## 文本格式化

```html
<body>
  <b>粗体文本</b>
  <br/>
  <code>代码文本 int z = x + y;</code>
  <br/>
  <em>强调文本</em>
  <br/>
  <i>斜体文本</i>
  <br/>
  <kbd>键盘输入文本</kbd>
  <br/>
  <pre>预格式化文本</pre>
  <br/>
  <small>更小的文本</small>
  <br/>
  <strong>重要的文本</strong>
  <br/>
  <abbr>缩写</abbr>
  <br/>
  <address>联系方式</address>
  <br/>
  <bdo>文字方向</bdo>
  <br/>
  <blockquote>引用</blockquote>
  <br/>
  <cite>工作的名称</cite>
  <br/>
  <del>删除的文本</del>
  <br/>
  <ins>插入的文本</ins>
  <br/>
  <sup>上标文本</sup>
  <br/>
  <sub>下标文本</sub>
</body>
```

## 标签简写及全称

| **标签** | **英文全称** | **中文说明** |
| --- | --- | --- |
| a | Anchor | 锚 |
| abbr | Abbreviation | 缩写 |
| acronym | Acronym | 取首字母的缩写词 |
| address | Address | 地址 |
| alt | Alter | 替用 |
| b | Bold | 粗体<font style="color:rgb(38, 38, 38);">文本</font> |
| bdo | Bi-Directional Override | 文本显示方向 |
| big | Big | 变大<font style="color:rgb(38, 38, 38);">文本</font> |
| blockquote | Block Quotation | 块引用 |
| br | Break | 换行 |
| cell | cell | 单元格 |
| cellpadding | Cellpadding | 单元格内边距 |
| cellspacing | Cellspacing | 单元格间距 |
| center | Centered | 居中<font style="color:rgb(38, 38, 38);">文本</font> |
| cite | Citation | 引用<font style="color:rgb(38, 38, 38);">文本</font> |
| code | Code | 代码<font style="color:rgb(38, 38, 38);">文本</font> |
| dd | Difinition Description | 定义描述 |
| del | Deleted | 删除的 |
| dfn | Defines a Definition Term | 定义条目 |
| div | Division | 分区 |
| dl | Definition List | 定义列表 |
| dt | Definition Term | 定义术语 |
| em | Emphasized | 加重<font style="color:rgb(38, 38, 38);">文本</font> |
| font | Font | 字体 |
| h1~h6 | Header 1 to Header 6 | 一级到六级标题 |
| hr | Horizontal Rule | 水平线 |
| href | hypertext reference | 超文本引用 |
| i | Italic | 斜体<font style="color:rgb(38, 38, 38);">文本</font> |
| iframe | Inline Frame | 内联框架 |
| ins | Inserted | 插入的<font style="color:rgb(38, 38, 38);">文本</font> |
| kdb | Keyboard | 键盘<font style="color:rgb(38, 38, 38);">文本</font> |
| li | List Item | 列表项目 |
| nl | Navigation List | 导航列表 |
| ol | Ordered List | 排序列表 |
| optgroup | Option Group | 选项组 |
| p | Paragraph | 段落 |
| pre | Preformatted | 预定义格式<font style="color:rgb(38, 38, 38);">文本</font> |
| q | Quotation | 引用语 |
| rel | Reload | 加载 |
| strike | Strikethrough | 删除线 |
| samp | Sample | 示例<font style="color:rgb(38, 38, 38);">文本</font> |
| small | Small | 变小<font style="color:rgb(38, 38, 38);">文本</font> |
| span | Span | 范围 |
| src | Source | 源文件链接 |
| strong | Strong | 加重<font style="color:rgb(38, 38, 38);">文本</font> |
| sup | Superscripted | 上标<font style="color:rgb(38, 38, 38);">文本</font> |
| sub | Subscripted | 下标<font style="color:rgb(38, 38, 38);">文本</font> |
| td | Table Data Cell | 表格中的一个单元格 |
| th | Table Header Cell | 表头 |
| tr | Table Row | 表格中的一行 |
| tt | Teletype | 打印机文本 |
| u | Underlined | 下划线文本 |
| ul | Unordered List | 不排序列表 |
| var | Variable | 变量文本 |

## References

1. [https://www.runoob.com/html/html-tutorial.html](https://www.runoob.com/html/html-tutorial.html)
