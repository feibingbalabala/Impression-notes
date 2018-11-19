# 表格与表单

## 表格

表格的组成

```html
<table>
    <caption>表格名称</caption>
  <thead>
    <tr>
      <th>表头</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>表格主体，用于呈现数据</td>
    </tr>
  </tbody>
  <tfoot>表尾，用来存放统计信息</tfoot>
</table>
```

单元格属性

cellpadding 设置单元格边框与单元格里的内容之间的距离

cellspacing 设置单元格间的距离

colspan 跨列（单元格和并，一行多列）给td加的

rowspan 跨行（单元格和并，一列多行）

border 表格边框

border-collapse：collapse；合并单元格边框

## 表单

```html
<form action="" method="">
  <div>
      <input type="text">
  </div>
</form>
```

form标签：用于提交数据

action：表单提交的地址路径

method：表单提交数据的形式get通常用于获取数据、post通常用于提交数据

单选框

```html
<input type="radio" />
```

复选框

```html
<input type="checkbox">
```

输入框

```html
<input type="text"/>
```

密码框

```html
<input type="password"/>
```

按钮

```html
<input type="button" value="button">
```

下拉框

```html
<select>
  <option>北京</option>
  <option>上海</option>
  <option>广州</option>
</select>
```

多行文本框

```html
<textarea></textarea>
```

选择文件

```html
<input type="file">
```

重置文件

```html
<input type="reset" value="reset">
```

隐藏域(用于提交页面用户没有书写的数据)

```html
<input type="hidden">
```

按钮

```html
<button type="submit">提交</button>
<button type="button">按钮</button>
<button type="reset">重置</button>
```

### label文本信息

label的绑定

1、显式绑定

```html
<label for="username">用户名</label>
<input type="text" id="username">
```

2、隐式绑定

```html
<label>
  用户名
  <input type="text">
</label>
```

### 禁用属性

readonly（只读）

disabled（禁止）

readonly与disabled的区别

1、使用范围不同。disabled适用于所有的表单元素；readonly只适用于输入文本的输入项（输入框、密码框、多行文本框、文件输入框）

2、文本框聚焦状态。disabled不能使输入框框获取焦点；readonly文本框可以聚焦和复制文本，但不能修改

### 表单中的选中属性

选中属性：

checked：

```html
<input type="checkbox" checked>
<input type="radio" checked>
```

selected：

```html
<select>
  <option selected>123</option>
</select>
```

## hack

```html
-     ie6
*    ie6、7
+     ie6、7
\9     ie6、7、8、9、10
\0     ie8、9、10、11
```