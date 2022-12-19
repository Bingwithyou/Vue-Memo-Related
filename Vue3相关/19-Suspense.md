### 等待异步组件时渲染一些额外内容，让应用用户体验更好
使用：
```js
// 异步引入组件
import {defineAsyncCommponent} from 'vue'
const child = defineAsyncComponent(() => import ('./components/Child.vue'))
```
> 使用`Suspense`包裹组件，并配置好`default`与`fallback`
```js
<template>
  <div class="app">
	<h3>我是App组件</h3>
	// Suspense是内置组件，不需要import
	<Suspense>
	  <template v-slot:defalut>
		<Child />
	  </template>
	  
	  // 在组件没有加载完成时显示
	  <template v-slot:fallback>
		<h3>加载中...</h3>
	  </template>
	</Suspense>
  </div>
</template>
```
