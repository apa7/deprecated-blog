#W3C School HTML 起步

20160412 

---

HTML 元素: `<p name="value" other-attr="value">{content here}</p>`

比如 `<br />` 是关闭空元素(没有内容的 HTML 元素)的正确方法.

HTML 标签对大小写不敏感：`<P>` 等同于 `<p>`; 属性和属性值 也大小写不敏感

属性值应该始终被包括在引号内。双引号、单引号 is OK.
协议规定了每个 HTML 元素可使用的合法属性



`<h1 align = "center">This is heading 1</h1>` : 对齐方式为居中

`<body bgcolor="yellow">` : 整个`body`的背景色为黄色, 不过也不是所有元素都有这个属性, `<title>`和`<p>`就都没有


HTML 水平线: `<hr /> `

HTML 段落: `<p>`

浏览器会移除源代码中多余的空格和空行：
```html
<p>This is<br />a para<br />graph with 
line breaks</p>

---
This is
a para
graph with line breaks
```

`<pre>` : 预定义格式文本. 原样输出
`<code>` : 其实这个元素本身并没用。并不会显示为*预定义格式*.

`<abbr>` : `The <abbr title="People's Republic of China">PRC</abbr> was founded in 1949.`  在鼠标指针移动到 <abbr> 元素上时显示出简称/缩写的完整版本。

`<blockquote>` : 会从常规文本中分离出来，经常会在左、右两边进行缩进（增加外边距）

#CSS
##内部样式表 : <head>的样式信息
```html
<html>

<head>
<style type="text/css">
h1 {color: red}
p {color: blue}
</style>
</head>

<body>
<h1>header 1</h1>
<p>A paragraph.</p>
</body>

</html>
```

##内联样式 : style=" "
```html
<a href="/example/html/lastpage.html" style="text-decoration:none">
这是一个链接！
</a>
```

##外部样式表
```html
<head>
<link rel="stylesheet" type="text/css" href="/html/csstest1.css" >
</head>
```

/html/csstest1.css
```css
h1           
{ 
color: green;
border: 1pt solid black;
}

p
{
color: red;
background-color:#EFE7D6;
border: 1pt solid black;
}
```

#分块

“块级元素”译为 block level element，“内联元素”译为 inline element。块级元素在浏览器显示时，通常会以新行来开始（和结束）。内联元素则不会。

##`<div>`  定义文档中的节或区域（块级）
`<div>` 元素没有特定的含义。除此之外，由于它属于块级元素，浏览器会在其前后显示折行。

```html
<div style="color:#00FF00">
  <h3>This is a header</h3>
  <p>This is a paragraph.</p>
</div>
---
就这部分变色了
```

##`<span>`  定义文档中的行内的小块或区域
HTML `<span>` 元素是内联元素，可用作文本的容器。

```html
<p><span style="color:#003399">some text </span>some other text.</p>
---
就扩起来的部分变色了，依然保持在一行。
```

#`<a>`

`<a href="http://www.w3school.com.cn/">Visit W3School</a>`

*Tips:在md里写html的笔记好危险，一旦没有`圈起来的元素`都会被解释*
##target="" 在何处显示

```html
<a href="http://www.w3school.com.cn/" target="_blank">Visit W3School!</a>
```

`target="_top"` 会跳出框架
在新窗口打开文档
##href->[name=""] name锚
```html
<a name="tips">基本的注意事项 - 有用的提示</a>
<a href="#tips">有用的提示</a>
<a href="http://www.w3school.com.cn/html/html_links.asp#tips">有用的提示</a>
```

*`name`不会以任何特殊方式显示，它对读者是不可见的。*
*id 属性来替代 name 属性，命名锚同样有效。*

>请始终将正斜杠添加到子文件夹。假如这样书写链接：`href="http://www.w3school.com.cn/html"`，就会向服务器产生两次 HTTP 请求。这是因为服务器会添加正斜杠到这个地址，然后创建一个新的请求，就像这样：`href="http://www.w3school.com.cn/html/"`


---
2016-04-13
---


#图像
```html
<img src="url" />
```

##alt=""
在浏览器无法载入图像时，替换文本属性告诉读者她们失去的信息

##body background=""
```html
<body background="/i/eg_background.jpg">
```

