#  React Redux

------

## 一、什么是 redux

### 1. React 实际上只是 UI 框架

+ 通过 JSX 生成动态 DOM 渲染 UI
+ 没有架构、没有模板、没有设计模式、没有路由、也没有数据管理

### 2. Redux

+ 剥离组件数据（ state ）
+ 数据统一存放在 store 中
+ 组件订阅 store 获取数据
+ store 同步推送数据更新

![image-20220704171802273](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/image-20220704171802273.png)

### 3. 什么时候需要使用 Redux

+ 组件需要共享数据（或者叫状态 state ）的时候
+ 某个状态需要在任何地方都可以随时访问的时候
+ 某个组件需要改变另一个组件状态的时候
+ 语言切换、暗黑模式切换、用户登录全局数据共享...

### 4. Redux 工作流

![iShot_2022-07-04_17.23.49](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/iShot_2022-07-04_17.23.49.png)

![iShot_2022-07-04_17.29.47](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/iShot_2022-07-04_17.29.47.png)

![iShot_2022-07-04_17.30.21](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/iShot_2022-07-04_17.30.21.png)

------



## 二、Redux 中间件

### 1. RESTful 的基本特点

+ 无状态

+ 面向 ”资源“

+ 使用 HTTP 的动词

  ![image-20220706092900120](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/image-20220706092900120.png)

+ HATOAS 超媒体即应用状态引擎

### 2. 什么是 MVC

+ 一种架构模式，同时也是一种思想
+ 模型（Model）、视图（View）和控制器（Controller）
+ 分离业务操作、UI 显示、逻辑控制
+ 视图 View
  1. 用户交互页面
  2. 仅展示数据，不处理数据
  3. React 项目的 JSX 代码
+ 模型 Model
  1. MVC 架构的核心
  2. 表示业务模型或数据模型
  3. 业务逻辑，如算法实现、数据的管理、输出对象的封装等等
+ 控制器 Controller
  1. 接收用户的输入，并调用模型和视图去完成用户的请求处理
  2. 不处理数据
  3. React -> MVVM 或 MV*（whatever）
+ React 和 MVC 模式毫不相干

### 3. Redux 中间件机制

![image-20220706143556995](https://burt-markdown.oss-cn-shenzhen.aliyuncs.com/markdown/image-20220706143556995.png)

### 4. Redux 中间件公式

```js
const middleware = (store) => (next) => (action) => {}
```

