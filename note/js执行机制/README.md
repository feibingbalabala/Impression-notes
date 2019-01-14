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

### 计时器

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