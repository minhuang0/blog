title: Phonegap and Appcelerator
date: 2015-10-11
tags: 
    - titanium
categories: 编程

---

# [Appcelerator Ti](http://www.appcelerator.com/)

<!--more--> 

最近使用Ti来进行Android和IOS的开发,与之前老版本的不同的是,在我所接触的版本不是之前的Web UI的形式,更多的是接近于原始的UI效果。

在4.0+ 之后的版本对Android的支持变得友善一些了,开始尝试的是Alloy框架,使用MVC分层的方式去调整代码UI与逻辑,后面发现在机型适配方面需要花费大量的时间来进行调整。

而后根据[kitchensink](https://github.com/appcelerator/KitchenSink)的方式进行开发,使用Js的Module export 和 export将每一个页面进行分割,并将逻辑和UI写在一个JS文件里面,将多处用到的功能和UI的适配封装成Module([网址参考](http://gitt.io/)),比之前的开发省下了大量的时间和精力。

 

# [PhoneGap](http://phonegap.com/)

> 下面是个人理解,等有机会去试一试

PhoneGap是一个WebView型的混合应用,对于平台的支持性优于Ti,底层运行原理是css,html绘制UI以及由JavaScript API来实现逻辑和调用手机的API,个人理解为是一层类手机页面打开了一个网页,在进行类手机APP的操作。


# 杂谈
淘宝软件现在的首页,支付宝的首页感觉也像是WebView,个人感觉应该是原生里面嵌套了Web页面