##align="" 对齐方式
```html
<p>图像 <img src="/i/eg_cute.gif" align="bottom"> 在文本中</p>

<p>图像 <img src ="/i/eg_cute.gif" align="middle"> 在文本中</p>

<p>图像 <img src ="/i/eg_cute.gif" align="top"> 在文本中</p>

<p>
<img src ="/i/eg_cute.gif" align ="left"> 
带有图像的一个段落。图像的 align 属性设置为 "left"。图像将浮动到文本的左侧。
</p>
```

##width="" height=""
```html
<img src="/i/eg_mouse.jpg" width="50" height="50">
```

##`<a><img></a>` 把图像作为链接
您也可以把图像作为链接来使用：
```html
<a href="/example/html/lastpage.html">
<img border="0" src="/i/eg_buttonnext.gif" />
</a>
```

#Table
```html
<table border="1">
<caption>我的标题</caption>
<!-- th 可忽略，即没有表头-->
<tr>
<th>Heading</th>
<th>Another Heading</th>
</tr>
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>row 2, cell 1</td>
<td>row 2, cell 2</td>
</tr>
</table>
```

`<th colspan="2">电话</th>` : 占据2个格子
`<th rowspan="2">电话</th>` : 占据竖排2个格子

##cellpadding="5"
单元格内容与其边框之间的空白

##bgcolor=""
背景颜色
##background=""
背景图像
##width="400"
宽度
##`<th align="left">`
向左对齐

#列表
##ul : 无序列表
```html
<ul>
  <li>咖啡</li>
  <li>茶</li>
  <li>牛奶</li>
</ul>
```

`type="circle"/disc/square` : 列表前的小点点的样式


##ol : 有序列表
```html
<ol>
<li>Coffee</li>
<li>Milk</li>
</ol>
```

`type="A"/"a"/"i"/"I"` : 列表的数字选项

##嵌套 : 注意嵌套项写法
```html
<ul>
  <li>咖啡</li>
  <!-- 注意 “茶” 的后面并不结束这一元素。表示下面的是他的子元素-->
  <li>茶
    <ul>
    <li>红茶</li>
    <li>绿茶
      <ul>
      <li>中国茶</li>
      <li>非洲茶</li>
      </ul>
    </li>
    </ul>
  </li>
  <li>牛奶</li>
</ul>
```


#一个简单的布局
css通过`div#container`定位到`<div id="container">`的元素。
这里`h1`,`h2`都是全局的。
*Tips: Sublime 输入html.elements后按`Tab`会自定产生标签。例如输入"h2"之后按`Tab`，出现`<h2></h2>`*

```html
<html>
<head>
<style type="text/css">
div#container{width:500px}
div#header {background-color:#99bbbb;}
div#menu {background-color:#ffff99; height:200px; width:100px; float:left;}
div#content {background-color:#EEEEEE; height:200px; width:400px; float:left;}
div#footer {background-color:#99bbbb; clear:both; text-align:center;}
h1 {margin-bottom:0;}
h2 {margin-bottom:0; font-size:14px;}
ul {margin:0;}
li {list-style:none;}
</style>
</head>

<body>

<div id="container">

<div id="header">
<h1>Main Title of Web Page</h1>
</div>

<div id="menu">
<h2>Menu</h2>
<ul>
<li>HTML</li>
<li>CSS</li>
<li>JavaScript</li>
</ul>
</div>

<div id="content">Content goes here</div>

<div id="footer">Copyright W3School.com.cn</div>

</div>

</body>
</html>
```

#`<form>` : 表单

##input
```html
<input type="text" name="firstname" />
<!-- name 定义同一组 -->
<input type="radio" name="sex" value="male" /> Male

<input type="checkbox" name="bike" />

<input type="submit" value="Submit" />

<input type="button" value="Hello world!">

```

##select
```html
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<!-- 默认选中 -->
<option value="fiat" selected="selected">Fiat</option>
<option value="audi">Audi</option>
</select>
```
选项分组
```html
<select>
  <optgroup label="Swedish Cars">
    <option value ="volvo">Volvo</option>
    <option value ="saab">Saab</option>
  </optgroup>

  <optgroup label="German Cars">
    <option value ="mercedes">Mercedes</option>
    <option value ="audi">Audi</option>
  </optgroup>
</select>
```

##Lable
```html
<!--请点击文本标记(点击文字部分），就可以触发相关控件（触发选中） -->
<form>
<label for="male">Male</label>
<input type="radio" name="sex" id="male" />
</form>
```

##TextArea
```html
<textarea rows="10" cols="30">
```

