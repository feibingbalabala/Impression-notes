# 移动端理解

## 横向px纵向px(2012年之前)

屏幕分辨率320*480，横向px纵向px

## 响应式布局(2013年)

响应式布局（跨平台）

1. 视口（viewport）控制；
2. 根据不同的分辨率加载不同的样式（css3媒体查询）；
3. 用相对单位来代替绝对单位（%>盒模型的px、em>字体的px）

```html
<meta name="viewport" content="width=device-width">
<!--等于设备宽度-->
<meta name="viewport" content="width=device-width,initial-scale=1,user-scalable=no,maximum-scale=1,minimum-scale=1">
<!--不能放大或者缩小,视口和窗体大小一样-->
<!--width=device-width ：表示宽度是设备屏幕的宽度-->

<!--initial-scale=1.0：表示初始的缩放比例-->

<!--minimum-scale=1.0：表示最小的缩放比例-->

<!--maximum-scale=1.0：表示最大的缩放比例-->

<!--user-scalable=no：表示用户是否可以调整缩放比例-->

<style>
@media(min-width: 1024px) {
  .box {
    background-color: #ccc;
  }
}
@media(max-width: 1024px) and (min-width: 640px) {
  .box {
    background-color: green;
  }
}
</style>
<link rel="stylesheet" type="text/css" media="screen and (max-width: 640px)" href="">
<!--断点：用于分割不能使用分辨率控制的样式，根据需求而定，通常480px、768px、1024px、均是断点-->
```

## 横向百分比；纵向px

对于img会出现图片的拉伸，视觉的不舒服

## 横向百分比，纵向百分比

盒模型百分比

width：父级的width

height：父级的height

margin、padding：父级的width

line-height设置百分比是根据当前标签字体大小进行计算的

## 横向em 纵向em

em更具当前元素字体大小进行计算

## 横向百分比，纵向em

## 横向百分比，纵向rem

rem根据html标签里的字体大小，横向纵向使用rem

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .box {
      height: 1rem;
      font-size: 0.5rem;
      background-color: #cfc;
    }
  </style>
</head>
<body>
  <div class="box">字体大小</div>
  <script>
    // 原理
    function rf () {
      let scale = 24 / 640;// 算出psd的最佳字体展示：24是字体 640是设计图的宽度，得到需要缩放的比例
      let rootFont = scale * document.body.offsetWidth; // 根据屏幕宽度 * 比例得到字体
      document.getElementsByTagName('html')[0].style.fontSize = rootFont + 'px';
    }
    rf()
    window.onresize = rf
    // 常见方式(使用需注释上方代码)
    (function (doc, win) {
      var docEl = doc.documentElement,
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
        recalc = function () {
          var clientWidth = docEl.clientWidth;
          var screenWidth = 750;
          if (!clientWidth) return;
          if (clientWidth >= screenWidth) {// 这里做了屏幕最大值的判断，避免因为屏幕宽度过宽导致页面变得十分巨大
            docEl.style.fontSize = '100px';
          }else{
            docEl.style.fontSize = 100 * (clientWidth / screenWidth) + 'px';
          }
        };

      if (!doc.addEventListener) return;
      win.addEventListener(resizeEvt, recalc, false);
      doc.addEventListener('DOMContentLoaded', recalc, false);
    })(document, window);
  </script>
</body>
</html>
```

rem兼容性ie9以上

ie9~ie11的：after和：before伪元素的line-height不支持rem

华为Mete7、魅族4不支持横向rem

这里做个补充：rem和em没有什么好坏之分，rem是根据HTML元素的字体大小，而em 单位基于使用他们的元素的字体大小。em 单位可能受任何继承的父元素字体大小影响。使用rem可以用统一的根字体作为所有页面高度的基准值；使用em只能根据父亲字体的高度，一旦出现字体调整所有的盒模型高度都要调整，

其实上面的布局也没有什么好坏之分，只有用的方便和公司的选择而已，

## 移动端发展

出现了Retina视网膜屏幕，使用2px x 2px的 device pixel 代表 1px x 1px 的 css pixel，所以假设设备像素数为750 x 1136px，而它的CSS逻辑像素数为375 x 568px。

[文章推荐](https://segmentfault.com/a/1190000007350680 "文章推荐")

### 拓展

1. 网易 纵向px>需要使用插件
2. 使用CSS3的缩放功能>需要使用插件
3. [px2rem插件使用](https://www.npmjs.com/package/postcss-px2rem "文章推荐")

### 基准字体大小

移动端浏览器的最小字体大小是12px；最小边距是320px屏幕宽度

| 屏幕 | 字体 |
| ------| ---- |
| 640px | 24px |
| 960px | 36px |
| 1080px | 42px |

字体大小不能是小数不能是单数所以1080的基准像素42
