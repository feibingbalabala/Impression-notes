# js执行机制

```js
setTimeout(function(){
  console.log('1')
});
new Promise(function(resolve){
  console.log('2');
  for(var i = 0; i < 10000; i++){
      i == 99 && resolve();
  }
}).then(function(){
  console.log('3')
});
console.log('4');
```

结果是2431

## 事件循环

js是单线程，那就像一辆公交车，乘客只能从前门上，同理js任务也要一个一个顺序执行。如果一个任务耗时过长，那么后一个任务也必须等着。那么问题来了，假如我们想浏览新闻，但是新闻包含的超清图片加载很慢，难道我们的网页要一直卡着直到图片完全显示出来？因此出现了两种任务：

1. 同步任务
2. 异步任务

当我们打开网站时，网页的渲染过程就是一大堆同步任务，比如页面骨架和页面元素的渲染。而像加载图片音乐之类占用资源大耗时久的任务，就是异步任务。

1. 同步任务和异步任务分别进入不同的地方，同步的进入主线程，异步的进入Event Table并注册函数。
2. 当指定的事情完成时，Event Table会将这个函数移入Event Queue。
3. 主线程内的任务执行完毕为空，会去Event Queue读取对应的函数，进入主线程执行。
4. 上述过程会不断重复，也就是常说的Event Loop(事件循环)。

### 主线程为空

js引擎存在monitoring process进程，会持续不断的检查主线程执行栈是否为空，一旦为空，就会去Event Queue那里检查是否有等待被调用的函数。

### ajax请求

```js
$ajax({
  url: '',
  data: [],
  success: function () {
    console.log(1)
  }
})
console.log(2)
```

1. ajax进入Event Table，注册回调函数success
2. 执行console.log(2)
3. ajax执行完毕后，success进入Event Queue
4. 主线程Event Queue执行success

### 计时器setTimeout

```js
setTimeout(test() {
  console.log(1)
}, 3000)
console.log(2);
```

1. setTimeout是异步的，进入Event Table，注册内部的函数test
2. 执行console.log(2)
3. setTimeout执行完毕后，test进入Event Queue
4. 主线程Event Queue执行test

```js
setTimeout(() => {
  console.log(1)
}, 3000)
sleep(10000)
console.log(2)
```

1. console.log(1)进入Event Table并注册,计时开始。
2. 执行sleep函数，很慢，非常慢，计时仍在继续。
3. 3秒到了，计时事件timeout完成，console.log(1)进入Event Queue，但是sleep也太慢了吧，还没执行完，只好等着。
4. sleep终于执行完了，console.log(1)终于从Event Queue进入了主线程执行

setTimeout这个函数，是经过指定时间后，把要执行的任务(本例中为console.log(1))加入到Event Queue中，又因为是单线程任务要一个一个执行，如果前面的任务需要的时间太久，那么只能等着，导致真正的延迟时间远远大于3秒。
我们还经常遇到setTimeout(fn, 0)这样的代码，0秒后执行又是什么意思呢？是不是可以立即执行呢？
答案是不会的，setTimeout(fn, 0)的含义是，指定某个任务在主线程最早可得的空闲时间执行，意思就是不用再等多少秒了，只要主线程执行栈内的同步任务全部执行完成，栈为空就马上执行。举例说明：

```js
//代码1
console.log('1');
setTimeout(() => {
  console.log('2')
}, 0);复制代码
//先执行这里
//执行啦

//代码2
console.log('3');
setTimeout(() => {
  console.log('4')
}, 3000);
//先执行这里
// ... 3s以后
// 执行啦
```

关于setTimeout要补充的是，即便主线程为空，0毫秒实际上也是达不到的。根据HTML的标准，最低是4毫秒

### 计时器setInterval

setInterval循环的执行。对于执行顺序来说，setInterval会每隔指定的时间将注册的函数置入Event Queue，如果前面的任务耗时太久，那么同样需要等待。

唯一需要注意的一点是，对于setInterval(fn,ms)来说，我们已经知道不是每过ms秒会执行一次fn，而是每过ms秒，会有fn进入Event Queue。一旦setInterval的回调函数fn执行时间超过了延迟时间ms，那么就完全看不出来有时间间隔了

### promise

macro-task(宏任务)：包括整体代码script，setTimeout，setInterval

micro-task(微任务)：Promise

不同类型的任务会进入对应的Event Queue，比如setTimeout和setInterval会进入相同的Event Queue。

事件循环的顺序，决定js代码的执行顺序。进入整体代码(宏任务)后，开始第一次循环。接着执行所有的微任务。然后再次从宏任务开始，找到其中一个任务队列执行完毕，再执行所有的微任务。

```js
setTimeout(function() {
  console.log(1);
})
new Promise(function(resolve) {
  console.log(2);
}).then(function() {
  console.log(3);
})
console.log(4);
```

1. 这段代码作为宏任务，进入主线程。
2. 先遇到setTimeout，那么将其回调函数注册后分发到宏任务Event Queue。
3. 接下来遇到了Promise，new Promise立即执行，then函数分发到微任务Event Queue。
4. 遇到console.log()，立即执行。
5. 整体代码script作为第一个宏任务执行结束，then在微任务Event Queue里面，执行。
6. 第一轮事件循环结束了，我们开始第二轮循环，当然要从宏任务Event Queue开始。我们发现了宏任务Event Queue中setTimeout对应的回调函数，立即执行。
7. 结束。

## 分析

```js
console.log('1');

setTimeout(function() {
  console.log('2');
  new Promise(function(resolve) {
    console.log('3');
    resolve();
  }).then(function() {
    console.log('4')
  })
})
new Promise(function(resolve) {
  console.log('5');
  resolve();
}).then(function() {
  console.log('6')
})

setTimeout(function() {
  console.log('7');
  new Promise(function(resolve) {
    console.log('8');
    resolve();
  }).then(function() {
    console.log('9')
  })
})
```

1. 执行console.log(1)
2. setTimeout回调函数注册后分发到宏任务Event Queue
3. 执行promise中console.log(5)，then被分发到微任务Event Queue中
4. setTimeout回调函数注册后分发到宏任务Event Queue
5. 宏任务执行完毕
6. 执行console.log(6)
7. 执行第一个setTimeout2、3、4
8. 执行第二个setTimeout7、8、9

## js的异步

javascript是一门单线程语言，不管是什么新框架新语法糖实现的所谓异步，其实都是用同步的方法去模拟的，这点一定要记住，不要随意就被误导。

## 事件循环Event Loop

事件循环是js实现异步的一种方法，也是js的执行机制。

## javascript的执行和运行

执行和运行有很大的区别，javascript在不同的环境下，比如node，浏览器等等，执行方式是不同的。而运行大多指javascript解析引擎，是统一的。
