## 安装：
`npm i axios`

`import axios from 'axios'`

## 使用：
```js
axios.get('http://localhost:xxxx'/xxx').then(
    response => {
        // .data返回响应的数据
        console.log('Request Success', response.data)
    },
    error => {
        // 请求失败返回错误信息
        console.log('Request Failed', error.message)
    }
)
```
>如果尝试跨域请求，服务器能响应但无法拿到数据，同时浏览器会报错：No 'Access-Control-Allow-Origin'。



## 跨域解决办法：

### 通过设置 CORS 响应头部解决：

```js
res.setHeader('Access-Control-Allow-Origin','*') 
```
表示允许来自任何域的请求，有安全风险。



### 通过 jsonp script src 方法规避同源策略：

只能解决 `get` 跨域请求，需要前后端配合，不常用。

`JSONP`是一个非官方的协议，它允许在服务器端返回javascript标签到浏览器，在浏览器端通过调用`javascript`函数的形式实现访问跨域资源或数据。

### 代理服务器方法（http 协议通信不受跨域影响）：

#### 利用 Vue-cli 创建代理服务器，第一种方法：
>在 vue.config.js 中配置，该代理服务器的端口号和本地主机一样：

```js
// 开启代理服务器
devServer: {
    // 这里端口号填写目标服务器的，只需要写端口号
    proxy: 'http://localhost:xxxx'
}
```

#### 缺点：

- 只能配置一个代理服务器。

- 会优先读取本地 `public` 同名已有的资源，可能因为重名问题导致请求不到数据（不能灵活配置是否走代理）。

- 之后需要改写 axios 请求：`axios.get('http://localhost:xxxx/xxx')`这里的端口号要填写本地计算机，后边请求的数据则保持原样。


### 第二种配置方法，可配置多个代理

```js
devServer {
    proxy: {
        '/api': {
            target:'<url>',

            // pathRewriter: {'key','value'}  用于重写请求路径，可以用来清除请求头：pathRewriter:{'^api':''} 将/api替换为空值。

            // ws: true  用于支持 websocket，通信方式

            // changeOrigin: true  为true时，服务器收到请求头host为：localhost:5000(相当于说谎), false 时为 localhost:8080。在React脚手架里默认false。
        },
        '/foo': {
            target: '<other_url>'
        }
    }
}
```

- api属于请求前缀，控制请求是否走代理，如果加上'/api'代表走代理，可更改名称。

- 同时要在 axios 中更改: `http://localhost:8080/api/...`

- `target:'<url>'` 填写目标服务器的地址，即向谁转发请求。

- 可灵活配置多个代理，缺点是配置略显繁琐，请求资源必须加前缀。


#### 一些常见的请求方法

1. `xhr = new XMLHttpRequest(), xhr.open(), xhr.sent()`
该方法属于 JS 内置，最原始且用起来比较麻烦，用的最多的是用一些封装过的插件

2. `jquery $.get $.post`
虽然包装了 XMLHttpRequest 方法，但因为`jQuery`现在用的比较少，体积不占优势。

3. `axios` 目前最常用

4. `fetch` 属于 windows 内置方法，用的不多，兼容性较差。
