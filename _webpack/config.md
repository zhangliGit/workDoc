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
