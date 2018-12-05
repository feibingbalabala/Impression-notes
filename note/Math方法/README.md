# Math方法

## PI

```js
Math.PI
```

## 随机数

Math.random（）;取值范围(0, 1)大于等于0小于1

```js
Math.random()

// 1到30
// 1 <parseInt(Math.random() *29 +1 ) <30
// 50到100
// 50 < Math,round() * 50+50 < 100
// 取整数
// 39 <= Math.radom() <=99
Math.ceil(Math.random * 61 +38)
```

Math.random()的取值应该是0-1（事实上取不到0和1）之间的随机小数，

乘以8之后应该是0-8之间的随机小数，也就是0.****到7.****之间的小数（大于0而小于8），经过int类型转换之后，应该是0-7之间的随机整数，所以"+1"之后就会得到1－8之间的

## 舍入取整方法

ceil，向上取整（整数就是本身）
floor，向下取整
round，四舍五入最近整数；

## 取数组中的最大值和最小值

Math.max(放需要比较的数字，用逗号隔开)

Math.min()

```js
var arr = [11, 13, 7, 3, 4, 6, 10];
var max = arr[0];
var min = arr[0];
for (var i = 1; i <= arr.length; i++){
  if (max < arr[i]) {
        max = arr[i];
  }
  if (min > arr[i]){
        min = arr[i]
  }
}
console.log(max);
console.log(min);
```

## 三角函数

<img src='./images/image1.png' width='400'>

```js
sin(0); // 0
sin(Math.PI / 2); // 1
sin(Math.PI); // 接近0
cos(0); // 1
cos(Math.PI / 2); // 接近0
cos(Math.PI); // -1
```

## 次幂

```js
Math.pow(x, y);
// x 的 y 次幂
```

## 算术平方根

```js
Math.sqrt(9);
```

## 构造函数

new 构造函数实例化

获得当前计算机时间

```js
var date = new Date();必须先获取时间
//年
date.getFullYear();
//月数值0~11;
date.getMonth();
//日
date.getDate();
//今天周几（0~6）
date.getDay();
//小时
date.getHours();
//分
date.getMinutes();
//秒
date.getSeconds();
//毫秒
date.getMilliseconds();
// 获取国际时间是UTC
date.getUTCMillisecond(); // 本初子午线时间
// 不能是date.getUTCyear（）；
date.getTime(); // 获取某个时间到现在的毫秒熟；
// 修改时间：
date.setFullYear(2013);
date.setMonth(0);
date.setDate(1);
date.setHours(0);
date.setMinutes(0);
date.setSeconds(0);
date.setMillseconds(0);
date.setDay(); // 报错
date.setUTCTime(); // 报错
date.setUTCDay(); // 报错
date.setUTCYear(); // 报错
```