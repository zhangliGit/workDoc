
### dom api

+ getElementById 通过id获取dom元素
+ getElementsByClassName() 通过class获取元素集合
+ getElementsByTagName() 通过标签获取元素集合
+ getElementsByName() 通过name属性获取元素集合

### 新增查询api

+ querySelector() 通过id或class或元素 获取dom节点
+ querySelectorAll() 通过class或元素获取dom节点列表

### dom元素位置属性

**event对象**

+ event.clientX 鼠标相对于网页可视区域左上角水平距离
+ event.clientY 鼠标相对于网页可视区域左上角垂直距离
+ event.pageX 鼠标相对于网页左上角水平距离 （没有滚动条时于clientX一样）
+ event.pageY 鼠标相对于网页左上角垂直距离（没有滚动条时于clientX一样））
+ event.offsetX 鼠标相对于点击元素水平距离
+ event.offsetY 鼠标相对于点击元素垂直距离
+ event.layerX 鼠标相对于点击元素父元素的水平距离 （没有父元素相对于自己）
+ event.layerY 鼠标相对于点击元素父元素垂直距离（没有父元素相对于自己）
+ event.screenX 鼠标相对于屏幕水平距离
+ event.screenY 鼠标相对于屏幕垂直距离

**dom对象event.target**
+ clientHeight 元素可视区域高度
+ clientWidth 元素可视区域宽度
+ offsetHeight 元素高度
+ offsetWidth 元素宽度
+ offsetLeft 元素相对于网页左边距离，如果父元素设置position属性，则为相对父元素左边距离
+ offsetTop 元素相对于网页上面距离，如果父元素设置position属性，则为相对父元素上面距离
+ scrollHeight 元素滚动高度，
+ scrollWidth 元素滚动宽度，

