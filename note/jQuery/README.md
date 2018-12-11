# jQuery

JavaScript技术核心：获取标签， 绑定事件，标签的变化

jQ的获取标签$(".wrap p")，括号内书写类名.wrap，#wrap，

```js
  window.onload = function(){}
```

onload事件：网站资源全部加载完成才执行；执行一次

ready方法：DOM结构加载完毕之后执行；执行多次，不会覆盖。

```js
$(document).ready(function(){
  alert("ready1")
});
// ready简写
$(function(){
  alert("ready2")
})
```

## 绑定事件两种方法

```js
$('.btn').click(function (e) {
  ...
});
$('.btn').on('click', target, function (e){
  ...
})
// target为事件委托的对象，没有实质的变化
```

## 事件移除

```js
$(".btn").off("click");
// 如果不在括号里，则移除所有事件
```

## on、bind、live区别

使用bind()方法是浪费资源的，因为他要匹配选择器中的每一项并且挨个设置相同的时间处理程序。

建议停止使用.live()方法，因为他已经弃用了。

1. 在调用live()方法之前，jquery会先获取与指定的选择器匹配的元素，这一点对于大型文档来说很花费时间。
2. 不支持链式写法，例如$('a').find('.classA, .classB').live()，不合法的写法。
3. 由于所有的live()时间被添加到document元素上，所以在时间被处理之前，可能会通过最长最慢的那条路去触发。
4. 在移动端ios(iphone,ipad,ipod)上，对于大多数元素而言，click()事件不会冒泡到文档body上，并且如果不满足如下情况之一，就不能和live()方法使用：使用原生的可被点击的元素，例如a或者Button，因为这两个元素可以冒泡到document。
5. 在doucment.body内的元素使用on()或者delegate()进行绑定，因为移动端ios只有在Body内才进行冒泡。
6. 需要click冒泡到元素上才能应用的css样式例如cursor。但是依然需要注意，这样会禁止元素上的复制、粘贴功能，当点击元素时，会导致该元素高亮。
7. 在事件处理中调用event.stopPropagation()来阻止事件处理被添加到document之后的结点中，是效率最低的。因为事件已经被传播到document上。
8. live()方法与其它事件方法的相互影响是会令人感到惊讶的。例如，$(document).unbind('click')会移除所有通过live()绑定的click事件。

delegate()方法'很划算'用来处理性能和响应动态添加元素。

新的on()方法主要是实现bind()、live()甚至delegate()的功能。

## jq的方法

css函数操作

|CSS 属性|描述|
|-|-|
|css()|设置或返回匹配元素的样式属性。|
|height()|设置或返回匹配元素的高度。|
|offset()|返回第一个匹配元素相对于文档的位置。|
|offsetParent()|返回最近的定位祖先元素。|
|position()|返回第一个匹配元素相对于父元素的位置。|
|scrollLeft()|设置或返回匹配元素相对滚动条左侧的偏移。|
|scrollTop()|设置或返回匹配元素相对滚动条顶部的偏移。|
|width()|设置或返回匹配元素的宽度。|

属性操作

|方法|描述|
|-|-|
|addClass()|向匹配的元素添加指定的类名。|
|attr()|设置或返回匹配元素的属性和值。|
|hasClass()|检查匹配的元素是否拥有指定的类。|
|html()|设置或返回匹配的元素集合中的 HTML 内容。|
|removeAttr()|从所有匹配的元素中移除指定的属性。|
|removeClass()|从所有匹配的元素中删除全部或者指定的类。|
|toggleClass()|从匹配的元素中添加或删除一个类。|
|val()|设置或返回匹配元素的值。|

.val() .html() .text() .attractive() .removeAttr()  .prop()  .removeProp()

### attr与prop的区别：

1、property记录的值会按照用户事实更新，而attribute记录都是初始值

2、property是DOM节点上的属性，attr是标签上的属性

3、推荐property只能操作布尔值的属性

## jQ常见操作

scrollTop(): 修改滚动的高度（通常和scrillHeight配合使用）

addClass(): 添加class类名（添加多个类名.addClass('test clearfix')）

removeClass(): 删除class类名

toggleClass(): 有就删除，没有就添加类名

append(): 添加结点（.append('&lt;div&gt;&lt;/div&gt;')）写法2：$('&lt;div&gt;&lt;/div&gt;').appendTo('.btn')

after(): 插入兄弟结点（afterTo）

eq(): 相等判断多用于数组index

hasClass(): 是否有这个类名

find(): 查找某个标签或者类名、id名

next(): 下一个结点

parents(): 所有父亲结点

children(): 所有子结点

siblings(): 兄弟结点

jQ对象转换原生对象（用数组形式）

原生与jQ不能混用，原生对象转换为jQ对象（$()）

## 动画

show(): 高度和透明度的变化

fadeIn(): 透明->不透明（fadeOut）

slideDown(): 高度变化从上到下

animate(): 动画(animate({'margin-top': '0px'}))，不能用于背景色的变化

stop(): 使用动画最需要注意的清除动画

stop(true): 停止当前动画（动画队列中的动画会继续）

stop(true, true)：停止当前所有动画，直接到达终点位置

## DOM操作

增

creatElement/creatTextNode

appendChild/insertbefore

删
removechild

替换

replaceChild
