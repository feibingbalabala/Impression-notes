# 元素的浮动

float: none|left|right;

float元素先浮后动（脱离文档流）

1. 漂浮在上面的图层，当浏览器宽度不够，就会在下一行，水槽浮动原理
2. 所有元素都可以浮动
3. 没有特殊设置可以和文字一样大小的边框
4. 往哪边靠（脱离文档流）

## 影响

高度塌陷：子元素浮动，父级元素会出现高度为0的现象

## 清除浮动

需要清浮动的情况：

1. 子标签浮动后，父标签的高度无法被撑开，所以需要清浮动；

2. 新加入的标签，希望不受之前浮动元素的影响，则需要清浮动；

清除浮动的方法：

1. clear: both; height: 0; overflow: hidden;
2. overflow:hidden；触发layout 常用于清除内浮动；
3. 和父标签一起浮动；
4. position: absolute;
5. after 伪对象：给当前对象设置

```css
.aa:after {
  content: "."
}
.aa {
  display: inline-block;
}
.aa {
  display: block;
}
```

常用清除浮动代码

```css
.clearfix {
  *zoom: 1; //兼容IE6,IE7。因为IE6和7没有一些元素
}
.clearfix:after {
  display: block;
  content: '/200b';
  clear: both;
  height: 0;
}
```

## 清浮动优缺点总结

1、子元素浮动，父级元素也浮动；

优点：不存在结构和语义化问题，代码量少；

缺点：使得与父元素相邻的元素的布局会受到影响。

2、给空标签设置属性clear: both;  

优点：通俗易懂，容易掌握；

缺点：会添加大量无语义空标签，结构与表现未分离，不利于维护。

3、br标签清浮动：br标签自带的属性： 

```html
  <br clear="all" />;
```

优点：比空标签方式语义稍强，代码量较少；

缺点：结构与表现未分离。

4、给父级标签设置 overflow: hidden/ auto;
hidden：超出内容隐藏；

auto：默认属性，在需要时剪切内容并添加滚动条；超出时显示滚动条。

优点：不存在结构和语义化问题；

缺点：

hidden——>内容增多时候容易造成不会自动换行，导致内容被隐藏，无法显示需要溢出的元素。

auto——>多个嵌套后，有些情形下会造成内容全选；IE中mouseover造成宽度改变时会出现最外层模块出现滚动条。

5、父元素设置display: table; ——清浮动：

优点：结构语义化完全正确，代码量少；

缺点：盒模型属性已经改变。

例

```html
<style>
  .main  {
    display: table;
}
</style>
<div class="main">...</div>
```

6、after伪元素清浮动：

优点：结构和语义化完全正确；

缺点：复用方式不当会造成代码量增加。

例

```css
.test  {
  height: 0;
  display: block;
  content:"\200B";
  clear :both;
}
```