title: ajax跨域理解和封装
date: 2016-01-15
tags: 
    - ajax
    - jquery
categories: 编程

---


### Ajax中的跨域请求

在使用ajax添加headers的过程中,方法很简单。[（解决方法）](http://stackoverflow.com/questions/3258645/pass-request-headers-in-a-jquery-ajax-get-call)。第一次写，没什么经验。一直以为是我的ajax的参数有问题。后台也太懂,还上stackoverflow提问，结果还被点了个负分。后面查到资料是需要后台开放请求头,这时候的自定义的请求才能够到达。如何请求的过程[在这](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS#Access-Control-Request-Headers),用自己的话说就是:
  
  - 小弟: 老大，我想要点东西（OPTIONS 发送一个预请求）
  - 老大: 瞅一下,（匹配通过）是我的小弟。嗯, 你说吧!
  - 小弟: 单子在这呢,您看一下(POST GET 请求)
  - 老大: 看在你平时孝敬我的份上,这批货就给你了(返回数据)

<!--more-->

### Ajax请求的封装

第一次写前端,后面遇到要给自己的每一个请求头(headers)都加上一组{key: value},一开始写的是直接将$.ajax请求包裹起来,用一个方法代替,如下:

```javascript
function publicAjax(args) {
    $.ajax({
        "url": args.url,
        "dataType": 'json',
        type: args.type || 'GET',
        data: args.data || '',
        xhrFields: {
            withCredentials: true
        },
        "success": function(data) {
            if (data.token) {
                setToken(data.token);
            }
            args.success(data);
        },
        "error": function() {
            alert("网络状况不好，请重试");
        }
    });
}
```
后来由于这个方法有局限性,不适用于某些插件(如:[datables](https://www.datatables.net/)),找到一种更好的方法。主要用到的jquery的`$.extend`方法,代码如下:

```
(function($) {
        //备份jquery的ajax方法  
        var _ajax = $.ajax;

        //重写jquery的ajax方法  
        $.ajax = function(opt) {
            //备份opt中error和success方法  
            var fn = {
                error: function(XMLHttpRequest, textStatus, errorThrown) {},
                success: function(data, textStatus) {}
            }
            if (opt.error) {
                fn.error = opt.error;
            }
            if (opt.success) {
                fn.success = opt.success;
            }

            //扩展增强处理  
            var _opt = $.extend(opt, {
                beforeSend: function(req) {
                    //req.setRequestHeader("mark", getToken());
                },
                error: function(xmlhttprequest, textstatus, errorthrown) {
                    switch (xmlhttprequest.status) {

                    }
                    //错误方法增强处理
                    fn.error(xmlhttprequest, textstatus, errorthrown);
                },
                success: function(data, textStatus, xhr) {
                    //成功回调方法增强处理  
                    fn.success(data, textStatus);
                },
                complete: function(XMLHttpRequest, textStatus) {

                },
            });
            _ajax(_opt);
        };
    })(jQuery);
```
解决的大部分的问题请求加上{key: value}的问题。看到这里的同学可以不要往下看了,下面的跟这个问题没有很大关联,只是记录我的一些问题。然而新的问题就是一些header的问题了。这种封装情况下:

```
xhrFields: {
    withCredentials: true
},
```
这个属性在上面函数的beforeSend中加并没有效果，使ResquestHeaders中的Cookie丢失了,只有将在外部的$.ajax参数中了。本想获取cookie值来手动添加的，后面查到文档中有一些自定义的header是不允许添加的。[详情查看](https://dvcs.w3.org/hg/xhr/raw-file/tip/Overview.html#dom-xmlhttprequest-setrequestheader)。 最后只有妥协,第一种和第二种方法都共用。
