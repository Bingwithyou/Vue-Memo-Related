## hash模式 (default)
浏览器显示路径`#`号后边的都属于hash值，**不会发送给服务器**。

### 修改路由该工作模式：
在`router/index.js`中设置`mode`属性
```js
new VueRouter({
  // hash, history
  mode:'hash',
  routes:[
    {...},
    {...},
  ]
})
```
