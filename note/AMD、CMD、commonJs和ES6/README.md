# AMD、CMD、commonJs和ES6

## AMD

AMD是RequireJS在推广过程中对模块定义的规范化产出。

依赖lib，就加载lib，通过回调函数的方式去调用。

```js
define(['package/lib'], function(lib){
    function fun() {
        lib.show('AMD');
    };
    return {
        fun: func
    };
});
```

## CMD

CMD是SeaJS在推广过程中对模块定义的规范化产出。

在什么地方使用就在什么地方引用

```js
define(function(require, exports, module){
    // 通过require引入依赖
    var $ = require('jquery');
    var spin = require('./spin');
});
```

## CommonJS规范-module.exports

在浏览器端是不支持的，在node环境中是支持的。

```js
exports.area = function(x) {
    return Math.PI * x * x;
};
exports.circumference = function(x) {
    return Math.PI * x * 2;
}
```

## ES6特性export/import

只有export才能import。

```js
export default {
    props: ['num'],
    data() {
        return {}
    },
    methods: {
        increment() {
            this.$emit('incre');
            import('./../util');
        },
        decrement() {
            this.$emit('decre');
        }
    }
}
```