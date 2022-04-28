# npm 搭建 uniapp + uview

------

## 一、创建 uniapp 项目

### 1. 安装 VueCLI

+ 要使用 4.5.15 版本的 CLI，5.0 以上版本会报错

  ```shell
  ERROR  Error: Cannot find module 'webpack/lib/RuleSet'  
  ```

+ 已安装 5.0 以上版本的 CLI 

  ```shell
  # 卸载vuecli5.0版本
  npm remove -g  @vue/cli
  ```

  ```shell
  # 安装vue4.5.15版本
  npm install -g @vue/cli@4.5.15
  ```

### 2. 创建 uniapp 项目

```shell
vue create -p dcloudio/uni-preset-vue my-project-name
```

+ 安装有问题请先科学上网
+ 模板选默认模板

## 二、使用 uView

### 1. 安装 sass

```shell
# 安装 sass
npm i sass -D
```

```shell
# 安装sass-loader，注意需要版本10，否则可能会导致vue与sass的兼容问题而报错
npm i sass-loader@10 -D
```

### 2. 安装 uView

```js
// 安装
// 去 https://www.npmjs.com/package/uview-ui 查阅最新版本号，写文档时不加版本号会默认安装 1.8.6
npm install uview-ui@2.0.31
```

### 3. 配置 uView

+ 引入 uView 主JS库

  在项目`src`目录中的`main.js`中，引入并使用uView的JS库，注意这两行要放在`import Vue`之后

  ```js
  // main.js
  import uView from "uview-ui";
  Vue.use(uView);
  ```

+ 在引入 uView 的全局SCSS主题文件

  在项目`src`目录的`uni.scss`中引入此文件。

  ```css
  /* uni.scss */
  @import 'uview-ui/theme.scss';
  ```

+ 引入 uView 基础样式

  注意！在`App.vue`中 **首行** 的位置引入，注意给style标签加入lang="scss"属性

  ```css
  <style lang="scss">
  	/* 注意要写在第一行，同时给style标签加入lang="scss"属性 */
  	@import "uview-ui/index.scss";
  </style>
  ```

+ 修改默认单位为rpx

  ```js
  // main.js
  uni["$u"].config.unit = 'rpx'
  ```

+ 配置 easycom 组件模式

  此配置需要在项目`src`目录的`pages.json`中进行。

  ```json
  // pages.json
  {
  	"easycom": {
  		"^u-(.*)": "uview-ui/components/u-$1/u-$1.vue"
  	},
  	
  	// 此为本身已有的内容
  	"pages": [
  		// ......
  	]
  }
  ```

+ CLI 模式额外配置

  ```js
  // vue.config.js，如没有此文件则手动创建
  module.exports = {
      transpileDependencies: ['uview-ui']
  }
  ```

+ 验证

  ```js
  console.log(uni.$u.config.v);  // 1.8.6
  ```