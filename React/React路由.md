# React 路由

------

## 一、路由与 SPA (单页网站应用)

### 1. 路由是什么？

+ 传统网站
  1.  当浏览器的 url 发送变化时，浏览器页面相应的发生改变
+ 现代的路由方式
  1. React、Vue 前后端分离，路有架构彻底改变

### 2. SPA 是什么？

+ JS、CSS、HTML 打包为一个超级大的文件，一次性丢给浏览器
+ JS 劫持浏览器路由，生成虚拟路由来动态渲染页面 dom 元素
+ 符合前后端分离的趋势，服务器不负责 UI 输出，而专注于数据支持
+ 同时支持桌面 App、手机 App，网站 App

### 3. 路由与 SPA 有什么关系？

+ React 网站使用的路由系统都是虚拟的
  1. 与后端服务器没有半毛钱关系，与实际文件也没有一一对应的关系
  2. 主页：http://localhost:3000
  3. 搜索页：http://localhost:3000/search
  4. 旅游详情页：http://localhost:3000/touristRoutes/{id}

### 4. React 路由框架

+ 综合性路由框架：react-router
+ 浏览器路由框架：react-keeper
+ 手机 app 框架 ( react-native )：react-navigation

------



## 二、配置 react-router

### 1. react-router

+ react-router-dom 用于浏览器，处理 Web App 的路由
+ react-router-native 用于 React Native，处理手机 App 的路由
+ react-router-redux 提供了路由中间件，处理 redux 的集成
+ react-router-config 用来静态配置路由

### 2. react-router-dom

+ 会自动安装 react-router 核心框架
+ `<Link />` 组件可以渲染出 `<a />` 标签
+ `<BrowserRouter />` 组件利用 H5 API 实现路由切换
+ `<HashRouter />` 组件利用原生 JS 中的 `window.location.hash` 来实现路由切换

### 3. 网站路由系统的要求

+ 路由导航与原生浏览器操作行为一致 `<BrowserRouter />`
+ 路由的路径解析原理与原生浏览器一致，可以自动识别 url 路径 `<Route />`
+ 路径的切换以页面为单位，不要页面堆叠 `<Routes />`