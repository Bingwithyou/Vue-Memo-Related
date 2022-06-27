1. `v-bind` 绑定数据，响应式更新`HTML`，绑定后可访问data中的数据，且为单向绑定，数据只能从`data`流向页面。

```js
<input type="text" v-bind:value="name">
<input type="text" :value="name">
```

2. `v-model` 双向绑定，数据能从`data`流向页面，也可以从页面流向`data`，`v-model`只能应用在表单类元素上 **(输入类元素)**。

```js
<input type="text" v-model:value="name">
<input type="text" v-model="name">
```

3. `v-on` 监听事件，缩写为`@`

### 常用鼠标事件：
- `@change`域的内容发生改变时触发的事件
- `@click`
- `@mouseenter`
- `@mouseleave`
- `@mousemove`
- `@mousedown`
- `@mouseup`
- `@input`输入文本时触发的事件
- `@focus`，`@blur`
