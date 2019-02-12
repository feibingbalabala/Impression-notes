# 事件与简单页面交互

## 声明

声明一个变量 var a = "abc"

申明一个对象var a = {}

## 所有效果实现的思路

1. 仔细检查功能，并根据基本功能构建结构样式
2. 用自己的语言进行功能的描述
3. 细化功能描述并装换成JS语言或命令
4. JS具体编码及代码优化，回顾成品代码

## 事件与绑定

事件是可以被Javascript侦测到的行为

事件可以分成三个总类：一般事件、页面事件、表单事件、

| 属性 | 触发事件 |
|--|--|
| onabort | 图像加载被中断 |
| onblur | 元素失去焦点 |
| onchange | 用户改变域的内容 |
| onclick | 鼠标点击某个对象 |
| ondblclick | 鼠标双击某个对象 |
| onerror | 当加载文档或图像时发生某个错误 |
| onfocus | 元素获得焦点 |
| onkeydown | 某个键盘的键被按下 |
| onkeypress | 某个键盘的键被按下或按住 |
| onkeyup | 某个键盘的键被松开 |
| onload | 某个页面或图像被完成加载 |
| onmousedown | 某个鼠标按键被按下 |
| onmousemove | 鼠标被移动 |
| onmouseout | 鼠标从某元素移开 |
| onmouseover | 鼠标被移到某元素之上 |
| onmouseup | 某个鼠标按键被松开 |
| onreset | 重置按钮被点击 |
| onresize | 窗口或框架被调整尺寸 |
| onselect | 文本被选定 |
| onsubmit | 提交按钮被点击 |
| onunload | 用户退出页面 |

### 绑定事件(on、addEventListener)

on事件

```js
// 方法1
btn.onclick = function() {
  ...
};
// 方法2
btn.onclick = sum;
function sum(){
  ...
}
```

addEventListener事件

addEventListener("事件名称",句柄、匿名函数，false/true)

```js
show () {
  ...
};
btn.addEventListener('click', show, false);
// 移除事件
ID.removeEventListener('click', show，false);
// 要和绑定事件的（true或者false）一样！
// 绑定事件尽量用句柄，方便移除，匿名函数无法移除
```

多个事件就绑定多次，false是事件冒泡，true事件捕获

事件流：从页面中接受事件的顺序

捕获阶段->获取标签->冒泡事件

addEventListener ie9+

ie不支持捕获事件

IE中的绑定事件ie8和一下

变量（元素）.attachEvent("on事件名称"+句柄)；

id,attachEvent("onclick"+show);

