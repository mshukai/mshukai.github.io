# webpack-dev-server 详解

本文假设大家已经知道了 Webpack 的一些基础配置以及 webpack-dev-server 的作用——概括一下就是：它是 Webpack 提供的一个文件访问服务器，用于提升开发效率，支持热更新、代理配置等重要功能。但是对于它的详细配置及原理，估计大多数人尚不清晰，这篇文章就是用案例记录一下与 webpack-dev-server 工作相关的核心配置项及**这些配置项在生产环境的对应关系**。

```javascript
const path = require('path')
const { CleanWebpackPlugin } = require('clean-webpack-plugin')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: './foo.js',
  output: {
    path: path.join(__dirname, 'dist'),
    filename: '[name]-[fullhash:8].js',
    publicPath: '/',
  },
  mode: 'development',
  devServer: {
    open: true,
    port: 3000,
    hot: true
  },
  plugins: [
      new CleanWebpackPlugin(),
      new HtmlWebpackPlugin({
        template: path.join(__dirname, `index.html`),
        filename: 'index.html'
      })
  ]
};

```

