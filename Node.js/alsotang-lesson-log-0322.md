# Node.js 包教不包会-1-安装, Hello World, HTML请求 
2016/3/22
[《Node.js 包教不包会》](https://github.com/alsotang/node-lessons)

---

1. 在一个没有nvm的Ubuntu 14.04 虚拟机开始一切
2. 查看下最新的版本 `https://github.com/creationix/nvm`
然后安装最新的nvm
`curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash`
2. `nvm install node` //安装最新版的node，现在是5.9
4. `node` 进入node terminal
5. `nvm ls` 查看所有的node 版本
6. 安装 express 通过淘宝的镜像
`npm install express —registry=https://registry.npm.taobao.org`
7. 查看下载的node\_modules
`ls node_modules`，使用`npm list`可以查看到树状整理的包依赖
8. `touch app.js` 新建一个文件！
9. hello world:

		// 这句的意思就是引入 `express` 模块，并将它赋予 `express` 这个变量等待使用。
		var express = require('express');
		// 调用 express 实例，它是一个函数，不带参数调用时，会返回一个 express 实例，将这个变量赋予 app 变量。
		var app = express();
		
		// app 本身有很多方法，其中包括最常用的 get、post、put/patch、delete，在这里我们调用其中的 get 方法，为我们的 `/` 路径指定一个 handler 函数。
		// 这个 handler 函数会接收 req 和 res 两个对象，他们分别是请求的 request 和 response。
		
		// request 中包含了浏览器传来的各种信息，比如 query 啊，body 啊，headers 啊之类的，都可以通过 req 对象访问到。
		// res 对象，我们一般不从里面取信息，而是通过它来定制我们向浏览器输出的信息，比如 header 信息，比如想要向浏览器输出的内容。这里我们调用了它的 #send 方法，向浏览器输出一个字符串。
		
		app.get('/', function (req, res) {
		  res.send('Hello World');
		});
		
		// 定义好我们 app 的行为之后，让它监听本地的 3000 端口。这里的第二个函数是个回调函数，会在 listen 动作成功后执行，我们这里执行了一个命令行输出操作，告诉我们监听动作已完成。
		app.listen(3000, function () {
		  console.log('app is listening at port 3000');
		});

10. 执行 `node app.js`
11. lesson2 先去复习HTML协议 《自顶向下》
	1. 存在持续TCP链接和非持续TCP链接两种HTTP协议，非持续是每一次请求都建立一个新的tcp链接。
	2. 一个HTML请求报文

			GET /SOMEDIR/CONTENT.HTML HTTP/1.1 /*请求行*/
			Host: www.sample.com /*首部行*/
			Connection: close /*首部行*/
			User-agent: Mozilla/5.0 /*首部行*/
			Accept-languege: fr /*首部行*/

		`GET`是方法，还可以有 `POST`,`HEAD`(不返回主体，只返回首部行）,`PUT`（上传对象）,`DELETE`（删除对象）。绝大部份采用`GET`.
		`Connection`告诉浏览器是否是持续性链接。`close` ＝ 不是。

	4. 使用`GET`时主体为空。`POST`才会使用主体。
	3. 而一个完整的HTML报文在请求行和若干首部行之后还有一个空行和实体主体。
	5. `GET`报文中可以出现的参数形如: `/test/demo_form.asp?name1=value1&name2=value2`
	6. HTML响应报文：
	

			HTTP/1.1 200 OK /*状态行*/
			Date: Sat, 26 Mar 2016 09:57:23 GMT /*首部行*/
			Server: Apache /*首部行*/
			Last-Modified: Tue, 12 Jan 2010 13:48:00 GMT /*首部行*/
			ETag: "51-47cf7e6ee8400" /*首部行*/
			Accept-Ranges: bytes /*首部行*/
			Content-Length: 81 /*首部行*/
			Cache-Control: max-age=86400 /*首部行*/
			Expires: Sun, 27 Mar 2016 09:57:23 GMT /*首部行*/
			Connection: Keep-Alive /*首部行*/
			Content-Type: text/html /*首部行*/
			
			<html> /*实体*/
			...
			</html>
			
	7. 状态码：
		`200`: OK, `301`: Moved Permanently, `400`: Bad Request, `404`: Not Found
	8. 获取一个报文的方法：`telnet baidu.com 80`(telnet ip/host port)
		等待响应后：

			GET / HTTP/1.1
			Host: baidu.com
		
		(GET 根目录，以上这个命令就是上面那个报文的来源。指向要报文行不要实体的话，使用HEAD)


12. 使用`npm install express utility --save` `--save`参数可以将包依赖添加到`package.json`中的`dependencies`字段

13. 使用代码：

		// 引入依赖
		var express = require('express');
		var utility = require('utility');

		// 建立 express 实例
		var app = express();

		app.get('/', function (req, res) {
		  // 从 req.query 中取出我们的 q 参数。
		  // 如果是 post 传来的 body 数据，则是在 req.body 里面，不过 express 默认不处理 body 中的信息，需要引入 https://github.com/expressjs/body-parser 这个中间件才会处理，这个后面会讲到。
		  // 如果分不清什么是 query，什么是 body 的话，那就需要补一下 http 的知识了
		  var q = req.query.q;

		  // 调用 utility.md5 方法，得到 md5 之后的值
		  // 之所以使用 utility 这个库来生成 md5 值，其实只是习惯问题。每个人都有自己习惯的技术堆栈，
		  // 我刚入职阿里的时候跟着苏千和朴灵混，所以也混到了不少他们的技术堆栈，仅此而已。
		  // utility 的 github 地址：https://github.com/node-modules/utility
		  // 里面定义了很多常用且比较杂的辅助方法，可以去看看
		  var md5Value = utility.md5(q);

		  res.send(md5Value);
		});

		app.listen(3000, function (req, res) {
		  console.log('app is running at port 3000');
		});

14. 访问 `http://localhost:3000/?q=alsotang`
