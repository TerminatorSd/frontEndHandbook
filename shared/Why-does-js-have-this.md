### 0、先看看作用域？

不管我们用什么语言写代码，都有一个绕不过去的概念，作用域。

作用域是指在程序中定义变量的区域，该位置决定了变量的生命周期。通俗地理解，作用域就是变量与函数的可访问范围，即作用域控制着变量和函数的可见性和生命周期。

因此，代码的工作方式跟作用域有很大的关系。

ES5里只有两种作用域：全局作用域和函数作用域（通过变量环境实现）

### 1、为什么会有this？

JS引擎在查找变量和函数可见性或生命周期时涉及到的相关作用域称之为作用域链。

>  因为JS的作用域链是由词法作用域定义的，词法作用域是代码阶段（代码怎么写的）就决定好的，和函数怎么调用没有关系。

导致的结果是：我们在使用js来写代码的时候发现它没有按照我们想象的方式工作。即不支持对象中的方法调用对象中的属性，例子如下。

```js
var bar = {
    myName: 'name in bar',
    // 函数级作用域，在作用域中的上一层为全局作用域，而不是bar这个对象
    printName: function() {
        console.log(myName);
    }
}
var name = 'name in global';
bar.printName(); // name in global
```

### 2、this是怎么解决这个问题的？

this，也叫当前执行上下文，在js中只有三种执行上下文：全局（指向window对象）、函数（指向调用者或者使用call、apply或bind改变）、eval（不讨论）

可以看到，this和作用域有着很高的相似性，两者都基本只有全局和函数级两种。但是，需要明确的一点是，作用域链和this是两套不同的系统，他们之间没有太多联系。至于到底如何区分，就看一个很简单的场景，作用域链下的变量可以继承，而this不可以。

```js
// demo 2
var bar = {
    myName: 'name in bar',
    // 此处只要稍微做一下改动，加一个this
    printName: function() {
        console.log(this.myName);
    }
}
var name = 'name in global';
bar.printName(); // name in bar
// 作用域和this
var bar = {
    myName: 'name in bar',
    // 这个例子可以证明this不可以继承
    printName: function() {
        function foo() {
            console.log(this.myName);
        }
        foo();
    }
}
var myName = 'name in global';
bar.printName(); // name in global
```

其他知识点：在全局环境中调用一个函数，函数内部的this指向window，通过一个对象调用其内部的方法则this指向该对象。

new的过程：创建空对象tempObj，调用call方法、把this指向该tempObj，执行函数内容，返回tempObj

3、我们常用的箭头函数是怎么回事？

this不可以继承的解决方案：使用一个变量保存this，或者使用箭头函数。

```js
// 保存变量
var bar = {
    myName: 'name in bar',
    printName: function() {
        var self = this;
        function foo() {
            console.log(self.myName);
        }
        foo();
    }
}
var myName = 'name in global';
bar.printName(); // name in bar
// ES6中的箭头函数不会创建自身的执行上下文
var bar = {
    myName: 'name in bar',
    printName: function() {
        var self = this;
        var foo = () => {
            console.log(self.myName);
        }
        foo();
    }
}
var myName = 'name in global';
bar.printName(); // name in bar
```
