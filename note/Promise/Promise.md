# Promise

## 函数对象与实例对象

函数对象：将函数作为对象使用时，简称函数对象
实例对象：new 函数产生的对象，简称对象

```js
function Fn() { //Fn函数
}
const fn = new Fn() // Fn是构造函数，fn是实例对象，简称对象
console.log(Fn.prototype) // Fn是函数对象
Fn.bind({}) //改变this，返回新的对象
Fn.call({}) // 改变this，并立即执行
```

## 两种类型的回调函数

### 同步回调

理解：立即执行，完全执行完了才结束，不会放入回调队列中
例子：数组遍历相关的回调函数 / Promise的excurot

```js
const arr = [1, 2, 3];
arr.forEach((item) => {
    console.log(item)
})
console.log('forEach()之后');
// 1
// 2
// 3
// forEach()之后
```

### 异步回调

理解：不会立即执行，会放入回调队列中将来执行
例子：定时器回调 / ajax回调 / Promise的成功、失败的回调

```js
setTimeout(() => {
    console.log('timeout callback()')
}, 0);
console.log('setTimeout之前')
// setTimeout之前
// timeout callback()
```

### Promise表达

异步编程的解决方案（过去是回调函数）

从语法上来说他是一个构造函数，从功能来说他是用来封装一个异步操作并可以获取其结果

一个Promise对象只有三种状态：等待态（pending）成功态（resolved）和失败态（rejected）

### 为什么要用Promise

指定回调函数的方式更加灵活：

旧：必须在启动异步任务前指定

给Promise: 启动异步任务，返回promise对象 => 给Promise对象绑定回调函数（可以是异步之后结束后指定）

```js
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        const time = Date.now()
        if (time % 2 === 0) {
            resolve('偶数')
        } else {
            reject('奇数')
        }
    }, 1000)
})
setTimeout(() => {
    p.then(value => {
        console.log('成功', value)
    },
    reason => {
        console.log('失败', reason)
    })
}, 2000)
````

支持链式调用，可以解决回调地狱问题

回调函数嵌套，不易于阅读

### PromiseAPI

1 Promise的构造函数: Promise(excutor) {}
    excutor函数：同步执行 （resolve, reject） => {}
    resolve函数：内部定义成功时调用的函数 value => {}
    reject函数：内部定义失败时调用的函数 reason => {}
    说明：excutor会在Promise内部立即同步回调，异步操作在执行器重执行

2 Promise.prototype.then方法:(onResolved, onRejected) => {}
    onResolved函数：成功的回调函数（value） => {}
    onRejected函数：失败的回调函数（reason） => {}
    说明：指定用于得到成功value的成功回调和用于得到失败reason的失败回调返回一个新的pormise对象
3 Promise.prototype.catch方法：(onRejected) => {}
    onRejected函数：失败的回调函数（reason）=> {}
    说明then()的语法糖， 相当于then(undefined, onRejected)
4 Promise.resolve方法：(value) => {
    value: 成功的数据或promise对象
    说明：放回一个成功或失败的promise对象
}
5 Promise.reject方法：(reason) => {
    reason: 失败的元婴
    说明：放回一个失败的promise对象
}
6 Promise.all方法：(promises) => {}
    promises: 包含n个promise的数组
    说明，返回一个新的promise，只有所有promise都成功才成功。只要有一个失败了就直接失败。
7 Promise.race方法：(promises) =>{}
    promises: 包含n个promise的数组
    说明，返回一个新的promise，第一个完成的promise就是最终结果

8 Promise.then返回的新promise结果由1、then()指定的回调函数执行的结果决定，2、如果抛出异常，新promise变为rejected，reason为抛出的异常。2如果放回非promise的人一直，新promise变为resovled，value为返回值，3、返回新的promise，此promise的结果就是新的promise的结果

9 如果需要中断promise的then()或catch()操作执行就 return new Promise(() => {})让这个promise处于pending状态，结合上一点。promise的结果由返回的决定。
