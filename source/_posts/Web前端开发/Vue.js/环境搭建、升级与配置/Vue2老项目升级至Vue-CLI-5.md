## 升级前场景（仅需升级的依赖）

```json
"dependencies": {
    "core-js": "^3.6.5",
    "vue": "^2.6.11",
    "@vue/cli-plugin-babel": "~4.5.0",
    "@vue/cli-plugin-router": "~4.5.0",
    "@vue/cli-plugin-typescript": "^4.5.15",
    "@vue/cli-plugin-vuex": "~4.5.0",
    "@vue/cli-service": "~4.5.0"
}
```

> Vue 的版本只是顺便升级至 2.x 最新版。

## 升级步骤

### 第一步：升级 Vue CLI 及相关官方依赖：

```shell
yarn add @vue/cli
```

执行后 Vue CII 会升级至最新版 5.x，可通过执行 `vue --version` 进行确认。

```shell
vue upgrade
```

执行后控制台会看到一下输出：

```shell
✔  Gathering package information...
  Name                        Installed       Wanted          Latest          Command to upgrade
  @vue/cli-service            4.5.13          4.5.19          5.0.8           vue upgrade @vue/cli-service
  @vue/cli-plugin-babel       4.5.13          4.5.19          5.0.8           vue upgrade @vue/cli-plugin-babel
  @vue/cli-plugin-eslint      4.5.13          4.5.19          5.0.8           vue upgrade @vue/cli-plugin-eslint
  @vue/cli-plugin-router      4.5.13          4.5.19          5.0.8           vue upgrade @vue/cli-plugin-router
  @vue/cli-plugin-typescript  4.5.13          4.5.19          5.0.8           vue upgrade @vue/cli-plugin-typescript
  @vue/cli-plugin-unit-jest   4.5.13          4.5.19          5.0.8           vue upgrade @vue/cli-plugin-unit-jest

<!--输入yes/y-->
? Continue to upgrade these plugins? Yes
```

>升级命令执行结束后同时也会更新 Babel 的配置文件，当然如果没有破坏性更新项的话，其内容是不会变的。

>注意：如果项目中没有使用 eslint 或者 TypeScript，当然就不会安装它们的升级版本，升级命令只会升级当前项目中用到的官方依赖。

### 第二步：常见问题解决
#### 问题一：polyfills 相关报错
```
ERROR in ./node_modules/mime-types/index.js 16:14-37
Module not found: Error: Can't resolve 'path' in 'D:\MuYuan\my-slaughter-logistic-frontend\node_modules\mime-types'

BREAKING CHANGE: webpack < 5 used to include polyfills for node.js core modules by default.
This is no longer the case. Verify if you need this module and configure a polyfill for it.

If you want to include a polyfill, you need to:
        - add a fallback 'resolve.fallback: { "path": require.resolve("path-browserify") }'
        - install 'path-browserify'
If you don't want to include a polyfill, you can use an empty module like this:
        resolve.fallback: { "path": false }
```

报错信息说得很明白，Webpack 5 中默认不再内置 polyfills 相关的 node.js 核心模块，需要通过 resolve.fallback 选项手动引入，前提当然是已经安装了这些依赖。

解决方案：先通过使用一个 Webpack 插件 node-polyfill-webpack-plugin 来安装这些相关 node.js 核心模块，然后修改 vue.config.js 文件中的 Webpack 配置项，新增 resolve.fallback 选项，手动指定构建时需要的 polyfills 模块（根据报错信息添加 ），相关配置内容如下：

```javascript  
const NodePolyfillPlugin = require("node-polyfill-webpack-plugin")
module.exports = {
    configureWebpack: {
        resolve: {
            alias: {
                vue$: "vue/dist/vue.esm.js", //加上这一句
            },
            fallback: {
                "util": require.resolve("util/"),
                "querystring": require.resolve("querystring-es3"),
                "stream": require.resolve("stream-browserify"),
                "zlib": require.resolve("browserify-zlib"),
                "path": require.resolve("path-browserify"),
                "fs": false
            }
        },
        plugins: [  
			new NodePolyfillPlugin()
        ]
    }
}
```

