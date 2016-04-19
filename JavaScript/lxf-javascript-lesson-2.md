#廖雪峰 JavaScript 教程-AJAX, 跨域访问, CORS, Promise

##AJAX

Asynchronous JavaScript and XML

JS本来就喜欢异步调用。

```js
var request = new XMLHttpRequest();
//设定请求完成后要回调的函数
request.onreadystatechange = function() {
    if(request.readystate === 4) { //=4 : 成功完成
        if(request.status === 200) { //response 响应码
            return request.responseText; //返回相应的文本
        }else {
            return null;
        }
    } else { //完成了成功响应的情况
        //处理失败的情况
}
}
//指定请求url
request.open('GET', '/api/123');
//执行请求
request.send();
```
###对于IE
```js
var request;
if (window.XMLHttpRequest) {
request = new XMLHttpRequest();
} else { //IE不支持XMLHttpRequest的情况下
    request = new ActiveXObject('Microsoft.XMLHTTP');
}
```

**不要根据浏览器的navigator.userAgent来检测浏览器是否支持某个JavaScript特性，一是因为这个字符串本身可以伪造，二是通过IE版本判断JavaScript特性将非常复杂。**

###XMLHttpRequest

`XMLHttpRequest` 对象的 `open()` 方法有3个参数，第一个参数指定是GET还是POST，第二个参数指定URL地址，第三个参数指定是否使用异步，默认是true，所以不用写。当然异步，不然就假死了。

GET请求不需要参数，POST请求需要把body部分以字符串或者FormData对象传进去。

##跨域访问

###浏览器的安全限制
浏览器的同源策略导致默认情况下，JavaScript在发送AJAX请求时，URL的域名必须和当前页面完全一致。

包括：域名要相同（www.example.com和example.com不同），协议要相同（http和https不同），端口号要相同。即五元组相同。

###使用代理服务器跨域
通过在同源域名下架设一个代理服务器来转发，JavaScript负责把请求发送到代理服务器：

```
'/proxy?url=http://www.sina.com.cn'
```

代理服务器再把结果返回，这样就遵守了浏览器的同源策略。这种方式麻烦之处在于需要服务器端额外做开发。

###JSONP 处理GET请求跨域
利用了浏览器允许跨域引用JavaScript资源：
```html
<html>
<head>
    <script src="http://other.com/abc.js"></script>
    ...
</head>
```

JSONP通常以函数调用的形式返回，例如，返回JavaScript内容如下：
```js
callback('data');
```
####实例: 163的股票查询URL
对URL：`http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice`, 指定callback函数为refreshPrice
你将得到如下返回：`refreshPrice({"0000001":{"code": "0000001", ... })` 

因此我们需要首先在页面中准备好回调函数：
```js
function refreshPrice(data) {
    var p = document.getElementById('test-jsonp');
    p.innerHTML = '当前价格：' +
        data['0000001'].name +': ' + 
        data['0000001'].price + '；' +
        data['1399001'].name + ': ' +
        data['1399001'].price;
}
```

用getPrice()函数触发：
```js
function getPrice() {
    var js = document.createElement('script'),
        head = document.getElementsByTagName('head')[0];
    js.src = 'http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice';
    head.appendChild(js);
}
```


###使用 CORS 跨域

Cross-Origin Resource Sharing，是HTML5规范定义的如何跨域访问资源。
![cors-example.png](img/cors-example.png)

当本地浏览器使用了来自my.com的js中的跨域请求 `GET /res/abc.data Host: sina.com` 当sina.com传回的应头Access-Control-Allow-Origin为 http://my.com, 或者是*，本次请求就可以成功。  

可见，跨域能否成功，取决于被请求服务器的设置，是否返回申请者所需的的Access-Control-Allow-Origin。

- CORS 支持GET、HEAD和POST（POST的Content-Type类型
仅限application/x-www-form-urlencoded、multipart/form-data和text/plain）

####CORS 的使用场景
通过 HTML5 引用外域资源时，除了JavaScript和CSS外，都要验证CORS。
例如，当你引用了某个第三方CDN上的字体文件时：
```css
@font-face {
  font-family: 'FontAwesome';
  src: url('http://cdn.com/fonts/fontawesome.ttf') format('truetype');
}
```

如果该CDN服务商未正确设置Access-Control-Allow-Origin，那么浏览器无法加载字体资源。

####使用 CORS 处理其他请求
对于PUT、DELETE以及其他类型如application/json的POST请求，在发送AJAX请求之前，浏览器会先发送一个OPTIONS请求（称为preflighted请求）到这个URL上，询问目标服务器是否接受：(本例在询问是否支持 `POST` )
```
OPTIONS /path/to/resource HTTP/1.1
Host: bar.com
Origin: http://my.com
Access-Control-Request-Method: POST
```

