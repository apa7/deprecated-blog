#廖雪峰 JavaScript 教程- JQuery !

- 消除浏览器差异：你不需要自己写冗长的代码来针对不同的浏览器来绑定事件，编写AJAX等代码；

- 简洁的操作DOM的方法：写$('#test')肯定比document.getElementById('test')来得简洁；

- 轻松实现动画、修改CSS等各种操作。

##版本
目前jQuery有1.x和2.x两个主要版本，区别在于2.x移除了对古老的IE 6、7、8的支持，因此2.x的代码更精简。

##JavaScript压缩
jQuery只是一个jquery-xxx.js文件，但你会看到有compressed（已压缩）和uncompressed（未压缩）两种版本，使用时完全一样，但如果你想深入研究jQuery源码，那就用uncompressed版本。

"code.jquery.com/jquery-1.11.3.min.js" 是一个经过压缩的版本。因此代码看起来是这样“

```js
$;
// (e,t){return new re.fn.init(e,t)}
window.jQuery;
// (e,t){return new re.fn.init(e,t)}
```

JavaScript压缩工具可以对函数名和参数改名，所以压缩过的jQuery源码$函数可能变成`a(b, c)`。

##jQuery 使用 CSS 选择器来选取 HTML 元素

##按 ID 查找
```
$('#test-jquery');
```
**注意，返回的永远是Array-like，`[{DOM},{...},...]`。如果没有找到，返回空Array-like `[]`**  
`$('head') instanceof Array; // false`

**选出来的元素是按照它们在HTML中出现的顺序排列的，而且不会有重复元素。例如，`<p class="red green">` 不会被上面的 `$('p.red,p.green')` 选择两次。**


##按 tag(Element) 查找
```js
$('head');
```


##$ 类型数据 和 DOM 类型数据 的转换
```js
$('#test-jquery').constructor === $; // true

// $ 转为 DOM => $.get()
$('#test-jquery').get(0).constructor; // HTMLDivElement() { [native code] }

// DOM 转为 $ => $()
$($('#test-jquery').get(0)).constructor === $; // true
```
##按 Class 查找
```js
var a = $('.red'); // 所有节点包含`class="red"`都将返回
// 符合条件的节点：
<div class="red">...</div>
<p class="green red">...</p>
```

有多个class，查找同时包含red和green的节点：
```js
var a = $('.red.green'); // 注意没有空格！
// 符合条件的节点：
<p class="green red">...</p>
```

##按 属性 查找
```js
var email = $('[name=email]'); 
// 找出<??? name="email">

// 当属性的值包含空格等特殊字符时，需要用双引号括起来。
var a = $('[items="A B"]'); // 找出<??? items="A B">
```

###前缀 或 后缀 查找
属性查找还可以使用前缀查找或者后缀查找
```js
var icons = $('[name^=icon]'); // 找出所有name属性值以icon开头的DOM
// 例如: name="icon-1", name="icon-2"
var names = $('[name$=with]'); // 找出所有name属性值以with结尾的DOM
// 例如: name="startswith", name="endswith"
```

这个方法尤其适合通过class属性查找，且不受class包含多个名称的影响：
```js
var icons = $('[class^="icon-"]'); // 找出所有DOM中包含至少一个以`icon-`开头的class的DOM
// 例如: class="icon-clock", class="abc icon-home"
```

##组合 查找
tag 和 属性：
```js
var emailInput = $('input[name=email]'); 
// 不会找出<div name="email">
```
tag 和 class：
```js
var tr = $('tr.red'); 
// 找出<tr class="red ...">...</tr>
```

##多项选择器

把多个选择器用,组合起来。输出所有选择器的结果。
```js
$('p,div'); 
// 把<p>和<div>都选出来
```

##层级选择器
对
```html
<div class="testing">
    <ul class="lang">
        <li class="lang-javascript">JavaScript</li>
        <li class="lang-python">Python</li>
        <li class="lang-lua">Lua</li>
    </ul>
</div>
```

