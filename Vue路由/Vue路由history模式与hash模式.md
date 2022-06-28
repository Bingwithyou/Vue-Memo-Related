## hash模式 (default)
>浏览器显示路径`#`号后边的都属于hash值，不包含在HTTP请求中**不会发送给服务器**。

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
>1. 地址中有#号，不美观
>2. 第三方手机app分享可能因校验问题，被标记为不合法
>3. 兼容性好

## history模式
>使用该模式的项目部署后，不能刷新页面，因为会将当前路径当作资源请求导致404。

❌错误示范：
```js
// 打包，生成dist文件夹
npm run build

// 打包好后的项目不能直接打开，需要部署，这里利用express测试
// 新建文件夹，运行 npm init 初始化
npm init

// 安装express
npm i express

// 新建server.js，写入代码：
const express = require('express')

const app = express()

app.get('/person', (req, res)=>{
  res.send({
    name:'admin',
    age:18,
  })
})

// 监听5005端口
app.listen(5005, (err)=>{
  if(!err) console('server startup successed!')
})

// 启动服务器
node server
```
通过路由切换页面时不会发送网路请求（浏览器Network页签没有动静），假设此时路径为：localhost:5005/home/message

如果刷新页面，则会把该路径作为资源请求，无法达到则发生404错误。

使用路由history模式可以避免此问题。

>1. 地址不带#号，美观
>2. 兼容性和hash模式相比略差
>3. 应用部署上线需要后端人员支持，解决刷新页面服务器端404问题
