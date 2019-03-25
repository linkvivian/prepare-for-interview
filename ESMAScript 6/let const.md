# let 
## 基本用法
作用类似var,但是所声明的变量，只在let代码块内有效

```
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10
```
上面的代码全部都输出10，原因在var声明的没有代码块的概念，全部共享了全局的i

```
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6
```
上面的代码会输出对应的i,因为for循环形成了代码块，所以i在作用域链找的时候会先找到函数外面一层的i  
**另外for循环声明变量是一个父级的作用域，而循环体内部是一个单独的子作用域**

```
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}
// abc
// abc
// abc
```
## 不存在变量提升
var 会存在变量提升的情况，这就很容易让我们在后面声明的变量在前面也可以用，而let声明的变量就一定要在声明后使用
## 暂时性死区
只要在块级作用域中一旦用let声明了某变量，在它之前这个变量都是不可用的，这称为暂时性死区
## 不允许重复声明
let不允许在相同的作用域中，重复声明同一个变量，**这就不允许在函数内声明形参**

```
function func(arg) {
  let arg; // 报错
}
```

## 块级作用域
允许块级作用域的任意嵌套

```
{{{{{let insane = 'Hello World'}}}}};
```
块级作用域的出现，所以我们可以在开发中逐渐淘汰立即执行函数
# const 
## 基本用法
声明一个只读的常量，只在块级作用域有效，对于const声明的常量，如果是简单数据类型（数值， 字符串， 布尔值），值就保存在变量指向的内存中，但是如果是复合类型的数据（对象、数组），变量只是指向一个指针，这个指针指向实际数据，所以这个数据是不是可变的就不能控制了，只能控制指针不能改变

```
const foo = {};

// 为 foo 添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123

// 将 foo 指向另一个对象，就会报错
foo = {}; // TypeError: "foo" is read-only
```
## object.freeze()方法
该方法可以将对象的浅层属性冻结

```
'use strict'
const foo = Object.freeze({a: {}});
foo.a.a = 'test'
console.log(foo)
```
如果要彻底冻结该对象，采用下面的方法

```
var constantize = (obj) => {
  Object.freeze(obj);
  Object.keys(obj).forEach( (key, i) => {
    if ( typeof obj[key] === 'object' ) {
      constantize( obj[key] );
    }
  });
};
```
遍历对象的属性，如果子属性的类型是对象，则递归调用这个方法
# 顶层对象的属性
顶层环境，浏览器指的是window对象，node指的是global对象，在之前，顶层属性和全局变量是等价的，就是说在声明全局变量的时候，会自动加到顶层属性中


```
window.a = 1;
a // 1

a = 2;
window.a // 2
```
但是es6声明的变量，顶层属性不包含全局变量

```
var a = 1;
// 如果在 Node 的 REPL 环境，可以写成 global.a
// 或者采用通用方法，写成 this.a
window.a // 1

let b = 1;
window.b // undefined
```



