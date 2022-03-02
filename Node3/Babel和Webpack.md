# Babel 和 Webpack

---

## 一. Babel

Babel 官网：https://babeljs.io/

Babel 在线编译：https://babeljs.io/repl



### 1. Babel 是什么

Babel 是 JavaScript 的编译器，使用 Babel 就可以使用下一时代的 js 语法

简单来说将 ES6 代码 -> ES5 代码

例子：

```js
// ES6
const data = {
  a: 100
}
const a = data?.a
```

```js
// ES5
"use strict";
const data = {
  a: 100
};
const a = data === null || data === void 0 ? void 0 : data.a;
```

注意：

+ Babel 本身可以编译 ES6 的大部分语法，比如 let、 const、箭头函数、类
+ 但是对于 ES6 新增的 API，比如 Set、Map、 Promise 等全局对象，以及一些定义在全局对象上的方法（比如 Object.assign / Array.from）都不能直接编译，需要借助其它的模块
+ Babel 一般需要配合 Webpack 来编译模块语法



### <font color='#dc5254'>2. Babel 的使用方式</font>

Babel 使用教程：https://babeljs.io/setup

常用使用方式：

+ 在 CLI（命令行）中使用 Babel
+ 在 Webpack 中使用 Babel



### <font color='#dc5254'>3. 使用 Babel 前的准备工作</font>

+ 什么是 Node.js 和 npm

  Node.js 是个平台或者工具，对应浏览器

  后端的 JavaScript = ECMAScript + IO + File + ...等服务端的操作

  npm：node 包管理工具 -> npm install ... 进行安装

  

+ 安装 Node.js

  官网：https://nodejs.org/zh-cn/

  ```shell
  node -v # 查看 Node.js 版本
  npm -v # 查看 npm 包管理工具版本
  ```

  

+ 初始化项目

  ```shell
  npm init
  ```

  注意：初始化项目时，name 不能为中文

  

+ 安装 Babel 需要的包

  ```shell
  npm install --save-dev @babel/core @babel/cli
  ```
  
  注意：npm 安装特定版本包：npm install xxx@版本号



### <font color='#dc5254'>4. 使用 Babel 编译 ES6 代码</font>

+ 编译命令

  首先在 package.json 中添加 "build": "babel src -d dist"

  babel src -d dist --> babel 编译目录 --out-dir的缩写 输出目录

  CLI 中使用：
  
  ```shell
  npm run build
  ```

+ Babel 配置文件

  ```shell
  npm install @babel/preset-env --save-dev
  ```
  
  包讲解：
  ```json
    @babel/cli  // 命令行工具
    @babel/core  // babel 核心包 - 负责调度
    @babel/preset-env  // babel 怎么转换语法
  ```
  
  新建 babel.config.json 文件，并配置
  
  ```json
  {
    "presets": ["@babel/preset-env"]
  }
  ```
  
  最后重新编译:
  
  ```shell
  npm run build
  ```



---

## 二. Webpack 入门

### 1. Webpack 是什么

+ 认识 Webpack

  webpack 是静态模块打包器。当 webpack 处理应用程序时，会将所有这些模块，打包成一个或者多个文件

+ 理解 Webpack

  模块：webpack 可以处理 js / css / 图片 / 图标字体 等单位

  静态：开发过程中存于本地的 js / css / 图片 / 图标字体等文件 都是静态文件

  动态内容：webpack 没办法处理，只能处理静态的



### <font color='#dc5254'>2. Webpack 初体验</font>

+ 初始化项目

  ```shell
  npm init
  ```

+ 安装 webpack 需要的包

  ```shell
  npm install --save-dev webpack-cli webpack
  ```

+ 配置 webpack

  新建 webpack.config.js 文件，并配置

  ```js
  const path = require('path');
  module.exports = {
    mode: 'development',  // 打包模式，不写默认为 production 1.development 2.production 3.none
    entry: './src/index.js',
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: 'bundle.js'
    }
  };
  ```

+ 打包并测试

  首先在 package.json 中添加 `"webpack": "webpack --config webpack.config.js"`

  ```js
  "scripts": {
    // 新增下面语句
    "webpack": "webpack --config webpack.config.js"
  }
  ```
  
  webpack --config webpack.config.js --> webpack --config 指定 webpack 配置文件，若不写则默认寻找 webpack.config.js 文件
  
  CLI 中使用
  
  ```shell
  npm run webpack
  ```

---

## 三. Webpack 的核心概念

### <font color='#dc5254'>1. entry 和 output</font>

+ entry 指定入口文件

  ```js
  module.exports = {
    // 单入口文件：等价下面 main 中写法
    entry: './src/index.js'
    
    // 多入口文件
    entry: {
      // main 可随意定义
      main: './src/index.js',
      search: './src/search.js'
    }
  };
  ```

