---
layout: post
title:  "Array Object String"
date:   2022-06-07 00:00:00 +0800
categories: jekyll update
---

## Array

1. shift 删除数组头部元素
2. unshift 添加元素到数组的头部
3. splice 通过索引删除某个元素, 多少个元素

```js
const x= [1,2,3,4,5,6,7]
undefined
const xxxx= x.splice(1,3)
// x [1, 5, 6, 7]
```

4. slice 方法返回一个新的数组对象，（包括 begin，不包括end）。原始数组不会被改变。

slice(begin, end)
```js
// 复制一个数组
let shallowCopy = fruits.slice() // this is how to make a copy
```

5. splice

splice(start[, deleteCount[, item1[, item2[, ...]]]])

```js
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at index 1
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "June"]
months.splice(4, 1, 'May');
// replaces 1 element at index 4
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "May"]
```

6. reduce

```js
const array1 = [1, 2, 3, 4];
const initialValue = 0;
const sumWithInitial = array1.reduce((pre, curr) => {
    return pre + curr;
}, initialValue);
console.log(sumWithInitial);
```

## Object

1. entries

```js
const object1 = {
  a: 'somestring',
  b: 42
};

for (const [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`);
}
```