id,attachEvent("onclick"+test）;

后面的先执行(ie没有捕获，只有冒泡)

IE中的移除

变量名.detachEvent("onclick",test)

绑定事件的兼容

```js
function addEventHandle(ele.eventName,eventHandle){
  if(document.addEventListener){
    ele.addEventListener(eventName, eventHandle ,false);
  }else if(documen.attachEvent) {
    ele.attachEvent("on"+eventName +,eventHandle )
  }else {
    ele["on" + eventHandle] = eventName;
  }
}
```

阻止默认事件（放在事件内部）

```js
// 阻止冒泡
if(event.Propagation){
  event.stopPropagation(); // chrome
}else {
  window.event.cancelBubble = true; // ie
}
```

## 事件委托

给元素外层绑定后，找到这个元素触发事件（多用于用dom有做删减操作）

```html
<ul id='wrap'>
  <li>inner</li>
</ul>
<script type='text/javascript'>
  var wrap = docuement.getElementById('wrap');
  wrap.onclick = function (event) {
    var event = event || window.event;
    if (event.target.tagName === 'LI') {
      console.log(event.target.innertHTML);
    };
  };
</script>
```

## 申明一个函数

```js
function func () {
  ...
}
// 或者
var func1 = function () {
  ...
}
```

匿名函数：没有函数名字

```js
(function() {
  ...
})
```

函数名也叫句柄

函数的默认返回值undefined

return可以改变函数默认的返回值

### 参数

形参：声明函数的时候，写在小括号里面的参数（两个形参用,隔开）

实参：在调用函数的时候，写在小括号里面的好的参数

```js
// 形参
function add(a, b) {
  return a + b
}
// 实参
add(1, 2) // 3
```

### 作用域

全局作用域

局部作用域

不同作用域的访问关系：

将函数理解为盒子，在行数内部声明的变量（局部变量），在函数外部并不能访问。在函数外部声明的变量（全局变量），在函数内部可以访问

作用域链:

在局部作用域当中出现属性的时候，首先查找当前的作用域当中是否具有存储空间，如果有，直接采用，如果没有，向其父级查找，如果父级没有，继续向上，直到查找到window为止。如果window下也不存在该空间，会在全局作用域之下进行空间的创建。

### 执行时期

编译器-开辟空间

执行期-存储值/执行语句

## 两个数相加

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <style type="text/css">
    .wrap form {
      width: 200px;
      margin: 0 auto;
    }
    .con input {
      margin: 3px auto;
    }
  </style>
</head>
<body>
  <div class="wrap">
    <h1>页面交互 - 效果制作</h1>
    <form action="" method="">
      <div class="con">
        <input type="text" id="first" />
        <input type="text" id="second" />
        <input type="button" id="btn" value="点击求和" />
        <p id="result">求和的结果是：</p>
      </div>
    </form>
  </div>
  <script type="text/javascript">
    //功能描述：输入两个数，点击按钮，求和结果输出在P标签
    //细化功能
    //1、输入两个数
    //2、点击按钮
    //3、获取input【type=“text”】的值，相加
    //4、结果输出的p标签中

    // 获取标签
    var firstNum = document.getElementById("first");
    var secondNum = document.getElementById("second");
    var btnClick = document.getElementById("btn");
    var result = document.getElementById("result")
    // 绑定事件
    btnClick.onclick = function() {
      // 获取内容
      var firstInput = firstNum.value;
      var secondInput = secondNum.value;
      // console.log(firstInput,secondInput);
      // console.log(typeof(firstInput),typeof(secondInput));
      // 数据类型转换
      var sum = parseInt(firstInput) + parseInt(secondInput);
      console.log(sum);
      console.log(typeof(sum));
      // 设置内容
      result.innerHTML = "求和的结果是：" + sum;
    }
  </script>
</body>
</html>
```

如果在输入框中输入非数字就会得到结果NaN，这里就牵扯到一个东西，数据转换问题。[相关文章](../JS初探2/README.md#数据类型转换)

## 元素变大变小

```html
<div class="outer">
  <input type="button" value="点击变大" id="c-big">
  <input type="button" value="点击变小" id="c-small">
</div>
<div class="wrap" id="box">
  <p>哈哈哈啊哈</p>
</div>
<script type="text/javascript">
  // 点击上面按钮 box变大
  // 点击下面按钮 box变小

  // 点击变大按钮，box的类名为"wrap big";
  // 点击变小按钮，box的类名为"wrap small";
  var bigbtn = document.getElementById("c-big");
  var box = document.getElementById("box");
  var smallbtn = document.getElementById("c-small")
  bigbtn.onclick = function() {
    box.className = "big";
  }
  smallbtn.onclick = function() {
    box.style.width = "100px";
  }
</script>
```

## 计算器

```html
<form method="" action="">
  <input type="text" id="one">
  <select id="fangfa">
    <option value ="+" >+</option>
    <option value ="-" >-</option>
    <option value ="*" >*</option>
    <option value ="/">/</option>
  </select>
  <input type="text" id="two">
  <input type="button" value="结果" id="dianji">
  <p id="jieguo">结果</p>
</form>
<script language="javascript">
  var fangfa = document.getElementById('fangfa');
  var a =  document.getElementById('one');
  var b = document.getElementById('two');
  var jieguo = document.getElementById('jieguo');
  var dianji = document.getElementById('dianji');
  dianji.onclick = function(){
    var zhi = fangfa.options[fangfa.selectedIndex].value;
    if (zhi == "+") {
      var j =  parseInt(a.value)+parseInt(b.value);
      jieguo.innerHTML="结果"+ j;
    } else if(zhi == "-") {
      var j =  parseInt(a.value)-parseInt(b.value);
      jieguo.innerHTML="结果"+ j;
    } else if(zhi == "*") {
      var j =  parseInt(a.value)*parseInt(b.value);
      jieguo.innerHTML="结果"+ j;
    } else {
      var j =  parseInt(a.value)/parseInt(b.value);
      jieguo.innerHTML="结果"+ j;
    }
  };
</script>
```