```js
$('ul.lang li.lang-javascript'); // [<li class="lang-javascript">JavaScript</li>]
$('div.testing li.lang-javascript'); // [<li class="lang-javascript">JavaScript</li>]
```
**注意，不仅子节点可以获得，孙节点都可以。**

###多层选择
```js
$('form.test p input'); // 在form表单选择被<p>包含的<input>
```
无论中间隔了多远。
```js
$('html div.test-selector ul li')
```

##过滤器 `:`
```js
$('ul.lang li'); // 选出JavaScript、Python和Lua 3个节点

$('ul.lang li:first-child'); // 仅选出JavaScript
$('ul.lang li:last-child'); // 仅选出Lua
$('ul.lang li:nth-child(2)'); // 选出第N个元素，N从1开始
$('ul.lang li:nth-child(even)'); // 选出序号为偶数的元素
$('ul.lang li:nth-child(odd)'); // 选出序号为奇数的元素
```

###针对表单元素，jQuery还有一组特殊的选择器

- :input：可以选择`<input>，<textarea>，<select>和<button>`；

- :file：可以选择`<input type="file">`，和input[type=file]一样；

- :checkbox：可以选择复选框，和input[type=checkbox]一样；

- :radio：可以选择单选框，和input[type=radio]一样；

- :focus：可以选择当前输入焦点的元素，例如把光标放到一个`<input>`上，用$('input:focus')就可以选出；

- :checked：选择当前勾上的单选框和复选框，用这个选择器可以立刻获得用户选择的项目，如`$('input[type=radio]:checked')`；

- :enabled：可以选择可以正常输入的`<input>、<select>`
等，也就是没有灰掉的输入；

:disabled：和:enabled正好相反，选择那些不能输入的。

此外，jQuery还有很多有用的选择器，例如，选出可见的或隐藏的元素：
```js
$('div:visible'); // 所有可见的div
$('div:hidden'); // 所有隐藏的div
```
##查找 `$.find()`

拿到一个jQuery对象后，就这个对象执行查找：
```js
$('html').find('head'); // 注意返回的是$
$('html').find('head').constructor === $; // true
```

##向上查找，使用 `parent()`
```js
$('html').find('head').parent(); //返回<html>节点
// ===
$('html').find('head').parent('html');

$('html').find('head').parent().constructor === $; //true
```

##同一层级， `next()` 和 `prev()`
```js
var swift = $('#swift');

swift.next(); // Scheme
swift.next('[name=haskell]'); // Haskell，因为Haskell是后续第一个符合选择器条件的节点

swift.prev(); // Python
swift.prev('.js'); // JavaScript，因为JavaScript是往前第一个符合选择器条件的节点
```

##`$.filter()` 过滤器
```js
var langs = $('ul.lang li'); // 拿到JavaScript, Python, Swift, Scheme和Haskell
var a = langs.filter('.dy'); // 拿到JavaScript, Python, Scheme
```
`filter(一个函数)`:

```
var langs = $('ul.lang li'); // 拿到JavaScript, Python, Swift, Scheme和Haskell
langs.filter(function () {
    return this.innerHTML.indexOf('S') === 0; // 返回S开头的节点
}); // 拿到Swift, Scheme

函数内部的this被绑定为DOM对象，不是jQuery对象.
```js
var lan = $('head'); // [{DOM}]
lan.filter(function() {
    console.log(this); // {DOM}
});
```

###表单选择范例
```html
<form id="test-form" action="#0" onsubmit="return false;">
    <p><label>Name: <input name="name"></label></p>
    <p><label>Email: <input name="email"></label></p>
    <p><label>Password: <input name="password" type="password"></label></p>
    <p>Gender: <label><input name="gender" type="radio" value="m" checked> Male</label> <label><input name="gender" type="radio" value="f"> Female</label></p>
    <p><label>City: <select name="city">
        <option value="BJ" selected>Beijing</option>
        <option value="SH">Shanghai</option>
        <option value="CD">Chengdu</option>
        <option value="XM">Xiamen</option>
    </select></label></p>
    <p><button type="submit">Submit</button></p>
