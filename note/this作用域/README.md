# this作用域

this相当于指针

this永远指向他的所有者，如果没有所有者，则指向window

```js
function test () {
  console.log(this);
};
test(); // window

var obj = {};
obj.test = function () {
  console.log(this);
};
obj.test() // obj
```

全局中的this   window

对象.方法种的this  对象

对象.onclick中的this  对象

在严格模式下，this将保持他进入执行上下文时的值，所以下面的this将会默认为undefined

```js
function f2(){
  "use strict"; // 这里是严格模式
  return this;
}

f2() === undefined; // true
```

this的确应该是undefined，因为f2是被直接调用的，而不是作为对象的属性或方法调用的（如 window.f2()）。有一些浏览器最初在支持严格模式时没有正确实现这个功能，于是它们错误地返回了window对象。

## call()和apply()

```js
var obj = {a: 'obj'};

// 这个属性是在global对象定义的。
var a = 'window';

function whatsThis(arg) {
  return this.a;  // this的值取决于函数的调用方式
}

whatsThis();          // 'window'
whatsThis.call(obj);  // 'obj'
whatsThis.apply(obj); // 'obj'
```

## 二者不同

```js
function add(c, d) {
  return this.a + this.b + c + d;
}

var o = {a: 1, b: 3};

// 第一个参数是作为'this'使用的对象
// 后续参数作为参数传递给函数调用
add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16

// 第一个参数也是作为'this'使用的对象
// 第二个参数是一个数组，数组里的元素用作函数调用中的参数
add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34
```

使用 call 和 apply 函数的时候要注意，如果传递给 this 的值不是一个对象，JavaScript 会尝试使用内部 ToObject 操作将其转换为对象。因此，如果传递的值是一个原始值比如 7 或 'foo'，那么就会使用相关构造函数将它转换为对象，所以原始值 7 会被转换为对象，像 new Number(7) 这样，而字符串 'foo' 转化成 new String('foo') 这样。

## bind方法

ECMAScript 5 引入了 Function.prototype.bind。调用f.bind(someObject)会创建一个与f具有相同函数体和作用域的函数，但是在这个新函数中，this将永久地被绑定到了bind的第一个参数，无论这个函数是如何被调用的

```js
function f(){
  return this.a;
}

var g = f.bind({a: 'azerty'});
console.log(g()); // azerty

var h = g.bind({a: 'yoo'}); // bind只生效一次！
console.log(h()); // azerty

var o = {a: 37, f: f, g: g, h: h};
console.log(o.f(), o.g(), o.h()); // 37, azerty, azerty
```

## ES6中箭头函数

在箭头函数中，this与封闭词法上下文的this保持一致。在全局代码中，它将被设置为全局对象

```js
var globalObject = this;
var foo = (() => this);
console.log(foo() === globalObject); // true

// 作为对象的一个方法调用
var obj = {foo: foo};
console.log(obj.foo() === globalObject); // true

// 尝试使用call来设定this
console.log(foo.call(obj) === globalObject); // true

// 尝试使用bind来设定this
foo = foo.bind(obj);
console.log(foo() === globalObject); // true
```

注意：如果将this传递给call、bind、或者apply，它将被忽略。不过你仍然可以为调用添加参数，不过第一个参数（thisArg）应该设置为null。

无论如何，foo 的 this 被设置为他被创建时的上下文（在上面的例子中，就是全局对象）。这同样适用于在其他函数内创建的箭头函数：这些箭头函数的this被设置为封闭的词法上下文的。

```js
// 创建一个含有bar方法的obj对象，
// bar返回一个函数，
// 这个函数返回this，
// 这个返回的函数是以箭头函数创建的，
// 所以它的this被永久绑定到了它外层函数的this。
// bar的值可以在调用中设置，这反过来又设置了返回函数的值。
var obj = {
  bar: function() {
    var x = (() => this);
    return x;
  }
};

// 作为obj对象的一个方法来调用bar，把它的this绑定到obj。
// 将返回的函数的引用赋值给fn。
var fn = obj.bar();

// 直接调用fn而不设置this，
// 通常(即不使用箭头函数的情况)默认为全局对象
// 若在严格模式则为undefined
console.log(fn() === obj); // true

// 但是注意，如果你只是引用obj的方法，
// 而没有调用它
var fn2 = obj.bar;
// 那么调用箭头函数后，this指向window，因为它从 bar 继承了this。
console.log(fn2()() == window); // true
```

