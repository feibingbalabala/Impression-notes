# Js初探

## Javascript历史

1994 Netscape

1995 LiveScript

1995 JavaScript

ie浏览器：JScript Scriptease：CEnvi

1997ECMAScript

ECMAScrpt5.0

2015年6月ECMAScript6

## JS的组成部分

ECMAScript（基本语法）+ DOM（Document Object Model 文档对象模型）+ BOM （browers Object Model 浏览器对象模型）

## 引入方式

标签内联

```html
<div class='wrap' onclick='show()'></div>
<script type='text/javascript'>
  function show () {
    ...
  }
</script>
```

内部写入

```html
<div id='btn'></div>
<script type='text/javascript'>
  var btn = document.getElementById('btn')
  btn.onclick = function () {
    ...
  }
</script>
```

外部引入

```html
<script type='text/javascript' src='demo.js'></script>
```

如果放到head元素里面时JavaScript代码会先执行后执行body里面的内容（从上到下执行）这时候JavaScript需要获取标签的时候访问不到，为了防止出错需要用window.onload的事件，把JavaScript代码放到内容后面（保证JS获取内容）

## Javascript的注释

单行注释

```js
// 使用条件、范围注释代码用的
```

多行注释

```js
/*使用条件：功能描述*/
/*
* 功能：
* 作者：
*/
```

## Javascript的弹窗方式

alert 警告弹窗(只有文字)

prompt 对话弹窗(可以输入东西)

confirm 确认弹窗(只有确认按钮取消按钮)

console.log("控制台输出")

### 不换行

```js
document.write("aaa");
document.write("aaa2");
```

### 换行

```js
document.writeln("aaa3");
document.writeln("aaa4");
```

## 调试

1. 注释
2. 控制台输出console.log("控制台输出")
