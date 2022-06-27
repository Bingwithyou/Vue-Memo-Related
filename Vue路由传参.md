## 为了复用路由组件，可以根据传递的参数来展示不同的页面数据

### 传递参数，to的字符串写法：
**父**路由组件通过在`<router-link>`中指定参数，以'?'开始，'&'分隔：
```js
<router-link to="/home/message/detail?id=123&title=Hola!"></router-link>
```
如果需要传递组件内的数据，应该先把to绑定：`:to`，然后用模板字符串\` \`与模板语法`${}`：
```js
:to="`/home/message/detail?id=${m.id}&title=${m.title}`"
```

### to的对象写法：
```js
<router-link :to="{
  path:'/home/message/detail',
  query:{
    id:???,
    title:???
  }
}"></router-link>
```

### 接收参数：
经过上一步的传参，detail路由组件身上多了一个`query`存储数据`query: {id: "123", title: "Hola!"}`
在`Detail.vue`组件中调用：
```js
$route.query.id
$route.query.title
```

## params参数
在`router-link`标签中传递参数：
```js
// message组件向detail子组件传参
<router-link :to="/home/message/detail/123/hola"></router-link>
```
之后在`roter/index.js`的`path`中定义接收：
```js
// message的子路由
children:[
  {
    name:'test',
    path:'detail/:id/:title',
    component:Detail,
  }
]
```
之后在子组件Detail身上存在`params: {id: "123", title: "hola"}`，其中id与title是在上方组件中定义的

#### 使用params
与`query`用法基本一致：
```js
$route.params.id
$route.params.title
```
>路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置
