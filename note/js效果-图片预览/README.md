# 图片预览

通过input[type='file']拿到对应的数据，并没有上传图片获取远程图片的url

```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML5上传图片预览</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <script src="moble_js/jquery-1.11.3.min.js"></script>
  </head>
  <body>
    <h3>请选择图片文件：JPG/GIF</h3>
    <form name="form0" id="form0" >
      <div>
        <input type="file" name="file0" id="file0" multiple="multiple" />
      </div>
      <div>
        <img src="" id="img0"  style="width: 100px;height: auto;">
      </div>
    </form>
    <script>
      $("#file0").change(function(){
        var objUrl = getObjectURL(this.files[0]);
        var objUrl1 = getObjectURL(this.files[1]);
        console.log("objUrl:" + objUrl);
        if (objUrl) {
          $("#img0").attr("src", objUrl);
        }
      });
      //建立一個可存取到該file的url
      function getObjectURL(file) {
        var url = null;
        if (window.createObjectURL != undefined) { // basic
          url = window.createObjectURL(file) ;
        } else if (window.URL != undefined) { // mozilla(firefox)
          url = window.URL.createObjectURL(file) ;
        } else if (window.webkitURL != undefined) { // webkit or chrome
          url = window.webkitURL.createObjectURL(file) ;
        }
        return url; // 无法得到绝对路径，只能得到浏览器返回的一个data:开头的数据,这是浏览器的安全机制
      }
    </script>
  </body>
</html>
```