服务器必须响应并明确指出允许的Method：
```
HTTP/1.1 200 OK
Access-Control-Allow-Origin: http://my.com
Access-Control-Allow-Methods: POST, GET, PUT, OPTIONS
Access-Control-Max-Age: 86400
```

浏览器确认服务器响应的`Access-Control-Allow-Methods`头确实包含将要发送的AJAX请求的Method (包含 `POST` )  ，才会继续发送AJAX，否则，抛出一个错误。

##Promise

类似Async的一个异步机制。是ES6的原生机制。

```js
// 模拟需要等待异步等待结果的函数

// 0.5秒后返回input*input的计算结果:
function multiply(input) {
    // 此处使用了一个 closeure 闭包
    //resolve, reject 分别在成功/失败的时候调用
    return new Promise(function (resolve, reject) {
        // 随便规定一个错误
        if(input * input > 1000000) {
            reject('too big');
        }
        log('calculating ' + input + ' x ' + input + '...');
        // setTimeout 从第三个参数起都会作为第一个参数的参数传入，即resolve(input*input)
        setTimeout(resolve, 500, input * input);
    });
}

// 0.5秒后返回input+input的计算结果:
function add(input) {
    return new Promise(function (resolve, reject) {
        log('calculating ' + input + ' + ' + input + '...');
        setTimeout(resolve, 500, input + input);
    });
}

// 执行链：func1(resolve, reject)- 调用resolve(123)- promise将resolve获得参数向下传递 -func2(123)- 返回123*123 - func3(123*123) -...
// 如果没问题，大家都执行的是 resolve 的话，一路执行到 func6 即输出log，结束。
// 如果出问题，即有人执行了 reject，那么直接跳到catch，执行func7
var p = new Promise(function (resolve, reject) { //func 1
    log('start new Promise...');
    resolve(123);
}).then(multiply) //func 2
 .then(add) //func 3
 .then(multiply) //func 4
 .then(add) //func 5
 .then(function (result) { //func 6
    log('Got value: ' + result);
}).catch(function (err) { //func 7
    log('fault: '+err);
});
```

###使用 Promise 执行 AJAX

```js
// 建立一个包装ajax的方法:
// ajax函数将返回Promise对象。
function ajax(method, url, data) {
    var request = new XMLHttpRequest();
    return new Promise(function (resolve, reject) {
        request.onreadystatechange = function () {
            if (request.readyState === 4) {
                if (request.status === 200) {
                    resolve(request.responseText);
                } else {
                    reject(request.status);
                }
            }
        };
        request.open(method, url);
        request.send(data);
    });
}

// 使用
var p = ajax('GET', '/api/categories').then(function (text) { // 如果AJAX成功，获得响应内容
    log.innerText = text;
}).catch(function (status) { // 如果AJAX失败，获得响应代码
    log.innerText = 'ERROR: ' + status;
});

```

感觉没有什么意义啊。我没用 Promise 实现了一种版本的ajax包装：

```js
function ajax (thenF, catchF, method, url, data){
    var request = new XMLHttpRequest();
request.onreadystatechange = function () {
console.log(request.readyState);

        if(request.readyState === 4) { 
            if(request.status === 200) {
            return thenF(request.responseText);
        } else {
            // 失败，根据响应码判断失败原因:
            return catchF(request.status);
        }
    } else {
        // 千万不要在这里执行任何处理，否则会直接跳出，不再循环接受 readyState 的变化
    }
}
// 发送请求:
request.open(method,url);
request.send(data);
}

ajax(function (text) { // 如果AJAX成功，获得响应内容
    console.log(text);
}, function (text) { // 如果AJAX成功，获得响应内容
    console.log(text);
},'GET','/api/categories');
```

###Promise 并行执行任务
Promise 提供2种并行机制。

- `Promise.all()`
- `Promise.race()`

```js
var p1 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 500, 'P1');
});
var p2 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 600, 'P2');
});
// 同时执行p1和p2，并在它们都完成后执行then:
Promise.all([p1, p2]).then(function (results) {
    // 无论谁先完成，输出的Array永远按 all() 里定义的顺序
    // 即all([p1, p2]) 总是会输出 ['P1', 'P2']
    console.log(results); // 获得一个Array: ['P1', 'P2']
});
// 同时执行p1和p2，只需要获得先返回的结果
// 如果p1执行较快，Promise的then()将获得结果'P1'。p2仍在继续执行，但执行结果将被丢弃。
Promise.race([p1, p2]).then(function (result) {
    console.log(result); // 'P1'
});
```

---
2016/4/19 22:49