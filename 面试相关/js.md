# Knowledge of js
> ### 事件代理
- 利用事件的冒泡机制将子元素的事件监听统一由父元素来管理
- 资源消耗少，代码可维护性和可扩展性好
- 适用事件代理的事件：click，mousedown，mouseup，keydown，keyup，keypress
- 不适用事件代理的事件：mousemove，focus，blur（后两者不存在冒泡特性）

> ### JS 模块化
##### (1) CommonJs
- 服务器端，同步加载。
- nodeJs 的模块化机制，使用exports 和require 导出和导入模块。
##### (2) AMD
- 浏览器端，异步加载。
- requireJs 为遵循AMD 的模块化工具。
- 使用define 和require 定义和加载模块。
##### (3) CMD
- 浏览器端，异步加载。
- seaJs 为遵循CMD 的模块化工具。
- AMD 与CMD 的区别在于
    - AMD 推崇依赖前置，在定义模块的时候就要声明其依赖的模块
    - CMD推崇就近依赖，只有在用到某个模块的时候再去require 
##### (3) ES6
- 使用export 和 import 导出和导入模块。
##### (4) 相关资料
- https://blog.csdn.net/crystal6918/article/details/74906757
- https://www.cnblogs.com/fayin/p/6831071.html
- https://www.cnblogs.com/goloving/p/7710951.html

> ### null 和undefined 的区别
- null 表示不存在的对象，undefined 表示存在的对象未赋值
```js
typeof null  // object
typeof undefined  // undefined
```

> ### 内置对象、原生对象、宿主对象
- 内置对象：是原生对象的一种，包含Global、Math 和JSON 等不需要new 可以直接使用的对象
- 原生对象：包含Object、Function、Array、String、Boolean、Number、Date、RegExp、Error、EvalError、RangeError、ReferenceError、SyntaxError、TypeError、URIError。简单来说，本地对象就是 ECMA-262 定义的引用类型，需要使用new 创建。（也就是说原生对象实际上包含引用类型和内置对象两种）
- 宿主对象：不是引擎的原生对象，而是由宿主框架通过某种机制注册到JavaScript 引擎中的对象，比如浏览器的window, document。

> ### apply、call、bind 的区别
- 三个方法的作用都是改变函数的执行上下文
- apply 和call 会立即执行，而bind 不会立即执行
- call() 在第一个参数之后的，后续所有参数就是传入该函数的值。apply() 只有两个参数，第一个是对象，第二个是数组，这个数组就是该函数的参数。
- bind 和call 的参数相同
- https://www.cnblogs.com/ly0612/p/6821124.html

> ### ajax 工作原理
- 通过XMLHttpRequest 对象向服务器发送异步请求，该对象包含的属性如下：
    - onreadystatechange 每次状态改变所触发事件的事件处理程序；
    - responseText 从服务器进程返回数据的字符串形式；
    - responseXML 从服务器进程返回的DOM兼容的文档数据对象；
    - status 从服务器返回的状态码（eg：200、404）
    - statusText 伴随状态码的字符串信息 （eg：200 OK）
- 通过监听readystatechange 事件来处理各个环节的响应

> ### attribute 和property
- attribute 是attributes 的子集，property 是properties 的子集；attributes 是properties 的子集
- property 是DOM中的属性，是JavaScript 里的对象；attribute 是HTML标签上的特性，它的值只能够是字符串
- 对于value 属性值来说，影响是单向的 attribute -> propery，但是两者的改动都会反映到html 中
- 对于其他属性来说，影响是双向的
- 对于新添加的非默认属性来说，互不影响

> ### load 和DOMContentLoaded 的区别
- load 事件在DOMContentLoaded 之后
- 解析html 构建dom 树完成之后触发DOMContentLoaded 事件，此时可以访问到dom 元素
- 图片等所有外部元素加载完后会触发load 时间
- 兼容性：onload事件所有浏览器都支持，DOMContentLoaded事件高级浏览器均支持。E6、IE7仅支持onreadystatechange，更低级的ie用doscroll事件来检测。

