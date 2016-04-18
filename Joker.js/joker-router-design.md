#众客路由设计

##版本

1. v0.1 20160330 20:00 @d4rkb1ue
2. v0.2 20160330 21:30 @d4rkb1ue
3. v0.3 20160331 01:00 @d4rkb1ue

##设计主要参考对象

- [MOOC](https://www.coursera.org) : 课程学习
    + [edX](https://www.edx.org)
    + [Udacity](https://www.udacity.com)
    + [Coursera](https://www.coursera.org)

- [Kickstarter](https://www.kickstarter.com) : 众筹
- [原网站](http://a.ray0.com)

##需求列表

- 众筹购买：首页项目展示，全部（分类）项目展示，项目详情
- 众筹发起：发起项目，更新项目信息
- 项目管理：管理员审核、管理和更新
- 课程：已购买课程，课程详情主页
- 教学方式：文字，图片，视频，留言讨论，课堂交流（实时交流），测验，家庭作业，站内信，实时语音视频?
- 账户：登录，注册，账户设置，*用户管理?*
- 订单：下订单，历史订单，报表
- 其他：收藏夹，帮助，*站内信?*，需求交流论坛，代金券，搜索，*草稿保存?*

##Routes界面文档结构 ~~不算逻辑图~~

- / @首页
    + /discover @全部（分类）项目展示
    + /help 
    + /about
    + /search @搜索
        * /search-result @搜索结果
    

- /user @账户
    + /login
    + /register
    + /setting
    + /fav @收藏


- /admin @后台管理
    + /projects @审核管理
    + /users @用户管理
    + /orders @订单管理，报表
    + /coupon @优惠券管理


- /project @项目
    + /some-project @项目详情
        * /updates @修改历史
        * /comments @评论
        * /edit @修改

    + /initial @发起


- /order @订单
    + /make-order @下订单
    + /funded @已购买


- /lesson @学习
    + /lessons @全部可学习列表
    + /some-lesson @课程详情主页
        * /videos @下方讨论区?
        * /bbs @交流
        * /test @测试?
        * /homeword @作业?
    
- /ideas @需求交流论坛（flat平面式）

##Project&Lesson

在设计逻辑的时候，清晰的看到这两个部分的分界。这么区分是：

project : 
```
项目审核 -> 项目众筹 -> 项目制作教学 -> 项目完成
                  -> 众筹失败
                  -> 项目制作教学 -> 投诉和退款
```


lesson : 在 project 的`项目制作教学`即开始。
```
                    项目制作教学 -> 项目完成 -> 原价选课入学动态课程 -> 项目继续开课
                                                   |<-------循环--------|

                               -> 项目完成 -> 原价购买静态课程

```

存在重叠。

##参考资源和Tips

- 翻墙() 
    + on Windows :[Shadowsocks-win](https://shadowsocks.org/en/download/clients.html)
    + on Mac : [Shadowsocks-for-OSX](https://shadowsocks.org/en/download/clients.html)
    + on iPhone : ipsec-vpn, [Surge](http://www.jianshu.com/p/de1eb844915d)
    + on Android : [Shadowsocks-android](https://shadowsocks.org/en/download/clients.html)
    + Shadowsocks 账户:
        * 地址 vpn1.ray0.com:7311
        * 加密方式 aes-256-cfb
        * 密码 fuckyougfwbitch

---

#产品

###产品形态

产品可以被描述成"课程服务平台"，就像博客，有人提供博客的平台，用户只需关心内容。
我们的平台面对有建立课程，收费课程，网络教学，YY语音教学的教学者。
我们提供灵活的课程实施方案，提供对文字，图片，视频（视频在线修改），讨论，在线交流，测验，家庭作业站内信，实时语音视频等教学方式的技术支持模块。
同时以众筹的形式，通过需求驱动课程的建立。提供给开课者资金来源，让其收益得到保障。避免无谓的浪费。
重视听课者的价值，听课者对课程的补充和理解。