+ output 出口文件

  ```js
  const path = require('path');
  module.exports = {
    // 单入口
    output: {
      // output 必须使用绝对路径，所以要引入 path
      // __dirname 指当前文件的绝对路径，resolve 方法用于将 __dirname 和 dist 拼接
      path: path.resolve(__dirname, 'dist'),
      // 打包后文件名
      filename: 'bundle.js'
    }
    
    // 多入口
    output: {
      path: path.resolve(__dirname, 'dist'),
      // [name] 为固定写法，值取自多入口定义的 key 值
      filename: '[name].js'
    }
  };
  ```

  

### <font color='#dc5254'>2. loader</font>

+ 什么是 loader

  loader 让 webpack 能够处理非 js 文件的模块

  具体可参考：https://webpack.docschina.org/loaders/



+ babel-loader

  将 webpack 和 babel 连同一起能使用的模块

  安装：

  ```shell
  npm install --save-dev babel-loader
  ```

  ```js
  module.exports = {
    module: {
      rules: [
        {
          // 正则
          test: /\.m?js$/,
          // 排除文件（正则）
          exclude: /node_modules/,
          // 使用 babel-loader
          loader: "babel-loader"
        }
      ]
    }
  };
  ```



+ babel-polyfill

  babel 可编译 ES6 新增的 API

  具体可参考：https://babeljs.io/docs/en/babel-polyfill

  安装：

  ```shell
  npm install --save @babel/polyfill
  ```

  使用：

  + 可在入口文件顶部或 webpack.config.js 顶部添加

    ```js
    require("@babel/polyfill");
    ```

  + 也可在 webpack 中配置（单入口文件使用）

    ```js
    entry: ["@babel/polyfill", "./src/index.js"]
    ```



### <font color='#dc5254'>3. plugins</font>

+ 什么是 plugins

  插件可用于执行范围更广的应用

  具体可参考：https://webpack.docschina.org/plugins/



+ html-webpack-plugin

  在 HTML 中自动引入 webpack 打包出来的 js，并复制到输出文件夹中

  安装：

  ```shell
  npm install --save-dev html-webpack-plugin
  ```

+ 配置 html-webpack-plugin 插件

  ```js
  const HtmlWebpackPlugin = require('html-webpack-plugin');
  
  module.exports = {
    plugins: [
      // 单入口配置
      new HtmlWebpackPlugin({
        // 指定 html 模板文件（不写，会生成一个默认页面）
        template: './index.html'
      })
      
      // 多入口配置
      new HtmlWebpackPlugin({
        template: './index.html',
      	// 指定输出文件名
        filename: "index.html",
      	// 指定入口文件（entry 中的 key 值）
        chunks: ['index'],
    		minify: {
          // 删除文档中的注释
          removeComments: true,
          // 删除文档中的空格
          collapseWhitespace: true,
          // 删除各种 html 标签属性值的双引号
          removeAttributeQuotes: true
        }
      }),
      new HtmlWebpackPlugin({
        template: './search.html',
        filename: "search.html",
        chunks: ['search']
      })
    ]
  }
  ```

  

---

## 四. Webpack 的应用

### 1. 处理 CSS 文件

+ css-loader

  让 webpack 识别 js 中引入 css 模块

  安装：

  ```shell
  npm install --save-dev css-loader
  ```

  配置 css-loader

  ```js
  module.exports = {
    module: {
      rules: [{
        test: /\.css$/,
        loader: "css-loader"
      }]
    }
  }
  ```



+ style-loader

  将引入的 css 模块，通过 style 内部样式的方式嵌入到 HTML 中

  安装：

  ```shell
  npm install --save-dev style-loader
  ```

  配置 style-loader

  ```js
  module.exports = {
    module: {
      rules: [{
        test: /\.css$/,
        // 此处同时配置多个 loader 时，需使用 use
        // use 可为对象，可为数组。注意：当为数组时，加载顺序为从右向左
        // loader: "css-loader",
        use: ['style-loader', 'css-loader']  // 注意顺序，从右向左加载
      }]
    }
  }
  ```

  

+ mini-css-extract-plugin

  将引入的 css 模块，通过 link 外部样式的方式嵌入到 HTML 中

  安装：

  ```shell
  npm install --save-dev mini-css-extract-plugin
  ```

  配置 mini-css-extract-plugin

  ```js
  const MiniCssExtractPlugin = require("mini-css-extract-plugin")
  module.exports = {
    module: {
      rules: [{
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader']  // 注意顺序，从右向左加载
      }]
    },
    plugins: [
      new MiniCssExtractPlugin({
        filename: "css/[name].css",
      })
    ]
  }
  ```

  

### 2. 使用 file-loader 处理 CSS 中的图片

+ 如果是外部图片资源，是不需要考虑 webpack 的，只有本地图片资源才需要被 webpack 处理

  

