# tab切换与函数调用

## tab切换

```html
<span>1</span>
<span>2</span>
<div id='content'>
  <div></div>
  <div></div>
</div>
<script>
  var spans = document.getElementsByTagName('span');
  var divs = ducument.getElementById('content').getElementsByTagName('div')
  for (var i = 0; i < spans.length; i++) {
    spans[i].onClick = function () {
      for (var j = 0; j < spans.length; j++) {
        if (this === spans[j]) {
          span[j].className = 'sel';
          divs[j].className = 'sel';
        } else {
          spans[j].className = '';
          divs[j].className = ''
        };
      };
    };
  };
</script>
```

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