# js效果-全选按钮

```html
<!DOCTYPE HTML>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>无标题文档</title>
  </head>
  <body>
    <form>
      请选择你爱好:<br>
      <input type="checkbox" name="hobby" id="hobby1">  音乐
      <input type="checkbox" name="hobby" id="hobby2">  登山
      <input type="checkbox" name="hobby" id="hobby3">  游泳
      <input type="checkbox" name="hobby" id="hobby4">  阅读
      <input type="checkbox" name="hobby" id="hobby5">  打球
      <input type="checkbox" name="hobby" id="hobby6">  跑步 <br>
      <input type="button" value = "全选" onclick = "checkall();">
      <input type="button" value = "全不选" onclick = "clearall();">
      <p>请输入您要选择爱好的序号，序号为1-6:</p>
      <input id="wb" name="wb" type="text" >
      <input name="ok" type="button" value="确定" onclick = "checkone();">
    </form>
    <script type="text/javascript">
      function checkall() {
        var hobby = document.getElementsByTagName("input");
        // 思路其实就是遍历所有的input，给他们添加checked
        for (let i = 0; i < hobby.length; i++) {
          if (hobby[i].type == 'checkbox') {
            hobby[i].checked = 'checked';
          }
        }
      }
      function clearall() {
        var hobby = document.getElementsByName("hobby");
        // 遍历所有的input，给他们清除checked
        for (let j = 0; j < hobby.length; j++) {
          if (hobby[j].type == 'checkbox') {
            hobby[j].checked = '';
          }
        }
      }
      function checkone() {
        var j = document.getElementById("wb").value;
        switch(Number(j)){
          case 1:
            document.getElementById("hobby1").checked = 'checked';
            break;
          case 2:
            document.getElementById("hobby2").checked = 'checked';
            break;
          case 3:
            document.getElementById("hobby3").checked = 'checked';
            break;
          case 4:
            document.getElementById("hobby4").checked = 'checked';
            break;
          case 5:
            document.getElementById("hobby5").checked = 'checked';
            break;
          case 6:
            document.getElementById("hobby6").checked = 'checked';
            break;
          default:
            alert("input is nou in 1~6!!");
        }
      }
    </script>
  </body>
</html>
```