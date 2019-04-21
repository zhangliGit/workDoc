### webpack 代理配置

**vue-cli 2.0配置**

在config目录的index.js中配置

```js
 dev: {
   proxyTable: {
      '/healthy': {
        target: 'http://test.coracle.com:10151/patachealth', // 服务器地址
        changneOrigin: true, // 跨域
        pathRewrite: {
          '^/healthy': '/healthy'   //重写接口
        }
      }
    }
 }
```

**vue/cli 3.0配置**

在根目录创建vue.config.js
```js
module.exports = {
  // 配置本地服务
  devServer: {
    open: true, // 默认打开浏览器
    host: '0.0.0.0',
    port: 8089,
    https: false,
    hotOnly: false,
    proxy: {
      '/healthy': {
        target: 'http://xiaoyueyue.com.cn:3000',
        changeOrigin: true,
        ws: true,
        pathRewrite: {
          '^/healthy': '/healthy'
        }
      }
    }
  }
}
```

!> 如果没有配置pathRewrite, 转发时不会带/healthy路径，`http://localhost:8080/healthy/list`则会被代理到`http://test.coracle.com:10151/patachealth/list`

!> 如果有配置pathRewrite, 则会带上配置的路径，`http://localhost:8080/healthy/list`则会被代理到`http://test.coracle.com:10151/patachealth/healthy/list`


### 第三方库cdn加速配置

`简单的手动配置`

使用cdn加速服务访问第三方模块，可以大大的降低打包文件体积大小提交网页加载速度

目前使用的是本地和打包文件都使用cdn加速

在html文件中直接加入cdn连接

```html
<script src="https://cdn.bootcss.com/vue/2.6.10/vue.min.js"></script>
<script src="https://cdn.bootcss.com/vue-router/3.0.2/vue-router.min.js"></script>
<script src="https://cdn.bootcss.com/vuex/3.1.0/vuex.min.js"></script>
<script src="https://cdn.bootcss.com/axios/0.19.0-beta.1/axios.min.js"></script>
```

在vue.config.js中加入配置
```js
chainWebpack: config => {
  config.externals = {
    'vue': 'Vue',
    'vue-router': 'VueRouter',
    'vuex': 'Vuex',
    'axios': 'axios'
  }
}
```

`自动配置`

通过htmlWebpackPlugin插件实现

1. 在生成的html配置中注入cdn脚本数组，注入后就可以通过esj语法htmlWebpackPlugin.options.cdnConfig在html界面获取配置的项，然后遍历

```js
// 多页面配置
exports.entries = function () {
  let entries = {}
  pageList.forEach((pageDir) => {
    entries[pageDir] = {
      // 入口文件
      entry: `src/pages/${pageDir}/main.js`,
      // 模板来源
      template: 'public/index.html',
      // 在 dist/index.html 的输出
      filename: `${pageList.length === 1 ? 'index' : pageDir}.html`,
      // 界面标题配置
      title: '',
      // 在这个页面中包含的块，默认情况下会包含
      // 提取出来的通用 chunk 和 vendor chunk
      cdnConfig: process.env.NODE_ENV === 'production' ? cdn : [],
      chunks: ['chunk-vendors', 'chunk-common', pageDir]
    }
  })
  return entries
}
```

2. 在html模板中遍历配置cdn脚步

```js
<% htmlWebpackPlugin.options.cdnConfig.forEach(function(item){ %>
  <script type="text/javascript" src="<%= item %>"></script>
<% }) %>
```

### vue-cli3.0配置多环境

在项目开发过程中，我们往往会有多个环境切换开发，一般有测试环境，开发环境和生产环境的区分，为了方便切换环境，可以在打包时自定义配置，不用手动更改

+ 测试环境：开发中一般用mock模拟接口来开发
+ 开发环境：调用后端服务器接口进行联调开发
+ 生产环境：用于上线发布的环境

**配置分为下面几个部分**

> 配置package.json

通过--mode配置了不同命令的打包模式，最终会指向根目录对应.env.[mode]文件，在里面可以重新设置打包模式和环境变量，通过环境变量来确定对应的url地址

```js
"scripts": {
  "dev": "vue-cli-service serve --open", // 默认开启开发环境
  "dev-test": "vue-cli-service serve --open --mode dev-test", // 开启测试环境
  "dev-prod": "vue-cli-service serve --open --mode dev-prod", // 开启生产环境
  "build": "vue-cli-service build", // 默认打包开发环境
  "build-test": "vue-cli-service build --mode build-test", // 打包测试环境
  "build-prod": "vue-cli-service build --mode build-prod", // 打包生产环境
  "lint": "vue-cli-service lint",
  "test:unit": "vue-cli-service test:unit"
}
```

> 新增对应的环境变量文件

需要在文件中重新设置模式为development和production 不然本地启动或打包会报错，因为默认的模式只支持development，production和test这三种

+ .env.dev-test 

```
//  本地开启测试环境
NODE_ENV = develoment
VUE_APP_URL = 'test'
```
+ .env.dev-prod

```
// 本地开启生产环境
NODE_ENV = development
VUE_APP_URL = 'prod'
```

+ .env.build-test

```
// 打包测试环境
NODE_ENV = production
VUE_APP_URL =  'test'
```

+ .env.build-prod

```
// 打包生产环境
NODE_ENV = production
VUE_APP_URL = 'prod'
```

> 配置接口环境文件

在项目文件中可以通过process.env.VUE_APP_URL拿到环境变量，通过判断设置不同的url

```js
const  CONFIG_ENV = process.env.VUE_APP_URL
let hostUrl = ''

if (CONFIG_ENV === 'test') {
  hostUrl = '我是测试环境'
}  else if (CONFIG_ENV === 'prod') {
  hostUrl = '我是正式环境 '
} else {
  hostUrl = '我是开发环境'
}

export default hostUrl
```

### vue-cli3.0打包history模式

```
打包的history模式需要在服务器中配置访问，还需配置刷新访问404问题， 本地不能访问
```