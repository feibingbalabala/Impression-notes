# 数组

## Array 对象

```js
new Array();
new Array(size);
new Array(element0, element1, ..., elementn);
```

### 参数

参数 size 是期望的数组元素个数。返回的数组，length 字段将被设为 size 的值。

参数 element ..., elementn 是参数列表。当使用这些参数来调用构造函数 Array() 时，新创建的数组的元素就会被初始化为这些值。它的 length 字段也会被设置为参数的个数。

### 返回值

返回新创建并被初始化了的数组。

如果调用构造函数 Array() 时没有使用参数，那么返回的数组为空，length 字段为 0。

当调用构造函数时只传递给它一个数字参数，该构造函数将返回具有指定个数、元素为 undefined 的数组。

当其他参数调用 Array() 时，该构造函数将用参数指定的值初始化数组。

当把构造函数作为函数调用，不使用 new 运算符时，它的行为与使用 new 运算符调用它时的行为完全一样。

## 数组方法

|方法|描述|语法|
|-|-|-|
|concat()|连接两个或更多的数组，并返回结果。|arrayObject.concat(arrayX,arrayX,......,arrayX)。arrayX必需。该参数可以是具体的值，也可以是数组对象。可以是任意多个。|
|join()|把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。|arrayObject.join(separator)。separator可选。指定要使用的分隔符。如果省略该参数，则使用逗号作为分隔符。|
|pop()|删除并返回数组的最后一个元素。（shift（）相反）|arrayObject.pop()|
|push()|向数组的末尾添加一个或更多元素，并返回新的长度。|arrayObject.push(newelement1,newelement2,....,newelementX)。newelement1必需。要添加到数组的第一个元素。newelement2可选。要添加到数组的第二个元素。|
|reverse()|颠倒数组中元素的顺序。|arrayObject.reverse()|
|shift()|删除并返回数组的第一个元素。（pop()相反）|arrayObject.shift()|
|slice()|从某个已有的数组返回选定的元素。|arrayObject.slice(start,end)。start必需。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。end可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。(不包含end)|
|sort()|对数组的元素进行排序。|arrayObject.sort(sortby)。sortby可选。规定排序顺序。必须是函数。|
|splice()|删除元素，并向数组添加新元素。|arrayObject.splice(index,howmany,item1,.....,itemX)。index必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。howmany必需。要删除的项目数量。如果设置为 0，则不会删除项目。item1, ..., itemX可选。向数组添加的新项目。|
|toSource()|返回该对象的源代码。|object.toSource()只有 Gecko 核心的浏览器（比如 Firefox）支持该方法，也就是说 IE、Safari、Chrome、Opera 等浏览器均不支持该方法。|
|toString()|把数组转换为字符串，并返回结果。|arrayObject.toString()|
|toLocaleString()|把数组转换为本地数组，并返回结果。|arrayObject.toLocaleString()|
|unshift()|向数组的开头添加一个或更多元素，并返回新的长度。|arrayObject.unshift(newelement1,newelement2,....,newelementX)。newelement1必需。向数组添加的第一个元素。newelement2可选。向数组添加的第二个元素。|
|valueOf()|返回数组对象的原始值|arrayObject.valueOf()。valueOf() 方法通常由 JavaScript 在后台自动调用，并不显式地出现在代码中|
