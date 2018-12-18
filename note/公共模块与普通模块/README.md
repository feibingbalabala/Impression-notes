# 公共模块与普通模块

公共模块的种类-网站的公共模块，页面的共用部分

## 如何制作一个具体的模块

1. 选择标签
2. 内部布局
3. 自身样式
4. 文本样式

选择标签要注意标签的语义性

1、h1~h6（整个页面用一次）

作为标题（文章标题、模块标题），常用h1~h3，h4~h6就不用了。h1的SEO权重最高，h1在一个页面上用1次，用于页面的标题（例如中原页面头部的公司名称）

2、span

跟div相似，没有语义性主要用于布局

3、修饰标签

em i  （倾斜）

strong b（加粗）

i和b是修饰类标签，em、strong表示强调 strong强调作用更好。。针对于seo的，显示效果一样

4、img 定义图片，用于在页面中显示

```html
<img src="路径"  alt="站位符，在图片路径出错或无法显示时的提示语言" title='鼠标停留时显示'/>
```

5、超链接

```html
<a href="" title="">超链接，title为鼠标长时间放在超链接上所提示的语言</a>
```

## CSS选择器

1、后代选择器语法：使用多个选择器的组合来找到要控制的标签

ID名为wrap中的p标签样式选择器志节使用空格分隔开

```css
#wrap p {
  border：1px；
}
```

```html
<div id='wrap'>
  <p></p>
</div>
```

2、群组选择器语法：把不同选择器中相同的CSS取出，减少代码冗余，选择器之间使用，隔开

```css
.wrap span, .wrap p {
  border: 1px solid #ccc;
}
```

```html
  <div class='wrap'>
    <span></span>
    <p></p>
  </div>
```

## 优先级的计算

| 标签内写入 | ID选择器 | 类选择器 | 标签选择器 |
| :----: | :----:  | :----: | :----:|
| 0 | 0 | 0 | 0 |

## 字体

在设置字体的时候，英文字体写在前面，中文字体写在后面

font-family: 字体属性   <font-family:"Arail","Microsoft Yahei","simsun">

font-size:字体大小，最小字体大小12px 默认16px

font-style:倾斜

font-weight:加粗

color：颜色

text-decoration: underline  下划线

text-indent: 2em首行缩进，

text-align:center;(center,center)

## 背景色

background的填充范围border + padding + content（填充起始位置：padding的左上角，背景图不会放在内容区里面，放到padding里）

background-position:center center;  水平垂直居中

background-repeat: no-repeat; 不重叠 | repeat-x  在X轴重复

缩写background：颜色 url（地址）no-repeat  center center ；repeat和center可以换位置

background-attachment:背景图片滚动方式scroll默认模式 | fixed随着滚动条滚动

单行文本居中 line-height：设置与模块高度相同就可以让文本居中

## 普通模块

1、border中solid（实心线） | dottle（虚线）

2、多个行元素并排显示，默认状态下，行元素之间会存在间隙，这个间隙由空格引起的，解决方法是给行元素加浮动

3、浮动对元素的影响：

1. 可以让元素并排显示
2. 在不设置宽高的情况下，宽高由内容决定
3. 元素会脱离文档流
4. 行元素浮动，宽高设置就有效果了

4、a的伪类：

1. link:有链接属性时
2. visited：链接属性地址已经被访问过
3. hover: 鼠标悬停在上面
4. active：被用户激活（鼠标点击与释放之间发生的事件）

书写顺序link:visited:hover:active

原因：如果不按照书写原因，会让伪类设置无效(部分浏览器)

5、背景图合并：

优点：减少服务器请求压力

考虑：

1. background-repeat
2. 背景图的显示范围

6、常见块元素的选用

p：定义段落

```html
<p>定义段落</p>
```

ol:有序列表，只能跟li

```html
<ol>
  <li>1</li>
  <li>2</li>
</ol>
```

ul:无序列表，也跟li

```html
<ul>
  <li>1</li>
  <li>2</li>
</ul>
```

dl：dt(标题) dd(列表的项) 自定义列表(两种用法，友情链接,图文并茂图片放在dt里面的)

```html
<dl>
  <dt>
    <img src='' />>
  </dt>
  <dd>内容</dd>
</dl>
```

7、基本模块

1. 选择标签，
2. 布局样式，
3. 文本样式，
4. 代码优化

## 选择标签考虑的内容：

seo

样式代码的控制难易程度

关于链接跳转

小ICON，使用背景还是img

在使用数据图的时候，一定要限制宽高     min/max-width, min/max-height

image下方有默认3px的BUG：

解决方案：

1. 给img设置浮动
2. 给img设置display：block

## CSS属性书写顺序

显示属性：float overflow position z-index

自身属性：margin,padding,border,width,height

文本属性：text font background

文本超出神略号（要固定高度和宽度，定义超出的范围）

```css
.ellipsis {
  width: 150px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```
