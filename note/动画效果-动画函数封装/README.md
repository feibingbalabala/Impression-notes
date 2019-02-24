# 动画函数封装

1. 实现瞬间动画
2. 获取目标
3. 点击控制运动函数、
4. 设置变化速度
5. 利用计时器代替点击控制
6. 有停止的运动
7. 防止计时器重复问题
8. 双方向运动
9. 实现缓冲运动
10. 处理缓冲运动的问题
11. 实现近距离自动贴合
12. 多物体同时运动问题
13. 优化多物体运动
14. 多物体多属性运动
15. 透明度属性的处理
16. 实现链式运动

## 取得标签的css属性

```js
var box = document.getElementById('box');
// 只能获得标签内写入的样式
var marginLeft = box.style.marginLeft;
// 获取标签内的属性(括号内第一个值是Id，第二个值一般是null，或者是after，before伪元素)
var width = window.getComputedStyle(box, null).width;
```

## ie和chrome浏览器的不同

```js
function getStyle(prop) {
  if (box.currentStyle) {
    console.log(wrap.currentStyle[prop])
  } else {
    console.log(window.getComputedStyle(wrap, null)[prop])
  };
};
getStyle('style');
```

## 数学公式

|方法|描述|
|--|--|
|abs(x)|返回数的绝对值|
|acos(x)|返回数的反余弦值|
|asin(x)|返回数的反正弦值|
|atan(x)|以介于-PI/2与PI/2弧度之间的数值来返回x的反正切值|
|atan2(y, x)|返回从x轴到点(x, y)的角度（介于-PI/2与PI/2弧度之间）|
|ceil(x)|对数进行上舍入|
|cos(x)|返回数的余弦值|
|exp(x)|返回e的指数|
|floor(x)|对数进行下舍入|
|log(x)|返回数的自然对数(底为e)|
|max(x, y)|返回x和y中的最大值|
|min(x, y)|返回x和y中的最小值|
|pow(x, y)|返回x的y次幂|
|random()|返回0~1之间的随机数|
|sin(x)|返回数的正弦值|
|sort(x)|返回数的平方根|
|tan(x)|返回角的正切值|
|toSource()|返回该对象的源代码|
|valueOf()|返回Math对象原始值|

## 遍历一个对象

```js
var obj = {
  'name': 'jwy',
  'age': 10
};
for (var prop in obj) {
  console.log(prop);
  console.log(obj.[prop]);
}
```

## 回调函数

执行一个函数后在执行下一个函数

## 动画效果封装

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<style>
  .wrap {
    width: 500px;
    height: 500px;
    border: 1px solid #000;
  }
</style>
<body>
<div id='wrap' class="wrap"></div>
<script type='text/javascript'>
  function change(ele, obj, changeStep, fn) {
    if (ele.timer) {
      clearInterval(ele.timer);
    };
    ele.timer = setInterval(sport, 20);
    function sport () {
      var flag = true;
      for (var prop in obj) {
        var startVal = 0;
        if (prop === 'opacity') {
          startVal = parseInt(getStyle(ele, prop) * 100);
        } else {
          startVal = parseInt(getStyle(ele, prop));
        };
        var distance = Math.abs(obj[prop] - startVal);
        if (prop === 'opacity') {
          var speed = Math.ceil(distance / changeStep);
          if (speed === 1) {
            speed = 2;
          };
        } else {
          var speed = Math.ceil(distance / changeStep);
        };
        if (startVal < obj[prop]) {
          startVal += speed;
        } else {
          startVal -= speed;
        }
        if (distance <= 5) {
          startVal = obj[prop];
        } else {
          flag = false;
        };
        if (prop === 'opacity') {
          ele.style[prop] = startVal / 100;
          ele.style['filter'] = 'alpha(opacity='+ startVal +')';
        } else {
          ele.style[prop] = startVal + 'px';
          // 这里的属性不能用.属性，因为这样会被认为是一个字符串
        };
      };
      if (flag) {
        clearInterval(ele.timer);
        if (fn) {
          fn(); // 执行回调函数，先判断有无回调函数，否则会报错。
        };
      };
    };
  };
  function getStyle(ele, prop) {
    if (ele.currentStyle) {
      return ele.currentStyle[prop];
    } else {
      return getComputedStyle(ele, null)[prop];
    };
  };
  var wrap = document.getElementById('wrap');
  change(wrap, {'width': '200'}, 3)
</script>
</body>
</html>
```