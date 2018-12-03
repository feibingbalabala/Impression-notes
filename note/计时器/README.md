# 计时器

js 定时器有以下两个方法：

setInterval() ：按照指定的周期（以毫秒计）来调用函数或计算表达式。方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。

setInterval(code,millisec,lang)

code：必需。要调用的函数或要执行的代码串。

millisec：必须。周期性执行或调用 code 之间的时间间隔，以毫秒计。

lang：可选。 JScript | VBScript | JavaScript

```js
setInterval(function () {
  ...
}, 1000, 'JavaScript')
```

setTimeout() ：在指定的毫秒数后调用函数或计算表达式。

setTimeout(code,millisec,lang)

code：必需。要调用的函数后要执行的 JavaScript 代码串。

millisec：必需。在执行代码前需等待的毫秒数。

lang：可选。脚本语言可以是：JScript | VBScript | JavaScript

```js
setTimeout(function () {
  ...
}, 1000, 'JavaScript')
```

js单线程理解

```js
function show () {
  var i = 0;
  var timer = setInterval(function () {
    i++;
    console.log(i);
    setTimeout(function() {
      clearInterval(timer);
    }, 1000);
  }, 1);
};
show();
// 并不会输出1000，因为代码执行也需要时间，就导致了还没有执行到1000的时候就停止了
```