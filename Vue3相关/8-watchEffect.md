### watchEffect函数
 - watch 的套路是：既要指明监视的属性，也要指明监视的回调。
 - watchEffect 的套路是：不用指明监视哪个属性，属性的回调中用到哪个属性就监视哪个属性。
 - watchEffect 有些类似于 computed：
   - computed 注重计算出来的值（回调函数的返回值），所以必须写返回值。
   - watchEffect 更注重的是过程（回调函数的函数体），所以不用写返回值。
```js
// watchEffect 所指定的回调中用到的数据只要发生变化，则直接重新执行回调。
watchEffect(()=>{
// 当 sum 和 age 变动时就会触发 watchEffect
  const x1 = sum.value
  const x2 = person.age
  console.log("watchEffect 回调执行了")
})
```
