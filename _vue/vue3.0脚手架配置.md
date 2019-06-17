
### vue/cli3.0安装使用

+ 安装全局模块

```js
npm install @vue/cli -g
or
yarn add @vue/cli global
```

+ 检查模块是否安装成功

```js
vue -V
```

+ 常见项目

```js
vue create vue-app

cd vue-app

yarn serve or npm run serve
```

### 路由代码分割

+ 路由使用按需打包实现懒加载，使用improt导入，针对每个路由文件单独打包，也可以通过webpackChunkName把某些路由合并一起打包,
```js
routes: [
    {
      path: "/",
      name: "home",
      component: Home
    },
    {
      path: "/about",
      name: "about",
      // 路由级别的代码分割打包
      // 此路由将会被打包成单独的一个js文件块，名字为about.[hash].js
      // 当此路由被访问时采取加载文件
      // 可以设置不同的路由文件打包的webpackChunkName，如果名字相同则会打包在一块
      // 如果不设置webpackChunkName,则打包js文件名为 chunk-xxx.[hash].js
      component: () =>
        import(/* webpackChunkName: "about" */ "./views/About.vue")
    },
    {
      path: "/list",
      name: "list",
      component: () => import(/* webpackChunkName: "List" */ "./views/List.vue")
    }
  ]
```

### css样式优化

+ vue/cli默认打包样式
  + 默认通过postcss加上不同浏览器前缀
  + 会把通过import或require引入的样式单独打包在一起，并且会把重复的样式代码合并，不会合并路由或组件样式里面的同名样式（样式代码分割）
  + vue/cli3.0脚手脚打包时默认把每个路由文件的style样式单独打包成css文件
  + 对于路由引入的组件，则会把组件的style打包在一起，不同的路由同时引入相同的组件，每个打包的路由样式文件都会包含组件的样式

+ 去除没用的css样式

+ css全局变量

新增全局变量时需要重启服务才能生效

1. 在vue.config.js中定义全局变量

```js
module.exports = {
  css: {
    loaderOptions: {
      less: {
        globalVars: {
          primary: '#fff'
        }
      }
    }
  }
}
```

2. 使用style-resources-loader配置

```js
module.exports = {
  chainWebpack: config => {
      const types = ['vue-modules', 'vue', 'normal-modules', 'normal']
      types.forEach(type => addStyleResource(config.module.rule('less').oneOf(type)))
  },
}
function addStyleResource(rule) {
	rule.use('style-resource')
	.loader('style-resources-loader')
	.options({
		patterns: [
			path.resolve(__dirname, 'src/assets/css/variables.less')
		],
	})
}
```

### eslint和standard（prettier）配置

vscode中可以安装eslint, prettier插件和自定义设置，

```js
"eslint.autoFixOnSave": true,
"eslint.validate": [
    "javascript",
    "javascriptreact",
    "html",
    { "language": "vue", "autoFix": true }
],
"eslint.options": {
    "plugins": ["html"]
},
"editor.tabSize": 2
```

相关插件

```js
"@vue/eslint-config-prettier": "^4.0.1",  // prettier代码格式化
"@vue/eslint-config-standard": "^4.0.0",  // vue standard代码格式化 （vue推荐）
"babel-eslint": "^10.0.1",
```

eslint配置 .eslintrc.js

```js
module.exports = {
  root: true,
  env: {
    node: true
  },
  extends: ["plugin:vue/essential", "@vue/standard"],
  rules: {
    "no-console": process.env.NODE_ENV === "production" ? "error" : "off",
    "no-debugger": process.env.NODE_ENV === "production" ? "error" : "off",
    "indent": [2, 2], // 缩进2个空格
    "no-const-assign": 2, // 禁止修改const声明的变量
    "no-multi-spaces": 1, // 禁止使用多余的空格
    "no-multiple-empty-lines": [1, {"max": 2}], // 空行不能超过两行
    "no-trailing-spaces": 1,  //一行结束后面不要有空格
    "quotes": [1, "single"], //引号使用单引号
    "semi": 2, //不使用分号结尾
  },
  parserOptions: {
    parser: "babel-eslint"
  }
};

```

### js打包优化

+ vue/cli 默认打包脚步
 + 默认会把每个路由分割打包成单独的js文件，js文件内容包括其自身的脚步以及组件的脚步

+ 清除js代码中的console.log

```js
configureWebpack: config => {
  // 去除调试信息
  config.optimization = {
    minimizer: [
      new UglifyJsPlugin({
        uglifyOptions: {
          compress: {
            drop_console: true,
            drop_debugger: true,
            pure_funcs: ["console.log"]
          }
        }
      })
    ]
  }
}
```

+ 配置babel

babel的作用主要是用来转码的，通过各种插件把最新的语法转换为浏览器可以支持的语法，但babel默认只转化语法，不会转化最新的api，或实例方法，此时需要通过babel-polyfill来进行转化，主要用到的插件

+ @babel/preset-env 用来转化各个版本（所支持浏览器）的语法
+ @babel/plugin-syntax-dynamic-import 动态的转化语法 
+ @babel/plugin-transform-runtime 用来转化所用到的api，并且避免全局污染



### ui组件库打包优化（vant）

+ vant安装

```js
cnpm i vant -S
```
+ vant组件按需加载

安装babel-plugin-import

```js
cnpm i babel-plugin-import -D
```

在babel.config.js中配置

```js
module.exports = {
  presets: ["@vue/app"],
  plugins: [
    [
      "import",
      {
        libraryName: "vant",
        libraryDirectory: "es",
        style: true
      },
      'vant'
    ]
  ]
};
```
