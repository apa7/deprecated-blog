#Angular.js&Socket.io&BootStrap 初步
2016/4/4

---

`npm install -g bower`

我们使用bower来管理TechNode使用到的前端类库，与npm类似，bower使用名为bower.json的文件来管理项目的依赖。在TechNode目录下运行bower init，生成bower.json文件。

bower默认将依赖的模块安装在bower_compoments下，为了便于管理，新建.bowerrc文件，添加如下内容，为bower指定依赖的安装目录：

{
  "directory" : "static/components"
}
接下来，试用bower安装我们需要的一些前端类库：

Bootstrap：快速构建web项目的前端UI库，依赖jQuery，bower在安装Bootstrap的同时，也会安装jQuery；
Angular.js：我们的主角，前端MVC框架。
bower install bootstrap angular --save
--save参数使得bower将依赖写入到bower.json中。


/socket.io/socket.io.js 是个什么鬼。。明明文件里没有这个