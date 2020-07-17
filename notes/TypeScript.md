# TypeScript 语言

解决 JavaScript 类型系统的问题，大大提高代码的可靠程度

## 类型系统

### 强类型与弱类型（类型安全）

- 强类型 语言层面限制函数的实参类型必须与形参类型相同（Java...）
- 弱类型  语言层面不会限制实参类型

强类型有更强的类型约束，而弱类型中几乎没有什么约束。强类型语言中不允许任意的隐式类型转换，而弱类型语言则允许任意的数据隐式类型转换

### 静态类型与动态类型（类型检查）

- 静态类型 一个变量声明时它的类型就是明确的，声明过后它的类型就不允许再修改
- 动态类型 运行阶段才能够明确变量类型，而且变量的类型随时可以改变。变量没有类型，变量中存放的值是有类型的



## JavaScript 自有类型系统的问题

JavaScript 类型系统特征：弱类型 且 动态类型，缺失了类型系统的可靠性。

### 弱类型的问题

- 运行阶段才能发现代码中的类型异常
- 类型不明确造成函数功能有可能发生改变
- 对对象索引器的错误用法

### 强类型的优势

- 错误更早暴露
- 代码更智能，编码更准确
- 重构更牢靠
- 减少不必要的类型判断

## Flow 静态类型检查方案

Flow —— JavaScript 的类型检查器。Flow 只是一个工具

通过编译 移除类型注解

```bash
$ yarn flow init
$ yarn flow
$ yarn flow-remove-types src -d dist

# 使用babel
$ yarn add @babel/core @babel/cli @babel/preset-flow --dev
# 配置.babelrc
# {
#  "presets": ["@babel/preset-flow"]
# }
$ yarn babel src -d dist
```

- 类型推断（Type Inference）
- 类型注解（Type Annotations）
- 原始类型（Primitive Types）
- 数组类型（Array Types）
- 对象类型（Object Types）
- 函数类型（Function Types）
- 特殊类型
- 任意类型（Mixed & Any）
  - Mixed 是强类型的
  - Any 是弱类型的

## TypeScript 语言规范与基本应用

TypeScript —— JavaScript 的超集（superset）,任何一种JS运行环境都可使用。功能更为强大，生态也更健全，更完善。

TypeScript 标准库就是内置对象所对应的声明

### 快速上手

```bash
$ yarn init --yes
$ yarn add typescript --dev
$ yarn ts xxx.ts
```

### 配置文件

```bash
$ yarn tsc --init # 生成配置文件

# 编译整个项目配置文件才会生效
$ yarn tsc
```

### 中文错误信息

``` bash
$ yarn tsc --locale zh-CN
```

### 类型

- 原始类型
- Object 类型（Object Types）所有非原始类型
- 数组类型（Array Types）
- 元组类型（Tuple Types）明确元素数量及类型的数组
- 枚举类型（Enum Types）可以给一组数字起别名，一个枚举中只能存在固定的值，enum 数字类型数值会自动累加值。会影响编译结果
- 函数类型（Function Types）
- 任意类型（Any Types）不检查类型，存在类型不安全问题

### 隐式类型推断（Type Inference）

虽然有隐式类型推断，但是建议给每个变量添加明确的类型

### 类型断言（Type assertions）

```js
// 假定这个nums 来自一个明确的接口
const nums = [1, 2, 3]

const res = nums.find(i => i > 0)

// const square = res * res

const num1 = res as number
```

### 接口（Interfaces）

一种规范，用来约定对象的结构。接口里有可选成员，只读成员，动态成员

### 类（Classes）

描述一类具体事物的抽象特征

ES6 以前，函数 + 原型 模拟实现类。

TS 增强了 class 的相关语法

### 访问属性 & 只读属性

public、private、protected、readonly

### 类与接口

公共特征使用接口进行抽象

```typescript
interface Eat {
  eat(food: string): void
}

interface Run {
  run(distance: number): void
}

class Person implements Eat, Run {
  eat(food: string): void {
    console.log(`进餐：${food}`)
  }

  run(distance: number): void {
    console.log(`行走：${distance}`)
  }
}

class Animal implements Eat, Run {
  eat(food: string): void {
    console.log(`呼噜呼噜地吃：${food}`)
  }

  run(distance: number): void {
    console.log(`爬行：${distance}`)
  }
}
```

### 抽象类

去约束子类当中必须要有某个成员，可包含具体的实现。只能够继承，不能使用 new 创建实例对象

```typescript
abstract class Animal {
  eat (food: string): void {
    console.log(`呼噜呼噜地吃：${food}`)
  }

  abstract run (distance: number): void
}

class Cat extends Animal {
  run(distance: number): void {
    console.log(`四脚爬行`, distance)
  }
}

const d = new Cat()
d.eat('dddd')
d.run(11)
```

### 泛型（Generics）

泛型就是在声明函数时不指定类型，再调用时再指定，提高代码复用率

```typescript
function crateNumberArray(length: number, value: number): number[] {
  const arr = Array<number>(length).fill(value)
  return arr
}

function crateStringArray(length: number, value: string): string[] {
  const arr = Array<string>(length).fill(value)
  return arr
}

function crateArray<T>(length: number, value: T): T[] {
  const arr = Array<T>(length).fill(value)
  return arr
}

// const res = crateNumberArray(2, 100)

const res = crateArray<string>(3, 'a')
```

### 类型声明（Type Declaration）

引用第三方模块，可能不包含类型声明模块，可安装对应的模块或使用 declare 进行声明