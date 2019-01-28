---
title: 回顾ES5中数组的一些方法
date: 2019-01-28 19:45:57
tags:
---
# 回顾 ES5 中数组的一些实用方法

现在es6的推进和普及大大提高了现在js的编程效率，但是在之前es5中更新的一些数组的操作方法，对我们在原生js中操作数组有着非常显著的提高，我们现在一起回顾一下es5中一些非常高效的数组方法

> 5个迭代方法：forEach()、map()、filter()、some()、every()；
>
> 2个索引方法：indexOf() 和 lastIndexOf()；
>
> 2个归并方法：reduce()、reduceRight()；

## 迭代方法

###1. forEach

- 简介： 


`forEach` 是es5中最基本也是目前用的非常多的一种数组方法，就是最基础的循环、遍历。让我们不用再无脑for循环

- 语法： 


```js
array.forEach(callback);
```

- 示例

```js
//遍历打印数组的value, index和数组本身
let arr = [1, 2, 3];
arr.froEach((value, index, arr) => {
    console.log(value, index, arr)
})
//1 0 [ 1, 2, 3 ]
//2 1 [ 1, 2, 3 ]
//3 2 [ 1, 2, 3 ]
```

### 2.map

- 简介： 

`map()` 是一种映射方法，对数组中的每一项运行指定的函数，并且返回函数每次调用的结果所组成的数组。用map可以对数组的

- 语法： 

```js
array.map(callback,[ thisObject]);
```

- 示例

```js
//对数组的每一项进行双倍处理，并返回新的数组
let arr2 = [2,4,6];
let sum2 = arr2.map((value,index,arr) => {
  return value += value;
});
console.log(sum2);  // [4, 8, 12] 
```



###3.filter

- 简介： 

`filter()` 是一种过滤方法，对数组中的每一项进行对应函数规则的筛选，并返回新的数组，用法和`map()`非常相似

- 语法： 

```js
array.filter(callback,[ thisObject]);
```

- 示例

```js
//对数组的每一项进行筛选，并返回能够被3整除的项
let arr3 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let flag = arr3.filter((value, index) => {
  return value % 3 === 0;
}); 
console.log(flag);  // [3, 6, 9]
```



### 4.some

* 简介

`some()`  判断数组中是否存在满足条件的项，只要有一项满足条件，就会返回true。

* 语法

```js
array.some(callback,[ thisObject]);
```

* 示例

```js
//用some()来判断一个数组中的每项是否含有偶数：
var arr5 = [1, 2, 3, 4, 5];
var flag = arr5.some(function(value, index) {
  return value % 2 === 0;
}); 
console.log(flag);   // true
```



### 5.every

- 简介： 

`filter()` 判断数组中每一项都是否满足所给条件，当所有项都满足条件，才会返回true。

- 语法： 

```js
array.every(callback,[ thisObject]);
```

- 示例

```js
//用every()来判断一个数组中的每项是否都是偶数：
var arr4 = [1, 2, 3, 4, 5];
var flag = arr4.every(function(value, index) {
  return value % 2 === 0;
}); 
console.log(flag);  // false
```



## 索引方法 

indexOf() 和 lastIndexOf()

这两个方法都接收两个参数，第一个参数是要查找的项，第二个参数是查找项起点位置的索引，该参数可选，如果缺省或是格式不正确，那么默认为0。

两个方法都返回查找项在数组中的位置，如果没有找到，那么返回-1。区别就是一个从前往后找，一个从后往前找。意思就是第二个参数是你立的一个flag，一个往flag右边找，一个往flag左边找。

### indexOf

* 简介

`indexOf()`，返回查找项的整数索引值，如果没有匹配（严格匹配），返回-1。这个方法与字符串方法ndexOf()的功能是一样的，不过是对数组的操作而已。

* 语法

```js
array.indexOf(searchElement[, fromIndex])
```

* 示例

```
var arr6 = [1, 3, 5, 3, 5];
console.log(arr6.indexOf(5, 'x'));  // 2 ('x'被忽略)
console.log(arr6.indexOf('5', 3));  // -1 (未找到，因为5 !== '5')
console.log(arr6.indexOf(5, '3'));  // 4 (从3号位开始向后搜索)
console.log(arr6.indexOf(5, 3));  // 4 (从3号位开始向后搜索)
console.log(arr6.indexOf(4));  // -1 (未找到)
```

### lastIndexOf

`lastIndexOf()`与`IndexOf()`类似,只是lastIndexOf()是从字符串的末尾开始查找，而不是从开头。

```
var arr7 = [1, 3, 5, 3, 5];
console.log(arr7.lastIndexOf(5));  // 4
console.log(arr7.lastIndexOf(3));  // 3
console.log(arr7.lastIndexOf(1));  // 0
console.log(arr7.lastIndexOf(5, '3'));  // 2 (从3号位开始向前搜索)
console.log(arr7.lastIndexOf(5, 3));  // 2 (从3号位开始向前搜索)
console.log(arr7.lastIndexOf(4));  // -1 (未找到)
```

## 归并方法

reduce()和reduceRight()

这两个方法相比前面可能稍微复杂一些，它们都会迭代数组中的所有项，然后生成一个最终返回值。它中文直译是缩减，应该是随着运算项数在递减，就类似于归并，迭代。

接收两个参数，第一个参数callback，函数接受4个参数分别是（初始值*total必选*，当前值*currentValue必选*，索引值*currentIndex可选*，和当前数组*arr可选*），函数需要返回一个值，这个值会在下一次迭代中作为初始值。第二个参数是迭代初始值（initialValue），参数可选，如果缺省，初始值为数组第一项，从数组第一个项开始叠加，缺省参数要比正常传值少一次运算。

### reduce

* 简介

reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。**注意:** reduce() 对于空数组是不会执行回调函数的。

* 语法

```js
array.reduce(callback[, initialValue])
```

* 示例

```
var arr9 = [1, 2, 3, 4];
var sum9 =arr9.reduce(function (total, curr, index, array) {
  return total * curr;
});
console.log(sum9);  // 24 
var sum9_1 =arr9.reduce(function (total, curr, index, array) {
  return total * curr;
}, 10);
console.log(sum9_1);  // 240
```

sum9中因为initialValue不存在，因此一开始的total值等于数组的第一个元素。从而curr值在第一次调用的时候就是2。

sum9_1，有了initialValue，就在第一次相乘时是10*2。

下面是一个二维数组扁平化的例子，感觉最近看书。视频还有和小伙伴聊天各种扁平化，组件数组方法……解耦不继承，那就……扁平化吧：

```
var matrix = [
  [1, 2],
  [3, 4],
  [5, 6]
];
var flatten = matrix.reduce(function (previous, current) {
  return previous.concat(current);
});
console.log(flatten); // [1, 2, 3, 4, 5, 6]
```

concat()方法是拼接数组的，会在下篇文章中详细讲到。我……争取早日写完，最近项目忙到原地炸裂，但学习效率却显著提高，每天地铁和午饭听个node视频都津津有味的。越忙越珍惜吧，呀，扯远了……回来！

### reduceRight

reduceRight()和reduce()相比，用法类似，差异在于reduceRight是从数组的末尾开始实现的。来做个简单的减法：

```
var arr9 = [2, 45, 30, 80];
var flag = arr9.reduceRight(function (total, curr, index) {
  return total - curr;
});
var flag_1 = arr9.reduceRight(function (total, curr, index) {
  return total - curr;
},200);
console.log(flag);  // 3
console.log(flag_1);  // 43
```