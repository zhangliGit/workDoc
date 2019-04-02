
### 什么是BFC

> BFC全称是Block Formatting Context, 即所谓的块格式化上下文，它是CSS2.1规范定义的，关于css渲染定位的一个概念，它定义了一块独立的渲染区域，包括的元素布局不会影响外面，外面的也不会影响到里面

### 常用定位方案

在定位的时候，浏览器会根据元素的盒类型和上下文对这些元素进行定位，可以说盒就是定位的基本单位，定位时，有三种定位方案：常规流，浮动和绝对定位

+ 常规流

  + 在常规流中，盒一个接着一个排列
  + 在块级格式化上下文里面，他们竖着排列
  + 在行内格式化上下文里面，他们横着排列
  + 当position为static和relative，并且flaot为none时会触发常规流
  + 对于静态定位position：static（默认值），盒的位置是常规流布局里的位置
  + 对于相对定位 position: relative, 盒偏移位置由这些属性定位，top，bottom，left and margin，即使有偏移，仍然保留原有的位置，其它常规流不能占用这个位置

+ 浮动

  + 盒称为浮动盒，不完全脱离文本流
  + 它位于当前行的开头和结尾
  + 这导致常规流环绕在它的周边，除非设置clear属性

+ 绝对定位

  + 绝对定位方案，盒从常规流中被移除，不影响常规流的布局
  + 它的定位相对于它的包含块，相关css属性 top  left bottom right
  + 如果元素的属性为position和fixed，那么他为绝对定位元素
  + 对应position属性，元素将相对于最近的一个relative，position或fixed进行定位，如果没有，则相对于body

### 块格式化上下文（BFC）

  **创建BFC的方法**

  + 根元素或其他包括它的元素
  + 浮动（float不为none的元素）
  + 绝对position定位 属性为absolute和fixed
  + display行内块元素 属性为inline-block， flex， grid，table-cell
  + overflow的值不为visible的元素



