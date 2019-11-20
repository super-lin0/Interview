本文收集了一些面试题目

## 基础

1、JavaScript 数组中有哪些迭代方法，分别代表什么意思
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

  为什么有人说闭包会导致性能问题

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

7、微任务和宏任务

```
/ 每办理完一个业务，柜员就会问当前的客户，是否还有其他需要办理的业务。（检查还有没有微任务需要处理）
// 而客户明确告知说没有事情以后，柜员就去查看后边还有没有等着办理业务的人。（结束本次宏任务、检查还有没有宏任务需要处理）
// Event Loop。
// 同步>异步，微任务>宏任务
console.log(1);

setTimeout(() => {
  console.log(2);
}, 0);  // 宏任务

// new Promise在实例化的过程中所执行的代码都是同步进行的();
// 而then中注册的回调才是异步执行的。
// 微任务
new Promise(resolve => {
  resolve();
  console.log(3);
}).then(_ => console.log(4));

console.log(5);
```

## React

1、如果我现在想要在 React 的生命周期中获取某个 dom 元素来做一些使，可以怎么做

componentDidMount + setTimeOut

componentDidUpdate

2、对 React 中间件有了解吗，谈谈它的原理以以及怎么实现一个中间件

3、React 中的 key 有什么用

## Vue

1、组件间通信

- 父组件 => 子组件
  props、\$attrs、引用 refs、 \$children

  (\$children 不保证顺序：为什么：可能会有异步组件)

- 子组件 => 父组件
  自定义事件（谁派发谁监听）

- 兄弟组件:通过共同祖辈组件
  （this.\$parent）

- 祖先和后代之间: provide/inject(只是正向的)

- 任意两个组件之间:事件总线（典型观察者模式） 或 vuex

2、 谈一谈 Vue 中的插槽

- 具名插槽
- 匿名插槽
- 作用域插槽(要显示的数据来自子组件)

3、响应式原理

4、用户在界面面修改了一个值，最终到 dom 更新，这个过程中发生了哪些事
用户在界面中修改值，触发 setter 函数，setter 触发 dep,dep 执行 notify 通知 watcher 更新，watcher 执行 updateComponent，updateComponent 需先 render，render 得到虚拟 dom，然后再执行\_update 得到最新的 dom 做更新

5、Vue 源码中实现依赖收集，实现了三个类：

Dep：扮演观察目标的角色，每一个数据都会有 Dep 类实例，它内部有个 subs 队列，subs 就是 subscribers 的意思，保存着依赖本数据的观察者，当本数据变更时，调用 dep.notify()通知观察者
Watcher：扮演观察者的角色，进行观察者函数的包装处理。如 render()函数，会被进行包装成一个 Watcher 实例
Observer：辅助的可观测类，数组/对象通过它的转化，可成为可观测数据

6、数据流双向绑定

## Webpack

3、提高首屏加载效率有哪些办法

**服务端渲染**

- 衍生
  1、服务端渲染有哪些实现方式，各有什么优缺点
  2、基于 Node.js 的同构应用都有什么生命周期（componentDidMount 及之后的都不会执行）

**代码切片**

- 衍生
  Webpack 提供了哪几种方式来实现代码切片（配置多个入口，抽取公有代码<CommontrunkPlugin、SplitChunk>）、动态加载(import、异步 chunk)

4、现在有一个基于 Webpack 打包的 Web 应用，页面层级嵌套的比较深，在开发过程当中，调试最内层的代码比较麻烦，有没有什么可以优化的地方，说说它的原理

HMR（模块热替换） 的核心就是客户端从服务器端拉取更新后的资源（准确地说，HMR 拉取的不是整个资源文件，而是 chunk diff,即 chunk 需要更新的部分）

## Git 使用

1、Git 提交规范

2、Git 工作流

## CSS

1、栅格布局 + Flex 布局优缺点
