#Joker 工作日志

---
#Joker Start! 2016/4/5
---
#TODO:
1. favicon


---
#Log
1. 建立最基本框架，使用ejs
2. 不使用`bin/www`，直接采用`app.js`和`routes/index`。和 nodeblog 的做法一致
3. 使用mongodb, [redis](https://github.com/nswbmw/N-drifter/wiki/第1章-初识-Redis)可能用于需要快速CURD(Create, Update, Read, Delete)的操作时候才需要。如聊天室，BBS，微博。
4. 使用BootStrap
5. 使用git做版本控制
6. 

---
#IDEA
1. 其实没必要做视频分发，一开始放百度云上就得了。或者yy语音。有钱了再说。

---

#joker 0406
##使用 Async 
##不使用 Mongoose

###modules/user.js的疑问：
~~这个User里面其实什么都没有也没事：~~
```
function User(user){
       // this.name = user.name;
       // this.password = user.password;
       // this.email = user.email;

};
```

~~压根就不用 User 里面的属性。都是直接调用`user.save()` `User.find()` 里面的user。~~
不，还是有用的，下面的user就是读取这个属性。写两遍多麻烦。

##TODO
1. 明文传输密码的解决！应该直接传md5.明文都不走https
2. re_password应该在本地解决, 还有是不是邮箱:angular
~~3. 邮箱也应该独一份~~ check
~~4. 使用邮箱登录~~ check
5. 检查注册是否重复应该用: angular
6. 邮箱验证

-

---

#joker 2016/4/7

##TODO

1. use angular to start a project
2. make full user profile
3. while update a project what can and what cannot be updated
4. while choose a category, how to assure the category is right if user change the post报文？
5. Donation — Funds will be collected automatically as pledged. :打赏功能立刻打钱
6. 先把购买全过程做齐吧。。。
7. 还是用mangoose吧。大家都在用
8. mongodb的访问限制！不能随便任何人都能访问啊！关闭27071端口不就好啦
9. 



##Tips

**每次都要重启下ubuntu!不然不更新时间！**

---

#joker 2016/4/7

##TODO

1. use angular to start a project
2. make full user profile
3. while update a project what can and what cannot be updated
4. while choose a category, how to assure the category is right if user change the post报文？
5. Donation — Funds will be collected automatically as pledged. :打赏功能立刻打钱
6. 先把购买全过程做齐吧。。。
7. 还是用mangoose吧。大家都在用
8. mongodb的访问限制！不能随便任何人都能访问啊！关闭27071端口不就好啦
9. 



##Tips

**每次都要重启下ubuntu!不然不更新时间！**

---
2016.4.20

发现 redirect('back') 的一个 bug。
如果用户刷新了一遍登陆界面，那么back也会再度返回登陆界面。
