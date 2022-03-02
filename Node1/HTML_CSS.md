# HTML

------

## 1. 如何理解 HTML 语义化

```html
<div>标题</div>
<div>
    <div>一段文字</div>
    <div>
        <div>列表1</div>
        <div>列表2</div>
    </div>
</div>
```

```html
<h1>标题</h1>
<div>
    <p>一段文字</p>
    <ul>
        <li>列表1</li>
        <li>列表2</li>
    </ul>
</div>
```

+ 让人更容易读懂（增加代码可读性）
+ 让搜索引擎更容易读懂（ SEO ）

## 2. 默认情况下，哪些 HTML 标签是块级元素、哪些是内联元素

+ `display: block / table;` 有 `div h1 h2 table ul ol p` 等
+ `display: inline / inline-block;` 有 `span a img input button` 等

# CSS

------

## 分析知识模块

#### **[布局](#overall) <font color="#FF3300">*</font>**

+ [盒子模型的宽度如何计算](#overall1)
+ [margin 纵向重叠问题](#overall2)
+ [margin 负值问题](#overall3)
+ [BFC 理解和应用](#overall4)
+ **[float 布局问题、以及 clearfix](#overall5)  <font color="#FF3300">*</font>**
+ **[flex 画骰子](#overall6)  <font color="#FF3300">*</font>**

#### **[定位](#position) <font color="#FF3300">*</font>**

+ [absolute 和 relative 分别根据什么定位](#position1)
+ **[居中对齐有哪些实现方式](#position2)  <font color="#FF3300">*</font>**

#### [图文样式](#style)

+ [line-height 的继承问题](#style1)

#### [响应式](#responsive)

+ [rem 是什么](#responsive1)
+ [如何实现响应式](#responsive2)

------

## <span id="overall">布局</span>

#### <span id="overall1">1. 盒模型宽度计算</span>

```html
<!-- 以下代码， 请问 div 的 offsetWidth 是多大？ -->
<style>
  #div {
    width: 100px;
    padding: 10px;
    border: 1px solid #ccc;
    margin: 10px;
  }
</style>
<div id="div"></div>
```

​	`offsetWidth` = （内容宽度 + 内边距 + 边框），无外边距

​	答案：`122px`

​	补充提问：如果让 `offsetWidth` 等于 `100px` ，怎么做？

​	答案：`box-sizing: border-box`

#### <span id="overall2">2. margin 纵向重叠问题</span>

```html
<!-- 以下代码， AAA 和 BBB 之间的距离是多少？ -->
<style>
  p {
    font-size: 16px;
    line-height: 1;
    margin-top: 10px;
    margin-bottom: 15px;
  }
</style>
<p>AAA</p>
<p></p>
<p></p>
<p></p>
<p>BBB</p>
```

+ 相邻元素的 `margin-top` 和 `margin-bottom` 会发生重叠
+ 空白内容的 `<p></p>` 也会重叠

​	答案：`15px`

#### <span id="overall3">3. margin 负值问题</span>

+ 对 `margin` 的 `top left right bottom` 设置负值，有何效果？

​	答案：

+ `margin-top` 和 `margin-left` 负值，元素向上、左移动
+ `margin-right` 负值，右侧元素左移，自身不受影响
+ `margin-bottom` 负值，下方元素上移，自身不受影响



#### <span id="overall4">4. BFC 理解和应用</span>

+ 什么是 `BFC` ？如何应用？

​	答案：

+ `Block Format Context` ，块级格式化上下文
+ 一块独立渲染区域，内部元素的渲染不会影响边界以外的元素

​	形成 `BFC` 的常见条件

+ `float` 不是 `none`
+ `position` 是 `absolute` 或 `fixed`
+ `overflow` 不是 `visible`
+ `display` 是 `flex inline-block` 等

​	`BFC` 的常见应用

+ 清除浮动



#### <span id="overall5">5. float 布局</span>

###### 1. 如何实现圣杯布局和双飞翼布局？

​	圣杯布局和双飞翼布局的目的

+ 三栏布局， 中间一栏最先加载和渲染（内容最重要）
+ 两侧内容固定，中间内容随着宽度自适应
+ 一般用于 PC 网页

​	技术总结

+ 使用 `float` 布局
+ 两侧使用 `margin` 负值，以便和中间内容横向重叠
+ 防止中间内容被两侧覆盖，一个用 `padding` 一个用 `margin`



###### 2. 手写  `clearfix`

```css
.clearfix:after {
  content: '';
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}
.clearfix {
  *zoom: 1; /* 兼容低版本 IE 浏览器 */
}
```



#### <span id="overall6">6. flex 布局</span>

​	常用语法：

+ `flex-direction` - 主轴方向
+ `justify-content` - 主轴对齐方式
+ `align-items` - 交叉轴对齐方式
+ `flex-wrap` - 是否换行
+ `align-self` - 子元素在交叉轴对齐方式

​	`flex` 实现一个三点的骰子

```css
/* flex 画三个点骰子 */
.box {
  display: flex;  /* flex 布局 */
  justify-content: space-between;  /* 两端对齐 */
}
.item {
  /* 背景色、大小、边框等 */
}
.item:nth-child(2) {
  align-self: center;  /* 第二项居中对齐 */
}
.item:nth-child(3) {
  align-self: flex-end;  /* 第三项尾对齐 */
}
```

------

## <span id="position">定位</span>

#### <span id="position1">1. absolute 和 relative 分别根据什么定位</span>

+ `relative` 根据自身定位
+ `absolute` 依据最近一层的定位元素定位 （`absolute relative fixed body`）

#### <span id="position2">2. 居中对齐有哪些实现方式</span>

##### 1. 水平居中

+ `inline` 元素：`text-align: center`
+ `block` 元素： `margin: auto`
+ `absoulte` 元素： `left: 50%;` + `margin-left` 负值

##### 2. 垂直居中

+ `inline` 元素：`line-height` 的值等于 `height` 值
+ `absoulte` 元素： `top: 50%;` + `margin-top` 负值
+ `absoulte` 元素： `transform(-50%, -50%)`
+ `absoulte` 元素： `top, left, right, bottom = 0` + `margin-left: auto`

------

## <span id="style">图文样式</span>

#### <span id="style1">1. line-height 如何继承</span>

```html
<!-- 如下代码， p 标签的行高将是多少？ -->
<style>
  body {
    font-size: 20px;
    line-height: 200%;
  }
  p {
    font-size: 16px;
  }
</style>

<body>
  <p>AAA</p>
</body>
```

​	答案： `40px`

+ 写具体数值，如 `30px` ，则继承该值（比较好理解）
+ 写比例，如 `2 / 1.5` ，则继承该比例（比较好理解）
+ 写百分比，如 `200%` ，则继承计算出来的值（重点）

------

## <span id="responsive">响应式</span>

#### <span id="responsive1">1. rem 是什么</span>

+ `rem` 是一个长度单位

​	`px`，绝对长度单位，最常用

​	`em`， 相对长度单位，相对于父元素，不常用

​	`rem`，相对长度单位，相对于根元素，常用于响应式布局

#### <span id="responsive2">2. 响应式布局的常见方案</span>

+ `media-query` ，根据不同的屏幕宽度设置根元素 `font-size`
+ `rem` ，基于根元素的相对单位
