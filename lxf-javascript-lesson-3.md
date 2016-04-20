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

- :checked：选择当前勾上的单选框和复选框，用这个选择器可以立刻获得用户选择的项目，如$('input[type=radio]:checked')；

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

