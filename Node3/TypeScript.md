# TypeScript

------



## 一、前言

### 1. 编程语言的类型

+ 动态类型语言（ Dynamically Typed Language ）

  如：JavaScript、Python

+ 静态类型语音（ Statically Typed Language ）

  如：C、C++、Java

### 2. TypeScript 究竟是什么

+ JavaScript that scales
+ 静态类型风格的类型系统
+ 从 es6 到 es10 甚至 esnext 的语法支持
+ 兼容各种浏览器，各种系统，各种服务器，完全开源

### 3. 为什么要使用 TypeScript

+ 程序更容易理解
  1. 问题：函数或者方法输入输出的参数类型，外部条件等
  2. 动态语言的约束：需要手动调试等过程
  3. 有了 TypeScript：代码本身就可以回答上述问题
+ 效率更高
  1. 在不同的代码块和定义中进行跳转
  2. 代码自动补全
+ 更少的错误
  1. 编译期间能够发现大部分错误
  2. 杜绝一些比较常见的错误
+ 非常好的包容性
  1. 完全兼容 JavaScript
  2. 第三方库可以单独编写类型文件
+ 一点小缺点
  1. 增加了一些学习成本
  2. 短期内增加了一些开发成本

------



## 二、原始数据类型和 Any 类型

```typescript
let isDone: boolean = false
let age: number = 25
let firstName: string = 'burt'
let message: string = `My name is ${firstName}`
let u: undefined = undefined
let n: null = null
let num: number = undefined

let notSure: any = 4
notSure = 'maybe a string'
notSure = true
notSure.name
notSure.getName()
```

------



## 三、数组和元组

```typescript
let arrOfNum: number[] = [1, 2, 3]
arrOfNum.push(1)

function test() {
    console.log(arguments)
}

// 元组
let usr: [string, number] = ['burt', 25]
usr.push(true)  // error: 只能传入 string || number
```

------



### 四、Interface 接口

+ 对对象的形状（ shape ）进行描述
+ Duck Typing （鸭子类型）

```typescript
interface IPerson {
    readonly id: number
    name: string
    age?: number
}

const burt: IPerson = {
    id: 10086,
    name: 'lzz'
}

burt.id = 9527  // error
```

------



### 五、Function 函数

```typescript
function add(x: number, y: number, z?: number): number {
    return z ? x + y + z : x + y
}

let res = add(1, 2)

let add2 = (x: number, y: number, z?: number): number => {
    return z ? x + y + z : x + y
}

let res2 = add2(1, 2);
let res3: (x: number, y: number, z?: number) => number = add2

interface ISum {
    (x: number, y: number, z?: number): number
}

let res4: ISum = add2
```

------



### 六、类型推论、联合类型和类型断言

```typescript
// 类型推论
const str = 'str'

// 联合类型
let numOrStr: number | string = '10'
numOrStr = 10

// 类型断言
function getLength(value: string | number): number {
    let str = value as string
    if (str.length) {
        return str.length
    } else {
        let num = value as number
        return num.toString().length
    }
}

// type guard
function getLength2(value: string | number): number {
    if (typeof value === 'string') {
        return value.length
    } else {
        return value.toString().length
    }
}
```

------



### 七、Class 类

+ 类 ( Class ) : 定义了一切事物的抽象特点
+ 对象( Object ) : 类的实例
+ 面向对象 ( OOP ) 三大特征：封装、继承、多态
+ TypeScript 中的类
  1. Public : 修饰的属性或方法是共有的
  2. Private : 修饰的属性或方法是私有的
  3. Protected : 修饰的属性或方法是受保护的

```typescript
class Animal {
    // 只读
    readonly name: string

    constructor(name: string) {
        this.name = name
    }
    // 公有方法
    public run() {
        return `${this.name} is running!`
    }
    // 私有方法
    private eat() {
        return `${this.name} is eating!`
    }
    // 继承类可以使用
    protected bark() {
        return `${this.name} is bark!`
    }
}
```

------



### 八、类和接口

+ 继承的困境
+ 类可以使用 implements 来实现接口

```typescript
interface IRadio {
    switchRadio(trigger: boolean): void
}

interface IBattery {
    checkBatteryStatus(): void
}

interface IRadioWithBattery extends IRadio {
    checkBatteryStatus(): void
}

class Car implements IRadio {
    switchRadio(trigger: boolean) {}
}

class cellPhone implements IRadio, IBattery {
    switchRadio(trigger: boolean) {}

    checkBatteryStatus() {}
}

class cellPhone2 implements IRadioWithBattery {
    switchRadio(trigger: boolean) {}

    checkBatteryStatus() {}
}
```

------



### 九、Enmu 枚举

```typescript
enum Direction {
    Up,
    Down,
    Left,
    Right
}

console.log(Direction.Up) // 0
console.log(Direction[0])  // Up

// 常量枚举
const enum Direction {
    Up = 'UP',
    Down = 'DOWN',
    Left = 'LEFT',
    Right = 'RIGHT'
}
```

------



### 十、 Generics 泛型

```typescript
function echo<T>(arg: T): T {
    return arg
}

let res = echo('str')

function swap<T, U>(tuple: [T, U]): [U, T] {
    return [tuple[1], tuple[0]]
}

let res2 = swap(['str', 1])
```

```typescript
function echoWithArr<T>(arg: T[]): T[] {
    console.log(arg.length)
    return arg
}

const arr = echoWithArr([1, 2, 3])

interface IWithLength {
    length: number
}

// 约束泛型
function echoWithLength<T extends IWithLength>(arg: T): T {
    console.log(arg.length)
    return arg
}

const str = echoWithLength('str')
const obj = echoWithLength({
    length: 10
})
```

```typescript
class Queue<T> {
    private data: any[] = []

    push(item: T) {
        return this.data.push(item)
    }

    pop(): T {
        return this.data.shift()
    }
}

const queue = new Queue<number>()
queue.push(1)
// queue.push('123')
console.log(queue.pop().toFixed())
interface IKeyPair<T, U> {
    key: T
    value: U
}

let key1: IKeyPair<string, number> = {key: 'str', value: 2}
let key2: IKeyPair<number, string> = {key: 1, value: 'str'}
let array: number[] = [1, 2, 3]
let array2: Array<number> = [1, 2, 3]
```

------



### 十一、类型别名、字面量和交叉类型

```typescript
// 类型别名
let sum: (x: number, y: number) => number
const res = sum(1, 2)
type PlusType = (x: number, y: number) => number
let sum2: PlusType
const res2 = sum2(1, 2)
type strOrNum = string | number
let res3: strOrNum = '123'
res3 = 123

// 字面量
const str: 'name' = 'name'
const num: 1 = 1
type Directions = 'Up' | 'Down' | 'Left' | 'Right'
const toWhere: Directions = 'Down'

// 交叉类型
interface IName {
    name: string
}

type IPerson = IName & { age: number }
let person: IPerson = {
    name: 'burt',
    age: 25
}
```

------



### 十二、声明文件

```typescript
// jQuery.d.ts
declare var jQuery: (selector: string) => any
```

```typescript
jQuery('#id')
```