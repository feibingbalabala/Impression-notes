# css技巧-换列

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<style>
  .column-list {
  height: 220px;
  width: 100%;

  /* overflow: scroll; */
  writing-mode: vertical-lr;

}
.column-list-item {
  float: left;
  width: 80px;

  writing-mode: horizontal-tb;
}

ul.ul-style {
  list-style: none;

  margin: 20px;
  padding: 0;

}
ul.ul-style  li {
    padding: 0 20px;
    margin: 0 20px 20px 0;

    color: #383838;
  }
  ul.ul-style .add {
    color: #3b90f1;
    cursor: pointer;
  }
</style>
<body>
  <ul class="ul-style column-list">
    <li class="column-list-item">
      <p>{{item}}1</p>
    </li>
    <li class="column-list-item">
      <p>{{item}}2</p>
    </li>
    <li class="column-list-item">
      <p>{{item}}3</p>
    </li>
    <li class="column-list-item">
      <p>{{item}}4</p>
    </li>
    <li class="column-list-item add">
      <p>5</p>
    </li>
  </ul>
</body>
</html>
```