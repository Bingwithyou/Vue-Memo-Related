### computed计算属性写法

#### 简写（没有考虑计算属性被修改的情况)
```js
// 需要引入 computed
import {reactive,computed} from 'vue'
setup(){
  let person = reactive({
    firstName: 'Arthur',
    lastName: 'Morgan'
  })
  // 当更改计算属性值时，会警告：Write operation failed: computed value is read only
  // 回调函数必须return，结果就是计算的结果。如果计算属性依赖的数据发生变化，那么会重新计算
  person.fullName = computed(()=>{
    return person.firstName + person.lastName
  })
  return {person}
}
```
#### 完整写法（考虑读写）
```js
person.fullName = computed({
  get(){
    // 如果读取计算属性的值，默认调用get方法
    return person.firstName +' '+ person.lastName
  },
  set(value){
    // 如果要想修改计算属性的值，默认调用set方法
    let nameArr = value.split(' ')
    person.fristName = nameArr[0]
    person.lastName = nameArr[1]
  }
})

```
### 总结：
1. 计算属性可以直接读取或者修改
2. 如果要实现计算属性的修改操作，那么computed的实参应该是对象
- 读取数据触发get方法
- 修改数据触发set方法，set函数的形参就是你赋给他的值
