# css选择器

## 属性选择器

```css
.wrap input[type="password"] {
  background-color: #cff;
}
```

## 毗邻选择器

(X + Y)它将只选择紧贴在X元素之后Y元素。下面的例子，仅每一个ul之后的第一个段落元素的文本为红色

```html
<style>
  ul + p {
    color: red;
  }
</style>
<ul></ul>
<p></p>
```

## 兄弟选择器

(X ~ Y)这是兄弟选择符和毗邻选择器一样，然而，它没有约束。与毗邻选择符（ul + li）仅选择前一个选择符后面的第一个元素比起来，兄弟选择符更宽泛。它会选择，我们上面例子中更在ul后面的任何p元素。

## 子代选择器

(X > Y)X Y和X > Y之间的不同点是后者只选择直接子代。

```html
<div class="container">
  <ul>
    <li> List Item
      <ul>
        <li> Child </li>
      </ul>
    </li>
    <li> List Item </li>
  </ul>
</div>
```

选择符.container > ul将只选择类名为container的div的直接子代ul。它不匹配更深层的li的子代的ul。因此，使用子代选择符有性能上的优势。