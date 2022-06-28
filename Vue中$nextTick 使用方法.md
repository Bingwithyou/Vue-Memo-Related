 `$nextTick( callback ) `

#### 在模板解析完后 **（DOM 更新结束）** 会执行 `callback` 回调函数

当改变数据后，要基于更新后的 DOM 进行某些操作时，要在`nextTick` 所指定回调函数中执行。

```js
// 例：自动获取输入框的输入焦点
this.$nextTick(function () {
    this.$refs.inputContent.focus();
});
```

>因为 Vue 为了提高渲染效率，会将全部代码读完后才会解析模板；
>
>如果直接尝试获取焦点 `focus` ，可能会因为**模板**上还没有解析渲染出输入框
>
>此时 `input` 输入框被 `v-if` 或 `v-show` 控制，导致不能自动获取焦点。
