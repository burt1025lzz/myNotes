# React 基础

------

## 一、 配置开发环境

### 1. 搭建 React 项目

+ 脚手架工具 create-react-app

  ```shell
  npx create-react-app my-app
  cd my-app
  npm start
  ```

------



## 二、React 的设计理念

### 1. 单向数据流

+ 数据与页界面绑定
+ 单向渲染
+ 就好像一个函数，同样的输入，同样的输出

### 2.虚拟 DOM

+ 类似 Docker 或 VMware 的 Snapshot 快照技术

  ![image-20220628214945219](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/zy/2022/20220628214947.png)

### 3. 组件化

+ 保持交互一致性
+ 保持视觉风格的统一
+ 便于程序员间相互协作

------



## 三、JSX 编程思想

### 1. 为什么使用 JSX

+ React 并不强制使用 JSX，也可以使用原生 JavaScript
+ React 认为视图的本质就是渲染逻辑与 UI 视图表现的内在统一
+ React 把 HTML 与渲染逻辑进行了耦合，形成了 JSX

### 2. JSX 的特点

+ 常规的 HTML 代码都可以与 JSX 兼容
+ 可以在 JSX 中嵌入表达式
+ 使用 JSX 指定子元素
+ JSX 命名约定
  1. 使用 camelCase ( 小驼峰 ) 方式定义属性
  2. 例如：class 变成了 className ，而 tabindex 变成为 tabIndex
  3. jsx 的自定义属性，以 data- 开头

### 3. TSX

+ 文件扩展名 .tsx
+ 在配置文件中 tsconfig.json 启用 jsx 选项

------



## 四、配置 React 的 CSS 模组

### 1. 如何架构项目中的样式文件

+ 文件位置：css 文件与 component 文件放在同一个目录下
+ 命名规范： *.module.css

### 2. CSS module (模组化)

+ 每个 jsx 或者 tsx文件就被视为一个独立存在的原件
+ 原件所包含的所有内容也同样都应该是独立存在的
+ `import './index.css'` --> `import style from './index.css'`

### 3. TS 的定义声明

+ *.d.ts
+ 只包含类型声明，不包含逻辑
+ 不会被编译，也不会被 webpack 打包

### 4. JSS 模块化引入组件

```jsx
import styles from './App.css'
<div className={styles.app}/>
```

```typescript
// 如果 css 文件以 *.module.css 命名，则不需要以下代码声明
declare module "*.css" {
  const css: { [key: string]: string }
  export default css
}
```

------



## 五、State vs Props

### 1.State 和 Props 的区别

+  props 是组件对外的接口，而 state 是组件对内的接口
+  props 用于组件间数据传递，而  state 用于组件内部的数据传递

### 2. state 正确的打开方式

+ state 是私有的，可以认为 state 是组件的 “私有属性”

+ 用 setState() 修改 State

  1. 直接修改 state，组件不会触发 render 函数，页面不会渲染

     ```js
     // 错误
     this.state.isOpen = true
     ```

  2. 正确的修改方式是使用 setState()

     ```js
     this.setState({ isOpen: !this.state.isOpen })
     ```

### 3. 初始化

+ 构建函数 constructor 是唯一可以初始化 state 的地方

  ```js
  // 生命周期第一阶段： 初始化
  constructor(props) {
      super(props);
      this.state = {
          isOpen: false
      }
  }
  ```

### 4. state 的更新是异步的

+ 调用 setState 后，state 不会立刻改变，是异步操作
+ 不要依赖当前的 state，计算下个 state

### 5. props

+ 本质上，props 就是传入函数的参数，是从传入组件内部的数据。
+ 更准确说，是父组件传递向子组件的数据

### 6. Immutable

+ 中文：不变的
+ 对象一旦创建就不可改变，只能通过销毁、重建来改变数据
+ 通过判断地内存地址是否一致，来确认对象是否有经过修改
+ props 是只读属性的
+ 函数式编程

------



## 六、setState 的异步开发

### 1. setState() 是异步还是同步

+ 异步更新，同步执行
  1. setState() 本身并非异步，但对 state 的处理机制给人一种异步的假象
  2. state 处理一般发生在生命周期变化的时候

------



## 七、 React 组件的生命周期

### 1. Mounting ：创建虚拟 DOM，渲染 UI

### 2. Updating：更新虚拟 DOM，重新渲染 UI

### 3. Unmounting：删除虚拟 DOM，移除 UI

------



## 八、钩子（hooks）

### 1. 非类组件中使用 state

+ 什么是 hooks
+ hooks 产生的原因
+ 常见的 hooks 函数

### 2. 什么是钩子( hooks )

+ 消息处理的一种方法，用来监视指定程序
+ 函数组件中需要处理副作用，可以用钩子把外部代码 “钩” 进来
+ 常用钩子：`useState`, `useEffect`, `useContext`, `useReducer`
+ hooks 一律使用 use 前缀命名：useXxxx

### 3. Hooks 的本质

+ 一类特殊的函数，为你的函数形式组件注入特殊的功能

### 4. React 为什么要创造 Hooks 这个概念？

+ 有些组件冗长而且复杂，难以复用
+ 解决方案：**无状态组件** 与 **HOC( 高阶组件 )** 但还是存在诸多问题
+ Hooks 的目的就是为了给函数式组件加上状态
+ 生命周期函数会同时处理多项任务：发起 ajax、跟踪数据状态、绑定事件监听
+ 函数式组件则轻量化很多，使用 Hooks 钩子来钩入组件状态

### 5. 常见钩子

+ 状态钩子：useState()

  ```js
  const [count, setCount] = useState(0);
  ```

  1. React 自带的一个 hook 函数，声明组件状态
  2. 参数可以设置 state 的初始值（initial state）
  3. 返回值是一个只有两个元素的数组：[ 状态，状态更新函数 ]

+ 副作用钩子：useEffect()

  ```js
  useEffect(() => {
    document.title = `点击${count}次`
  }, [count])
  ```

  1. 可以取代生命周期函数 componentDidMount, componentDidUpdate 和 componentWillUnmount
  2. 给函数式组件添加副作用（side effect）

------



## 九、副作用 Side-effect

### 1. 什么是副作用

+ 与药物的副作用类似：减肥药（拉肚子）
+ 纯函数（pure function）
  1. 给一个函数同样的参数，那么这个函数永远返回同样的值
  2. 函数式编程理念
  3. React 组件输入相同的参数(props)，渲染 UI 应该永远一样
  4. 副作用与纯函数相反，指一个函数处理了与返回值无关的事情

### 2. 副作用是件坏事吗？

+ 不是，很多代码必须得借助副作用才能实现，如：ajax、修改 DOM，甚至是 console.log
+ React： state 状态的改变，生命周期，构建函数

------



## 十、自定义高阶组件 HOC

### 1. HOC 的公式

+ `const hoc = higherOrde(wrappedComponent);`
+ 高阶组件（HOC）就是一个返回了组件的函数
+ 通过组件嵌套的方法给子组件添加更多的功能
+ 接收一个组件作为参数并返回一个经过改造的新组件

### 2. 为什么要使用高阶组件

+ 抽取重复代码，实现组件复用
+ 条件渲染，控制组件的渲染逻辑（渲染劫持）
+ 捕获 / 劫持被处理组件的生命周期

### 3. 命名规范

+ withXXX() -> withAddToCart()

------

