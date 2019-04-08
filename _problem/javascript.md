### 在浏览器中监听点击事件无效出现警告

[参考](https://blog.csdn.net/userkang/article/details/80857870)
对 touchstart 和 touchmove 事件处理函数，会默认设为 passive: true。因此默认也会忽略 preventDefault() 的调用

**解决方案**
+ 取消被动模式

```
window.addEventListener('touchmove', function(){}, { passive: false })
```

+ 利用css解决

```
body {
  touch-action: none
}
```