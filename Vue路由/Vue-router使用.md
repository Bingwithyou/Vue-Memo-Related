## 安装：
`npm i router`
>现在vue-router默认版本为4，只能在vue3中使用。vue2应该安装vue-router@3

## 在main.js中引入:
```js
    import VueRouter from 'vue-router'
    Vue.use(VueRouter)  

    // 引入下方建好的路由，一般只需要一个路由就足够  
    import router from ./router'

    // 在Vue实例中引入，与上方 import 中的 router 名字要一致，这里简写了：router: router
    new Vue({
      router,
      render: (h) => h(App),
    }).$mount("#app");

```
## 新建路由：
在`src`目录下新建`router`文件夹，并新建`index.js`文件，写入如下代码（home路由组件为例）：

```js
//引入路由
import VueRouter from 'vue-router'

//引入组件
import Home from '../components/Home'

//创建一个路由器
const router = new VueRouter({
    routers: [
        {
            path: '/home',
            component: '/Home',
        },
    ]
})
```

## 路由导航：

```js 
<router-link to="/home"></router-link>
```

使用该标签代替`<a href>`标签实现路由跳转

## 指定组件展示的位置：

使用`<router-view>`标签指定

### 指定路由组件存放位置，以区分一般组件与路由组件：

在`src`目录下新建`pages`文件夹，新建路由组件：`Home.vue`，同时在`router/index.js`中也要修改引入：
```js
import Home from '../pages/Home'
```

---

### 路由切换原理：

路由组件页面切换时，通过不断挂载与销毁展示（通过`mounted`与`beforeDestory`测试），可以通过配置使组件不做销毁处理。

1. 每个路由组件身上的`$route`不同，存储着自己的路由信息

2. 每个路由组件身上的`$router`相同，整个应用只有一个`router`

### 嵌套路由写法：
```js
export default new VueRouter({
    routers:[
        {
            // 一级路由
            path:'/home',
            component:Home,
            
            // 二级路由，注意路径不带斜线'/'
            children:[
                {
                    path:'news',
                    component:News,
                },
                {
                    ...
                }
            ]
        }
    ]
})
```
#### 在跳转`<router-link>`中要写完整路径（一般写法）
```js
<router-link to="/home/news">
```

### 命名路由的使用：
在`router/index.js`中可以给各个路由定义`name`属性，在`to`跳转时方便书写：
```js
routes:[
    {
        name:'home',
        path:'/home'
        component:Home
    }
]
```
#### 直接通过`name`跳转，必须要绑定`:to`，且书写成对象形式：
```js;
<router-link :to="{name:'home'}">
```
---
### 路由两种工作模式
#### push (defalut)
即带有浏览历史记录的模式

#### replace
没有历史记录的模式，替换当前记录。
开启方法：
```js
<router-link replace>
```
