本文收集了一些面试题目

## 基础

1、JavaScript 数组中有哪些迭代方法，分别有代表什么意思
map、filter、every、some、forEach

- 衍生问题
  怎么样去实现一个自己的 map 方法
  ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10"].map(parseInt)

  ```
  const map = (array, fn) => {
    let result = [];
    for (let i of array) {
      result.push(fn(i));
    }
    return result;
  };
  ```

2、谈一谈你理解的闭包

- 函数在被调用的时候还保持着该函数在声明时所拥有的作用域链

- 闭包就是能够读取其他函数内部变量的函数；定义在一个函数内部的函数；闭包就是将函数内部和函数外部连接起来的一座桥梁。

```
var sayName = function() {
  var name = 'My Object'

  return function() {
    return function() {
      return function() {
        console.log('name', name) // My Object 产生闭包，在调用的时候持有该函数的作用域链
      }
    }
  }
}
sayName()()()()
```

3、 谈谈你对 JavaScript 作用域链的理解

4、有哪些办法可以实现异步编程

回调函数、事件监听、发布/订阅、Promise 对象

5、请解释以下变量声明提升

6、ES6 里面数组去重可以怎么玩
（Array.from(new Set(arr))、[...new Set(arr)]）

## React

1、如果我现在想要在 React 的生命周期中获取某个 dom 元素来做一些使，可以怎么做

componentDidMount + setTimeOut

componentDidUpdate

2、对 React 中间件有了解吗，谈谈它的原理以以及怎么实现一个中间件

## Webpack

3、提高首屏加载效率有哪些办法

**服务端渲染**

- 衍生
  1、服务端渲染有哪些实现方式，各有什么优缺点
  2、基于 Node.js 的同构应用都有什么生命周期（componentDidMount 及之后的都不会执行）

**代码切片**

- 衍生
  Webpack 提供了哪几种方式来实现代码切片（配置多个入口，抽取公有代码<CommontrunkPlugin、SplitChunk>）、动态加载(import、异步 chunk)

4、现在又一个基于 Webpack 打包的 Web 应用，页面层级嵌套的比较深，在开发过程当中，调试最内层的代码比较麻烦，有没有什么可以优化的地方，说说它的原理

HMR（模块热替换） 的核心就是客户端从服务器端拉取更新后的资源（准确地说，HMR 拉取的不是整个资源文件，而是 chunk diff,即 chunk 需要更新的部分）

## Git 使用

1、Git 提交规范

2、Git 工作流
