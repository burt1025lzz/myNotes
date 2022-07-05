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

