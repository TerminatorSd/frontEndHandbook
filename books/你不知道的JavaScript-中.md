> JS 的阿克琉斯之踵：简单易用、应用广泛，但是语言机制微妙而复杂

- 显式类型转换与隐式类型转换
    - 显式与隐式的定义是相对的
    - 如果你了解，一眼就能认出它，那就是显式的
- 因为无需深入理解就能用它来编程，所以人们常常放松对它的学习
- 基本类型与引用类型：Null、Undefined、String、Number、Boolean、Object
- 函数不仅是对象，还可以拥有属性，比如fun.length
- 通过typeof 可以检测undefined 和undeclared，尽管两者并不是一回事
- 使用delete 后，数组的length 属性不会发生变化
- 在JS 中，字符串是不可变的；字符串下标不会记录数组长度
```js
var a = [];
a[0] = 1;
a['foo'] = 2;
a.length // 1
```
- 字符串反转，简单粗暴
```js
str.split('').reverse().join('');
```
- toFixed
```js
42.toFixed(3) // SyntaxError
(42.)toFixed(3) // fine
```
- 浮点数精度问题
```js
// 所有遵循IEEE 754 规范的语言都是如此
0.1 + 0.2 !== 0.3
```
- 安全整数检测
```js
// in es6
Number.isSafeInteger()
```
- isNaN bug
```js
isNaN('b') // true
```
- 一个常见的关于引用失效的疑惑点
```js
function foo(x) {
  x.push( 4 );
  x; // [1,2,3,4]
  // 然后
  x = [4,5,6];
  x.push( 7 );
  x; // [4,5,6,7]
}
var a = [1,2,3];
foo(a);
a; // 是[1,2,3,4]
```

- true or false
```js
-0 === 0 // true
// in es6
Object.is(-0, 0) // false
```

// stop at 4.1 yinshi


