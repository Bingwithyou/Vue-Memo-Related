在事件处理程序中调用 `event.preventDefault()` 或 `event.stopPropagation()` 是非常常见的需求。

尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 `DOM` 事件细节。

为了解决这个问题，`Vue.js` 为 `v-on` 提供了事件修饰符。修饰符是由点开头的指令后缀来表示的。

- .prevent: 阻止默认时间（常用）；
- .stop: 阻止时间冒泡（常用）；
- .once: 事件只触发一次（常用，2.1.4新增）；
- .capture: 使用事件的捕获模式；
- .self: 只有event.taget是当前操作的元素时才触发事件；
- .passive: 事件的默认行为立即执行，无需等待事件回调执行完毕。（2.3.0新增，这个修饰符尤其能够提升移动端的性能。）

```js
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>
```

使用修饰符时，**顺序**很重要；相应的代码会以同样的顺序产生。

因此，用 `v-on:click.prevent.self` 会阻止所有的点击，而 `v-on:click.self.prevent` 只会阻止对元素自身的点击。
