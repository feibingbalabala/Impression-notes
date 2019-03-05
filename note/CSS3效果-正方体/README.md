# 正方体的旋转

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <style>
      div {
        margin: 0;
        padding: 0;
      }
      .wrap-box {
        perspective: 800px;
      }
      .wrap {
        color: white;
        position: relative;
        transform-style: preserve-3d;
        animation: mupiao 3s infinite linear running;
        transform-origin: center 100px -100px;
      }
      .wrap div {
        width: 200px;
        height: 200px;
        position: absolute;
        top: 0px;
        left: 0px;
        opacity: 0.6;
        border-radius: 50px;
        border: 1px solid white;
        transform-origin: center center -100px;
      }
      .wrap div:nth-of-type(1) {
        background: red;
        transform: rotateY(0deg);
      }
      .wrap div:nth-of-type(2) {
        background: green;
        transform: rotateY(90deg);
      }
      .wrap div:nth-of-type(3) {
        background: blue;
        transform: rotateX(180deg);
      }
      .wrap div:nth-of-type(4) {
        background: purple;
        transform: rotateY(270deg);
      }
      .wrap div:nth-of-type(5) {
        background: yellow;
        transform: rotateX(90deg);
      }
      .wrap div:nth-of-type(6) {
        background: cyan;
        transform: rotateX(270deg);
      }
      @keyframes mupiao{
        0%{
          transform: rotateY(0deg);
        }
        100%{
          transform: rotateY(-360deg);
        }
      }
    </style>
  </head>
  <body>
    <div class="wrap-box">
      <div class="wrap">
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
      </div>
    </div>
  </body>
</html>
```