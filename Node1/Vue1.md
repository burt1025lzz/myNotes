# Vue - 1

------

## vue 基本使用

#### 1. 指令、插值

+ 插值、表达式
+ 指令、动态属性
+ `v-html`: 会有 `XSS` 风险，会覆盖子组件



#### 2. computed 和 watch

+ `computed` 有缓存，`data` 不变则不会发生变化
+ `watch` 如何深度监听

```js
watch: {
  info: {
			hander(oldVal, val) {
      // 引用类型，拿不到 oldVal 。因为指针相同，此时已经指向了新的 val
      console.log('watch info', oldVal, val) 
    },
      deep: true  // 深度监听
  }
}
```

+ `watch` 监听引用类型，拿不到 `oldVal`



#### 3. class 和 style

+ 使用动态属性
+ 使用驼峰式写法



#### 4. 条件渲染

+ `v-if` `v-show` 的用法，可使用变量，也可使用 `===` 表达式
+ `v-if` 和 `v-show` 的区别
+ `v-if` 和 `v-show` 的使用场景



#### 5. 循环（列表）渲染

+ 如何遍历对象？--- 也可以用 `v-for`
+ `key` 的重要性。`key` 不能乱写（如 `random` 或者 `index`）
+ `v-for` 和 `v-if` 不能一起使用



#### 6. 事件

+ `event` 参数，自定义参数
+ 【观察】事件被绑定到哪里

1. `event` 是原生的
2. 事件被挂载到当前元素

+ 事件修饰符，按键修饰符

```vue
<!-- 事件修饰符 -->

<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>
<!-- 提交事件不再重载页面 -->
<form @submit.prevent="onSubmit"></form>
<!-- 修饰符可以串联 -->
<a @click.stop.prevent="doThat"></a>
<!-- 只有修饰符 -->
<form @submit.prevent></form>
<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div @click.capture="doThis"></div>
<!-- 只当在 event.target 是当前元素自身时触发函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div @click.self="doThat"></div>
```

```vue
<!-- 按键修饰符 -->

<!-- 即是 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下时才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下时才会触发 -->
<button @click.exact="onClick">A</button>
```



#### 7. 表单

+ `v-model`
+ 常见表单项 `textarea checkbox radio select`
+ 修饰符 `lazy number trim`



------

## Vue 组件使用

#### 1. prop 和 $emit

#### 2. 组件间通讯 - 自定义事件

#### 3. 组件生命周期（单个组件）

+ 挂载阶段
+ 更新阶段
+ 销毁阶段

<img src="https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/lifecycle.png" alt="vue生命周期" style="zoom: 33%;" />



#### 4. 组件生命周期（父子组件）

<img src="https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/image-20211213153914983.png" alt="image-20211213153914983" style="zoom:33%;" />



------

## Vue 高级特性

+ 自定义 `v-model`
+ `$nextTick`

1. `Vue` 是异步渲染
2. `data` 改变后，`DOM` 不会立刻渲染
3. `$nextTick` 会在 `DOM` 渲染之后被触发，以获取最新 `DOM` 节点
4. 页面渲染时会将 `data` 的修改做整合，多次 `data` 修改只会渲染一次

+ `refs`
+ `slot`

1. 基本使用
2. 作用域插槽
3. 具名插槽

+ 动态、异步组件

1. `:is = "component-name"` 用法

2. 需要根据数据，动态渲染的场，即组件类型不确定

   <img src="https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/image-20211213171729194.png" alt="image-20211213171729194" style="zoom: 33%;" />

3. `import()` 函数

3. 按需加载，异步加载大组件


+ `keep-alive`

1. 缓存组件
2. 频繁切换，不需要重复渲染
3. `Vue` 常见性能优化


+ `mixin`

1. 多个组件有相同的逻辑，抽离出来
2. `mixin` 并不是完美的解决方案，会有一些问题
3. `Vue3` 提出的 `Compositin API` 解决这些问题

问题：

1. 变量来源不明确，不利于阅读
2. 多 `mixin` 可能会造成命名冲突
3. `mixin` 和组件可能会出现多对多的关系，复杂度较高

------

## Vuex

#### 1. 基本概念

+ `state`
+ `getters`
+ `action`
+ `mutation`

![image-20211215142721574](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/image-20211215142721574.png)

------

## Vue-router 使用

#### 1. 路由模式（hash、H5 history）

+ `hash` 模式（默认），如 `http://abc.com/#/user/10`
+ `H5 history` 模式，如 `http://abc.com/user/10`
+ 后者需要 `server` 端支持，因此无特殊需求可选择前者

![image-20211215150744804](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/image-20211215150744804.png)

#### 2. 路由配置（动态路由、懒加载）

![image-20211215150847617](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/image-20211215150847617.png)

![image-20211215151021885](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/image-20211215151021885.png)