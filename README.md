# antd-demo

基于create-react-app创建的antd PC端demo



## 过程

执行如下命令生成项目：

```
create-react-app antd-demo
```

执行：

```
npm start
```

可以在浏览器中看到`localhost:3000`打开了React默认的页面。

### 暴露所有内建的配置

```
npm run eject
```



接下来：

### 引入antd

```
npm install --save antd
```



使用 babel-plugin-import:

```
// Process JS with Babel.
{
  test: /\.(js|jsx)$/,
  include: paths.appSrc,
  loader: require.resolve('babel-loader'),
  options: {
+   plugins: [
+     ['import', { libraryName: 'antd', style: 'css' }],
+   ],
    // This is a feature of `babel-loader` for webpack (not Babel itself).
    // It enables caching results in ./node_modules/.cache/babel-loader/
    // directory for faster rebuilds.
    cacheDirectory: true
  }
},
```







