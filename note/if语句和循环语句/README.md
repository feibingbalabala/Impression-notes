# if语句和循环语句

## if

```js
if () {
  ...
} else {
  ...
}
```

<img src='./images/image1.jpg' width='400'>

else与if的配对原则：else与其之上的没有else配对的if配对，else的数量永远小于或等于if的数量

## for

for循环的使用情况：数量方面有一定的范围限制，为多个类似或同一类型的标签添加同样的或有规律的动作
for（初始化；判断条件；递增语句）{}三个条件都可以少，但是;不能少

```js
for (var i = 0; i < length; i ++) {

}
```

<img src='./images/image2.jpg' width='400'>

```js
// 案例1
var sum = 0;
for (var i = 1 ; i < 100 ; i++) {
  if  (i % 3 == 0) {
    sum = sum + i;
  } else {
    sum = sum + 1;
  }
}
console.log(sum);

// 案例2
var sum = 0;
for (var i = 1;i <= 9;i ++){
  for (var j = 1; j <= 9; j++) {
    sum = i*j +sum
  }
}
console.log(sum);

// 案例3
var i = 0;
for (;;) {
  if (i >= 10) {
    // 跳出循环
    break
  }
  console.log(i)
  i++;
}

// 案例4
for (var i = 0; i < 10: i++) {
  if (i === 5) {
    // 跳出当前循环，继续下次循环
    continue
  }
  console.log(i)
}
```

## while

<img src='./images/image3.jpg' width='400'>

## switch

```js
switch
var x = 7;
switch(x) {
  case 1: console.log("one");
          break;
  case 2: console.log("two");
          break;
  case 3: console.log("three");
          break;
  case 4: console.log("four");
          break;
  case 5: console.log("fine");
          break;
  case 6: console.log("six");
          break;
  default: console.log('seven');
}
```

## forEach

没有返回值，每个item都执行，设置return没用

```js
let arr = [1, 2, 3, 4, 5];
arr.forEach((value, index) => {
  if (value > 3) {
    console.log(value) // 4 5
  } else {
    console.log(value) // 1 2 3
  }
});
```

## some

当内部return true时跳出整个循环

```js
let arr = [1, 2, 3, 4, 5];
arr.some((value, index) => {
  if (value === 3) {
    return true; //当内部return true时跳出整个循环
  }
  console.log(value)// 1 2
});
```

## every

当内部return false时跳出整个循环

```js
//every()当内部return false时跳出整个循环
let arr = [1, 2, 3, 4, 5];
arr.every((value, index) => {
  if (value > 3) {
    console.log(value)// 4
    return false;
  } else {
    console.log(value)// 1 2 3
    return true;
    // 如果没有返回值true 的话，也会跳出循环(函数默认返回值是undefined，转换成Boolean也是false)
  }
});
```