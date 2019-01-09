# js效果-交集、并集、差集

## 利用filter和indexOf进行数学集操作，但是，由于indexOf方法中NaN永远返回-1，所以需要进行兼容处理。

```js
var a = [1,2,3];
var b = [2,4,5];
// 并集
var union = a.concat(b.filter(function(v) {
      return a.indexOf(v) === -1
    }))
// 交集
var intersection = a.filter(function(v){ return b.indexOf(v) > -1 });
// 差集
var difference = a.filter(function(v){ return b.indexOf(v) === -1 });
console.log(union); // [1,2,3,4,5]
console.log(intersection); // [2]
console.log(difference); // [1,3]
```

### 数组中可能存在NaN这种情况

```js
var a = [1, 2, 3, NaN];
var b = [2, 4, 5];
var aHasNaN = a.some(function (v) {
  return isNaN(v)
})
var bHasNaN = b.some(function (v) {
  return isNaN(v)
})
// 并集
// 这里先把NaN取出来，到最后在判断有没有NaN，有就加入
var union = a.concat(b.filter(function (v) {
    return a.indexOf(v) === -1 && !isNaN(v)
  })
).concat(!aHasNaN & bHasNaN ? [NaN] : [])
// 交集
// 最后在判断是不是a、b都有NaN
var intersection = a.filter(function (v) {
  return b.indexOf(v) > -1
}).concat(aHasNaN & bHasNaN ? [NaN] : [])
// 差集
// 这里先把NaN取出来，到最后在判断有没有NaN，有就加入
var difference = a.filter(function (v) {
  return b.indexOf(v) === -1 && !isNaN(v)
}).concat(aHasNaN && !bHasNaN ? [NaN] : [])

console.log(union) // [1,2,3,4,5,NaN]
console.log(intersection) // [2]
console.log(difference)//1,3,NaN
```

## Array.from方法，用于将类数组对象和可遍历对象转化为数组。只要类数组有length长度，基本都可以转化为数组。结合Set结构实现数学集求解。(ES6中)

(Set是ES6提供的新的数据结构，类似于数组，但是值都是唯一的，不会有重复的值)

```js
let a = [1, 2, 3];
let b = [2, 4, 5];
let aSet = new Set(a);
let bSet = new Set(b);
// 并集
let union = Array.from(new Set(a.concat(b)))
console.log(union) // [1,2,3,4,5]
// 交集
let intersection = Array.from(new Set(a.filter(v => bSet.has(v))))
console.log(intersection) // [2]
// 差集
let differenceNew = Array.from(new Set(a.concat(b).filter(v => aSet.has(v) && !bSet.has(v))) [1,3])
console.log(differenceNew)
```