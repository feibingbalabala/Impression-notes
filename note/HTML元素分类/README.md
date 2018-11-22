# HTML元素的分类

## 块元素

div：无语义，常用于布局

aside：表示article元素的内容之外的与article元素的内容相关内容

figure：表示一段独立的流内容；使用&lt;figcaption&gt;元素为其添加标题

例：

```html
 <figure>
  <figcaption>PRC</figcaption>
  <p>the people......</p>
</figure>
```

dialog：该标签定义对话

例：

```html
<dialog>
  <dt>老师</dt>
  <dd>2+2等于？</dd>
  <dt>学生</dt>
  <dd>4</dd>
</dialog>
```

## 行元素

span：无语义，多用于布局

mark：呈现突出显示的&lt;mark&gt;...&lt;/mark&gt;

time：表示日期会时间；

meter：表示度量衡，用于已知最大与最小值得度量；

progress：表示运行中的进程；

## 行元素——块元素的区别：

行元素：不能设置宽高，内容撑开宽度，自左向右排列；

块元素：默认占用一整行，并且总是从新的一行开始，默认是自适应宽度；

## 第三类元素

### 结构元素

section：定义文档的衣蛾区段，如章节、页眉等，可以与h1...h6配合使用；

article：表示文档中的一块独立的内容，如博客或报纸的一篇文章；

header：表示页面中一个内容区块或整个页面的标题；

nav：表示导航链接的部分；

footer：表示整个页面或页面中一个内容区块的脚注。

### 多媒体元素：

video和audio：分别用来插入视频和声音；

### 交互性元素

details：表示用户要的并可得到的细节信息，可与summary配合使用；

例：

```html
<details>
  <summary>HTML5</summary>
  <code>this document teachers you have to learn about HTML5.</code> 
</details>
```

datagrid：表示可选数据的列表，通常用于显示树列表；

menu：表示菜单列表，通常用于列出表单控件；

例：

```html
<menu>
  <li><input type="checkbox"/>Red</li>
  <li><input type="checkbox"/>Blue</li>
</menu>
```

command：表示命令按钮，如单选、复选、普通按钮。

### input元素类型

email：用于应包含E-mail地址的输入域；

url：用于应包含URL地址的输入域；

number：用于应包含数值的输入域；

range：用于应包含一定范围内数字值得输入域；

search：用于搜索域，如站点搜索；

### HTML5的多个供选取日期和时间的新输入类型

date：——选取年、月、日；

month：——选取月、年；

week：——选取周、年；

time：——选取时间（小时和分钟）；

datetime：——选取时间、日、月、年；

datetime-local：选取时间、日、月、年（本地时间）；