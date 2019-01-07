# 去重

## 简单数组去重

```js
function uniq(array){
  var temp = []; // 一个新的临时数组
  var len = array.length;
  for(var i = 0; i < len; i++){
    // 使用indexOf判断temp数组中是否存在，不存在则进入temp数组中
    if(temp.indexOf(array[i]) == -1){
      temp.push(array[i]);
    }
  }
  return temp;
}
var array = [1, 2, 2, 3];
console.log(uniq(array)) // p[1, 2, 3]
```

## 利用对象中key的唯一性去重

```js
function uniq(array){
    var temp = {};
    var r = [];
    var len = array.length;
    var val = '';
    var type = '';
    for (var i = 0; i < len; i++) {
      val = array[i];
      type = typeof val;
      // 新建一js对象以及新数组，遍历传入数组时，判断值是否为js对象的键，不是的话给对象新增该键并放入新数组。
      if (!temp[val]) {
        temp[val] = [type];
        r.push(val);
        // 判断是否为js对象键时，会自动对传入的键执行“toString() 使用indexOf判断”，
      } else if (temp[val].indexOf(type) < 0) {
        temp[val].push(type);
        r.push(val);
      }
    }
    return r;
}

var array = [1, 2, "2", 4, 4];
console.log(uniq(array));
```

## 排序将相邻的数字先放在一起（缺点是数据会被打乱）

```js
function uniq(array) {
  // 做一个排序，相同的值就会相邻在一起
  array.sort();
  var temp = [array[0]];
  var len = array.length;
  for(var i = 1; i < len; i++){
    // 遍历数组后，新数组把与前面值不同的加入进去
    if(array[i] !== temp[temp.length - 1]){
      temp.push(array[i]);
    }
  }
  return temp;
}

var array = [1, 2, "2", 4, 4];
console.log(uniq(array));
```

## 利用数组下标

```js
function uniq(array){
  var temp = [];
  var len = array.length;
  for(var i = 0; i < len i++) {
    // 如果当前数组的第i项在当前数组中第一次出现的位置是i，才存入数组；否则代表是重复的
    // 利用indexOf()返回的是数组下标
    if(array.indexOf(array[i]) == i){
      temp.push(array[i])
    }
  }
  return temp;
}

var array = [1, 2, "2" ,4 , 4];
console.log(uniq(array));
```

## 保存最右边的

```js
function uniq(array){
  var temp = [];
  var index = [];
  var len = array.length;
  for(var i = 0; i < len; i++) {
    for(var j = i + 1; j < len; j++){
      if (array[i] === array[j]){
        i++;
        j = i;
      }
    }
    temp.push(array[i]);
    index.push(i);
  }
  console.log(index);
  return temp;
}

var array = [1, 2, 2, 3, 4, 3];
console.log(uniq(array));
```

## 数组中包含对象去重

这里必须需要一个对象中的key作为唯一值判断

```js
var oldArr = [
  {id: 1, name: "zhangs1"},
  {id: 1, name: "zhangs2"},
  {id: 2, name: "zhangs3"},
  {id: 3, name: "zhangs4"},
  {id: 4, name: "zhangs5"},
  {id: 4, name: "zhangs6"}
];
var allArr = [];
for(var i = 0;i < oldArr.length; i++){
  var flag = true;
  // 利用状态来一个标记来判断是否需要进入数组
  for(var j = 0; j < allArr.length; j++){
    if(oldArr[i].id == allArr[j].id){
      flag = false;
    };
  };
  if(flag){
    allArr.push(oldArr[i]);
  };
};
```