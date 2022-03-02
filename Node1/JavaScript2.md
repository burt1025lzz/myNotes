# JavaScript - 2

------

## 分析知识模块

#### [DOM 和 BOM](#domAndBom)

+ [DOM 操作](#domOperation)
+ [DOM 操作的性能优化](#performance)
+ [BOM 操作](#bom)

#### [事件](#event)

+ [事件绑定和事件冒泡](#eventBind)
+ **[事件代理](#eventProxy) <font color="#FF3300">*</font>**（**[或称事件委托](#eventProxy)**）

#### [ajax](#ajax)

+ [XMLHttpRequest](XMLHttpRequest)
+ [状态码](#statusCode)
+ **[同源策略和跨域](#crossDomain) <font color="#FF3300">*</font>**

#### [存储](#storage)

+ [理解 Cookie](#Cookie)
+ [cookie 、localStorage 、sessionStorage 三者的区别](#CLSDifference)

#### [节流和防抖](#throttleAndDebounce)

+ [手写防抖 debounce](#debounce)
+ [手写节流 throttle](#throttle)

------

## 从 JS 基础知识到 JS Web API

+ #### JS 基础知识，规定语法（ ECMA 262 标准）

+ #### JS Web API，网页操作的 API（ W3C标准）

+ #### 前者是后者的基础，两者结合才能真正实际应用

------

## <span id="domAndBom">DOM 操作 ( Document Object Model)</span>

#### 前言

+ `vue` 和 `react` 框架应用广泛，封装了 `DOM` 操作
+ 但 `DOM` 操作一直都是前端工程师的基础、必备知识
+ 只会 `vue` 而不懂 `DOM` 操作的前端工程师，不会太长久

#### 前置知识

##### 1. DOM 本质

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<note>
    <to>Everybody</to>
    <from>Company</from>
    <heading>Note</heading>
    <body>Welcome</body>
</note>
<!--标签可拓展>
```

```html
<!doctype html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div>this is div</div>
</body>
</html>
<!--标签不可拓展，参照 W3C 规定>
```

​	`DOM` 本质是一棵树。`DOM` 和 `HTML` 不一样，`HTML` 是一个文件，可以理解成是 `DOM` 结构

##### <span id="getDom">2. 获取 DOM 节点</span>

```js
const div = document.getElementById('div')  // 元素
const divList = document.getElementsByTagName('div')  // 集合
const boxList = document.getElementsByClassName('.box')  // 集合
const pList = document.querySelectorAll('p')  // 集合
```



##### 3. DOM 节点的 property

```js
const p = document.querySelectorAll('p')[0]
console.log(p.style.width)  // 获取样式
p.style.width = '100px'  // 修改样式
console.log(p.className)  // 获取 class
p.className = 'p1'  // 修改 class

// 获取 nodeName 和 nodeType
console.log(p.nodeName)
console.log(p.nodeType)
```



##### 4. DOM 节点的 attribute

```js
const p = document.querySelectorAll('p')[0]
p.getAttribute('data-name')
p.setAttribute('data-name', 'data')
p.getAttribute('style')
p.setAttribute('style', 'font-size: 30px;')
```



##### <span id="domOperation">5. DOM 结构操作</span>

+ 新增 / 插入节点

```js
const div = document.getElementById('div')
// 添加新节点
const p1 = document.createElement('p')
p1.innerHTML = 'this is p1'
div.appendChild(p1)  // 添加新创建的元素
// 移动已有节点
const p2 = document.getElementById('p2')
div.appendChild(p2)
```

+ 获取子元素列表，获取父元素

```js
const div = document.getElementById('div')
// 获取子元素列表
const child = div.childNodes
// 获取父元素
const parent = div.parentNode
```

+ 删除子元素

```js
const div = document.getElementById('div')
const child = div.childNodes
div.removeChild(child[0])
```



##### <span id="performance">6. DOM 性能</span>

+ `DOM` 操作非常 ‘昂贵’ ，避免频繁 `DOM` 操作
+ 对 `DOM` 查询做缓存

```js
// 不缓存 DOM 查询结果
for (let i = 0; i < document.getElementsByTageName('p').length; i++) {
  // 每次循环，都会计算 length ，频繁进行 DOM 查询
}
// 缓存 DOM 查询结果
const pList = document.getElementsByTageName('p')
const length = pList.length
for (let i = 0; i < length; i++) {
  // 缓存 length ，只进行一次 DOM 查询
}
```

+ <span id="oneTimeOperation">将频繁操作改成一次性操作</span>

```js
const listNdoe = document.getElementById('list')

// 创建一个文档片段，此时还没有插入到 DOM 树中
const frag = document.createDocumentFragment()

// 执行插入
for (let x = 0; x < 10; x++) {
  const li = document.createElement('li')
  li.innerHTML = 'List item ' + x
  frag.appendChild(li)
}

// 都完成后，再统一插入到 DOM 树中
listNode.appendChild(frag)
```

------



#### 1. DOM 是哪种数据结构

​	树（ DOM 树）

#### 2. DOM 操作的常用 API

+ [DOM 节点操作](#getDom)
+ [DOM 结构操作](#domOperation)

#### 3. attribute 和 property 的区别

+ `property` 修改对象的属性， `DOM` 元素上 `js` 变量的一种修改（比如：样式）不会提现到 `html` 结构
+ `attribue` 修改的是 `html`属性（比如：结构）会改变 `html` 结构
+ 两者都有可能引起 `DOM` 重新渲染（尽量优先使用 `property` ）

#### 4. 一次性插入多个 DOM 节点，考虑性能

​	[将频繁操作改成一次性操作](#oneTimeOperation)

#### 5. 小结

+ `DOM` 本质
+ `DOM` 节点操作
+ `DOM` 结构操作
+ `DOM` 性能

------

## <span id="bom">BOM 操作（Brower Object Model）</span>

#### <span id="bomKnowledge">前置知识</span>

+ navigator
+ screen
+ location
+ history

```js
// navigator
const ua = navigator.userAgent
const isChrome = ua.indexOf('Chrome')
console.log(isChrome)

// screen
console.log(screen.width)
console.log(screen.height)

// location
console.log(location.href)
console.log(location.protocol)  // 'http:' 'https:'
console.log(location.host)  // 'www.baidu.com'
console.log(location.pathname) // '/content/10086'
console.log(location.search)  // '?id=10086'
console.log(location.hash)  // path 中 # 后的内容

// history
history.back()  // 后退
history.forward()  // 前进
```



#### 1. 如何识别浏览器的类型

​	[前置知识](#bomKnowledge)

#### 2. 分析拆解 url 各个部分

​	[前置知识](#bomKnowledge)

------

## <span id="event">事件</span>

#### 前置知识

##### <span id="eventBind">1. 事件绑定</span>

```js
const btn = document.getElementById('btn')
btn.addEventListener('click', event => {
  event.preventDefault()  // 阻止默认行为
  console.log('clicked')
})
```

##### 2. 事件冒泡

```html
<div id="div1">
    <p id="p1">激活</p>
    <p id="p2">取消</p>
    <p id="p3">取消</p>
    <p id="p4">取消</p>
</div>
<div id="div2">
    <p id="p5">取消</p>
    <p id="p6">取消</p>
</div>
```

```js
const p1 = document.getElementById('p1')
const body = document.body
bindEvent(p1, 'click', event => {
  event.stopPropagation()  // 注释这一行，体会事件冒泡
  alert('激活')
})
bindEvent(body, 'click', event => {
  alert('取消')
})
function bindEvent(elem, type, fn) {
  elem.addEventListener(type, fn)
}
```

##### <span id="eventProxy">3. 事件代理</span>

```html
<div id="div">
    <a href="#">a1</a>
    <a href="#">a2</a>
    <a href="#">a3</a>
    <a href="#">a4</a>
</div>
<button id="btn">点击增加一个 a 标签</button>
```

```js
const div = document.getElementById('div')
div.addEventListener('click', e => {
  e.preventDefault()  // 阻止默认行为
  const target = e.target
  if (target.nodeName === 'A') {
    alert(target.innerHTML)
  }
})
```

------

#### 1. 编写一个通用的事件监听函数

```js
// 通用的绑定函数
function bindEvent(elem, type, selector, fn) {
  if (fn == null) {
    fn = selector
    selector = null
  }
  elem.addEventListener(type, event => {
    const target = event.target
    if (selector) {
      // 代理绑定
      if (target.matches(selector)) {
        fn.call(target, event)
      }
    } else {
      // 普通绑定
      fn.call(target, event)
    }
  })
}
// 普通绑定
const btn = document.getElementById('btn')
bindEvent(btn, 'click', function (event) {
  event.preventDefault()
  alert(this.innerHTML)
})
// 代理绑定
const div = document.getElementById('div')
bindEvent(div, 'click', 'a', function (event) {
  event.preventDefault()
  alert(this.innerHTML)
})
```



#### 2. 描述事件冒泡的流程

+ 基于 `DOM` 树形结构
+ 事件会顺着触发元素向上冒泡
+ 应用场景：代理



#### 3. 无限下拉的图片列表，如何监听每个图片的点击

+ 事件代理
+ 用 `e.target` 获取触发元素
+ 用 `matches` 来判断是否是触发元素



#### 4. 小结

+ 事件绑定
+ 事件冒泡
+ 事件代理

------

## <span id="ajax">ajax</span>

#### 前置知识

##### <span id="XMLHttpRequest">1. XMLHttpRequest</span>

```js
const xhr = new XMLHttpRequest()

// get 请求
xhr.open("GET", "/api/get", true)
// 这里的函数异步执行, 可参考之前 js 基础中的异步模块
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4) {
    if (xhr.status === 200) {
      console.log(xhr.responseText)
    }
  }
}
xhr.send(null)

// post 请求
xhr.open("POST", "/api/post", true)
xhr.onreadystatechange = function () { ... }
const postData = {
  username: 'zhangsan',
  password: 123456
}
xhr.send(JOSN.stringify(postData))
```

​	`xhr.readyState` 状态

+ 0 - （未初始化）还没有调用  `send()` 方法
+ 1 - （载入）已调用  `send()` 方法，正在发送请求
+ 2 - （载入完成） `send()` 方法执行完成，已经接收到全部响应内容
+ 3 - （交互）正在解析响应内容
+ 4 - （完成）响应内容解析完成，可以在客户端调用

##### <span id="statusCode">2. 状态码</span>

+ 2xx - 表示成功处理请求，如 200
+ 3xx - 需要重定向，浏览器直接跳转，如 301 302 304
+ 4xx - 客户端请求错误，如 403 404
+ 5xx - 服务端错误

##### <span id="crossDomain">3. 跨域：同源策略，跨域解决方案</span>

​	同源策略

+ `ajax` 请求时，浏览器要求当前网页和 `server` 必须同源（安全）
+ 同源：协议、域名、端口号，三者必须一致
+ 前端：http://a.com:8080/ ; server ：https://b.com/api/xxx

​	   注意：加载图片、`css` 、`js` 可无视同源策略

​	跨域

+ 所有的跨域，都必须经过 `server` 端的允许和配合
+ 未经 `server` 端允许就实现跨域，说明浏览器有漏洞，危险信号

​	<span id="JSONP">JSONP</span>

+ 访问 https://www.baidu.com/ ，服务端一定返回一个 `html` 文件吗？
+ 服务器可以任意动态拼接数据返回，只要符合 `html` 格式要求
+ 同理于 `<script src="https://xxx.com/getData.js">`
+ `<script>` 就可以获得跨域的数据，只要服务端愿意返回

```html
<script>
  window.callback = function (data) {
    // 这是跨域得到的信息
    console.log(data)
  }
</script>
<script src="https://xxx.com/getData.js"></script>
<!-- 将返回 callback({ x: 100, y: 200 }) -->
```

```js
// jQuery 实现 jsonp
$.ajax({
  url: 'https://xxx.com/getData.js',
  dataType: 'jsonp',
  jsonCallback: 'callback',
  success: function (data) {
    console.log(data)
  }
})
```



#### 1. 手写一个简易的 ajax

```js
function ajax(url, method, data) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest()
    xhr.open(method, url, true)
    xhr.onreadystatechange = function () {
      if (xhr.readyState === 4) {
        if (xhr.status === 200) {
          resolve(JSON.parse(xhr.responseText))
        } else {
          reject(new Error(xhr.status))
        }
      }
    }
    xhr.send(JSON.stringify(data))
  })
}
```



#### 2. 跨域的常用实现方式

​	[JSONP](#JSONP)

#### 3. 小结

+ `XMLHttpRequest`
+ 状态码：`readyState` `status`
+ 跨域：同源策略（如何绕过），`JSONP`

------

## <span id="storage">存储</span>

#### 前置知识

##### <span id="Cookie">1. cookie</span>

+ 本身用于浏览器和 `server` 通讯
+ 被 "借用" 到本地存储
+ 可用 `document.cookie = '...'` 方式来修改

缺点：

+ 存储大小限制，最大 4 KB
+ `http` 请求时需要发送到服务端，增加请求数据量
+ 只能用 `document.cookie = '...'` 来修改，太过简陋

##### 2. localStorage 和 sessionStorage

+ `HTML5` 专门为存储而设计，最大可存 5M
+ `API` 简单易用 `setItem` 、`getItem`
+ 不会随着 `http` 请求被发送出去

两者区别：

+ `localStorage` 数据会永久储存，除非代码或手动删除
+ `sessionStorage` 数据只存在于当前会话，浏览器关闭则清空
+ 一般用 `localStorage` 更多一点

#### <span id="CLSDifference">1. 描述 cookie 、localStorage 、sessionStorage 三者区别</span>

+ 容量
+ `API` 易用性
+ 是否跟随 `http` 请求发送出去

------

## <span id="throttleAndDebounce">防抖和节流</span>

#### <span id="debounce">1. 防抖 debounce</span>

+ 监听一个输入框，文字变化后触发 `change` 事件
+ 直接用 `keyup` 事件，则会频繁触发 `change` 事件
+ 防抖：用户输入结束或暂停时，才会触发 `change` 事件

```js
// 防抖 debounce
function debounce(fn, delay = 500) {
  // timer 是在闭包中
  let timer = null
  return function () {
    if (timer) {
      clearTimeout(timer)
    }
    timer = setTimeout(() => {
      fn.apply(this)
      // 清空定时器
      timer = null
    }, delay)
  }
}

const input = document.getElementById('input')
input.addEventListener('keyup', debounce(function () {
  console.log(input.value)
}))
```



#### <span id="throttle">2. 节流 throttle</span>

+ 拖拽一个元素时， 要随时拿到该元素被拖拽的位置
+ 直接使用 `drag` 事件，则会频繁触发， 很容易导致卡顿
+ 节流：无论拖拽速度有多快，都会每隔 `100ms` 触发一次

```js
// 节流 throttle
function throttle(fn, delay = 100) {
  let timer = null
  return function () {
    if (timer) return
    timer = setTimeout(() => {
      fn.apply(this, arguments)
      timer = null
    }, delay)
  }
}

const div = document.getElementById('div')
div.addEventListener('drag', throttle(function (e) {
  console.log(e.offsetX, e.offsetY)
}))
```

