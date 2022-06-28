## 路由守卫以用来在跳转某个路由组件时，进行一些逻辑判断是否放行（权限）

例：要访问`views`组件需要满足下面条件
1. `localStorage`中的`name`值为`admin`
2. 如果访问的是其他组件则不受限制

### 使用：
在`router/index.js`中定义：
```js
// 全局前置路由守卫 --- 初始化、每次路由切换之前被调用，接收三个参数
router.beforeEache((to, from, next) => {
    if(to.path === '/home/views' && localStorage.getItem('name') === 'admin' ){  
      // 只有调用了next路由才会放行
      next()
    }
})
export default router
```
>to 代表去哪，from代表从哪来

>需要修改默认暴露的路由组件，定义一个router常量接收，暴露放在beforeEach下方
