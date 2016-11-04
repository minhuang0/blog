title: js 快速排序
date: 2016-07-14
tags: 
    - javascript

categories: 编程

---

在学校的时候用c写过快速排序，老师讲了半天才理解，过了这么久都忘记的差不多了。

我理解的快速排序是取数组中一个基数，用这个基数与其他的数比较，比它小的放左边，比它大的放右边。然后往复递归, 返回本身，结束递归。


```javascript
function quickSort(arr){
    if(arr.length === 0){
        return arr;
    };
    var left = [],
        right = [],
        pivot = arr[0];
    for(var i = 1; i < arr.length; i++){
        if(arr[i] < pivot){
            left.push(arr[i]);
        }else{
            right.push(arr[i]);
        }
    };
    return quickSort(left).concat([pivot],quickSort(right));
}
```

<!--more-->  

用上面的方法对数组`var arr = [1, 2, 7, 4, 0, 5, 11, 8]`进行排序,用了17次递归调用quickSort。现在可以优化部分代码，将退出条件修改为:

```javascript
function quickSort(arr){
    //下面三行是优化后的代码
    if(arr.length <= 1){
        return arr;
    };
    var left = [],
        right = [],
        pivot = arr[0];
    for(var i = 1; i < arr.length; i++){
        if(arr[i] < pivot){
            left.push(arr[i]);
        }else{
            right.push(arr[i]);
        }
    };
    return quickSort(left).concat([pivot],quickSort(right));
}
```

这种情况下面，当递归进来`arr`长度为1的时候则直接返回本身。此时数组`arr`排序的递归次数为13次。

当我们的数组为 `["1_z","7_b","6_K","2_b","3M"]`的时候，我们还想要自定义的去排序，例如将字符串`parseInt`后再排序时，可以将排序规则抽出来，当做参数传递。

```javascript
function quickSort(arr,customSort){
    if(!customSort) {
        customSort = function(a, b) {
            return a < b;
        };
    };
    if(arr.length <= 1){
        return arr;
    };
    var left = [],
        right = [],
        pivot = arr[0];
    for(var i = 1; i < arr.length; i++){
        if(customSort(arr[i],pivot)){
            left.push(arr[i]);
        }else{
            right.push(arr[i]);
        }
    };
    return quickSort(left).concat([pivot],quickSort(right));
}
```

此时我们使用

```javascript
quickSort(array, function(a, b){
    return parseInt(a, 10) < parseInt(b, 10); 
});
```
则可以有效的返回自己需要的结果。

> 这里的提到 parseInt的参数，如果是 "k_6"的字符串是不会被正确解析的。[w3c parseInt](http://www.w3school.com.cn/jsref/jsref_parseInt.asp)
> 如果字符串的第一个字符不能被转换为数字，那么 parseFloat() 会返回 NaN。  

我们还能继续优化，将这个sort方法变成prototype里面的属性。

```javascript
Array.prototype.quickSort = function(customSort){
    var arr = this;
    if(!customSort) {
        customSort = function(a, b) {
            return a < b;
        };
    };
    if(arr.length <= 1){
        return arr;
    };
    var left = [],
        right = [],
        pivot = arr[0];
    for(var i = 1; i < arr.length; i++){
        if(customSort(arr[i],pivot)){
            left.push(arr[i]);
        }else{
            right.push(arr[i]);
        }
    };
    return left.quickSort(customSort).concat([pivot],right.quickSort(customSort));
}
```

则可以通过prototype方式调用quickSort方法。

```javascript
["1_z","7_b","6_k","2_b","3M"].quickSort();
```

