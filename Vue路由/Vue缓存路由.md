### 路由切换页面时，会进行 销毁/挂载 页面，如果要保存页面数据：
```js
// 使用 keep-alive 标签包括 router-view 标签，include 指定要缓存哪个路由组件，不设置默认缓存所有
// include 指定的是 路由组件的名字
<keep-alive include="xxx">
  <router-view></router-view>
</keep-alive>
```
### 当需要缓存多个页面时：
```js
// include 写为数组形式，下边代表缓存 aa bb cc 三个路由组件
<keep-alive include="['aa','bb','cc']">
  <router-view></router-view>
</keep-alive>
```
