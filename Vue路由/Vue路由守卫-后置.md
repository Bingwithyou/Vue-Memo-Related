### 与前置路由一样接收to,from参数，但没有next
```js
// 全局后置路由守卫 --- 初始化的时候被调用、每次路由切换之后被调用
router.afterEach((to, from) => {})
```
>这里的`next`为`undefined`

例：在切换组件后，浏览器页签名字为对应组件名
```js
// 在meta中定义好相关属性值，或者使用其他属性值代替
meta:{title:'主页'}

// 修改页签名
router.afterEach((to, from) => {
  document.title = to.meta.title
})
```

[前置路由守卫](https://github.com/Octopustraveler/Vue-Memo-Related/blob/main/Vue%E8%B7%AF%E7%94%B1/Vue%E8%B7%AF%E7%94%B1%E5%AE%88%E5%8D%AB-%E5%89%8D%E7%BD%AE.md)