一个赋值给了 obj.bar的函数（称为匿名函数 A），返回了另一个箭头函数（称为匿名函数 B）。因此，在 A 调用时，函数B的this被永久设置为obj.bar（函数A）的this。当返回的函数（函数B）被调用时，它this始终是最初设置的。在上面的代码示例中，函数B的this被设置为函数A的this，即obj，所以即使被调用的方式通常将其设置为 undefined 或全局对象（或者如前面示例中的其他全局执行上下文中的方法），它的 this 也仍然是 obj 。

## 作为对象的方法

当函数作为对象里的方法被调用时，它们的 this 是调用该函数的对象。

```js
var o = {
  prop: 37,
  f: function() {
    return this.prop;
  }
};
// 当 o.f()被调用时，函数内的this将绑定到o对象。
console.log(o.f()); // logs 37
```

这样的行为，根本不受函数定义方式或位置的影响。在前面的例子中，我们在定义对象o的同时，将函数内联定义为成员 f 。但是，我们也可以先定义函数，然后再将其附属到o.f。这样做会导致相同的行为，这表明函数是从o的f成员调用的才是重点

```js
var o = {prop: 37};

function independent() {
  return this.prop;
}

o.f = independent;

console.log(o.f()); // logs 37
```

this 的绑定只受最靠近的成员引用的影响。在下面的这个例子中，我们把一个方法g当作对象o.b的函数调用。在这次执行期间，函数中的this将指向o.b。事实证明，这与他是对象 o 的成员没有多大关系，最靠近的引用才是最重要的。

```js
o.b = {g: independent, prop: 42};
console.log(o.b.g()); // 42
```

## 原型链中的 this

对于在对象原型链上某处定义的方法，同样的概念也适用。如果该方法存在于一个对象的原型链上，那么this指向的是调用这个方法的对象，就像该方法在对象上一样。

```js
var o = {
  f: function() {
    return this.a + this.b;
  }
};
var p = Object.create(o);
p.a = 1;
p.b = 4;

console.log(p.f()); // 5
```

对象p没有属于它自己的f属性，它的f属性继承自它的原型。虽然在对 f 的查找过程中，最终是在 o 中找到 f 属性的，这并没有关系；查找过程首先从 p.f 的引用开始，所以函数中的 this 指向p。也就是说，因为f是作为p的方法调用的，所以它的this指向了p。这是 JavaScript 的原型继承中的一个有趣的特性。

## getter 与 setter 中的 this

相同的概念也适用于当函数在一个 getter 或者 setter 中被调用。用作 getter 或 setter 的函数都会把 this 绑定到设置或获取属性的对象。

```js
function sum() {
  return this.a + this.b + this.c;
}

var o = {
  a: 1,
  b: 2,
  c: 3,
  get average() {
    return (this.a + this.b + this.c) / 3;
  }
};

Object.defineProperty(o, 'sum', {
  get: sum,
  enumerable: true,
  configurable: true
});

console.log(o.average, o.sum); // logs 2, 6
```

## 构造函数

当一个函数用作构造函数时（使用new关键字），它的this被绑定到正在构造的新对象。

虽然构造器返回的默认值是this所指的那个对象，但它仍可以手动返回其他的对象（如果返回值不是一个对象，则返回this对象）。

```js
/*
 * 构造函数这样工作:
 *
 * function MyConstructor(){
 *   // 函数实体写在这里
 *   // 根据需要在this上创建属性，然后赋值给它们，比如：
 *   this.fum = "nom";
 *   // 等等...
 *
 *   // 如果函数具有返回对象的return语句，
 *   // 则该对象将是 new 表达式的结果。
 *   // 否则，表达式的结果是当前绑定到 this 的对象。
 *   //（即通常看到的常见情况）。
 * }
 */

function C() {
  this.a = 37;
}

var o = new C();
console.log(o.a); // logs 37


function C2(){
  this.a = 37;
  return {a: 38};
}

o = new C2();
console.log(o.a); // logs 38
```

因为在调用构造函数C2的过程中，手动的设置了返回对象，与this绑定的默认对象被丢弃了。（这基本上使得语句“this.a = 37;”成了“僵尸”代码，实际上并不是真正的“僵尸”，这条语句执行了，但是对于外部没有任何影响，因此完全可以忽略它）