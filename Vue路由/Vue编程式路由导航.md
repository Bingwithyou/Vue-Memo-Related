### 作用：不借助 `<router-link>` 实现路由跳转，让路由跳转更加灵活
具体代码：
```js
// $router 的两个API
this.$router.push({
  name:'detail',
  params:{
      id:xxx,
      title:xxx
   }
})

this.$router.replace({
  name:'breakdown',
  params:{
    id:xxx,
    title:xxx
  }
})
//----------------------------
// 举例，原始写法:
<router-link :to="{
  name:'detail',
  query:{
    id:x.id,
    title:x.title
  }
}">
</router-link> 

// 新写法，to后边直接复制过来：
methods: {
  pushPage(){
    this.$router.push({
      name:'detail',
      query:{
        id:x.id,
        title:x.title
      }
    })
  }
}
```


> push 模式相当于压栈，产生浏览器历史记录
> replace 模式是替换当前最新的一次历史记录
```js
// 前进
this.$router.forward()
// 后退
this.$router.back()
// 传入数字，例如 '-1' 代表后退一次
this.$router.go()
```
