# 动画效果-返回顶部

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .wrap-box {
      background: #cfc;   
    }
    .wrap-box li {
      height: 30px;
      line-height: 30px;
    }
    .btn {
      position: fixed;
      bottom: 100px;
      right: 100px;
      width: 50px;
      height: 50px;
      border: 1px solid #000;
      background-color: #fff;
    }
  </style>
</head>
<body>
  <div id='btn' class='btn'>返回顶部</div>
  <ul id="wrap" class="wrap-box"></ul>
  <script>
    // 这一段和返回顶部没有什么关系，就是为了增加页面的可滚动高度
    var wrap = document.getElementById('wrap')
    for (var i = 0; i < 200; i++) {
      wrap.innerHTML = wrap.innerHTML + '<li>' + i + '</li>'
    }

    // 获取标签
    var btn = document.getElementById('btn');
    var timer = null;
    // 添加事件
    btn.onclick = function () {
      // 获取页面已经滚动的距离
      var valtop = document.documentElement.scrollTop || document.body.scrollTop;
      timer = setInterval(function () {
        // 在计时器修改滚动距离，并且赋值给页面滚动高度(这里利用计时器，是为了让滚动不生硬)
        valtop = valtop - 50;
        // 注意零界值的判断
        if (valtop <= 0) {
          valtop = 0;
          clearInterval(timer);
        }
        if (document.documentElement.scrollTop) {
          //有值就是火狐、ie
          document.documentElement.scrollTop = valtop;
        } else {
          //没值就是google
          document.body.scrollTop = valtop;
        }
      }, 20)
    }
  </script>
</body>
</html>
```