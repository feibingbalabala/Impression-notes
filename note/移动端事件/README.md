# 移动端事件

移动端的meta

```html
<meta name="viewport" content="width=device-width,initial-scale=1,user-scalable=no,maximum-scale=1,minimum-scale=1">
```

## 移动端和PC端的区别：键盘和手势

事件：

click事件在手机端会产生300ms的延迟，单机后还有双击缩放操作，这个涉及到触摸设备的手势交互行为为原生设计，设备通过事件判断，是单击事件。（有一个fastClick可以解决这个问题）

hover事件失效。（其实并不是失效，而是没有这个类型操作）。

触摸事件：

touchstart：当手指触摸屏幕时触发

touchmove：当手指从屏幕上滑动触发

touchend：当手指从屏幕移开触发

触摸属性：

touches：当前位于屏幕上的所有手指的列表。

```html
<div id='conTwo'></div>
<script type='text/javascript'>
  let conTwo = document.getElementById('conTwo');
  conTwo.addEventListener("touchstart", function(event){
    event.preventDefault();
    this.innerHTML = "touches当前屏幕" + event.touches.length;
  });
  conTwo.addEventListener("touchmove", function(event){
    event.preventDefault();
    this.innerHTML = "touches当前屏幕" + event.touches.length;
  });
  conTwo.addEventListener("touchend", function(event){
    event.preventDefault();
    this.innerHTML = "touches当前屏幕" + event.touches.length;
  });
  targetTouches：位于当前DOM元素上手指的列表
  conThree.addEventListener("touchstart", function(event){
    event.preventDefault();
    this.innerHTML = "targetTouches当前节点" + event.targetTouches.length;
  });
  conThree.addEventListener("touchmove", function(event){
    event.preventDefault();
    this.innerHTML = "targetTouches当前节点" + event.targetTouches.length;
  });
  conThree.addEventListener("touchend", function(event){
    event.preventDefault();
    this.innerHTML = "targetTouches当前节点" + event.targetTouches.length;
  });
  changedTouches：涉及当前事件的手指列表

  conOne.addEventListener("touchstart", function(event){
    event.preventDefault();
    this.innerHTML = "changedTouches涉及当前事件" + event.changedTouches.length;
  });
  conOne.addEventListener("touchmove", function(event){
    event.preventDefault();
    this.innerHTML = "changedTouches涉及当前事件" + event.changedTouches.length;
  });
  conOne.addEventListener("touchend", function(event){
    event.preventDefault();
    this.innerHTML = "changedTouches涉及当前事件" + event.changedTouches.length;
  });
</script>
```

identifier：手指的一个ID（触摸会话）是一个整数；

target ：目标，触发的函数

pageX：触摸点相当于页面左边位置

pagey：触摸点相当于页面上边位置

clientX：触摸点相当于浏览器视口左边位置

clientY：触摸点相当于浏览器视口上边位置

screenX：触摸点相当于屏幕左边位置

screenY：触摸点相当于屏幕上边位置

总结：page包含滚动距离：client不包含滚动距离，screen以屏幕为基准

## 向左滑动出现菜单栏

```html
<style>
html, body {
  height: 100%;
}
.wrap {
  /*position: relative;*/
  height: 100%;
  background: #000;
  color: #fff;
  font-size: 30px;
}
.box {
  position: absolute;
  left: -100px;
  width: 100px;
  height: 100%;
  background: #f00;
}
</style>
<body>
<div class="wrap" id="wrap">
  <div class="box" id="box"></div>
</div>
<script type="text/javascript" src="js/zepto.min.js"></script>
<script type="text/javascript" src="js/zepto-master/src/touch.js"></script>
<script>
var btn = document.getElementById('wrap');
var box = document.getElementById('box');
var disS = 0;
var disE = 0;
btn.addEventListener("touchstart", function(event) {
  // event.preventDefault();
  if (event.touches.length == 1) {
    disS = event.touches[0].clientX;
  };
}, false);
btn.addEventListener("touchmove", function(event) {
    if (event.touches.length == 1) {
      disE = event.touches[0].clientX;
  };
}, false);
btn.addEventListener("touchend", function(event) {
  // event.preventDefault();
  var res = disE - disS;
  console.log(res)
  if (res >= 100 ) {
    console.log('a')
    box.style.left = "0px";
    btn.style.marginLeft = "100px";
  } else {
    box.style.left = "-100px";
    btn.style.marginLeft = "0px";
  };
}, false);
</script>
```