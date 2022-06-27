### 在App.vue中使用组件时，可以添加一些图片，视频等数据在组件中间：

```js
<template>
    <Category>
        <img>
        <video>
    </Category>
</template>
```

#### 之后在组件中定义插槽slot，图片视频资源会自动放到插槽中（没有命名则是默认插槽）。

```<slot></slot>```

>可以指定插槽名字属性 `name`，指定哪些资源加载到哪个插槽中

### 给资源指定插槽位置：

```js
<img v-slot:center></img>

//v-slot缩写为#
// 例：
<img #center></img>
```


### 给插槽命名
```js
<slot name="center"></slot>
```

这样图片资源会自动放到`name="center"`的插槽中。

相关样式可以写在App.vue中，也可以写在组件中。



### 作用域插槽：

使用插槽时，可以将数据传给App.vue，更灵活。

1. 将数据绑定到插槽上（组件里定义）：
```js
<slot :game="games"></slot>
```


2. 接收使用数据（App.vue）：
```js
<template>
  <HelloWorld>
    <template v-slot:test="slotProps">
      {{ slotProps.??? }}
    </template>
  </HelloWorld>
</template>
```
>要多包裹一层`template`，`slotProps`可以自己定义名字，之后通过该名字访问数据
