### 柯里化

柯里化实际上是一个高阶函数的特殊用法，是把接收多个参数的函数变成接收一个单一参数的函数，并且返回接收如下的参数而且返回结果的新函数的技术

**柯里化的作用**

+ 参数的封装复用

公用封装

```js
// 支持多参数传递
function progressCurrying(fn, args) {

    var _this = this
    var len = fn.length;
    var args = args || [];

    return function() {
        var _args = Array.prototype.slice.call(arguments);
        Array.prototype.push.apply(args, _args);

        // 如果参数个数小于最初的fn.length，则递归调用，继续收集参数
        if (_args.length < len) {
            return progressCurrying.call(_this, fn, _args);
        }

        // 参数收集完毕，则执行fn
        return fn.apply(this, _args);
    }
}
```

### 节流函数

节流函数用来优化JavaScript性能，对于频繁的请求进行控制，常用的场景用 onsroll onresize onmousemove等高频词的触发事件 

原理：使用时间间隔来处理事件，触发一次函数后，下次触发必须经过一段时间才能重新触发，否则不触发，重新计算时间，类似于水龙头滴水一样，不能太快流出

### 防抖函数

### 惰性函数

### 偏函数

### 高阶函数

### 纯函数

