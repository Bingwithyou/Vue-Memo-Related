### 自定义 hook 函数
 - 什么是 hook? 本质是一个函数，把 setup 中函数使用的 Composition API 进行了封装。
 - 类似于 Vue2 中的 mixin。
 - 自定义 hook 的优势：复用代码，让 setup 中的逻辑更清楚易懂。
### 举例：
1. 在 src 新建文件夹命名为：hooks
2. 在 hooks 中新建 js 文件，在里面实现功能
```js
// 引入使用到的钩子函数，文件命名为 getPoint.js
import {reactive, onMounted, onBeforeUnmount} from 'vue'
// 获取鼠标坐标
export default funciton (){
  let point = reactive({
    x:0,
    y:0
  })
  funtion getPoint(event){
	point.x = event.pageX
	point.y = event.pageY
  }
  // 添加鼠标监听事件
  onMounted(() => {
	window.addEventListener('click', getPoint)
  })
  // 解绑事件
  onBeforeUnmount(() => {
	window.removeEventListener('click',getPoint)
  })
  // 返回值
  return Point
}
```
3. 在 setup 中引用：
```js
<template>
  <h1>鼠标坐标为：X:{{point.x}}, y:{{point.y}}</h1>
</template>

import getPoint from '../hooks/getPoint'
export default {
  setup(){
	let point = getPoint()
    return {point}
  }
}
```
