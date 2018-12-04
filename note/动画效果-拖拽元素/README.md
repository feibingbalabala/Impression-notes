# 推拽元素

|属性|描述|
|--|--|
|mousedown|鼠标按下事件|
|mouseup|鼠标抬起事件|
|mouseup|鼠标抬起事件|
|mouseover|鼠标在标签上事件|
|mouseout|鼠标在标签外事件|
|mouseenter|鼠标移入标签事件|
|mouseleave|鼠标移出标签事件|
|mousemove|鼠标在标签内移动事件|

不论鼠标指针穿过被选元素或其子元素，都会触发 mouseover 事件。对应mouseout

只有在鼠标指针穿过被选元素时，才会触发 mouseenter 事件。对应mouseleave

mouseenter子元素不会反复触发事件，否则在IE中经常有闪烁情况发生。

event 对象 执行一个事件，他会提供鼠标的位置或者键盘的按键

阻止默认事件 preventDefault

```js
if(evt.preventDefault){
  evt.preventDefault(); //chrome
} else {
  evt.returnVale = false; //ie
}
```

## 拖拽案例