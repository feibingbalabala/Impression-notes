# tab切换与函数调用

## 闭包和函数默认返回值

函数如果没有return，是没有返回值的也就是undefined

```js
function add (x, y) {
  return x + y;
}
var sum = add(1, 1)

function f (x) {
  x += 5;
  return function () {
    x++; // x只是自加1但是没有赋值给x所以x还是5、15、10
    console.log(x)
  }
}
var a = f(5);
// 此时a是return的函数
a(); // 11
var b = f(15)(); // 21
console.log(b) // undefined
// b直接调用了函数所以返回值是undefined
var c = f(10);
c(); // 16
// a和c都是引用这个函数而不是调用
```

## tab切换

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>H5course</title>
  <style>
    .wrap {
      width: 600px;
    }
    .tab-tit span {
      float: left;
      width: 200px;
      height: 100px;
      background-color: skyblue;
    }
    .tab-con div {
      display: none;
      height: 300px;
      background-color: #999;
    }
    .wrap .sel {
      background-color: rgb(68, 185, 233);
    }
    .wrap .show {
      display: block;
    }
  </style>
</head>
<body>
  <div class="wrap">
    <div class="tab-tit clearfix" id="tabTit">
      <span class="sel">体育</span>
      <span>新闻</span>
      <span>音乐</span>
    </div>
    <div class="tab-con" id="tabCon">
      <div class="show">体育体育体育体育体育体育</div>
      <div>新闻新闻新闻新闻新闻新闻</div>
      <div>音乐音乐音乐音乐音乐音乐音乐音乐</div>
    </div>
  </div>
  <script>
    ...
  </script>
</body>
</html>
```

### 简单版本(思路1)

```js
var titArr = document.getElementById("tabTit").getElementsByTagName("span");
var conArr = document.getElementById("tabCon").getElementsByTagName("div");

titArr[0].onclick = function (){
  titArr[0].className = "sel";
  conArr[0].className = "show";
  titArr[1].className = "";
  conArr[1].className = "";
  titArr[2].className = "";
  conArr[2].className = "";
}

titArr[1].onclick = function (){
  titArr[0].className = "";
  conArr[0].className = "";
  titArr[1].className = "sel";
  conArr[1].className = "show";
  titArr[2].className = "";
  conArr[2].className = "";
}

titArr[2].onclick = function (){
  titArr[0].className = "";
  conArr[0].className = "";
  titArr[1].className = "";
  conArr[1].className = "";
  titArr[2].className = "sel";
  conArr[2].className = "show";
}
```

### 简单版本(思路2)

```js
var titArr = document.getElementById("tabTit").getElementsByTagName("span");
var conArr = document.getElementById("tabCon").getElementsByTagName("div");
var len = titArr.length;

titArr[0].onclick = function (){
  for (var i = 0; i < len; i++) {
    titArr[i].className = "";
    conArr[i].className = "";
  };
  titArr[0].className = "sel";
  conArr[0].className = "show";
}

titArr[1].onclick = function (){
  for (var i = 0; i < len; i++) {
    titArr[i].className = "";
    conArr[i].className = "";
  };
  titArr[1].className = "sel";
  conArr[1].className = "show";
}

titArr[2].onclick = function (){
  for (var i = 0; i < len; i++) {
    titArr[i].className = "";
    conArr[i].className = "";
  };
  titArr[2].className = "sel";
  conArr[2].className = "show";
}
```

### 函数封装（提取公共部分）

```js
var titArr = document.getElementById("tabTit").getElementsByTagName("span");
var conArr = document.getElementById("tabCon").getElementsByTagName("div");
var len = titArr.length;

titArr[0].onclick = function (){
  change(0);
}

titArr[1].onclick = function (){
  change(1);
}

titArr[2].onclick = function (){
  change(2);
}

function change(index) {
  for (var i = 0; i < len; i++) {
    titArr[i].className = "";
    conArr[i].className = "";
  };
  titArr[index].className = "sel";
  conArr[index].className = "show";
  
  // 说道一个点arguments是函数实参的数组
  // 在函数调用的时候，传递进来的参数作为数组，和形参的数量没有没关系
  console.log(arguments);
}
```

argunments

```js
function ar (a, b) {
  console.log(arguments)
};
ar(1,2); // [1,2]
ar(1); // [1]
ar(1,2,3); // [1, 2, 3]
```

### 使用自定义属性

```js
var titArr = document.getElementById("tabTit").getElementsByTagName("span");
var conArr = document.getElementById("tabCon").getElementsByTagName("div");
var len = titArr.length;

for (var i = 0; i < len; i++) {
  titArr[i].index = i; // 给它添加了一个自定义属性，并存储了他的数组下标
  titArr[i].onclick = function() {
    for (var j = 0; j < len; j++) {
      titArr[j].className = "";
      conArr[j].className = "";
    };
    titArr[this.index].className = "sel";
    conArr[this.index].className = "show";
  }
};
```

### 利用this指向

```js
var titArr = document.getElementById("tabTit").getElementsByTagName("span");
var conArr = document.getElementById("tabCon").getElementsByTagName("div");
var len = titArr.length;

for (var i = 0; i < len; i++) {
  titArr[i].onclick = function() {
    console.log(i); //这里i永远是3，因为for循环在3的时候停止了循环
    // 点击事件触发后，我们遍历了所有数组的内容，找到我们点击的那个对象。
    for (var j = 0; j < len; j++) {
      if (titArr[j] == this) { // this指向他的所有者，也就是titArr[i]
        titArr[j].className = 'sel';
        conArr[j].className = 'show';
      } else {
        titArr[j].className = '';
        conArr[j].className = '';
      };
    };
  };
};
```

### 使用闭包

```js
var titArr = document.getElementById("tabTit").getElementsByTagName("span");
var conArr = document.getElementById("tabCon").getElementsByTagName("div");
var len = titArr.length;

for (var i = 0; i < len; i++) {
  titArr[i].onclick = function(num) {
    return function () {
    console.log(i); // 这里i永远是3，因为for循环在3的时候停止了循环
    console.log(num); // num就是立即执行函数中的i，每次执行后我们就立即执行了这个函数并把num保存在内部环境中
    for (var j = 0; j < len; j++) {
      titArr[j].className = "";
      conArr[j].className = "";
    };
      titArr[num].className = "sel";
      conArr[num].className = "show";
    };
  }(i); //立即执行函数。将返回值存在内存之中
};
```

理解闭包的核心就是函数调用完成之后，其执行上下文环境不会被销毁，变量不会被释放。