</form>
```
用jQuery获取表单的JSON字符串，key和value分别对应每个输入的name和相应的value：

```js
$('#test-form :input[type!=submit]').map(function(){
  if(this.type !== "radio" || this.checked){
     json[this.name] = this.value;
  }
});
```

##使用 JQuery 操作 DOM
对于
```html
<ul id="test-ul">
    <li class="js">JavaScript</li>
    <li name="book">Java &amp; JavaScript</li>
</ul>
```

无参数调用`text()`/`html()`是获取文本，传入参数就变成设置文本.
```js
$('#test-ul li[name=book]').text(); // 'Java & JavaScript'

// 设置HTML，添加span的color
j1.html('<span style="color: red">JavaScript</span>');
// 设置Text也OK
j2.text('JavaScript & ECMAScript');
```

一个jQuery对象可以包含0个或任意个DOM对象，它的方法实际上会作用在对应的每个DOM节点上。
```js
$('#test-ul li').text('JS'); // 两个节点都变成了JS
```

对于没找到的对象，也不报错
```js
$('#not-exist').text('Hello'); // 代码不报错，没有节点被设置为'Hello'
```

###链式传递
jQuery对象的所有方法都返回一个jQuery对象（可能是新的也可能是自身），这样我们可以进行链式调用。
```js
$('#test-css li.dy>span').css('background-color', '#ffd351').css('color', 'red');
```

###CSS
为了和JavaScript保持一致，CSS属性可以用'background-color'和'backgroundColor'两种格式。

除了直接修改`<span>`, `<div>`的 style 信息，还可以通过预定义class.css，执行时动态为元素添加class。

```html
<style>
.highlight {
    color: #dd1144;
    background-color: #ffd351;
}
</style>
```

```js
div.addClass('highlight'); // 添加highlight这个class

div.hasClass('highlight'); // class是否包含highlight

div.removeClass('highlight'); // 删除highlight这个class
```

###显示和隐藏DOM
>要隐藏一个DOM，我们可以设置CSS的display属性为none，利用css()方法就可以实现。不过，要显示这个DOM就需要恢复原有的display属性，这就得先记下来原有的display属性到底是block还是inline还是别的值。

jQuery直接提供show()和hide()方法，我们不用关心它是如何修改display属性的，总之它能正常工作

```js
var a = $('a[target=_blank]');
a.hide(); // 隐藏
a.show(); // 显示
```

###获取DOM信息
```js
// 浏览器可视窗口大小:
// 注意这里是传参！直接传window，而不是获取的tag
$(window).width(); // 800
$(window).height(); // 600

//不用$的写法
window.innerWidth；

// -------
// HTML文档大小:
$(document).width(); // 800
$(document).height(); // 3500

$(document).width(600); // 试图更改但是失败了

// -------
// 某个div的大小:
var div = $('#test-div');
div.width(); // 600
div.height(); // 300
div.width(400); // 设置CSS属性 width: 400px，是否生效要看CSS是否有效
div.height('200px'); // 设置CSS属性 height: 200px，是否生效要看CSS是否有效
```

###DOM 属性
####`attr()`
和removeAttr()`

```js
// <div id="test-div" name="Test" start="1">...</div>
var div = $('#test-div');
div.attr('data'); // undefined, 属性不存在
div.attr('name'); // 'Test'
div.attr('name', 'Hello'); // div的name属性变为'Hello'
div.removeAttr('name'); // 删除name属性
div.attr('name'); // undefined
```

####`prop()`

HTML5规定有一种属性在DOM节点中可以没有值，只有出现与不出现两种，
```
<input id="test-radio" type="radio" name="test" checked value="1">

// === 等价于

<input id="test-radio" type="radio" name="test" checked="checked" value="1">
```

