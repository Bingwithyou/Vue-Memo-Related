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
有局限性，不能满足部分使用场景

### 
