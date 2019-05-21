### 本地存储

#### sessionStorage
> 本地会话存储，只对当前的会话窗口有效，如果当前窗口关闭，则被自动销毁，sessionStorage在不同tab窗口间数据是不能共享的

```js
window.sessionStorage.setItem('my-tag', 'true')
```
#### localStorage
> 本地持久存储，存储的值在浏览器中一直存在，就算关闭也不会清除存在的值，会存在浏览器安装目录的磁盘中，除非手动清除，并且在浏览器中不同的窗口中可以共享

```js
window.localStorage.setItem('my-tag', true)
```

### 离线缓存（application cache）

**本地缓存应用所需要的文件**

**优点**

+ 离线缓存所有需要的文件

+ 提升界面加载速度

+ 减轻服务器压力

**缺点**

+ 会缓存所有动态的资源文件，包括html界面，当html界面更新的时候仍然会读取缓存的文件，达不到更新的效果 

> 使用方法

+ 创建manifest文件，必须为xx.appcache后缀，请文件类型为text/cache-manifest

+ 在网页html标签中引入 <html manifest = "xx.appcache">


### service worker


### cacheStorage


### indexedDB

**索引性数据库**



### web worker

> web worker是运行于后台的一个JavaScript进程，可以理解为脱离主线程的一个子线程，其不会对主线程的运行造成影响，所以其常用来执行一些耗时长，容易阻塞的任务

!> web worker只是创建了一个子线程来执行JavaScript代码，并不能说明JavaScript是多线程的，执行完脚本之后通过postMessage方法把数据发送到主线程（通过实例的onmessage接收）

+ web worker不能访问widnow对象
+ web worker不能操作dom对象
+ web worker不能parent 对象

```js
// work.js

setTimeout(() => {
  postMessage('执行完成')
}, 2000)

// work.html
let w = new Worker('work.js')
w.onmessage = function(event) {
  conosle.log(event.data)
}

// 停止执行
function stop() {
  w.terminate()
}
```

### canvas画布



### webgl