> ### 尾调用优化
##### (1) 尾调用
- 某函数的最后一步调用了另一个函数
```js
function f(x){
  return g(x);
}
```
##### (2) 尾调用优化
- 尾调用由于是函数的最后一步操作，所以不需要保留外层函数的调用记录。
- 尾调用优化的意义就在于每次执行时，调用记录只有一项，这将大大节省内存。
##### (3) 尾递归
- 函数尾调用自身
- 对于普通递归来说，非常消耗内存，要同时保存成百上千个调用记录，很容易导致栈溢出，但是对于进行了尾调用优化的尾递归来说，则永远不会发生栈溢出错误
```js
function factorial(n, total) {
  if (n === 1) return total;
  return factorial(n - 1, n * total);
}
```
##### (4) 参考
- http://www.ruanyifeng.com/blog/2015/04/tail-call.html

> ### Event Loop
- js 中存在执行栈和事件队列
- js 先去执行执行栈中的方法，执行完后再去查询事件队列中是否有任务，如果有的话则将其拿出放到执行栈中执行，如此循环，被称为事件循环
- 事件队列中的异步任务又分为宏任务与微任务
    - 宏任务包含setInterval 和setTimeout
    - 微任务包含Promise 和MutationObserver
    - 微任务先于宏任务执行
    ```js
    setTimeout(function () {
      console.log(1);
    });
    new Promise(function(resolve,reject){
      console.log(2)
      resolve(3)
    }).then(function(val){
      console.log(val);
    })
    // 2 3 1
    ```

> ### js 操作cookie
##### (1) 设置
- 通过给document.cookie 直接赋值的方式设置cookie 的值、域名、及过期时间等信息
```js
function setCookie(name,value) 
{ 
    var Days = 30; 
    var exp = new Date(); 
    exp.setTime(exp.getTime() + Days*24*60*60*1000); 
    document.cookie = name + "="+ escape (value) + ";expires=" + exp.toGMTString(); 
} 
```
##### (2) 读取
- 通过使用正则匹配查找你要读取的cookie
```js
function getCookie(name) 
{ 
    var arr,reg=new RegExp("(^| )"+name+"=([^;]*)(;|$)");
    if(arr=document.cookie.match(reg)) {
        return unescape(arr[2]); 
    }
    else {
        return null; 
    }
} 
```
##### (3) 删除
- 通过设置cookie 过期时间的方式删除cookie
```js
function delCookie(name) 
{ 
    var exp = new Date(); 
    exp.setTime(exp.getTime() - 1); 
    var cval = getCookie(name); 
    if(cval != null) {
        document.cookie = name + "="+cval+";expires="+exp.toGMTString(); 
    }
} 
```

> ### ajax 异步提交表单的两种方式
##### (1) 将form表单数据序列化
```js
// 使用这种方法的前提是form表单中的项一定要有name属性
$.ajax({  
    type: 'POST',  
    url: 'url',  
    data: $('#yourformid').serialize(),  
    async: false,  
    error: function(request) {  
        alert('Error');  
    },  
    success: function(data) {  
        // ...  
    }  
});
```
##### (2) 通过窗口查找form提交
```js
// form表单都必须要有name属性，没有试过这种方法
var obj = document.getElementById("xx_iframe").contentWindow;  
  obj.$("#yourform").form("submit",{  
    success :function(data){  
        //对结果处理  
    }    
  });
```

> ### 万恶的正则表达式
- 基本语法：https://www.cnblogs.com/moqiutao/p/6513628.html
- 正则校验身份证：https://www.jb51.net/article/136639.htm

> ### 如何判断一个对象是数组
- typeof
- instanceof 不可靠
- arr.constructor === Array 不可靠
- Object.prototype.toString
- ES5 中的Array.isArray