### props配置后使用，与`data, methods, computed`等同级。


```js
// 简单声明，使用组件同时传递参数
props:['name', 'age', 'sex']

// 例：
<Student name="李四" sex="女" age="20" />
```
### 接收的同时对数据类型进行限制
```js
props:{
    name:String,
    age:Number,
    sex:String
}
```

### 接收的同时对数据类型进行限制，对单独对每个属性定义规则
```js
props:{
    name:{
        type:String,   //指定数据类型
        required:true,  //指定非空属性
        default:99      //指定默认值
    }
}
```
1. `props`是**只读**的，如果尝试修改会产生警告⚠
2. `props`优先级高，可以在`data`配置中通过`this.`获取传入的值，从而间接对数据进行更改。
