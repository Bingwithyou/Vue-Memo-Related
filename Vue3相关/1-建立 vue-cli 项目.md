## 创建Vue3.0工程
### 1.使用 vue-cli 创建
```js
// 确保 @vue-cli 版本在 4.5.0 以上
vue --version

// 安装或者升级 @vue-cli
npm install -g @vue-cli

// 创建
vue create vue_test

//启动
npm run serve
```
### 2.使用 vite 创建
```js
// 初始化项目
npm init vite-app <project-name>

// 进入工程目录安装依赖
npm install

// 运行
npm run dev
```
>vite 创建不会自动安装相关依赖（没有node_modules文件夹）需要手动 npm install