##Form 属性
`<form name="input" action="html_form_action.asp" method="get">` : form的属性

#Button
```html
<button type="button">Click Me!</button>
```

#框架
*不能将 <body></body> 标签与 <frameset></frameset> 标签同时使用！*
```html
<html>
<!-- rows/columns 的值规定了每行或每列占据屏幕的面积 -->
<frameset cols="25%,50%,25%">
<!-- noresize="noresize" 规定这个列的面积不允许被用户调整-->
  <frame noresize="noresize" src="/example/html/frame_a.html">
  <frame src="/example/html/frame_b.html">
  <frame src="/example/html/frame_c.html">

</frameset>
</html>
```

##Tab标签页！
```html
<html>

<frameset cols="120,*">
  <frame src="/example/html/html_contents.html">
  <frame src="/example/html/frame_a.html" name="showframe">
</frameset>

</html>
```

/example/html/html_contents.html
```html
<html>
<body>

<a href ="/example/html/frame_a.html" target ="showframe">Frame a</a><br />
<a href ="/example/html/frame_b.html" target ="showframe">Frame b</a><br />
<a href ="/example/html/frame_c.html" target ="showframe">Frame c</a>

</body>
</html>
```

`target`定义了显示的目标，`"showframe"`即`<frame src="/example/html/frame_a.html" name="showframe">` 定义的`name`属性

#head 的可选属性
```html
<title>标题不会显示在文档区,出现在标签页上</title>

<base target="_blank" />
<a href="http://www.w3school.com.cn">这个连接</a>将在新窗口中加载，即使没有 target 属性。
<base href="http://www.w3school.com.cn/images/" />
所有<a>默认指向上述的base</a>

<meta name="author" content="w3school.com.cn">

5秒后被重定向到新的地址
<meta http-equiv="Refresh" content="5;url=http://www.w3school.com.cn" />

<!-- 内联css -->
<style type="text/css">
body {background-color:yellow}
p {color:blue}
</style>
```

#Script
```html
<!-- 这段script可以被插入到任何位置，在那个位置中被执行-->
<script type="text/javascript">
document.write("Hello World!")
</script>
```

#实体

*实体名称对大小写敏感!*

<table class="dataintable">
    <tr>
      <th style="width:20%">显示结果</th>
      <th style="width:20%">描述</th>
      <th style="width:30%">实体名称</th>
      <th style="width:30%">实体编号</th>
    </tr>

    <tr>
      <td>&nbsp;</td>
      <td>空格</td>
      <td>&amp;nbsp;</td>
      <td>&amp;#160;</td>
    </tr>

    <tr>
      <td>&#60;</td>
      <td>小于号</td>
      <td>&amp;lt;</td>
      <td>&amp;#60;</td>
    </tr>

    <tr>
      <td>&gt;</td>
      <td>大于号</td>
      <td>&amp;gt;</td>
      <td>&amp;#62;</td>
    </tr>

    <tr>
      <td>&amp;</td>
      <td>和号</td>
      <td>&amp;amp;</td>
      <td>&amp;#38;</td>
    </tr>

    <tr>
      <td>&quot;</td>
      <td>引号</td>
      <td>&amp;quot;</td>
      <td>&amp;#34;</td>
    </tr>

    <tr>
      <td>'</td>
      <td>撇号&nbsp;</td>
      <td>&amp;apos; (IE不支持)</td>
      <td>&amp;#39;</td>
    </tr>

    

    <tr>
      <td>§</td>
      <td>小节</td>
      <td>&amp;sect;</td>
      <td>&amp;#167;</td>
    </tr>

    <tr>
      <td>&copy;</td>
      <td>版权</td>
      <td>&amp;copy;</td>
      <td>&amp;#169;</td>
    </tr>

    <tr>
      <td>&#174;</td>
      <td>注册商标</td>
      <td>&amp;reg;</td>
      <td>&amp;#174;</td>
    </tr>

    <tr>
      <td>&trade;</td>
      <td>商标</td>
      <td>&amp;trade;</td>
      <td>&amp;#8482;</td>
    </tr>

    <tr>
      <td>×</td>
      <td>乘号</td>
      <td>&amp;times;</td>
      <td>&amp;#215;</td>
    </tr>

    <tr>
      <td>÷</td>
      <td>除号</td>
      <td>&amp;divide;</td>
      <td>&amp;#247;</td>
    </tr>
</table>

可以使用 `<p>a&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;b</p>` 强制显示很多空格