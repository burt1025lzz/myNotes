#### 1. 默认情况下，哪些 HTML 标签是块级元素、哪些是内联元素







#### 2. 居中对齐有哪些实现方式









#### 3. 以下代码运行结果是多少

```js
const a = 100 + 10
const b = 100 + '10'
const c = true + '10'
```



#### 4. 以下代码运行结果是多少

```js
function print(fn) {
  let a = 200
  fn()
}
let a = 100
function fn() {
  console.log(a)
}
print(fn)
```

```js
function create() {
  let a = 100
  return function () {
    console.log(a)
  }
}
let fn = create()
let a = 200
fn()
```



#### 5. 打印顺序是什么

```js
console.log(1)
setTimeout(() => {
  console.log(2)
}, 1000)
console.log(3)
setTimeout(() => {
  console.log(4)
}, 0)
console.log(5)
```



#### 6. Js 获取 DOM 节点 有哪些方式







#### 7. 描述 cookie 、localStorage 、sessionStorage 三者区别







#### 8. Vue 的生命周期是怎样的









#### 9. vue 组件中 data 为什么必须是一个函数







#### 10. vue 中父子组件传值都能想到几种实现方式