attr()和prop()对于属性checked 还有 selected 的处理有所不同.
```js
var radio = $('#test-radio');
radio.attr('checked'); // 'checked'
radio.prop('checked'); // true

radio.is(':checked'); // true
```
####`is()`
>is() 根据选择器、元素或 jQuery 对象来检测匹配元素集合，如果这些元素中至少有一个元素匹配给定的参数，则返回 true。

我的理解是 a.is('b'): a集合和$'b'集合有不为空的交集。

###JQuery 和表单
jQuery对象统一提供`val()` 方法获取和设置对应的value属性

```js
var input = $('#test-input');

input.val(); // 'test'
input.val('abc@example.com'); // 文本框的内容已变为abc@example.com
```

###添加节点 `$.append()`

```html
<div id="test-div">
    <ul>
        <li><span>JavaScript</span></li>
        <li><span>Python</span></li>
        <li><span>Swift</span></li>
    </ul>
</div>
```

```js
// #id>ul === #id ul 
var ul = $('#test-div>ul');
ul.append('<li><span>Haskell</span></li>'); // append(html)


var ps = document.createElement('li');
ps.innerHTML = '<span>Pascal</span>'; 
ul.append(ps); // append(DOM Object)

ul.append($('#scheme')); // append($)

ul.append(function (index, html) {
    return '<li><span>Language - ' + index + '</span></li>'; //返回一个字符串、DOM对象或者jQuery对象。
}); //append(function)
```

>如果要添加的DOM节点已经存在于HTML文档中，它会首先从文档移除，然后再添加，也就是说，用append()，你可以移动一个DOM节点。

```js
$('#test-div ul').append($('#test-div ul li:first-child'))
[<ul>​…​</ul>​] // 像这样，就可以把第一个元素放到最后了
```

###其他相似函数
－ `prepend()` : DOM添加为子元素，放在到最前

－ `after()` : DOM放在同级，在此元素之后

－ `before()` : DOM放在同级，在此元素之前

###删除节点

>jQuery对象包含若干DOM节点，可以一次删除多个DOM节点

```js
var li = $('#test-div>ul>li');
li.remove(); // 所有<li>全被删除
```

##事件
```html
<a id="test-link" href="#0">点我试试</a>
```

```js
// a.on('click', function () { 也可以
a.click(function () { 
    alert('Hello!');
});
```

###重要的 ready 事件
**ready事件在DOM完成初始化后触发，且只触发一次，所以非常适合用来写其他的初始化代码。**

