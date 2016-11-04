title: jquery笔记
date: 2015-12-25
tags: 
    - jquery
    - javascript
categories: 编程

---

记录一些使用jquery遇到的问题和解决方法

<!-- more -->

- 使用[localResizeIMG](https://github.com/think2011/localResizeIMG)做图片压缩的时候碰到的一个问题。

hash: 

```javascript
var hash = {};
var number = [0,1,2,3,4,5];
for(var hashNum = 0; hashNum < number.length; hashNum++){
    hash["number" + hashNum] = number[hashNum];
}
```

```console
//输出结果
//Object {number0: 0, number1: 1, number2: 2, number3: 3, number4: 4…}
```

array:

```javascript
var array = [];
var number = [0,1,2,3,4,5];
for(var arrayNum = 0; arrayNum < number.length; arrayNum ++){
    array.push(number[arrayNum]);
}
```
```console
//输出结果
//[0, 1, 2, 3, 4, 5]
```

多图上传代码

```
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <title>测试代码</title>
    <script src="http://cdn.bootcss.com/jquery/1.11.3/jquery.min.js"></script>
    <script src="dist/lrz.bundle.js"></script>
</head>

<body>
    <p>测试</p>
    <input name="newCaseImagesInput" type="file" id="newCaseImagesInput" accept="image/*" multiple/>
    <div id="newCaseImagesDiv"></div>
    <button type="button" id="commit">提交</button>
    <script>
    var imagesData = [];
    $('#newCaseImagesInput').on('change', function() {
        for (var fileNum = 0; fileNum < this.files.length; fileNum++) {
            lrz(this.files[fileNum])
                .then(function(rst) {
                    imagesData.push(rst);
                    $("#newCaseImagesDiv").append('<img class="img-thumbnail" style="min-height:50px;height:50px;margin-left: 10px;" src="' + rst.base64 + '" >')
                        // 处理成功会执行
                });
        }
    });

    $("#commit").on('click', function() {
        console.info(imagesData);
    })
    </script>
</body>

</html>
```


## 插件

### 制作表格的插件: 

- [datatables](https://www.datatables.net/)  

![](http://i.imgur.com/i74NLwt.png)

- [Extjs](https://www.sencha.com/products/extjs/)

    ![](https://www.sencha.com/wp-content/uploads/2015/03/sencha-extjs-inline.png)

- [x-editable](https://vitalets.github.io/x-editable/) 

    ![实例](https://vitalets.github.io/x-editable/assets/img/bootstrap.png)
    
## 问题:

上传图片:
- [jquery file input](http://stackoverflow.com/questions/166221/how-can-i-upload-files-asynchronously)
