# bind介绍
- bind会接受的第一个参数是函数要绑定的对象，剩下的参数是作为返回函数的参数传进去
- 用new操作符构建已经经过bind绑定的函数时，绑定的this会失效

# 思路
- 首先将参数类数组截下来
- 然后判断当前的this值是不是instanceof返回的函数，等于的话就表明要绑定的函数经过new操作符，没有的话就绑定context
- 用一个中转函数来承载原型，避免修改到绑定函数的原型

```
Function.prototype.bind2 = function (context) {

    if (typeof this !== "function") {
      throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var self = this;
    var args = Array.prototype.slice.call(arguments, 1);

    var fNOP = function () {};

    var fBound = function () {
        var bindArgs = Array.prototype.slice.call(arguments);
        return self.apply(this instanceof fNOP ? this : context, args.concat(bindArgs));
    }

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();
    return fBound;
}
```
# 参考
[JavaScript深入之call和apply的模拟实现](https://github.com/mqyqingfeng/Blog/issues/11)
