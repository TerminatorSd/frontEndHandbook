# Something about ES6.
> ### Set & WeakSet
##### (1) Set
- Set 类似数组，但是成员的值是唯一的，没有重复
- Set 内部判断两个值是否相等用的方法类似精确相等运算符（===），主要区别是这里NaN 等于NaN
- Set api 包含add、delete、has、clear
- Set 遍历api 包含keys、values、entries、forEach
##### (2) WeakSet
WeakSet 与Set 有以下区别：
- WeakSet 的成员只能是对象，而不能是其他值
- WeakSet 的对象都是弱引用，及引用计数不考虑WeakSet 的引用
- WeakSet 有多少成员取决于内存回收机制有没有运行，所以其不可遍历

> ### Map & WeakMap
##### (1) Map
- Map 的键不限于字符串
- 任何具有Iterator 接口，且每个成员都是双元素数组的数据结构都可以当做Map 构造函数的参数
- Map api 包含set、get、has、delete、clear
- Map 遍历api 包含keys、values、entries、forEach
##### (2) WeakMap
WeakMap 与Map 有以下区别：
- WeakMap 只接受对象作为键名（null 除外）
- WeakMap 的键名所指向的对象不计入引用计数
- WeakMap 没有遍历操作，无法清空
- 应用场景：注册监听事件、部署私有属性

> ### Symbol
##### (1) 是什么？
- Symbol 是ES6 中引入的一种新的原始数据类型，是JS 语言的第7 种数据类型
- Symbol 与字符串类似，但是其表示独一无二的值
```js
let a = Symbol('foo');
let b = Symbol('foo');
console.log(a === b); // false
```
##### (2) 有什么用？
- 消除魔术字符串
```js
function getArea(shape, options) {
    var area = 0;
    switch(shape) {
        case: 'Triangle' :
            // ...
            break;
    }
    return area
}
getArea('Triangle', {});

// 使用Symbol 修改后如下
const shapeType = {
    triangle: Symbol()
}
// 然后使用shapeType.triangle 替换上面的'Triangle'

```
- 实现非私有但只希望内部访问的属性
##### (3) 重新使用一个Symbol 值
- 使用Symbol.for, 声明的变量会被登记在全局环境中供搜索
```js
let a = Symbol.for('foo');
let b = Symbol.for('foo');
console.log(a === b); // true
```
- 使用Symbol.keyFor 可以返回一个已登记的Symbol 类型值的key
```js
let s = Symbol.for('foo');
Symbol.keyFor(s); // 'foo'
```
##### (4) 内置Symbol 值
- Symbol.hasInstance、isConcatSpreadable、species、match、replace、search、split、iterator、toPrimitive、toStringTag、unscopables
##### (5) 参考资料
- http://es6.ruanyifeng.com/#docs/symbol

> ### Proxy
##### (1) 是什么？
- Proxy 用于修改某些操作的默认行为，相当于对编程语言进行编程，他通过重写或指定某些方法来改变js 的默认行为。
##### (2) 拦截方法
- get() 方法用来拦截属性的读取操作
- set() 方法用来拦截属性的设置操作
- apply() 方法用来拦截函数的调用、call 和apply 操作
- has() 方法用来拦截HasProperty 操作
- construct() 方法用于拦截new 命令
- deleteProperty() 用于拦截delete 操作
- getOwnPropertyDescriptor() 用于拦截获取属性描述符对象
- getPrototypeOf() 用于拦截获取对象原型
- isExtensible() 拦截Object.isExtensible 操作
- ownKeys() 用于拦截对象自身属性的读取操作
- preventExtensions() 用于拦截Object.preventExtensions() 操作
- setProtorypeOf() 用于拦截Object.setPrototypeOf 方法
##### (3) 可取消实例
- Proxy.revocable 方法返回一个可取消的Proxy 实例
```js
let target = {};
let handler = {};

let {proxy, revoke} = Proxy.revocable(target, handler);

proxy.foo = 123;
proxy.foo // 123

revoke();
proxy.foo // TypeError: Revoked
```
##### (4) 参考资料
- http://es6.ruanyifeng.com/#docs/proxy

> ### Promise
- 是ES6 中异步编程的一种解决方案，相比于传统的回调可以解决回调地狱的问题
- Promise 是一个对象，可以获取异步操作的消息，有三种状态：pending、fulfilled、rejected，变成fulfilled 或者rejected 的状态都称为resolved
- Promise api 有then、catch、resolve、reject、all、race

> ### Iterator
##### (1) 是什么？
- 是一种遍历器接口，部署了Iterator 接口的数据结构可以使用ES6 的for...of 进行遍历
    - for...in 遍历键名，for...of 遍历键值
##### (2) 在哪里
- ES6 规定，默认的Iterator 接口部署在数据结构的Symbol.iterator 属性，或者说，一个数据结构只要具有Symbol.iterator 属性就认为是可遍历的
- ES6 中原生具备遍历器接口的数据结构包含：Array、Map、Set、String、TypedArray、函数的arguments 对象、NodeList 对象、字符串
##### (3) 对象为什么不具备遍历器接口？
- 因为对象属性的遍历顺序是不确定的，需要开发者手动指定。遍历器本质上是一种线性结构，对于非线性的数据结构，部署遍历器结构就等于部署一种线性转换
##### (4) 默认调用Iterator 接口的场合
- 解构赋值
- 扩展运算符
- yield*
- 任何接受数组作为参数的场合，比如
    - for...of
    - Array.from()
    - Promise.all()、Promise.race()
    - Map()、Set()、WeakMap()、WeakSet()

> ### Generator
##### (1) 是什么？
- 是ES6 中异步编程的一种解决方案，函数名前带星号，函数中可以使用yield 进行暂停操作
- Generator 函数中遇到yield 关键字的时候会暂停执行后面的内容，并将紧跟在yield 后面的返回值作为对象的value 值
##### (2) 怎么用？
- 调用该函数会返回一个内部指针（遍历器），执行它不会返回结果，而是返回指针对象，可以通过next 方法移动内部指针
- 利用该函数可以在任意对象上部署Iterator 接口，之后我们可以通过for of 进行访问
##### (3) Generator 与协程
- Generator 函数是协程在ES6 中的实现，最大特点就是可以交出函数的执行权（即暂停执行）
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

> ### async & await
##### (1) 是什么？
- 是generator 函数的语法糖
- async 函数的返回值是Promise 对象
- await 命令后面是一个Promise 对象，如果不是，会被转成一个立即resolve 的Promise 对象
##### (2) 如何实现的？
- async 的实现原理就是将generator 函数和自动执行器包装在一个函数里
##### (3) 有什么优点？
- async & await 相对于generator 的改进
    - 内置执行器
    - 更好的语义
    - 更广的实用性
    - 返回值是Promise，await 相当于函数内部then 命令的语法糖
##### (4) 异步Generator 函数
- Generator 函数返回一个同步遍历器对象，异步Generator 返回一个异步遍历器对象，在语法上，异步Generator 函数就是async 函数与Generator 函数的结合
- async 函数返回的是一个Promise 对象，异步Generator 函数返回的是一个异步Iterator 对象。前者自带执行器，后者通过for await...of 执行
