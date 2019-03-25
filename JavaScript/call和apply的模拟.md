# call
思路是
- call方法会将将函数的this绑定在传进来的对象，并且当参数为null时将会绑定到window上
- 首先将方法赋值到对象的一个属性fn中
- 从第二个参数遍历arguments类数组，将参数推到数组里，然后执行这个函数，用eval() （有其他方法）
- 删除这个函数
- 返回函数执行的结果
```
Function.prototype.call2 = function (context) {
    var context = context || window;
    context.fn = this;

    var args = [];
    for(var i = 1, len = arguments.length; i < len; i++) {
        args.push('arguments[' + i + ']');
    }

    var result = eval('context.fn(' + args +')');

    delete context.fn
    return result;
}

// 测试一下
var value = 2;

var obj = {
    value: 1
}

function bar(name, age) {
    console.log(this.value);
    return {
        value: this.value,
        name: name,
        age: age
    }
}

bar.call2(null); // 2

console.log(bar.call2(obj, 'kevin', 18));
// 1
// Object {
//    value: 1,
//    name: 'kevin',
//    age: 18
// }
```
# apply
和call类似，但是传进来的参数为一个数组

# 参考

[JavaScript深入之call和apply的模拟实现](https://github.com/mqyqingfeng/Blog/issues/11)

