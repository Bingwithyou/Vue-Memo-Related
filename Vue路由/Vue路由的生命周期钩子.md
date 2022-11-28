### activated()
当组件生效，展示出来时触发`activated()`钩子

### deactivated()
某个组件被切换后，触发`deactivated()`钩子
>在组件中声明调用，与data,name同等级别位置

### $nextTick
真实 DOM 放入页面后再调用某个函数
```js
this.$nextTick(funciton(){
  // 获取输入焦点
  this.$refs.inputTitle.focus()
})
```
