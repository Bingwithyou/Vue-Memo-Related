### 通过`<router-link>`标签跳转，会自动渲染为`<a>`标签
```js
<router-link to="???">

// 身上有`$router.forward`和`back`方法，可以前进和后退历史记录（不确定能不能指定步数）
// 前进
$.router.forward()

// 后退
$.router.back()

// go方法可以指定方向和步数
$.route.go(2)
$.route.go(-1)
```

### 路由切换组件时，会默认销毁之前的组件
利用`<keep-alive>`标签包裹`<roter-view>`可以使组件保持挂载，达到缓存目的。
```js
// 通过include指定缓存哪个组件（填写组件名），不指定则默认全部缓存
<keep-alive include="???">
  <router-view></router-view>
</keep-alive>

```
### [路由生命周期钩子函数](https://github.com/Octopustraveler/Vue-Memo-Related/blob/main/Vue%E8%B7%AF%E7%94%B1%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E9%92%A9%E5%AD%90.md)