+ <font color='#dc5254'>注意：下面内容可能被弃用</font>

  在 webpack5 中 已经弃用 file-loader 和 url-loader，下面内容仅供学习 webpack 做参考

  且最新版本中的 css-loader 已经新增本地图片的加载器（不支持图片命名）

  如需在 webpack5 中正确使用 file-loader 需参考下面配置

  ```js
  module.exports = {
    module: {
      rules: [{
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader']
      }, {
        test: /\.(png|jpg|gif)$/,
        use: [{
          loader: "file-loader",
          options: {
            // file-loader 默认采用ES模块语法，即import './'的形式
            // 如果想使用 commonjs 规范的话 则需要配置下项
            esModule: false
          }
        }],
        type: "javascript/auto"  // 使用 file-loader 加载本地图片
      }]
    }
  }
  ```

  具体其他内容可参考：

  [webpack5打包图片背景图片文件出现的问题](https://blog.csdn.net/wms_swag/article/details/120631602?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~aggregatepage~first_rank_ecpm_v1~rank_v31_ecpm-1-120631602.pc_agg_new_rank&utm_term=webpack%E6%89%93%E5%8C%85%E8%83%8C%E6%99%AF%E5%9B%BE%E7%89%87%E5%87%BA%E7%8E%B0%E4%B8%A4%E5%BC%A0&spm=1000.2123.3001.4430)

  [Webpack打包生成多余图片的解决方案和Webpack5正确打包图片姿势](https://blog.csdn.net/weixin_43714543/article/details/121201846?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~aggregatepage~first_rank_ecpm_v1~rank_v31_ecpm-2-121201846.pc_agg_new_rank&utm_term=webpack%E6%89%93%E5%8C%85%E8%83%8C%E6%99%AF%E5%9B%BE%E7%89%87%E5%87%BA%E7%8E%B0%E4%B8%A4%E5%BC%A0&spm=1000.2123.3001.4430)



+ file-loader

  让 webpack 识别本地中的 其他类型文件 模块

  安装：

  ```shell
  npm install --save-dev file-loader
  ```

  

+ file-loader 配置

  ```js
  const MiniCssExtractPlugin = require("mini-css-extract-plugin")
  module.exports = {
    module: {
      rules: [{
        test: /\.css$/,
        // 因为使用了 mini-css-extract-plugin 插件
        // 可能导致打包出来的 css 引入图片路径有问题
        use: [{
          loader: MiniCssExtractPlugin.loader,
          options: {
            // 需要配置 mini-css-extract-plugin 插件的公共路径（新版本中可以不用配置）
            publicPath: '../'
          }
        }, 'css-loader']
      }, {
        test: /\.(png|jpg|gif)$/,
        use: [{
          loader: "file-loader",
          options: {
            // 配置 file-loader 将本地图片统一放到指定路径下
            // ext -> 原本后缀
            name: 'img/[name].[ext]',
            esModule: false
          }
        }],
        type: "javascript/auto"
      }]
    },
    plugins: [
      new MiniCssExtractPlugin({
        filename: "css/[name].css",
      })
    ]
  }
  ```

  

### 3. 使用 html-withimg-loader 处理 HTML 中的图片

+ html-withimg-loader

  让 webpack 识别 HTML 中的本地图片

  安装：

  ```shell
  npm install --save-dev html-withimg-loader
  ```

  

+ html-withimg-loader 配置

  ```js
  module.exports = {
    module: {
      rules: [{
        test: /\.(png|jpg|gif)$/,
        use: [{
          loader: "file-loader",
          options: {
            name: 'img/[name].[ext]',
            // 此处配合 html-withimg-loader 关闭 ES6 模块化导出模式
            esModule: false
          }
        }],
        type: "javascript/auto"
      }, {
        test: /\.(html|htm)$/,
        loader: "html-withimg-loader"
      }]
    }
  }
  ```

  

### 4. 使用 file-loader 处理 JS 中的图片

+ 配置与 file-loader 配置相同

  ```js
  import img from './img/logo.png'
  console.log(img)  // 此处为打包后 dist 文件夹中的路径，而不是上面引入时的路径（/img/logo.png）
  const imgElement = document.createElement('img')
  imgElement.src = img
  document.body.appendChild(imgElement)
  ```



### 5. 使用 url-loader 处理图片

+ url-loader

  比 file-loader 更全面，底层为 file-loader 部分功能

  安装：

  ```shell
  npm install --save-dev url-loader
  ```

  

+ url-loader 配置（注意点同 file-loader，可能被弃用）

  ```js
  module.exports = {
    module: {
      rules: [{
        test: /\.(png|jpg|gif)$/,
        use: [{
          loader: "url-loader",
          options: {
            name: 'img/[name].[ext]',
            esModule: false,
            limit: 10000  // 限制 10k 大小以下图片会被转成 base64
          }
        }],
        type: "javascript/auto"
      }]
    }
  }
  ```

  

### 6. 使用 webpack-dev-server 搭建开发环境

+ 安装

  ```shell
  npm install --save-dev webpack-dev-server
  ```

  

+ 在 package.json 中配置

  ```json
  "scripts": {
    "build": "webpack",
    // 新增下面语句，添加 --open 参数则会打开默认浏览器
    "dev": "webpack-dev-server --open"
  }
  ```

  

+ 其他配置内容请参考 [`devServer`](https://www.webpackjs.com/configuration/dev-server/)
