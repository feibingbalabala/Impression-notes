# Js初探

## 常量和变量

常量：一直不变的量；

变量：其值可能发生变量的量

定义变量：var a；var操作符

javascript的变量为弱变量，可以用来保存数据和数据类型

标识符指的是变量，函数，属性的名字，或者行数的参数，变量命名的规范，关键字与保留字

标识符命名规范

1. 第一个字符必须是一个字母，下划线(_）说是一个美元符号$，其他字符可以是字母，下划线，美元符号或数字
2. 区分大小写
3. 不能有空格
4. 不能以关键字或保留字命名

标识符的命名方法：

匈牙利命名法：（属性+类型+对象描述）g_bStatus
小驼峰命名法：clickBtn 第一个小写
大驼峰命名法：ClickBtn 第一个大写

## 推荐(具体还是根据公司项目来定)

1. 遵循小驼峰命名法，
2. 变量和属性：以名词开头
3. 方法和函数：以动词开头
4. 常量：全部字母大写，如果出现多个单词组合，使用下划线分开（PI_API）
5. 构造函数：首字母大写，也就是遵循大驼峰命名法；

## 避免命名冲突的方法

1、协同命名（在项目之初确认好命名规则）

2、对象命名空间

```js
var a = {}；
    a.name = 1;
var b = {};
    b.name = 2;
```

3、匿名函数

```js
(function () {
  ...
})
```

## JS中的六种数据类型

undefined：值未定义，不做任何定义的值

Null：空对象

Number：数字NaN（not a number）比如a/3就不是一个数字

String：字符串“” ''双引号单引号都可以，整个是字符串

Boolean：布尔值 true false(这里有一个点值得注意，作为布尔值的判断只有1是true，其他都是false，但如果使用Boolean()函数则只有0是false其他都是true)

Object：对象

声明对象

每个属性用,隔开，结束没有符号
var a = {
  "属性"："属性值"
}

```js
var a = {
  "name": "jwy",
  "sex": "18",
  "age": "12"
}
```

## 操作符

赋值操作符：=，+=，-=，*=，/=，a+=1（a=a+1）

算术操作符：+,-,*,/,%(取余)和被除数有关，和除数无关如3%-7=3

关系操作符：>,<,<=,>=,==等于(值一不一样),===全等（值和类型）,!=

"ba"<"b";false

"ba">"b“；true先比较第一个值，在比较第二个值

条件操作符：（条件判断语句）？（语句1）：（语句2）真的执行语句1，假的执行语句2

逻辑操作符：||（或） &&（与） ！（非）！true是false！false是true

递增操作符：++，a = a+1

递减操作符：--，b = b-1

a = 3; b = 3

c=a++  +b :c=a+b,a++,c=6, a=4;先做别人的东西

c=++a  +b：a++，c=a+b，c=7, a=4；先做自己的，在做别人的

## 值判断

```js
undefined // false

null // false

{} // 对象 true

'' // 空字符串  false

'   ' // 空格字符串 true

0 // false

1 // true

NaN // false

NaN == NaN // false (javascript中唯一自己不等于自己的)

undefind == null // true

undefind == undefind // true

null == null // true

{} == {} // false(对象的存储空间不同)

2 == true // false

Boolean(2) == true // true
```

## 操作符的优先级

逻辑非

算术

关系

逻辑与逻辑或

条件操作符

赋值操作符

小括号可以提升优先级

## 数据类型转换

<!-- 将数字转化成字符串，将字符串转换成数字

隐式装换

数字->字符串

1. “+" 字符串拼接123+""="123"，数字+字符串=字符串

字符串->数字

+-*/$

1. “123”-0=123
2. “123”/1
3. “123”*1
4. +“123”
5. “123”%比数字大

显示转换

字符串->数字

1. Number()，0xf十六进制，console.log(Number())
2. parseInt()整数，从左往右取数字，到第一个非数字console.log(parseInt())
3. parseFloat()小数，取到第二个小数点之前的数console.log(parseFloat())
4. toFixed()保留几位小数 a=123.456;a.toFixed(2)// 保留两位小数，四色五入

数字->字符串

1. a.toString(2)括号内代表进制；
2. string(a) -->

### NaN

1. Not a Number
2. undefined进行任何数学运算
3. 非数字型字符串，进行了数学运算（+会变为连字符，所以+通常不会触发问题）

### tips

1. NaN 类型为 数字（number）
2. NaN != NaN
3. NaN在布尔值中是false
4. 两种检测数据属于那种布尔值的方法，一种是将数据与两种布尔值比较（==）；另一种是对数据取反，如(!NaN)

### Infinity

无穷 Infinity；负无穷 -Infinity；类型：number

### 数据类型之间的比较

1. 字符串类型，逐位比较（"54" > "200121"）
2. undefined == undefined == null == null
3. {} != {} ; var obj = {}; obj == obj
4. 数字类型的字符串与数字相等 "3434" == 3434

```js
// 1、显示转换
// 1.1字符串转数字
  // Number()
    var num1 = Number(true);             // 1
    var num2 = Number(12);              // 12
    var num3 = Number(null);            // 0
    var num4 = Number(undefined);       // NaN
    var num5 = Number("Hello World");  // NaN，调用toString()
    var num6 = Number("0000011");     // 11
    var num7 = Number(" ");             // 0
    var num8 = Number(1.222);          // 1
    // 如果是对象，则调用valueOf()方法
    var obj = {
        "name": "3",
        "age": "4"
    }
    console.log(obj.valueOf());
    // 总结：
        // 1.  如果是Boolean值，true和false转换就是1和0。
        // 2.  如果是数值，只是简单的传入和返回。
        // 3.  如果是null值，则返回0。
        // 4.  如果是undefined，返回NaN。
        // 5.  如果字符串只包含数字（包括前面正负号）则转成十进制如： “123”变成123; “0123”变成123
        // 6.  如果字符包含浮点格式如“1.1”会忽略小数点转变成1
        // 7.  如果字符串是空的，则转成0
        // 8.  如果字符串包含上述格式外的，则转成NaN
        // 9.  如果是对象，则调用对象valueOf()方法，
        // 10. 如果转换的结果是NaN,那么调用toString()方法。

  // parseInt()
    var num1 = parseInt("123sf") ;      // 123
    var num2 = parseInt(" ");           // NaN
    var num3 = parseInt("0xA");        // 10（16进制）
    var num4 = parseInt("22.5");       // 22
    var num5 = parseInt("070");       // 56(八进制)
    var num6 = parseInt("70");        // 70
    var num7 = parseInt("0xf");       // 15
    console.log(num7);

    // 在使用parseInt()解析像八进制字面的字符串时，比如parseInt（"010"）方法在不同浏览器下存在兼容问题谷歌：10；IE6、IE7、IE8会按照8进制进行转换，结果为8；
    var num8 = parseInt("010");
    // console.log(num8);
    // 解决方法是：
    // var num8 = parseInt("010", 10);

    // 总结：
      // parseInt()函数在转换字符串时，更多的是看其是否符合数值模式。它会忽略字符串前面的空格，直至找到第一个非空格字符。如果第一个字符不是数字字符或者负号，parseInt()就会返回NaN，如果是空字符串，则会返回NaN。如果第一个字符是数字字符，parseInt()会继续解析第二个字符，直到解析完所有后续字符或者遇到非数字字符。

  // parseFloat()
    var num1 = parseFloat("1234blue");   //1234
    var num2 = parseFloat("0xA");        // 0
    var num3 = parseFloat("22.5");       // 22.5
    var num4 = parseFloat("22.34.5");    // 22.34
    var num5 = parseFloat("3.125e7");   // 31250000
    console.log(num5);

    // 总结：
      // parseFloat()可以返回小数。parseFloat()转换的时候，也是从第一个字符开始解析每个字符，直到解析到字符串末尾，或者解析到遇见一个无效的浮点数字字符为止，也就是说，字符串中的第一个小数点是有效的，而第二个小数点就是无效的。

// 1.2数字转字符串
  // toString()方法引入：
    // 当然toString可以通过输入基数以二进制，八进制，十六进制，乃至其他有效的进制格式表示字符串。
    var num = 10;
    console.log(num.toString());    // '10'
    console.log(num.toString(2));   // '1010'
    console.log(num.toString(16));  // 'a'
  // toFixed()方法引入：
      // 保留几位小数。  输出类型：string
      // toFixed() 方法可把 Number数值 四舍五入为指定小数位数的数字。
      var a = 0.1;
      var b = 0.23;
      var c = a + b;
      console.log(c); //0.33
      console.log(c.toFixed(3)); //0.330
      console.log(typeof(c.toFixed(2))); // String

// 2、隐式转换
  // 隐式转换的方式可以通过+""、* 1、/ 1的运算来把数值转换成字符串。（可相互）
    // 2.1、数字——字符串： +（连字符）;          数字+字符串=字符串；
        var num = 10;
        var str = num + " ";
        console.log(typeof(str));   //String

    // 2.2、字符串——数字： + - * / %;
      // "123"-0  "123"*0  "123"/0  +"123" "123"%比前面的数值字符串大的数字；
      var num = "520";
      console.log(typeof(num - 0));
      console.log(typeof(num * 0));
      console.log(typeof(num / 0));
      console.log(typeof(+ num));
      console.log(typeof(num % 600));

// 显示隐式的选用原则——使用显示转换
```