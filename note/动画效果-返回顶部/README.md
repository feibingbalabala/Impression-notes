# 动画效果-返回顶部

```js
var btn = document.getElementById('btn');
var timer = null;
btn.onclick = function () {
  var valtop = document.documentElement.scrollTop || document.body.scrollTop;
  timer = setInterval(function () {
    valtop -= 50;
    if (valtop <= 0) {
      valtop = 0;
      clearInterval(timer);
    }
    if (document.documentElement.scrollTop) {
      //有值就是火狐
      document.document.scrpllTop = valTop;
    } else {
      //没值就是google
      document.body.scrollTop = valTop;
    }
  }, 20)
}
```

