### 作用：实现祖与后代组件间通信
父组件有一个`provide`选项来提供数据，后代组件有一个`inject`选项来使用这些数据。
```js
// 1. 在祖 组件中
setup(){
  ...
  let car = reactive({name:'Benz', price:'55W'})
  // 第一个参数代表名字，第二个参数才是数据
  provide('car',car)
  ...
}

// 2. 在后代组件中
setup(){
  ...
  const car = inject('car')
  return car
  ...
}
```
