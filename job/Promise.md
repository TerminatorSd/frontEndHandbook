### Promise
- 是ES6 中异步编程的一种解决方案，相比于传统的回调可以解决回调地狱的问题
    - 用给第三方提供扣款方法的方式来解释回调地狱问题，有可能重复扣、不扣、或者参数不正确等
- Promise 是一个对象，可以获取异步操作的消息，有三种状态：pending、fulfilled、rejected，变成fulfilled 或者rejected 的状态都称为resolved
- Promise api 有then、catch、resolve、reject、all、race
- 回调函数是控制反转，Promise在此之上又进行了反转，因此是反控制反转
- Promise 是可信任的，因为他的状态一旦改变就不会在发生变化
- 使用Promise.resolve() 包装返回值使得thenable 的行为更可控、稳定
