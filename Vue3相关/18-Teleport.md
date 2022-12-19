### `Teleport`是一种能够将我们的组件html结构移动到指定位置的技术
> 当点击弹窗时，可以将指定html元素传送到指定的位置，从而不会影响原来位置其他htlm元素的位置与样式。
```js
// 会将teleport包裹的元素传送到body标签下
<teleport to="body">
  <div v-if="isShow" class="mask">
	<div class="dialog">
	  <h3>我是弹窗</h3>
	  <button @click="isShow = false">关闭弹窗</button>
	</div>
  </div>
</teleport>
```
