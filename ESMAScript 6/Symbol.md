# 概述
Symbol是是一种新的原始数据类型，是js的第七种数据类型，表示独一无二的值

```
let s1 = Symbol('foo');
let s2 = Symbol('bar');

s1 // Symbol(foo)
s2 // Symbol(bar)

s1.toString() // "Symbol(foo)"
s2.toString() // "Symbol(bar)"
```
如果Symbol的参数是一个对象，就直接调用对象的toString方法

```
const obj = {
  toString() {
    return 'abc';
  }
};
const sym = Symbol(obj);
sym // Symbol(abc)
```
# 作为属性名
作为属性名，能够防止对象的属性名被无意覆盖

```
let mySymbol = Symbol();

// 第一种写法
let a = {};
a[mySymbol] = 'Hello!';

// 第二种写法
let a = {
  [mySymbol]: 'Hello!'
};

// 第三种写法
let a = {};
Object.defineProperty(a, mySymbol, { value: 'Hello!' });

// 以上写法都得到同样结果
a[mySymbol] // "Hello!"
```
但是Symbol作为属性名的时候不能用.运算符，因为该运算符后面都是字符串，所以Symbol会自动转为String

```
const mySymbol = Symbol();
const a = {};

a.mySymbol = 'Hello!';
a[mySymbol] // undefined
a['mySymbol'] // "Hello!"
```
# 属性名的遍历
Symbol作为属性名，不会出现在被for...in 、for... of循环中。需要用Object.getOwnPropertySymbols方法获取

```
let a = Symbol()
let b = Symbol()
let obj = {
    [a]: 1,
    [b]: 2
}
for(let i = 0; i < Object.getOwnPropertySymbols(obj).length; i ++) {
    console.log(obj[Object.getOwnPropertySymbols(obj)[i]])
}
```
如果遍历对象中所有类型的属性，用下面的方法

```
let a = Symbol()
let b = Symbol()
let obj = {
    [a]: 1,
    [b]: 2,
    e: 1
}
for(let i = 0; i < Reflect.ownKeys(obj).length; i ++) {
    console.log(obj[Reflect.ownKeys(obj)[i]])
}
```
# Symbol.for()和Symbol.keyFor()
## Symbol.for()
这个方法有一个登记机制，如果调用这个方法，会现在登记表查看有没有这个Symbol值，如果有的话直接用原来的那个，若没有的话，就创建一个新变量，并把它登记到登记表上

## Symbol.keyFor()
这个方法归返回一个已登记的类型值的key，但是Symbol()没有登记机制，所以用Symbol() 创建的变量不会被Symbol.keyFor()返回

```
let s1 = Symbol.for("foo");
Symbol.keyFor(s1) // "foo"

let s2 = Symbol("foo");
Symbol.keyFor(s2) // undefined
```



