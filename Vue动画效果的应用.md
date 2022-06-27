### 先定义好动画效果(@keyframes)：

```js
@keyframes someAnimation {
    from{
        transform: translateX(-100px)
    }
    to{
        transform: translateX(0px)
    }
}
```


### 定义好动画类名，将其添加到需要用到动画效果的元素
#### 一般写法：

```js
.come{
    animation: someAnimation 1s;
}
.go{
    animation: someAnimation 1s reverse;
} 
```


#### Vue写法：

>在 template 模板中，将需要动画效果的标签用 transition 包括起来（多个元素用 transition-group 并指定 key 属性值），之后定义类 `v-enter-active` 和 `v-leave-active`，在元素隐藏与加载时，Vue会自动调用动画。

```js
<template>
    <transition>
        <h1> testText </h1>
    </transition>
</template>
```
```js
<style>
    .v-enter-active{
        animation: someAnimation 1s;
    }
    .v-leave-active{
        animation: someAnimation 1s reverse;
    }
</style>
```


1. 其中v开头为默认，如果 `transition` 有 `name` 属性，则将 `v` 替换为 `name` 属性的值。

2. 如果要最开始就有动画效果，可以给元素添加 `appear` 属性（默认值为true）。

3. 最终解析完后的模板里，不包含 `transition` 标签。

#### 过渡写法（完整）：

```js
/* 进入的起点 */
.v-enter{
    transform: translateX(-100%)
}

/* 进入的终点 */
.v-enter-to{
    transform: translateX(0)
}

/* 离开的起点 */
.v-leave{
    transform: translateX(0)
}

/* 离开的终点 */
.v-leave-to{
    transform: translateX(-100%)
}
```


#### 进入的起点和离开的终点是一样的，上述可简写为：

```js
/* 进入的起点、离开的终点 */
.v-enter, .v-leave-to{
    transform: translateX(-100%)
}

/* 进入与离开的中间，这里可以写动画持续时间与效果，相当于省略了在对应元素样式中写transition效果 */
.v-enter-active, .v-leave-active{
    transition: 0.5s linear
}

/* 进入的终点、离开的起点 */
.v-enter-to, .v-leave{
    transform: translateX(0)
}
```
