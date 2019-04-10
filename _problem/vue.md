### vue单页面中监听浏览器前进和返回键

vue中路由使用动画切换，点击界面元素时可以很容易的判断前进和后退使用动画，但是对应浏览器的操作则很难判断，可以使用路由监听然后判断history中的state的key值对比，确定是前进还是后退

```js
export default {
  watch: {
    $route (to, from) {
      // 默认第一个界面state为null,每次push一个新的路由 都会产生一个key值，新打开的都比之前的大
      // 每次打开路由时缓存当前的key值，当前进和后退时，新的key值和缓存的对比，如果大则是前进，小则是后退 
      if (history.state == null || history.state.key < this.lastKey) {
        // 后退操作
        this.transitionName = 'slide-right'
      } else {
        // 前进操作
        this.transitionName = 'slide-left'
      }
      // 缓存key
      this.lastKey = history.state == null ? 0 : history.state.key
    }
  },
}
```

### vue-cli3.0路由history模式打包后界面显示不了