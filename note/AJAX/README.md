# AJAX

AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。

AJAX 不是新的编程语言，而是一种使用现有标准的新方法。

AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容（异步加载，局部刷新）。

AJAX 不需要任何浏览器插件，但需要用户允许JavaScript在浏览器上执行。

AJAX最初的目的：是为了改善表单的用户的体验。

当前的AJAX：懒加载，瀑布流，朋友圈的各种数据加载方式。

## 基本原理

1. 创建向后抬服务器一个请求
2. 确定发送的方式方法
3. 发送请求
4. 确定后台加载完毕
5. 获取到请求的返回数据

## 基础语法

```js
var xhr = new XMLHttpRequest();
var url = "text.txt";
xhr.onload = function(){
  console.log(xhr.responseText);
}
xhr.open("get", url, true);
//get post数据请求方式
//true false异步或同步的却别（true表示异步）
xhr.send(null);
//如果使用的是get方法，send函数中的参数使用的是null
```

需要配合JS的基本事件以及DOM操作共同使用，AJAX负责的是获取数据，但是将获取到的数据放置到网页当中的任务任然是JS中的DOM操作的，而JS中事件的一些功能，能够更好的控制AJAX的请求条件

AJAX和HTML文件的加载在实际开发当中会比较少，当前了解HTML文件加载的主要目的是了解如何处理文件。之后主要要处理的文件类型为JSON.

## 异步的好处

1. 减少流量。
2. 更好的用户体验（局部刷新，表单能够及时得到验证，操作步骤简化，成功率提高）。
3. 能够进行JS控制数据加载，灵活性提升。

## get和post

### 安全性

get明文（基本数据会显示在url地址中）发送，安全性较低

post暗文，安全性相对高

### 长度、数据大小

post没有数据大小限制

由于数据防止在URL地址中传递，不同的浏览器对url的地址长度进行了不同的限制，因此个get发送的个数据长度受限，

### 性能

get相对来说比POST要好，post的性能大概在GET的三分一左右

### 写法

```js
let url = 'https://www.api.com'
// get
var xhr = new XMLHttpRequest();
xhr.open('get', url, true);
xhr.send(null)

// post
let val = 'data'
var xhr2 = new XMLHttpRequest();
xhr.open('post', url, true);
xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
xhr.send('keyword=' + val)
```