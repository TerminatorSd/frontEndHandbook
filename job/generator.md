### Generator
##### (1) 是什么？
- 是ES6 中异步编程的一种解决方案，函数名前带星号，函数中可以使用yield 进行暂停操作
- Generator 函数中遇到yield 关键字的时候会暂停执行后面的内容，并将紧跟在yield 后面的返回值作为对象的value 值
- 遇到yield表达式，就暂停执行后面的操作，并将紧跟在yield后面的那个表达式的值，作为返回的对象的value属性值
- yield 为JavaScript 提供了手动的惰性求值，关于这一点，有个很好的例子
- 可以说 Generator 生成了一系列的值，这也就是它的名称的来历（生成器）
##### (2) 怎么用？
- 调用该函数会返回一个内部指针（遍历器），执行它不会返回结果，而是返回指针对象，可以通过next 方法移动内部指针
- 利用该函数可以在任意对象上部署Iterator 接口，之后我们可以通过for of 进行访问
- yield表达式如果用在另一个表达式之中，必须放在圆括号里面
- 读懂它
```js
function* foo(x) {
  var y = 2 * (yield (x + 1));
  var z = yield (y / 3);
  return (x + y + z);
}

var a = foo(5);
a.next() // Object{value:6, done:false}
a.next() // Object{value:NaN, done:false}
a.next() // Object{value:NaN, done:true}

var b = foo(5);
b.next() // { value:6, done:false }
b.next(12) // { value:8, done:false }
b.next(13) // { value:42, done:true }
```
##### (3) Generator 与协程
- Generator 函数是协程在ES6 中的实现，最大特点就是可以交出函数的执行权（即暂停执行）
```js
function *asyncJob() {
    // ...
    // 此时函数的执行权交到readFile 函数手中
    var f = yield readFile(fileA);
    // ...
}
```
##### (4) Generator 异步应用
- 将Generator 函数和Promise 封装在一起组成异步Generator 函数，用来处理异步流程
- 使用Thunk 函数进行异步流程管理

##### More
- ES6 中最完美的世界就是生成器（看似同步的异步代码）和Promise（可信任、可组合）的结合。【尚未掌握】