### class 类
[参考](https://www.jianshu.com/p/fc79756b1dc0)
class是es6中新增的功能，可以更方便的来定义类和继承，功能跟es5中构造函数定义类类似

**定义类**

```js
class Father {
    // 静态方法 （类方法) 直接调用 不用实例化
    // es6规定 class内部只能有静态方法，不能定义静态属性
    static getMethod () {
        return 'method'
    }
    constructor (name, sex) {
        this.name = name
        this.sex = sex
    }
    // 类的内部方法，此方法会被指向类的原型prototype上，实例化后此方法不会被枚举，而es5定义的可以枚举（两者此地方存在区别）
    getName () {
        return name
    }
}
// 静态属性只能在外面申明
Father.type = 'type'

// 动态扩展类的原型
Object.assign(Father.prototype, {
    getSex () {
        return this.sex
    },
    hegiht: 177
})
```

**继承父类**

```js
// extends继承实际也是基于原型的继承 类似于 Child.prototype = new Parent()
class Child extends Parent {
    // 每一个class都会有一个对应的constructor构造函数，如果没有自定义，则会默认的添加一个
    // 如果自定义了constructor函数，则必须使用super()调用，因为子类没有this，必须继承父类的this，否则会报错
    // super被使用时可以有两种情况，被当做函数或者对象使用
    constructor (name, sex, age) {
        // 此时的super就代表父类的构造函数，执行构造函数用来继承父类的this
        super(name, sex)
        // 如果当做对象使用时，就代表父类的原型对象，此时this的执行指向子类的实例
        console.log(super.getSex()) // Parent.prototype.call(this, props)
        super.type = 'type' // 此时super指向子类实例this
        console.log(super.type) // undefined 类似于 Parent.prototype.type
        this.age = age
        console.log(super) // 此时super不知道是函数还是对象的形式，所有不能直接被使用，必须以函数或对象的形式调用
    }
}
var child = new Child('zhangli', 'nan', '30')
```


#### create方法

Object.create方法用来创建一个对象,第一个参数为对象或null，为对象的原型对象，第二个参数可选，表示添加到对象的可枚举属性

```js
var obj = Object.create(null, {
    a: {
        value: 12
    }
})
```

### setPrototypeOf

Object.setPrototypeOf(obj, null) 此方法用来设置对象的原型对象，可以用来切断原型链

### 