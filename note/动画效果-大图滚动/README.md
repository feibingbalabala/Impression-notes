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
// step1:分析效果，搭建结构和样式；
// step2:刷新页面，直接跳转到第二张图片；
//  outer.scrollLeft = 200;
// step3:点击跳转下一张；
//  outer.onclick = function(){outer.scrollLeft = 200;}
// step4:点击视口，滚动条向后滚动5px；
//  outer.scrollLeft += 5;
// step5:添加计时器，让图片滚动；
// step6:滚动到第二张，停止计时器；
// step7:常量改变量；
// step8:点击视口，滚动到第二张；
// step9:点击多次，计时器重叠，要清除(防叠加)；
// step10:单向运动要改变成双向运动；(获取当前位置，与目标进行对比，计算出最终要达到的位置，让滚动条到该位置)；
// step11:封装函数，改变点击事件的书写方式；
// step12:获取距离，计算速度/步长；
// setp13:target修改为参数；
// setp14:添加图片索引值，点击视口之后，跳到下一张；
// step15:将点击事件更换成计时器；
// step16:添加序号：
// 16.1通过循环、绑定事件’移动到点击图片序号位置;
// 16.2清除计时器timescr;
// 16.3重新启动计时器timescr；
// step17:封装循环滚动函数scroll；
// step18:添加左右按钮功能。
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
    }, 2000);
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