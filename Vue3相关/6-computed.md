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
    return person.firstName +' '+ person.lastName
  },
  set(value){
    let nameArr = value.split(' ')
    person.fristName = nameArr[0]
    person.lastName = nameArr[1]
  }
})

```
