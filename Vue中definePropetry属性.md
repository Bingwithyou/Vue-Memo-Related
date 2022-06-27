```js
 //用definePropetry方法给对象定义新属性
let number = 18
let person = {
    name: '张三',
    sex: '男',
}

Object.definePropetry(person, 'age',{
    value: 18,

    enumerable: true,  //控制属性是否可以枚举，默认值false（能否被遍历）

    writable: true,  //控制属性是否可以被修改，默认值false

    configurable: true,  //控制属性是否可以被删除，默认值false（.delete）

    //每当被读取Person的age属性时，get函数(getter)就会被调用，且返回值就是age的值
    get(){
        console.log('age属性被读取')
        //这里将age属性动态绑定到number身上，每次读取age时会访问number返回他的值
        return number   
    },

    //Person的age属性被修改时，set函数(setter)就会被调用，且收到修改的值
    set(value){
        console.log('age属性被修改，值为:', value)
        number = value    //这里将要修改的值赋给number，这样每次get获取age值的时候会读取最新的number值
    }
})
```
