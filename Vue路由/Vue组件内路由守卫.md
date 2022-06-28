### 进入组件时的路由守卫
```js
// 通过路由规则，进入该组件时被调用
beforeRouteEnter (to, from, next) {
  ...
  next()
}
```
### 离开组件时的路由守卫
```js
// 通过路由规则，离开该组件时被调用
beforeRouteLeave (to, from, next) {
  ...
  next()
}
```
>注意与全局前后置路由守卫区分，只有全局的才叫前后置。
>
>通过路由规则开，路径发生变化后才会触发beforeLeave路由守卫。
