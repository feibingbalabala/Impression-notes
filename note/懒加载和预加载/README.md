# 懒加载和预加载

原理：懒加载，延迟图片加载和符合某些条件时才加载某些资源。他的核心思想：当用户想看页面某个区域时，在加载该区域的数据。这在一定程度上减轻了服务器端的压力，也加快了页面的呈现速度。

应用范围：大多数大型网站，空间，微博，蘑菇街等等。

## 懒加载的呈现方式

1. 纯粹的延时加载，使用setTimeout或者setInterval进行加载延迟，如果用户在加载前就离开了，那么自然就不会进行加载。
2. 条件加载，符合某些条件，或者触发了某些事件才开始异步加载。
3. 可视区域加载，仅仅加载用户可以看到的区域，这个主要是监控滚动条来实现，一般根据用户看到的底边距离很近的时候才开始加载，这样才能保证用户下来的时候图片正好连接上，没有过多的停顿。

## 瀑布流

优点：

1. 布局简单，有效的降低了界面复杂度，节省了空间，比如，我们不需要在做负载的页码连接和按钮了。
2. 不用明确知道数据块的高度，当数据快中有图片时，就不需要指定图片高度。

缺点：

1. 列数固定，拓展不易，当浏览器窗口大小变化时，只能固定的n列，如果需要添加一列，很难调整数据块的排列。
2. 无限滚动的方式只时候某些产品的部分特定内容。

```html
<style type="text/css">
  .container {
    width: 960x;
    margin: 60px auto;
  }
  .container ul {
    float: left;
    width: 300px;
    margin-right: 20px;
  }
  .container ul li {
    margin-bottom: 20px;
  }
  .container ul li img {
    width: 300px;
  }
</style>
</head>
<body>
  <div class="container" id="container">
    <ul class="col">
      <li><img src="" alt="" /></li>
    </ul>
    <ul class="col">
      <li><img src="" alt="" /></li>
    </ul>
    <ul class="col">
      <li><img src="" alt="" /></li>
    </ul>
  </div>
</body>
<script type="text/javascript">
// 一定要引入jquery
// var a = document.getElementsByTagName(li);
function loadMeinv() {
  var data = 0;
  for (var i = 0; i < 9; i++) {
    data = parseInt(Math.random() * 9);
    var html = "";
    html = '<li><img src="images/'+data+'.jpg"></li>';
    $minUl = getMinUl();
    $minUl.append(html);  
  };
};
loadMeinv();
function getMinUl() {
  var $arrUl = $("#container .col");
  console.log($arrUl)
  var $minUl =$arrUl.eq(0);
  $arrUl.each(function(index, elem){
    console.log(elem)
    if ($(elem).height() < $minUl.height()) {
      $minUl = $(elem);
    }
  });
  return $minUl;
}
```

## 懒加载插件

lazy Load一个jquery插件。它可以延迟加载页面中的图片，在浏览器可视区域外的图片不会被载入，直到用户将页面滚动到他们所在的位置。
