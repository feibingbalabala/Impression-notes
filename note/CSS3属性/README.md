# css3属性

## 圆角(border-radius)

4 左上，右上，右下，左下

3 左上，右下\左上，右下

2 左上右下，右上左下

顺时针

两个值加斜杠/:水平和竖直

1到8个值

水平的改变/竖直的改变

border-radius: 1-4 length|% / 1-4 length|%

遵循顺时针

## 文本阴影(text-shadow)

四个值：0 0 0 color;水平位置，垂直位置，模糊度（不能是负值，可省略）颜色。

color：transparent文字透明

-webkit-text-stroke: 1px #fff;文字描边

## 盒阴影(box-shadow)

box-shadow：0 0 0 0 color;

水平移动 垂直移动 模糊度 阴影外延（可以省略）

box-shadow: inset 内阴影

颜色可以在前面或后面，inset也可以。但是，放在前面inset要在最前面（inset color 0 0 0 0），在后面的inset一定要在最后（0 0 0 0 color inset）

## 背景图(background-size)

只有一个值，另外一个会默认auto

第一个水平，第二垂直

cover等比例放到覆盖容器，背景图可能超出容器

contain将背景图像等比例缩放到宽度或高度与容器的宽度或高度相等，背景图像始终被包括在容器内

### 背景切割

background-clip:

border-box：从border开始背景色的覆盖。（图片的话从padding开始）

padding-box：从padding开始背景色覆盖（可用背景图）

content-box：从width开始覆盖（可用背景图）

### 背景原点

背景图起始点（只对背景图有效）

background-origin: border-box | padding-box | content-box;

## 半透明兼容问题（会导致文字透明）

background：blue

filter：alpha（opacity=50）；取值0~100

opacity：0.5；取值0~1

如果需要背景图半透明，文字不透明可以选用background-color: rgba(red, green, blue, alpha)这个写法