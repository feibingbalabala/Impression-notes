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

## 实现一次滚动

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>大图滚动</title>
  <style>
    div, ul {
      list-style: none;
    }
    .wrap {
      overflow: scroll;
      width: 200px;
      height: 310px;
      margin: 50px auto 0;
      border: 1px solid #f00;
    }
    .con {
      width: 1000px;
      height: 310px;
    }
    .con div {
      float: left;
      width: 200px;
      height: 310px;
    }
    .list {
      width: 350px;
      height: 50px;
      margin: 0 auto;
    }
    .list li {
      float: left;
      width: 50px;
      height: 50px;
      line-height: 50px;
      font-size: 24px;
      text-align: center;
      cursor: pointer;
    }
    .bg-green {
      background-color: green;
    }
    .bg-black {
      background-color: black;
    }
    .bg-red {
      background-color: red;
    }
    .bg-pink {
      background-color: pink;
    }
    .bg-blue {
      background-color: blue;
    }
  </style>
</head>
<body>
<!-- 	注意：子级的宽度需要大于父级的宽度
		  采用几张图片，跟无缝滚动有什么区别？ -->
<!-- img中的title添加索引值，方便调试 -->
  <div class="wrap" id="outer">
    <div class="con" id="inner">
      <div class="bg-green"></div>
      <div class="bg-black"></div>
      <div class="bg-red"></div>
      <div class="bg-pink"></div>
      <div class="bg-blue"></div>
    </div>
  </div>
  <ul class="list" id="btn">
    <li>←</li>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>→</li>
  </ul>
  <script>
    // 获取标签
    var outerBox = document.getElementById("outer");
    var innerBox = document.getElementById("inner");
    var btns = document.getElementById("btn").getElementsByTagName("li");
    var timer = null;

    function startMove(endPos) {
      // 获取起点
      var startPos = outerBox.scrollLeft;
      var speed;

      if (timer) {
        clearInterval(timer);
      };
      timer = setInterval(move, 20); 

      /*
        * [move 缓冲运动函数]
        * @return {[type]} [无返回值]
        */
      function move() {
        // 起点与终点的距离不需要添加绝对值 0~200或者 200~0
        speed = (endPos - startPos) / 10;
        startPos += speed;

        // 输出步长，发现步数存在多位小数点
        console.log(speed);

        // 起点到达终点清除计时器
        if (startPos == endPos) {
          clearInterval(timer);
        };

        outerBox.scrollLeft = startPos;
      }
    }
    startMove(600);
  </script>
</body>
</html>
```

## 利用两个计时器和索引值

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>大图滚动</title>
  <style>
    div, ul {
      list-style: none;
    }
    .wrap {
      overflow: hidden;
      width: 200px;
      height: 310px;
      margin: 50px auto 0;
      border: 1px solid #f00;
    }
    .con {
      width: 1000px;
      height: 310px;
    }
    .con div {
      float: left;
      width: 200px;
      height: 310px;
    }
    .list {
      width: 350px;
      height: 50px;
      margin: 0 auto;
    }
    .list li {
      float: left;
      width: 50px;
      height: 50px;
      line-height: 50px;
      font-size: 24px;
      text-align: center;
      cursor: pointer;
    }
    .bg-green {
      background-color: green;
    }
    .bg-black {
      background-color: black;
    }
    .bg-red {
      background-color: red;
    }
    .bg-pink {
      background-color: pink;
    }
    .bg-blue {
      background-color: blue;
    }
  </style>
</head>
<body>
<!-- 	注意：子级的宽度需要大于父级的宽度
      采用几张图片，跟无缝滚动有什么区别？ -->
  <div class="wrap" id="outer">
    <div class="con" id="inner">
      <div class="bg-green"></div>
      <div class="bg-black"></div>
      <div class="bg-red"></div>
      <div class="bg-pink"></div>
      <div class="bg-blue"></div>
    </div>
  </div>
  <ul class="list" id="btn">
    <li>←</li>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>→</li>
  </ul>
  <script>
    // 获取标签
    var outerBox = document.getElementById("outer");
    var innerBox = document.getElementById("inner");
    var btns = document.getElementById("btn").getElementsByTagName("li");

    var timer = null;
    var timerIndex	= null;
    var index 		= 0 ;

    /*
      * [大图滚动函数]
      * @param  {[type]} endPos [description]
      * @return {[type]}        [description]
      */
    function startMove(endPos) {
      // 获取起点
      var startPos = outerBox.scrollLeft;
      var speed;

      if (timer) {
        clearInterval(timer);
      };
      timer = setInterval(move, 20); 

      /*
        * [move 缓冲运动函数]
        * @return {[type]} [无返回值]
        */		
      function move() {
        // 起点与终点的距离不需要添加绝对值 0~200或者 200~0
        speed = (endPos - startPos) / 10;
        speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);
        startPos += speed;

        // 输出步长
        console.log(speed);

        // 实现自动贴合
        if (Math.abs(endPos - startPos) <= 6) {
          startPos = endPos;
          // 清除计时器
          clearInterval(timer);
        };

        outerBox.scrollLeft = startPos;
      }
    }

    /*
      * [利用索引值实现多次滚动]
      * @return {[type]} [description]
      */
    function indexChange() {
      index++;
      if (index == 5) {
        index = 0;
      };
      startMove(index * 200);
    }

    timerIndex = setInterval(indexChange, 3000);
  </script>
</body>
</html>
```

