# 水平垂直居中的方法

## 利用table属性

根据内容可以动态改变高度（不需要CSS中定义）。当wrap里没有足够空间,con不会被截断

```html
<style>
.wrap {
  width: 600px;
  height: 600px;
  border: 1px solid black;
  display: table;
}
.inner {
  display: table-cell;
  vertical-align: middle;

}
.con {
  text-align: center;
  margin: 0 auto;
  width: 300px;
  height: 300px;
  background-color: #cff;
}
</style>
<div class="wrap">
  <div class="inner">
    <div class="con">
  </div>
</div>
```

## 定位和margin负值

这个方法使用绝对定位的div，把他的top设置为50%，top margin设置为负的content高度。这意味着对象必须在CSS中指定固定的高度
因为有高度，或许想给content指定额overflow： auto，这样如果content太多就会出现滚动条，一面content溢出

```html
<style>
.wrap {
  position: relative;
  width: 600px;
  height: 600px;
  border: 1px solid black;
}
.content {
  position: absolute;
  top: 50%;
  left: 50%;
  height: 300px;
  width: 300px;
  margin: -150px 0 0 -150px;
}
</style>
<div class="wrap">
  <div class="inner">
    <div class="con">
  </div>
</div>
```

## 利用margin负值

在content元素插入一个div，设置此div height50%；margin-bottom: -content teight；content清除浮动并显示在中间

```html
<style>
.floater {
  float: left;
  height: 50%; /*(大的div)*/
  margin-bottom:-120px;
}
.content {
  position: relative;
  clear: both;
  height: 240px;
}
</style>
<div class='wrap'>
  <div class="floater"></div>
  <div class="content">Content here</div>
</div>
```

## 定位

这个方法使用了position：absolute有固定宽度和高度的div。这个div被设置为top: 0; bottom: 0；但是因为他有固定高度，其实并不能上下间距都为0，因此margin: auto会使居中。

```html
<style>
wrap {
  position: relative;
}
.content {
  position:absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100px;
  width: 100px;
  margin: auto;
  background-color: red;
}
</style>
<div class='wrap'>
  <div class="content">Content here</div>
</div>
```

## padding挤压

```html
<style>
.wrap {
  width: 600px;
  padding: 150px 0;
}
.inner {
  width:300px;
  height: 300px;
  margin: 0 auto;
}
</style>
<div class='wrap'>
  <div class="inner">Content here</div>
</div>
```