### Promise
- 是ES6 中异步编程的一种解决方案，相比于传统的回调可以解决回调地狱的问题
    - 用给第三方提供扣款方法的方式来解释回调地狱问题，有可能重复扣、不扣、或者参数不正确等
- Promise 是一个对象，可以获取异步操作的消息，有三种状态：pending、fulfilled、rejected，变成fulfilled 或者rejected 的状态都称为resolved
- ES6 规定，Promise对象是一个构造函数，用来生成Promise实例
    - Promise 新建后就会立即执行
```js
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```
- Promise api 有then、catch、resolve、reject、all、race
- 回调函数是控制反转，Promise在此之上又进行了反转，因此是反控制反转
- Promise 是可信任的，因为他的状态一旦改变就不会在发生变化
- 使用Promise.resolve() 包装返回值使得thenable 的行为更可控、稳定
- 如果外层promise resolve 了内层promise，那么最终状态由内层resolve 决定
```js
const p1 = new Promise(function (resolve, reject) {
  setTimeout(() => reject(new Error('fail')), 3000)
})

const p2 = new Promise(function (resolve, reject) {
  setTimeout(() => resolve(p1), 1000)
})

p2
  .then(result => console.log(result))
  .catch(error => console.log(error))
```
- 调用resolve 并不会终结Promise 函数的执行
```js
new Promise((resolve, reject) => {
  resolve(1);
  console.log(2);
}).then(r => {
  console.log(r);
});
// 2
// 1
```
- Promise.prototype.catch()方法是.then(null, rejection)或.then(undefined, rejection)的别名，用于指定发生错误时的回调函数;另外，then()方法指定的回调函数，如果运行中抛出错误，也会被catch()方法捕获
- Promise 会吃掉错误的意思是，如果Promise 中的错误没有被捕获，也不会影响代码的运行
```js
const someAsyncThing = function() {
  return new Promise(function(resolve, reject) {
    // 下面一行会报错，因为x没有声明
    resolve(x + 2);
  });
};

someAsyncThing().then(function() {
  console.log('everything is great');
});

setTimeout(() => { console.log(123) }, 2000);
// Uncaught (in promise) ReferenceError: x is not defined
// 123
```
- catch 可以出现在链的中间
```js
const someAsyncThing = function() {
  return new Promise(function(resolve, reject) {
    // 下面一行会报错，因为x没有声明
    resolve(x + 2);
  });
};

someAsyncThing()
.catch(function(error) {
  console.log('oh no', error);
})
.then(function() {
  console.log('carry on');
});
// oh no [ReferenceError: x is not defined]
// carry on
```
