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

## 定位属性

|属性|描述|值|
|-|-|-|
|position|规定元素的定位类型。|absolute:生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。fixed:生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。relative:生成相对定位的元素，相对于其正常位置进行定位。static:默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。|

## 边框属性（Border 和 Outline）

|属性|描述|值|
|-|-|-|
|border|在一个声明中设置所有的边框属性。|一个值:上右下左。两个值:上下 左右。三个值:上 左右 下。四个值:上 右 下 左。|
|outline|在一个声明中设置所有的轮廓属性。|invert none medium|

## Box 属性

|属性|描述|值|
|-|-|-|
|overflow|规定当内容溢出元素框时发生的事情。||
|overflow-x|如果内容溢出了元素内容区域，是否对内容的左/右边缘进行裁剪。|visible:不裁剪内容，可能会显示在内容框之外。hidden:裁剪内容 - 不提供滚动机制。scroll:裁剪内容 - 提供滚动机制。auto:如果溢出框，则应该提供滚动机制。|
|overflow-y|如果内容溢出了元素内容区域，是否对内容的上/下边缘进行裁剪。||

## 背景属性（Background）

|属性|描述|值|
|-|-|-|
|background|在一个声明中设置所有的背景属性。|background: #00FF00 url(bgimage.gif) no-repeat fixed top;|
|background-attachment|设置背景图像是否固定或者随着页面的其余部分滚动。|scroll:默认值。背景图像会随着页面其余部分的滚动而移动。fixed:当页面的其余部分滚动时，背景图像不会移动。inherit:从父元素继承 background-attachment 属性的设置。|
|background-color|设置元素的背景颜色。|transparent:背景颜色为透明。可以是颜色值为颜色名称的背景颜色（比如 red）。颜色值为十六进制值的背景颜色（比如 #ff0000）。颜色值为 rgb 代码的背景颜色（比如 rgb(255,0,0)）。inherit：父元素继承 background-color 属性的设置。|
|background-image|设置元素的背景图像。|url('URL'):指向图像的路径。none:默认值。不显示背景图像。inherit:从父元素继承 background-image 属性的设置。|
|background-position|设置背景图像的开始位置。|top,left,right,bottom,center。x% y%。px px。|
|background-repeat|设置是否及如何重复背景图像。|repeat:默认。背景图像将在垂直方向和水平方向重复。repeat-x:背景图像将在水平方向重复。repeat-y:背景图像将在垂直方向重复。no-repeat:背景图像将仅显示一次。inherit|
|background-clip|规定背景的绘制区域。|border-box:背景被裁剪到边框盒。padding-box:背景被裁剪到内边距框。content-box:	背景被裁剪到内容框。|
|background-origin|规定背景图片的定位区域。|padding-box:背景图像相对于内边距框来定位。border-box:背景图像相对于边框盒来定位。content-box:背景图像相对于内容框来定位。|
|background-size|规定背景图片的尺寸。|cover:把背景图像扩展至足够大，以使背景图像完全覆盖背景区域。背景图像的某些部分也许无法显示在背景定位区域中。contain:把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域。length:设置背景图像的高度和宽度。第一个值设置宽度，第二个值设置高度。如果只设置一个值，则第二个值会被设置为 "auto"。|

background的填充范围border + padding + content（填充起始位置：padding的左上角，背景图不会放在内容区里面，放到padding里）

background-position:center center;  水平垂直居中

background-repeat: no-repeat; 不重叠 | repeat-x  在X轴重复

缩写background：颜色 url（地址）no-repeat  center center ；repeat和center可以换位置

background-attachment:背景图片滚动方式scroll默认模式 | fixed随着滚动条滚动

单行文本居中 line-height：设置与模块高度相同就可以让文本居中

## 字体

|属性|描述|值|
|-|-|-|
|font|在一个声明中设置所有字体属性。|font:italic bold 12px/20px arial,sans-serif;|
|font-family|规定文本的字体系列。|font-family:"Times New Roman",Georgia,Serif;|
|font-size|规定文本的字体尺寸。|可以是像素或者百分比|
|font-style||normal:默认值。浏览器显示一个标准的字体样式。italic:浏览器会显示一个斜体的字体样式。oblique:	浏览器会显示一个倾斜的字体样式。|

在设置字体的时候，英文字体写在前面，中文字体写在后面

font-family: 字体属性   <font-family:"Arail","Microsoft Yahei","simsun">

font-size:字体大小，最小字体大小12px 默认16px

font-style:倾斜

font-weight:加粗

color：颜色

text-decoration: underline  下划线

text-indent: 2em首行缩进，

text-align:center;(center,center)

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
