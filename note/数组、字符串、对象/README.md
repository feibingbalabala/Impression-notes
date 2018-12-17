# 数组 字符串 对象

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
|:-|:-|:-|
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

## String 对象

```js
new String(s);
String(s);
```

### 参数

参数 s 是要存储在 String 对象中或转换成原始字符串的值。

### 返回值

当 String() 和运算符 new 一起作为构造函数使用时，它返回一个新创建的 String 对象，存放的是字符串 s 或 s 的字符串表示。

当不用 new 运算符调用 String() 时，它只把 s 转换成原始的字符串，并返回转换后的值。

<img src='./images/image1.png' width='400'>

## 字符串方法

|方法|描述|语法|
|:-|:-|:-|
|anchor()|创建 HTML 锚。|stringObject.anchor(anchorname)。anchorname必需。为锚定义名称。|
|big()|用大号字体显示字符串。|stringObject.big()|
|blink()|显示闪动字符串。|stringObject.blink()|
|bold()|使用粗体显示字符串。|stringObject.bold()|
|charAt()|返回在指定位置的字符。|stringObject.charAt(index)。index必需。表示字符串中某个位置的数字，即字符在字符串中的下标。|
|charCodeAt()|返回在指定的位置的字符的 Unicode 编码。|stringObject.charCodeAt(index)。index。必需。表示字符串中某个位置的数字，即字符在字符串中的下标。|
|concat()|连接字符串。|stringObject.concat(stringX,stringX,...,stringX)。stringX必需。将被连接为一个字符串的一个或多个字符串对象。|
|fixed()|以打字机文本显示字符串。|stringObject.fixed()|
|fontcolor()|使用指定的颜色来显示字符串。|stringObject.fontcolor(color)。color必需。为字符串规定 font-color。该值必须是颜色名(red)、RGB 值(rgb(255,0,0))或者十六进制数(#FF0000)。|
|fontsize()|使用指定的尺寸来显示字符串。|stringObject.fontsize(size)。size 参数必须是从 1 至 7 的数字。|
|fromCharCode()|从字符编码创建一个字符串。|String.fromCharCode(numX,numX,...,numX)。numX必需。一个或多个 Unicode 值，即要创建的字符串中的字符的 Unicode 编码。|
|indexOf()|检索字符串。|stringObject.indexOf(searchvalue,fromindex)。searchvalue必需。规定需检索的字符串值。fromindex可选的整数参数。规定在字符串中开始检索的位置。它的合法取值是 0 到 stringObject.length - 1。如省略该参数，则将从字符串的首字符开始检索。indexOf() 方法对大小写敏感！|
|italics()|使用斜体显示字符串。|stringObject.italics()|
|lastIndexOf()|从后向前搜索字符串。|stringObject.lastIndexOf(searchvalue,fromindex)。searchvalue必需。规定需检索的字符串值。fromindex可选的整数参数。规定在字符串中开始检索的位置。它的合法取值是 0 到 stringObject.length - 1。如省略该参数，则将从字符串的最后一个字符处开始检索。|
|link()|将字符串显示为链接。|stringObject.link(url)。url必需。规定要链接的 URL。|
|localeCompare()|用本地特定的顺序来比较两个字符串。|stringObject.localeCompare(target)。target要以本地特定的顺序与 stringObject 进行比较的字符串。|
|match()|找到一个或多个正则表达式的匹配。|stringObject.match(searchvalue。stringObject.match(regexp)。searchvalue必需。规定要检索的字符串值。regexp必需。规定要匹配的模式的 RegExp 对象。如果该参数不是 RegExp 对象，则需要首先把它传递给 RegExp 构造函数，将其转换为 RegExp 对象。|
|replace()|替换与正则表达式匹配的子串。|stringObject.replace(regexp/substr,replacement)。regexp/substr必需。规定子字符串或要替换的模式的 RegExp 对象。replacement必需。一个字符串值。规定了替换文本或生成替换文本的函数。|
|search()|检索与正则表达式相匹配的值。|stringObject.search(regexp)。regexp该参数可以是需要在 stringObject 中检索的子串，也可以是需要检索的 RegExp 对象。var str="Visit W3School!"
document.write(str.search(/w3school/i))。忽略大小写|
|slice()|提取字符串的片断，并在新的字符串中返回被提取的部分。|stringObject.slice(start,end)。start要抽取的片断的起始下标。如果是负数，则该参数规定的是从字符串的尾部开始算起的位置。也就是说，-1 指字符串的最后一个字符，-2 指倒数第二个字符，以此类推。end紧接着要抽取的片段的结尾的下标。若未指定此参数，则要提取的子串包括 start 到原字符串结尾的字符串。如果该参数是负数，那么它规定的是从字符串的尾部开始算起的位置。(不包括end)|
|small()|使用小字号来显示字符串。|stringObject.small()|
|split()|把字符串分割为字符串数组。|stringObject.split(separator,howmany)。separator必需。字符串或正则表达式，从该参数指定的地方分割 stringObject。howmany可选。该参数可指定返回的数组的最大长度。如果设置了该参数，返回的子串不会多于这个参数指定的数组。如果没有设置该参数，整个字符串都会被分割，不考虑它的长度。|
|strike()|使用删除线来显示字符串。|stringObject.strike()|
|sub()|把字符串显示为下标。|stringObject.sub()|
|substr()|从起始索引号提取字符串中指定数目的字符。|stringObject.substr(start,length)。start必需。要抽取的子串的起始下标。必须是数值。如果是负数，那么该参数声明从字符串的尾部开始算起的位置。也就是说，-1 指字符串中最后一个字符，-2 指倒数第二个字符，以此类推。length可选。子串中的字符数。必须是数值。如果省略了该参数，那么返回从 stringObject 的开始位置到结尾的字串。|
|substring()|提取字符串中两个指定的索引号之间的字符。|stringObject.substring(start,stop)。start必需。一个非负的整数，规定要提取的子串的第一个字符在 stringObject 中的位置。stop可选。一个非负的整数，比要提取的子串的最后一个字符在 stringObject 中的位置多 1。如果省略该参数，那么返回的子串会一直到字符串的结尾。|
|sup()|把字符串显示为上标。|stringObject.sup()|
|toLocaleLowerCase()|把字符串转换为小写。|stringObject.toLocaleLowerCase()|
|toLocaleUpperCase()|把字符串转换为大写。|stringObject.toLocaleUpperCase()|
|toLowerCase()|把字符串转换为小写。|stringObject.toLowerCase()|
|toSource()|代表对象的源代码。||
|toString()|返回字符串。|stringObject.toString()|
|valueOf()|返回某个字符串对象的原始值。|stringObject.valueOf()|

## object对象

JavaScript 提供多个内建对象，比如 String、Date、Array 等等。

对象只是带有属性和方法的特殊数据类型。

创建新对象有两种不同的方法：

1. 定义并创建对象的实例
2. 使用函数来定义对象，然后创建新的对象实例

```js
// 定义并创建对象的实例
let person = new Object();
person.firstname = "Bill";
person.lastname = "Gates";
person.age = 56;
person.eyecolor = "blue";
// 使用函数来定义对象，然后创建新的对象实例
function person(firstname,lastname,age,eyecolor)
{
  this.firstname = firstname;
  this.lastname = lastname;
  this.age = age;
  this.eyecolor = eyecolor;
};
var myFather = new person("Bill", "Gates", 56, "blue");

let obj = {
  name: '',
  action: function () {
    ...
  }
}
// 访问对象的属性
obj.name
// 访问对象的方法
obj.action()
```

### 循环取对象中的值

JavaScript for...in 语句循环遍历对象的属性。

```js
var person = {fname: "Bill", lname: "Gates", age: 56};

for (x in person) {
  txt = txt + person[x];
}
```

### 对象属性的删除

delete运算符可以删除对象中的属性。这里先讲一下delete运算符的内容。

```js
var o = {x: 1, y: 2};
// 删除x属性
delete o.x;
```

### 检测对象的属性属否存在

要判断某一个属性是否存在于某一个对象中。可以通过in运算符，hasOwnProperty()方法或是propertylsEnumerable()方法来进行判断。

hasOwnProperty方法只能测试当前属性是不是对象的自有属性。

propertyIsEnumerable()方法。只有当当前的属性是自有属性，并且是可枚举(enumerable属性为true)的的时候，这一方法才会返回true。

```js
// in运算符
var point = {x: 1};
"x" in point; //这一个表达式最后返回的将会是true。
"toString" in point; //由于toString是继承方法，所以也是返回true.
"z" in point; //这一表达式最后返回false，因为point对象中没有z属性.

// hasOwnProperty()方法
var o = {x: 1};
o.hasOwnProperty("x"); //true：o有这一属性，
o.hasOwnProperty("z"); //false;
o.hasOwnProperty("toString"); //false

// propertyIsEnumerable()方法
o.propertyIsEnumerable("x"); // true
o.propertyIsEnumerable("z"); // false
o.propertyIsEnumerable("toString"); // false。继承属性不可枚举
```

当前的js一般的属性都是有4中属性。分别是：数值属性value，可读属性writable，可枚举属性enumerable，和可配置属性configurable。但是由于对象中存在一类特别的属性存取器属性，所以对于存取器属性的值实际上是有点不同的，他有自己的特别的属性特性包括，读取（get），写入（set），可枚举和可配置。为了实现这一对象属性的描述，js中定义了一个属性描述符对象。并且可以通过Object.getOwnPropertyDescriptor()方法来获取某个对象中的特定属性的描述符。当然当前函数只能获取对象自有属性的描述，如果要获取继承属性的描述符的话，需要使用Object.getPrototypeOf();

```js
var person = {
    name:'jiang',
    age: '18',
    sex: 'boy'
}

Object.defineProperty(person,'age',{
  enumerable:true, //可以被枚举
});
Object.defineProperty(person,'sex',{
  enumerable:false, //可以被枚举
})
```

当我们在定义一个对元素的属性的时候，我们要注意上面两个方法在某些情况之下是会报错误的，情况如下

对象是不可扩展的，所以我们只能对原有的自有属性进行编辑，但是不可以添加新的属性。

如果属性是不可配置的，则不可以修改他的可配置性和可枚举性。

存储器属性是不可配置的，则不可以修改他的setter和getter属性，并且不可以改成数据属性。

数据属性不可配置则不能修改为存储器属性。

数据属性是不可配置情况下，其可写属性不可改false为true，但是可以修改true为false。

如果数据属性是不可配置不可写，不能修改其值，但是可配置不可写，则可以修改。