#### 问题二：Webpack 废弃选项报错问题

```shell
ValidationError: Invalid options object. Dev Server has been initialized using an options object that does not match the API schema.
         - options has an unknown property 'disableHostCheck'. These properties are valid:
           object { allowedHosts?, bonjour?, client?, compress?, devMiddleware?, headers?, historyApiFallback?, host?, hot?, http2?, https?, ipc?, liveReload?, magicHtml?, onAfterSetupMiddleware?, onBeforeSetupMiddleware?, onListening?, open?, port?, proxy?, server?, setupExitSignals?, setupMiddlewares?, static?, watchFiles?, webSocketServer? }
```

解决方案：修改 vue.config.js 中的 devServer 选项，改动如下：

```javascript
module.exports = {
    devServer: {
	    // hotOnly: true,	// 删除
    	// disableHostCheck: true,	// 删除
    	historyApiFallback: true,
    	allowedHosts: "all",
    }
}
```

参考来源：[Vue.config.js 配置报错 ValidationError: Invalid options object._validationerror: invalid options object. dev serve-CSDN博客](https://blog.csdn.net/c327127960/article/details/128799614)

#### 问题三：core-js 相关报错

```
Cannot find module ‘core-js/modules/xxx.js
```

解决方案：尝试升级 core-js 至最新版即可。

#### 问题四：报错内容如下

```
[ error ] ./node_modules/destroy/index.js
Module not found: Can't resolve 'fs' in '**/node_modules/destroy'
```

这个报错的原因是：浏览器中无法使用 node.js 的核心模块 fs，可以通过 resolve.fallback 选项中新增 `"fs": false` 指定为空模块，<mark>新增配置已经在问题一的解决方案中体现。</mark>

#### 问题五：TypeScript 类型错误
```shell
Vue: CheckboxGroup only refers to a type, but is being used as a value here.
```

此问题报错位置是在笔者的项目入口文件 main.ts 中：笔者使用了 vxe-table 的 v3.7.5 版本，按需引入了 CheckboxGroup 组件使用，在 Vue.use(CheckboxGroup) 表达式中报告出了此类错误。

解决方案：tsconfig.js 文件中的 target 选项修改为 "es6" 降低转义输出的 EcmaScript 版本。<mark>笔者在最后又发现这个问题又消失不见了，所以可能是其他原因导致的这个问题，如果临时遇见了，可以先通过此方法解决。</mark>

#### 问题六：通用解决办法

有时候按照已有解决方案安装依赖后，问题仍然存在，这时候可以尝试删除 node_modules 目录，问题即可消失。

#### 问题七：Vue 运行时报错占满屏
![[attachments/Pasted image 20240510120715.png]]

这是升级之后 Webpack 5 默认配置导致的，解决办法可参考文章：[vue-cli 关闭 Uncaught error 的全屏提示_vue报错如何不显示在屏幕上-CSDN博客](https://blog.csdn.net/qq_33733799/article/details/130681501)，新增关键配置如下：
```JavaScript
module.exports = {
    devServer: {
	    client: {
			overlay: false    
		}
    }
}
```
## 写在最后
---
除了 package.json 中核心依赖的版本发生变化，vue.config.js 也有很多变化，这些变化在常见问题解决的过程中已经体现。
## 参考资料
---
- [vue-cli V4 升级到 V5 - 掘金 (juejin.cn)](https://juejin.cn/post/7239523196976939063)
- [ts问题处理(2): 'Promise' only refers to a type, but is being used as a value here. - 唐安 - 博客园 (cnblogs.com)](https://www.cnblogs.com/andy-lehhaxm/p/10540482.html)