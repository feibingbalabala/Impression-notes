# require.js

在浏览器中可以作为JS文件的模块加载器，也可以用在Node和rhino环境，

## 正常编写方式

index.html:

```html
<!DOCTYPE html>
<html>
  <head>
    <script type="text/javascript" src="a.js"></script>
  </head>
  <body>
    <span>body</span>
  </body>
</html>
```

a.js

```js
function fun1(){
  alert("it works");
};
fun1();
// 或者
(function(){
  function fun1(){
    alert("it works");
  }
  fun1();
})()
```

第二中方法使用了块作用域的方法来申明function防止全局变量，本职还是一样的，根据页面是从上往下读取的，会先运行a.js的弹窗，然后才会继续读取下面的内容，这样就是js阻止浏览器的渲染导致的结果。

## requirejs写法

index.html:

```html
<!DOCTYPE html>
<html>
  <head>
    <script type="text/javascript" src="require.js"></script>
    <script type="text/javascript">
        require(["a"]);
    </script>
  </head>
  <body>
    <span>body</span>
  </body>
</html>
```

a.js:

```js
define(function(){
  function fun1(){
    alert("it works");
  }
  fun1();
})
```

浏览器会提示it works,同时下面的html也出现在页面之中了，require.js的好处：

1. 防止js加载阻塞页面渲染；
2. 使用外部引入的方式加载js，防止出现多行js引入

```html
<script type="text/javascript" src="a.js"></script>
```

require会定义三个变量：define，require，require.js 其中后面两个的功能是一样的，一般使用前面那个require，更加简短。
define用来定义一个模块，require加载依赖模块，并执行加载完后的回调函数

```js
define(function(){
  function fun1(){
    alert("it works");
  }
  fun1();
})
```

通过define函数定义了一个模块，然后再页面中使用：

```js
require(["js/a"]);
```

来加载该模块(注意require中的依赖是一个数组，即使只有一个依赖，你也必须使用数组来定义)，require API的第二个参数是callback，一个function，是用来处理加载完毕后的逻辑，如：

```js
require(["js/a"], function () {
  alert("load finished");
})
```

之前的例子中加载模块都是本地js，但是大部分情况下网页需要加载的JS可能来自本地服务器、其他网站或CDN，这样就不能通过这种方式来加载了，我们以加载一个jquery库为例：

```js
require.config({
  paths: {
      "jquery" : ["http://libs.baidu.com/jquery/2.0.3/jquery"]
  }
});
require(["jquery", "js/a"], function($){
  $(function(){
    alert("load finished");
  })
})
```

require.config是用来配置模块加载位置，简单点说就是给模块起一个更短更好记的名字，比如将百度的jquery库地址标记为jquery，这样在require时只需要写["jquery"]就可以加载该js，本地的js我们也可以这样配置：

```js
require.config({
  paths: {
    "jquery": ["http://libs.baidu.com/jquery/2.0.3/jquery"],
    "a": "js/a"
  }
});
require(["jquery","a"], function($){
  $(function(){
      alert("load finished");
  })
})
```

通过paths的配置会使我们的模块名字更精炼，paths还有一个重要的功能，就是可以配置多个路径，如果远程cdn库没有加载成功，可以加载本地的库，如：

```js
require.config({
  paths : {
    "jquery": ["http://libs.baidu.com/jquery/2.0.3/jquery", "js/jquery"],
    "a": "js/a"
  }
})
require(["jquery","a"],function($){
  $(function(){
    alert("load finished");
  })
})
```

这样配置后，当百度的jquery没有加载成功后，会加载本地js目录下的jquery

在使用requirejs时，加载模块时不用写.js后缀的，当然也是不能写后缀

上面例子中的callback函数中发现有$参数，这个就是依赖的jquery模块的输出变量，如果你依赖多个模块，可以依次写入多个参数来使用：

```js
require(["jquery","underscore"], function($, _){
  $(function(){
    _.each([1,2,3],alert);
  })
})
```

如果某个模块不输出变量值，则没有，所以尽量将输出的模块写在前面，防止位置错乱引发误解

## 全局配置

上面的例子中重复出现了require.config配置，如果每个页面中都加入配置，必然显得十分不雅，requirejs提供了一种叫"主数据"的功能，我们首先创建一个main.js：

```js
require.config({
  paths : {
    "jquery": ["http://libs.baidu.com/jquery/2.0.3/jquery", "js/jquery"],
    "a": "js/a"
  }
})
```

然后再页面中使用下面的方式来使用requirejs：

```html
<script data-main="js/main" src="js/require.js"></script>
```

解释一下，加载requirejs脚本的script标签加入了data-main属性，这个属性指定的js将在加载完reuqire.js后处理，我们把require.config的配置加入到data-main后，就可以使每一个页面都使用这个配置，然后页面中就可以直接使用require来加载所有的短模块名

data-main还有一个重要的功能，当script标签指定data-main属性时，require会默认的将data-main指定的js为根路径，是什么意思呢？如上面的data-main="js/main"设定后，我们在使用require(['jquery'])后(不配置jquery的paths)，require会自动加载js/jquery.js这个文件，而不是jquery.js，相当于默认配置了：

```js
require.config({
  baseUrl : "js"
})
```

## 第三方模块

通过require加载的模块一般都需要符合AMD规范即使用define来申明模块，但是部分时候需要加载非AMD规范的js，这时候就需要用到另一个功能：shim，shim解释起来也比较难理解，shim直接翻译为"垫"，其实也是有这层意思的，目前我主要用在两个地方

### 非AMD模块输出

非AMD模块输出，将非标准的AMD模块"垫"成可用的模块，例如：在老版本的jquery中，是没有继承AMD规范的，所以不能直接require["jquery"],这时候就需要shim，比如我要是用underscore类库，但是他并没有实现AMD规范，那我们可以这样配置

```js
require.config({
  shim: {
    "underscore": {
      exports: "_";
    }
  }
})
```

这样配置后，我们就可以在其他模块中引用underscore模块：

```js
require(["underscore"], function(_){
  _.each([1,2,3], alert);
})
```

### 插件形式的非AMD模块

插件形式的非AMD模块，我们经常会用到jquery插件，而且这些插件基本都不符合AMD规范，比如jquery.form插件，这时候就需要将form插件"垫"到jquery中：

```js
require.config({
  shim: {
    "underscore": {
      exports : "_";
    },
    "jquery.form": {
      deps : ["jquery"]
    }
  }
})
// 或者
require.config({
  shim: {
    "underscore": {
      exports : "_";
    },
    "jquery.form": ["jquery"]
  }
})
```

这样配置之后我们就可以使用加载插件后的jquery了

```js
require.config(["jquery", "jquery.form"], function($){
  $(function(){
    $("#form").ajaxSubmit({...});
  })
})
```