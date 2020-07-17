# ECMAScript

ECMAScript 通常看作 JavaScript 的标准化规范，但实际上 JS 是 ECMAScript 的扩展语言

ECMAScript 只提供最基本的语法，它无法完成实际功能开发

Web 环境中， JS = ECMAScript + Web APIs(BOM + DOM)

Node 环境中，JS = ECMAScript + Node APIs(fs, net ...)

## ES2015

- 解决原有语法上的一些问题或不足
- 对原有语法进行增强
- 全新的对象、方法、功能
- 全新的数据类型和数据结构

### let 与块级作用域

作用域——某个成员能够起作用的范围

- 全局作用域
- 函数作用域
- 块级作用域——用{}包裹起来的范围

通过 let 声明的变量它只能在所声明的代码块中起作用

### const (恒量/常量)

在 let 的基础上多了只读特性，声明过后不允许再被修改，在声明的同时必须设置初始值，const 所声明的成员不能被修改只是说不允许在声明过后去指向新的内存地址，并不是说不允许修改常量中的属性成员

最佳实践：不用 var，主用 const，配合 let

### 数组的解构（Destructuring）

根据位置去提取

### 对象的解构

根据属性名去提取

### 模板字符串字面量（Template literals）

```js
`${a}`
```

可支持多行字符串

### 模板字符串标签函数（Tagged templates）

在定义模板字符串之前添加标签，这个标签是一个特殊的函数，其实就相当于调用了这个函数。数据的转换加工时可用到，比如国际化等

### 字符串的扩展方法

- includes()
- startsWith()
- endsWith()

### 参数默认值（Default parameters）

带默认值的形参一定要出现参数列表的最后

### 剩余参数（Rest parameters）

...args ，参数数组，只能出现在参数列表最后一位且只能使用一次

### 展开数组（Spread）

```javascript
console.log(...arr) 
```

### 箭头函数 （Arrow functions）

=> 箭头符号，简化函数定义，箭头左边为参数列表，右边为函数体

### 箭头函数与 this

箭头函数不会改变 this 指向。箭头函数中没有 this 的机制，所以它不会改变 this 指向。箭头函数外面 this 是什么，里面就是什么

### 对象字面量增强（Enhanced object literals）

变量名与对象属性相同，可以省略掉冒号和变量名。可以使用表达式返回值来作为属性名（计算属性名）

### 对象扩展方法

- Object.assign：将多个源对象的属性复制到一个目标对象中
- Object.is：判断两个值是否相等

### 代理对象 （Proxy）

监视对象中的属性读写，可以使用 Object.defineProperty 来监听，也可以使用ES6 Proxy

- Proxy vs Object.defineProperty()

  1. defineProperty 只能监视属性的读写，Proxy 能够监视到更多对象操作（delete, 对象方法的调用等）

     |       handler 方法       |                           触发方式                           |
     | :----------------------: | :----------------------------------------------------------: |
     |           get            |                         读取某个属性                         |
     |           set            |                         写入某个属性                         |
     |           has            |                          in 操作符                           |
     |      deleteProperty      |                        delete 操作符                         |
     |       getProperty        |                   Object.getPrototypeOf()                    |
     |       setProperty        |                   Object.setPrototypeOf()                    |
     |       isExtensible       |                    Object.isExtensible()                     |
     |    preventExtensions     |                  Objet.preventExtensions()                   |
     | getOwnPropertyDescriptor |              Object.getOwnPropertyDescriptor()               |
     |      defineProperty      |                   Object.defineProperty()                    |
     |         ownKeys          | Object.getOwnPropertyNames()、Object.getOwnPropertySymbols() |
     |          apply           |                         调用一个函数                         |
     |        construct         |                     用 new 调用一个函数                      |

  2. Proxy 更好的支持数组对象的监视

     重写数组的操作方法等

  3. Proxy 是以非侵入的方式监管了对象的读写

### Reflect （统一的对象操作 API）

Reflect 属于一个静态类，不能通过 new 的方式创建，Reflect 内部封装了一系列对对象的底层操作。Reflect 成员方法就是 Proxy 处理对象的默认实现。统一提供一套用于操作对象的 API

### Promise

一种更优的异步编程解决方案，通过链式调用的方式解决了传统异步编程中回调函数嵌套过深的问题

### class 类（Classes）

```js

class Person {
  constructor(name) {
    this.name = name;
  }

  say() {
    console.log(`hi, my name is ${this.name}`)
  }
}

const p = new Person('tom')
p.say()
```

### 静态成员（static）

实例方法 vs. 静态方法

实例方法，通过这个类型构造的实例对象去调用

静态方法，直接通过类型本身去调用

### 类的继承（extends）

比使用原型继承更方便清楚

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  say() {
    console.log(`hi, my name is ${this.name}`)
  }
}

class Student extends Person {
  constructor(name, age) {
    super(name)
    this.age = age;
  }

  hello() {
    super.say()
    console.log(`my age is ${this.age}`)
  }
}

const s = new Student('hhh', 22)
s.hello()
```

### Set 数据结构

Set 内部成员不允许重复，值具有唯一性。常用于为数组去重

### Map 数据结构

Object 的键名只能是字符串，所以受限。map 可以用任意类型的数据作为键

### Symbol

一种全新的原始数据类型，表示一个独一无二的值。最主要的作用就是为对象添加独一无二的属性名

### for...of 循环

for 适合遍历普通数组，for...in 适合遍历键值对

for...of 是一种数据统一遍历方式，可以跳出循环

### 可迭代接口（Iterable）

为了给各种各样的数据结构提供统一遍历方式，提供了 Iterable 接口。实现 Iterable 接口就是 for...of 的前提

### 迭代器模式 Iterator

### 生成器 (Generator)

避免异步编程中回调嵌套过深，提供更好的异步编程解决方案

## ES2016

数组 includes 方法，指数运算符**

## ES2017

- Object.values
- Object.entries
- Object.getOwnPropertyDescriptors
- String.prototype.padStart / padEnd
- 在函数参数中添加尾逗号
- Async / Await