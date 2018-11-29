# 动画效果

1. 实现基本的结构样式，以方便JS代码的实现，
2. 实现获取标签绑定事件控制样式的基本功能，
3. 利用计时器实现动画的持续性变化，
4. 利用if语句控制临界值在临界值执行相应操作,
5. 代码优化

## 计时器

setInterval：执行多次 ，精确度比setTimeout低

setTimeout：执行一次，精确度比setInterval高

```js
setInterval(function() {
  ...
}, 1000)
setTimeout(function() {
  ...
}, 1000)
// 最后的数字是时间，毫秒单位
```

记时器的使用要注意清除计时器(clearInterval())，否则会导致内存溢出。

## 无缝滚动

scrollLeft | scrollTop

设置或获取位于对象最顶端左端和窗口中可见内容的最顶和最左端之间的距离。即当前上滚或左滚的距离。

scrollHeight | scrollWidth

获取对象可滚动的总高度、宽度

offsetLeft | offsetTop

获取当前对象与相对父元素之间的距离（不包含父元素的边框）

offsetWidth | offsetHeight

获取元素自身的宽度、高度(border + padding + width/height)

clientLeft | clientTop

效果和边框宽度相同，很少使用

clientWidth | clinentHeight

不含边框元素的自身高度、宽度

```js
var speed = 5;
var timer = setInterval(function() {
  main.scrollLeft += speed;
  if (speed > 0 && main.scrollLeft === 800) {
    main.scrollLeft = 0;
  };
  if (speed < 0 && main.scrollLeft === 0) {
    main.scrollLeft = 800;
  };
}, 17);

// 每2秒后停止
var timerScroll = null;
var timer = setInterval(stop, 10);
function stop() {
  main.scrollLeft += 5;
  if (main.scrollLeft >= main.clientWidth) {
    main.scrollLeft = 0;
  };
  if (main.scrollLeft % 200 === 0) {
    clearInterval(timer);
    timerScroll = setTimeout(function() {
      timer = setInterval(stop, 20);
    }, 200);
  };
};
```

## 兼容

document.documentElement;获取HTmL标签

document.body;获取body标签

google 在body里面

firefox在HTML里面

```js
var topval = document.body.scrollTop || document.documentElement.scrollTop;
```

## 重力反弹

```js
var main = document.getElementById('main');
var ball = document.getElementById('ball');
var posX = 0;
var posY = 0;
var moveX = true;
var moveY = true;
var timer = setInterval(function() {
  parseInt(posX);
  parseInt(posY);
  if (moveY) {
    posY += 50;
    if (posY >= main.clientWidth - ball.offsetWidth) {
      posY = main.clientWidth - ball.offsetWidth;
      moveY = false;
    };
  } else {
    posY -= 50;
    if (posY <= 0) {
      posY = 0;
      moveY = true;
    };
  };
  if (moveX) {
    posX += 50;
    if (posX >= main.clientHeight - ball.offsetHeight) {
      posX = main.clientHeight - ball.offsetHeight;
      moveX = false;
    };
  } else {
    posX -= 50;
    if (posY <= 0) {
      posX = 0;
      moveX = true;
    };
  };
  ball.style.top = posX + 'px';
  ball.style.left = posY + 'px';
}, 200)

```