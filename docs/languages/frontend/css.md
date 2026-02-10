# CSS

CSS (Cascading Style Sheets) 层叠样式表, 用于渲染 HTML 元素标签的样式.

## 注释

```css
/* 通用样式   base.css     */
/* 布局样式   layout.css    */
/* 组件样式   components.css  */
/* 页面特定样式  pages.css    */
```

## 选择器

```css
p {
    color: red;
}

/* id 选择器, "#" 前缀, 用于唯一元素 */
#blue-text {
    color: blue;
}

/* class 选择器, "." 前缀, 用于具有相同属性的一类元素 */
.text-bold {
    font-weight: bold;
}
.text-italic {
    font-style: italic;
}

```

```html
<body>
  <p>一段红色的文本</p>

  <!-- id 选择器 -->
  <p id="blue-text">一段蓝色的文本</p>

  <!-- class 选择器, 能用 class 就不要用 id -->
  <p class="text-bold">加粗文本</p>
  <p class="text-italic">倾斜文本</p>
  <p class="text-bold text-italic">加粗倾斜文本</p>
</body>
```

## 插入样式表

插入样式表方法有三种:

+ 外部样式表(External style sheet)
+ 内部样式表(Internal style sheet)
+ 内联样式(Inline style)

```css
h1 {
    color: red;
}

h2 {
    color: green;
}

h3 {
    color: yellow;
}
```

```html
<head>
  <meta charset="utf-8">
  <title>插入样式表</title>
  <!-- 插入外部样式表 -->
  <link rel="stylesheet" type="text/css" href="insert_style_sheet.css">
  <!-- 插入内部样式表 -->
  <style>
    h2 {
      color: blue;
    }
    h3 {
      color: orange;
    }
  </style>
</head>

<body>
  <h1>应用外部样式表</h1>
  <h2>应用内部样式表</h2>
  <h3 style="color: purple">应用内联样式</h3>
</body>
```

## 背景

```css
body {
  background-color: antiquewhite;
  background-image: url('background.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}
```

## 文本

```css
h1 {
  text-decoration: overline;
}

h2 {
  text-decoration: line-through;
}

h3 {
  text-decoration: underline;
}

p {
  text-indent: 30px;
}

p.date {
  text-align: right;
}

p.main {
  text-align: justify;
}

p.uppercase {
  text-transform: uppercase;
}

p.lowercase {
  text-transform: lowercase;
}

p.capitalize {
  text-transform: capitalize;
}

```

```html
<body>
  <h1>一级标题</h1>
  <h2>二级标题</h2>
  <h3>三级标题</h3>
  <p class="date">2025年06月09日</p>
  <p class="main">我想试一试，看看自己能不能做到。虽然心里有点忐忑，但更多的是跃跃欲试的兴奋。就像站在泳池边，既害怕水凉，又迫不及待想跳进去感受那份畅快。不管结果如何，至少我勇敢地迈出了第一步，这本身就是一种成长。万一成功了呢？那该多棒啊！</p>
  <p><small>可调整窗口大小查看 &quot;justify&quot; 作用</small></p>
  <p class="uppercase">AaBbCcDd</p>
  <p class="lowercase">AaBbCcDd</p>
  <p class="capitalize">aabbccDd</p>
</body>
```

## 链接

```css
/* 未访问链接 */
a:link {
  color: #000000;
}

/* 已访问链接 */
a:visited {
  color: #00ff00;
}

/* 鼠标移动到链接上 */
a:hover {
  color: #ff00ff;
}

/* 鼠标点击时 */
a:active {
  color: #0000ff;
}

```

## 列表

```css
ul.circle {
  list-style-type: circle;
}

ul.square {
  list-style-type: square;
}

ol.upper-roman {
  list-style-type: upper-roman;
}

ol.lower-alpha {
  list-style-type: lower-alpha;
}

```

## 分组和嵌套

```html
<body>
    <h1>分组与嵌套示例</h1>
    <h2 class="marked">分组与嵌套</h2>
    <p class="marked">下划线文本</p>
    <div class="marked">
        <p>白色文本</p>
        <p class="marked">白色下划线文本</p>
    </div>
</body>
```

```css
h1,
h2,
p {
  color: blue;
  text-align: center;
}

.marked {
  background-color: red;
}

.marked p {
  color: white;
}

p.marked {
  text-decoration: underline;
}

```

## 导航栏

```html
<body>
  <h1>导航栏</h1>
  <nav class="navbar">
    <ul>
      <li><a class="active" href="#home">首页</a></li>
      <li><a href="#about">关于</a> </li>
      <li><a href="#services">服务</a></li>
      <li><a href="#contact">联系</a></li>
    </ul>
  </nav>
  <div class="content">
    <p>这里是内容区域。</p>
  </div>
  <div class="dropdown">
    <button>下拉菜单</button>
    <div class="dropdown-content">
      <a href="#">链接1</a>
      <a href="#">链接2</a>
      <a href="#">链接3</a>
    </div>
  </div>
</body>
```

## References

1. [https://www.runoob.com/css/css-tutorial.html](https://www.runoob.com/css/css-tutorial.html)
2. [https://www.jyshare.com/examples/](https://www.jyshare.com/examples/)
