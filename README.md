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

### 使用 babel-plugin-import:

```
babel-plugin-import
```

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

### 支持less

```
npm install --save less less-loader
```

修改webpack配置

```
  {
    exclude: [
      /\.html$/,
      /\.(js|jsx)$/,
      /\.css$/,
+     /\.less$/,
      /\.json$/,
      /\.bmp$/,
      /\.gif$/,
      /\.jpe?g$/,
      /\.png$/,
    ],
    loader: require.resolve('file-loader'),
    options: {
      name: 'static/media/[name].[hash:8].[ext]',
    },
  }

...

  // Process JS with Babel.
  {
    test: /\.(js|jsx)$/,
    include: paths.appSrc,
    loader: 'babel',
    options: {
      plugins: [
-       ['import', [{ libraryName: 'antd', style: 'css' }]],
+       ['import', [{ libraryName: 'antd', style: true }]],  // import less
      ],
   },

...

+  // Parse less files and modify variables
+  {
+    test: /\.less$/,
+    use: [
+      require.resolve('style-loader'),
+      require.resolve('css-loader'),
+      {
+        loader: require.resolve('postcss-loader'),
+        options: {
+          ident: 'postcss', // https://webpack.js.org/guides/migrating/#complex-options
+          plugins: () => [
+            require('postcss-flexbugs-fixes'),
+            autoprefixer({
+              browsers: [
+                '>1%',
+                'last 4 versions',
+                'Firefox ESR',
+                'not ie < 9', // React doesn't support IE8 anyway
+              ],
+              flexbox: 'no-2009',
+            }),
+          ],
+        },
+      },
+      {
+        loader: require.resolve('less-loader'),
+      },
+    ],
+  },
],
```

## 完毕

详见代码



## 参考链接

[在 create-react-app 中使用](https://ant.design/docs/react/use-with-create-react-app-cn)