## 添加序号控制

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>大图滚动</title>
  <style>
    div, ul {
      list-style: none;
    }
    .wrap {
      overflow: hidden;
      width: 200px;
      height: 310px;
      margin: 50px auto 0;
      border: 1px solid #f00;
    }
    .con {
      width: 1000px;
      height: 310px;
    }
    .con div {
      float: left;
      width: 200px;
      height: 310px;
    }
    .list {
      width: 350px;
      height: 50px;
      margin: 0 auto;
    }
    .list li {
      float: left;
      width: 50px;
      height: 50px;
      line-height: 50px;
      font-size: 24px;
      text-align: center;
      cursor: pointer;
    }
    .bg-green {
      background-color: green;
    }
    .bg-black {
      background-color: black;
    }
    .bg-red {
      background-color: red;
    }
    .bg-pink {
      background-color: pink;
    }
    .bg-blue {
      background-color: blue;
    }
  </style>
</head>
<body>
<!-- 	注意：子级的宽度需要大于父级的宽度
		  采用几张图片，跟无缝滚动有什么区别？ -->
  <div class="wrap" id="outer">
    <div class="con" id="inner">
      <div class="bg-green"></div>
      <div class="bg-black"></div>
      <div class="bg-red"></div>
      <div class="bg-pink"></div>
      <div class="bg-blue"></div>
    </div>
  </div>
  <ul class="list" id="btn">
    <li>←</li>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>→</li>
  </ul>
  <script>
    // 获取标签
    var outerBox = document.getElementById("outer");
    var innerBox = document.getElementById("inner");
    var btns = document.getElementById("btn").getElementsByTagName("li");
    var len = btns.length;

    var timer = null;
    var timerIndex = null;
    var index = 0 ;

    /*
      * [大图滚动函数]
      * @param  {[type]} endPos [description]
      * @return {[type]}        [description]
      */
    function startMove(endPos) {
      // 获取起点
      var startPos = outerBox.scrollLeft;
      var speed;

      if (timer) {
        clearInterval(timer);
      };
      timer = setInterval(move, 20); 

      /*
      * [move 缓冲运动函数]
      * @return {[type]} [无返回值]
      */
      function move() {
        // 起点与终点的距离不需要添加绝对值 0~200或者 200~0
        speed = (endPos - startPos) / 10;
        speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);
        startPos += speed;

        // 输出步长
        console.log(speed);

        // 实现自动贴合
        if (Math.abs(endPos - startPos) <= 6) {
          startPos = endPos;
          // 清除计时器
          clearInterval(timer);
        };

        outerBox.scrollLeft = startPos;
      }
    }

    /*
      * [利用索引值实现多次滚动]
      * @return {[type]} [description]
      */
    function indexChange() {
      index++;
      if (index == 5) {
        index = 0;
      };
      startMove(index * 200);
    }

    timerIndex = setInterval(indexChange, 3000);

    // 添加序号功能
    for (var i = 1; i < len; i++) {
      btns[i].onclick = function(num) {
        return function() {
          // 清除计时器
          clearInterval(timerIndex);
          // 序号的索引要与自动滚动的索引保持一致
          index = num -1;
          startMove(index * 200);
          // 再次启动计时器
          timerIndex = setInterval(indexChange, 3000);
        }
      }(i);
    };

  </script>
