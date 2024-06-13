- [This dependency was not found: vxe-table/lib/vxe-table in ./src/main.js_to install it, you can run: npm install --save vxe-CSDN博客](https://blog.csdn.net/LXang723/article/details/132018776)

## 使用教程
## 常见问题

### 问题一：运行依赖报错

#### 报错内容

```shell
This dependency was not found:

* vxe-table/lib/vxe-table in ./src/main.js

To install it, you can run: npm install --save vxe-table/lib/vxe-table
```

#### 原因分析与解决

在使用 vxe-table 时最好是按需加载模块，按照官方教程使用了插件 babel-plugin-imort，babel.config.js 文件配置内容如下：

```javascript
module.exports = {
  presets: [
    '@vue/cli-plugin-babel/preset'
  ],
  plugins: [
    // ["import", { libraryName: "ant-design-vue", libraryDirectory: "es", style: true }],
    ["component", {"libraryName": "view-design", "libraryDirectory": "src/components"}],
    ["import", {"libraryName": "vxe-table", "style": true}]
  ]
}

```