####事件绑定失效情况
可能失效的代码：
```html
<html>
<head>
    <script>
        // 代码有误:
        $('#testForm).on('submit', function () {
            alert('submit!');
        });
    </script>
</head>
<body>
    <form id="testForm">
        ...
    </form>
</body>
```
因为JavaScript在此执行的时候，<form>尚未载入浏览器，所以$('#testForm)返回[]，并没有绑定事件到任何DOM上。

####解决方式
**初始化代码必须放到document对象的ready事件中，保证DOM已完成初始化**
```html
<html>
<head>
    <script>
        $(document).on('ready', function () {
            $('#testForm).on('submit', function () {
                alert('submit!');
            });
        });
    </script>
</head>
<body>
    <form id="testForm">
        ...
    </form>
</body>
```

代码会在DOM树初始化后再执行

ready 事件绑定的简写：
```js
// 这3种方式的效果都一样
$(document).on('ready', function () { 
}
$(document).ready(function () {
}
$(function () { //!
}
```

####ready 事件绑定执行顺序
完全可以反复绑定事件处理函数，它们会依次执行
```js
$(function () {
    console.log('首先执行');
});
$(function () {
    console.log('再执行');
});
$(function () {
    console.log('最后执行');
});
```

###事件参数: `e`

可以从Event对象 `e` 上获取到更多的信息
```js
$(function () {
    $('#testMouseMoveDiv').mousemove(function (e) {
        $('#testMouseMoveSpan').text('pageX = ' + e.pageX + ', pageY = ' + e.pageY);
    });
});
```

###取消绑定 `off()`
```js
function hello() {
    alert('hello!');
}

a.click(hello); // 绑定事件

// 10秒钟后解除绑定:
setTimeout(function () {
    a.off('click', hello); //第二个参数需要是之前函数的指针
}, 10000);
```

####减少参数
```js
$.off('click');
```

一次性移除已绑定的click事件的所有处理函数.
```js
$.off();
```

一次性移除已绑定的所有类型的事件处理函数。


###代码触发事件
事件的触发总是由用户操作引发的。例如，我们监控文本框的内容改动
```js
input.change(function () {
    console.log('changed...');
});
```

当用户在文本框中输入时，就会触发change事件。但是，如果用JavaScript代码, `input.val('change it!'); ` 去改动文本框的值，**将不会触发change事件**.

####代码执行触发
希望用代码触发change事件，可以直接调用无参数的 `change()` 方法来触发该事件
```js
input.change(); // 触发change事件

input.trigger('change'); // 一样
```

###浏览器安全限制
```js
window.open('/');


```

直接执行 `window.open()` 会被浏览器拦截.

在click事件处理函数内执行，这是浏览器允许的.
```js
$('body').click(function(){
    window.open('/');
});
```

但是下面这个不行。因为执行者不再是`click()`函数。
```js
button2.click(function () {
    // 不立刻执行popupTestWindow()，100毫秒后执行:
    setTimeout(popupTestWindow, 100);
});
```


###参考：所有能处理的事件
####鼠标事件

- click: 鼠标单击时触发；

- dblclick：鼠标双击时触发；

- mouseenter：鼠标进入时触发；

- mouseleave：鼠标移出时触发；

- mousemove：鼠标在DOM内部移动时触发；

- hover：鼠标进入和退出时触发两个函数，相当于mouseenter加上mouseleave。


####键盘事件

键盘事件仅作用在当前焦点的DOM上，通常是`<input>`和`<textarea>`。

- keydown：键盘按下时触发；

- keyup：键盘松开时触发；

- keypress：按一次键后触发。

####其他事件

- focus：当DOM获得焦点时触发；

- blur：当DOM失去焦点时触发；

- change：当`<input>、<select>或<textarea>`的内容改变时触发；

- submit：当`<form>`提交时触发；

- ready：当页面被载入并且DOM树完成初始化后触发。


###案例：多选框的全选逻辑
```html
<form id="test-form" action="test">
    <legend>请选择想要学习的编程语言：</legend>
    <fieldset>
        <p><label class="selectAll"><input type="checkbox"> <span class="selectAll">全选</span><span class="deselectAll">全不选</span></label> <a href="#0" class="invertSelect">反选</a></p>
        <p><label><input type="checkbox" name="lang" value="javascript"> JavaScript</label></p>
        <p><label><input type="checkbox" name="lang" value="python"> Python</label></p>
        <p><label><input type="checkbox" name="lang" value="ruby"> Ruby</label></p>
        <p><label><input type="checkbox" name="lang" value="haskell"> Haskell</label></p>
        <p><label><input type="checkbox" name="lang" value="scheme"> Scheme</label></p>
        <p><button type="submit">Submit</button></p>
    </fieldset>
</form>
```
看起来是这样的

<fieldset>
        <p><label class="selectAll"><input type="checkbox"> <span class="selectAll">全选</span><span class="deselectAll">全不选</span></label> <a href="#0" class="invertSelect">反选</a></p>
        <p><label><input type="checkbox" name="lang" value="javascript"> JavaScript</label></p>
        <p><label><input type="checkbox" name="lang" value="python"> Python</label></p>
        <p><label><input type="checkbox" name="lang" value="ruby"> Ruby</label></p>
        <p><label><input type="checkbox" name="lang" value="haskell"> Haskell</label></p>
        <p><label><input type="checkbox" name="lang" value="scheme"> Scheme</label></p>
        <p><button type="submit">Submit</button></p>
</fieldset>
    
>实现以下逻辑：

>当用户勾上“全选”时，自动选中所有语言，并把“全选”变成“全不选”；
>
>当用户去掉“全不选”时，自动不选中所有语言；
>
>当用户点击“反选”时，自动把所有语言状态反转（选中的变为未选，未选的变为>选中）；
>
>当用户把所有语言都手动勾上时，“全选”被自动勾上，并变为“全不选”；
>
>当用户手动去掉选中至少一种语言时，“全不选”自动被去掉选中，并变为“全选”。

####我的垃圾未完成答案

```js
// $.each(function(index, dom){}); each API
// selectAll.get(0).checked = false // 不能直接 $.checked，需要 DOM.checked

function allSet(tof){
 langs.each(function(a,h){
     h.checked = tof;
    });
};

function allSelAndChange(){
    allSet(true);
    selectAllLabel.hide();
    deselectAllLabel.show();
    selectAll.click(allDeSelAndChange);
}

function allDeSelAndChange(){
    allSet(false);
    selectAllLabel.show();
    deselectAllLabel.hide();
    selectAll.click(allSelAndChange);
}

function init(){
    selectAll.click(allSelAndChange);
}

function reverse(){
    langs.each(function(a,h){
        h.checked = !h.checked ;
    });
};

function checkSel(){
    var notSet = true;
    var selected = true;
    var allTheSame = true;
    langs.each( function(a,h) {
        if(notSet){
            selected = h.checked;
            notSet = false;
        }
        if(h.checked !== selected){
            allTheSame = false;
            // continue;
        }
    });
    if(allTheSame){
        selectAll.get(0).checked = selectAllLabel.hide();
        if(selected){
            selectAllLabel.hide();
            deselectAllLabel.show();
            selectAll.click(allDeSelAndChange);
        }else{
            selectAllLabel.show();
            deselectAllLabel.hind();
            selectAll.click(allSelAndChange);
        }
    }else{
     // 不想写了。   
    }
        
}
```

####极其漂亮的实现

```js
// @author: lmtooT_T@http://www.liaoxuefeng.com/
selectAll.click(function(){
     langs.prop('checked',this.checked);
     selectAllLabel.toggle(!this.checked); // toggle(show?)
     deselectAllLabel.toggle(this.checked);
});
invertSelect.click(()=>langs.click());
langs.click(function(){
     var isAllChecked=langs.map(function(){return this.checked;}).get().reduce((x,y)=>x&&y);
     if(isAllChecked||selectAll.is(":checked")){
         selectAll.prop('checked',isAllChecked);
         selectAllLabel.toggle(!isAllChecked);
         deselectAllLabel.toggle(isAllChecked);
     }
});
```

##$ 动画

其实HTML5, CSS3都有动画方式。不知道哪个更合适。

```js
// 左上角逐渐展开或收缩
div.hide(3000); // 在3秒钟内逐渐消失        
div.show('slow'); // 在0.6秒钟内逐渐显示
div.toggle(3000); // show? hide:show;

// 垂直方向逐渐展开或收缩
div.slideUp(3000); // 在3秒钟内逐渐向上消失

// slideDown, slideToggle

// 淡入淡出
div.fadeOut('slow'); // 在0.6秒内淡出

// fadeIn(), fadeToggle

// 自定义动画
div.animate({
    opacity: 0.25,
    width: '256px',
    height: '256px'
}, 3000, function () { // 动画结束时，该函数将被调用
    
    console.log('动画已结束');
    // 恢复至初始状态:
    $(this).css('opacity', '1.0').css('width', '128px').css('height', '128px');
});
// 实际上这个回调函数参数对于基本动画也是适用的
```

###串行动画
```js
div.slideDown(2000)
   .delay(1000)
   .animate({
       width: '256px',
       height: '256px'
   }, 2000)
   .delay(1000)
   .animate({
       width: '128px',
       height: '128px'
   }, 2000);
```

###动画作用对象

>有的动画如slideUp()根本没有效果。这是因为jQuery动画的原理是逐渐改变CSS的值，如height从100px逐渐变为0。

非块级元素，对它们设置height根本就不起作用，所以动画也就没有效果。

>此外，jQuery也没有实现对background-color的动画效果，用animate()设置background-color也没有效果。这种情况下可以使用CSS3的transition实现动画效果。

###注意，隐藏不等于删除！
上述所有函数，执行效果类似`show()` 和 `hide()`。其实元素都还存在。如果需要彻底删除。需要调用`remove()`

```js
tr.fadeOut('slow', function(){$(this).remove();})
```
>因为动画执行需要一段过程，如果后面紧跟着remove，那么它立马就直接执行了，就看不到渐变过程了。所以需要等动画过程完成后再调用删除命令。 

## `$.ajax`
`ajax(url, settings)`

```js
var jqxhr = $.ajax('/api/categories', {
    dataType: 'json'
}).done(function (data) {
    ajaxLog('成功, 收到的数据: ' + JSON.stringify(data));
}).fail(function (xhr, status) {
    ajaxLog('失败: ' + xhr.status + ', 原因: ' + status);
}).always(function () {
    ajaxLog('请求完成: 无论成功或失败都会调用');
});
```

###常用 settings


- method：发送的Method，缺省为'GET'，可指定为'POST'、'PUT'等；

- contentType：发送POST请求的格式，默认值为'application/x-www-form-urlencoded; charset=UTF-8'，也可以指定为text/plain、application/json；

- data：发送的数据，可以是字符串、数组或object。如果是GET请求，data将被转换成query附加到URL上，如果是POST请求，根据contentType把data序列化成合适的格式；

- headers：发送的额外的HTTP头，必须是一个object；

- dataType：接收的数据格式，可以指定为'html'、'xml'、'json'、'text'等，缺省情况下根据响应的Content-Type猜测。

###`$.get()`
```js
var jqxhr = $.get('/path/to/resource', {
    name: 'Bob Lee',
    check: 1
});
```

jQuery自动把第二个参数变成query string然后加到URL后面, 实际请求url: `/path/to/resource?name=Bob%20Lee&check=1`

###`$.post()`
```js
var jqxhr = $.post('/path/to/resource', {
    name: 'Bob Lee',
    check: 1
});
```

实际构造的数据name=Bob%20Lee&check=1作为POST的body被发送

###`$.getJSON(url)` === `$.get(url, {dataType: 'json'})`

```js
var jqxhr = $.get('/api/categories', {
    dataType: 'json'
});
// ===
var jqxhr = $.getJSON('/api/categories');
```

##`$.myFunction()` 自定义方法

###使用场景
```js
$('span.hl').css('backgroundColor', '#fffceb').css('color', '#d85030');

$('p a.hl').css('backgroundColor', '#fffceb').css('color', '#d85030'); // 一样的css操作
```

统一为
```js
$('span.hl').highlight();

$('p a.hl').highlight();
```

###编写
```js
$.fn.highlight = function () {
    // this已绑定为当前jQuery对象:
    this.css('backgroundColor', '#fffceb').css('color', '#d85030');
    return this; // jQuery对象支持链式操作，让扩展方法也要能继续链式下去
}
```
###[编写jQuery插件的原则](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014356468967974219593d94f64d06b370c87fc38eade4000)


###案例：为所有外链加跳转提示
```js
$.fn.external = function () {
    // return返回的each()返回的$，支持链式调用
    return this.filter('a').each(function () {
        // 注意: each()内部的回调函数的this绑定为DOM本身!
        // 因此需要$()一下得到它的$对象。
        var a = $(this);
        // 保存原url
        var url = a.attr('href');
        // 确保是外链
        if (url && (url.indexOf('http://')===0 || url.indexOf('https://')===0)) {
            // 设定链接为#0,即跳转到id="0"的地方，既然没有就不跳了
            a.attr('href', '#0')
            // 把target属性删除，因为target="_blank"会新开一个浏览器空白窗口
             .removeAttr('target')
             .append(' <i class="uk-icon-external-link"></i>')
             .click(function () {
                if(confirm('你确定要前往' + url + '？')) {
                    window.open(url);
                }
            });
        }
    });
}
```