</body>
</html>
```

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>大图滚动</title>
  <style>
    div, ul {
      list-style: none;
    }
    .wrap {
      width: 200px;
      margin: 0 auto;
      overflow: auto;
    }
    .box {
      width: 800px;
    }
    .box img {
      display: block;
      float: left;
      width: 200px;
      height: 300px;
    }
    .foot {
      width: 200px;
      margin: 10px auto 0;
      padding-left: 8px;
    }
    input[type = "button"] {
      width: 28px;
      height: 28px;
    }
    .bg-green {
      background-color: green;
    }
    .bg-black {
      background-color: black;
    }
    .bg-red {
      background-color: red;
    }
    .bg-pink {
      background-color: pink;
    }
    .bg-blue {
      background-color: blue;
    }
  </style>
</head>
<body>
  <div class="wrap" id="outer">
    <div class="box" id="inner">
      <div class="bg-green"></div>
      <div class="bg-black"></div>
      <div class="bg-red"></div>
      <div class="bg-pink"></div>
    </div>
  </div>
  <div class="foot" id="button">
    <input type="button" value="左">
    <input type="button" value="1">
    <input type="button" value="2">
    <input type="button" value="3">
    <input type="button" value="4">
    <input type="button" value="右">
  </div>
  <script type="text/javascript">
  // step1:分析效果，搭建结构和样式；
  // step2:刷新页面，直接跳转到第二张图片；
  //    outer.scrollLeft = 200;
  // step3:点击跳转下一张；
  //    outer.onclick = function(){outer.scrollLeft = 200;}
  // step4:点击视口，滚动条向后滚动5px；
  //    outer.scrollLeft += 5;		
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
  //    16.1通过循环、绑定事件’移动到点击图片序号位置;
  //    16.2清除计时器timescr;
  //    16.3重新启动计时器timescr；
  // step17:封装循环滚动函数scroll；
  // step18:添加左右按钮功能。
  var outer = document.getElementById("outer");
  var box = document.getElementById("inner");
  var btn = document.getElementById("button").getElementsByTagName("input");
  //获取控制按钮；
  // var target = 200; //目标值
  var timer = null; // 图片滚动计时器
  var timescr = null;// 自动更换图片计时器；
  var index = 0; // 图片的序号；

  //一张一张滚动的函数；
  function scroll(){
    timescr = setInterval(function () {//隔多久走一次
      index++;
      if (index >= 4) {
        index = 0;
    }
    move(index * 200);
    },1000);
  }
  scroll();//调用该函数刷新页面即自动更换图片；

  // 添加序号控制：
  for (var i = 1; i < btn.length; i++) {
    btn[i].index = i - 1;
    btn[i].onclick = function () {
      if (timescr) {
        clearInterval(timescr);
      }
      index = this.index;
      move(this.index * 200);
      scroll();//重新唤起计时器，更换图片；
    }
  };

  //左按钮：
  btn[0].onclick = function(){
    if (timescr) {
      clearInterval(timescr);
    }
    index--;
    if(index < 0){
      index = 3;
    }
    move(index * 200);
    scroll();
  }
  //右按钮:
  btn[5].onclick = function(){
    if (timescr) {
      clearInterval(timescr);
    }
    index++;
    if(index >= 4){
      index = 0;
    }
    move(index * 200);
    scroll();
  }

  // 刷新页面产生滚动效果：
  function move(target){
    if (timer) {
      clearInterval(timer);
    }
    var start = outer.scrollLeft; //获取开始位置；
    // Math.abs();取绝对值；
    var distance = Math.abs(target - start); //获取路程绝对值；
    var speed = distance / 20; //获取改变的速度
    timer = setInterval(function () {
      if (start < target) {
    //初始位置小于目标值，继续+speed滚动;到了大于或等于，就清除计时器，并且目标位置等于初始位置，产生新的初始位置；
        start +=speed;
        if (start >= target) {
          clearInterval(timer);
          start = target;
        }
      }else {
        start -= speed;
        if(start <= target){
          clearInterval(timer);
          start = target;
        }
      }
      outer.scrollLeft = start;//为新的初始位置赋值；
    },17);
  }
  </script>
</body>
</html>
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