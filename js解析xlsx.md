title: js-xlsx解析xlsx转成xml格式
date: 2016-09-19
tags: 
    - nodejs

categories: 编程

---

XML格式的文件在代码中常用于配置文件,而JSON常用于代码中的数据存储.

- 解析xlsx文件使用的`js-xlsx`,原因就是api提供的功能够满足我的需求,而且也方便扩展;
- 在XML输入方面选择的`xmlbuilder`,当然`xml-write`也可以,只是前者链式操作和JSON输入比较好用。
- 需要输入输出文档,还的需要`fs`

<!-- more -->

package.json使用到的依赖如下:

```
"devDependencies": {
    "xlsx": "^0.8.0",
    "xmlbuilder": "^8.2.2"
}
```

### 步骤

总体可以分为三个阶段

xlsx --> JSON --> XML


- 引入依赖:

```
var XLSX = require('xlsx'),
    builder = require('xmlbuilder'),
    fs = require('fs');
```

- 解析xlsx文件

workbook是解析之后xlsx的所有数据

```
const workbook = XLSX.readFile('xlsx/myXlsx.xlsx', { type: 'base64' });
```

- 解析xlsx中的json数据

这个方法主要是循环xlsx数据中的sheet,将其输入到一个数组中,[sheet_to_json](https://github.com/SheetJS/js-xlsx#utilities)是XLSX的工具类,

```
var to_json = (workbook) => {
    "use strict";
    let result = [],
        sheetNames = workbook.SheetNames;

    workbook.SheetNames.forEach((sheetName) => {
        let worksheet = workbook.Sheets[sheetName];
        result.push(XLSX.utils.sheet_to_json(worksheet));
    });
    return result;
};

let workbookData = to_json(workbook);
```

- 将处理好的json数据输入到xmlBuilder里面

我处理的过程比较复杂,数据也比较多,就不贴在这里了,主要的数据是通过ele()方法添加的,参数为key: value的obj,value也可以array。

`builder.create('root', { encoding: 'UTF-8' })`是创建了

```
<?xml version="1.0" encoding="UTF-8"?>
<root>
</root>
```

- `ele()` 添加obj,
- `up()` 回到上一层的dom节点
- `end()` 结束书写dom;
- `remove()` 删除一个节点;

下面是完整的代码,可参照[API](https://github.com/oozcitak/xmlbuilder-js/wiki#creating-child-nodes):


```
var obj = {
  person: {
    name: "John",
    '@age': 35,
    address: {
      city: "Istanbul"
    },
    phone: [
      { '#text': "555-1234", '@type': 'home' }, 
      { '#text': "555-1235", '@type': 'mobile' }
    ],
    id: function() {
      return 42;
    }
  }
};

let xml = builder.create('root', { encoding: 'UTF-8' })
     .ele({
        options: {
            "@id": "加@符号的时候是属性(attribute)",
            "#text": "#text里面是内容(content)"
        }
     })
     .ele(xmlData)
     .up()
     .end({ pretty: true }),
```

- 写入文件

我们可以将上面生成的xml写入到文档输入流中,需要注意的是不会自动创建`/tmp`文件夹,需要自己手动创建或者用`fs`创建文件的方法。最后关闭文档流

```
let ws = fs.createWriteStream('./tmp/test.xml');

ws.write(xml);
ws.end();
```

### 其他

解析excle有好多node package,下面是有人总结出来的区别([链接](https://aotu.io/notes/2016/04/07/node-excel/)),可以根据自己的需求使用不同的package。
