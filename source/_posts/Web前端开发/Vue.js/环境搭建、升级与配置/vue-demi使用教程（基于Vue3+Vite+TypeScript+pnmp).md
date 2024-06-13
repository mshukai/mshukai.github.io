## 安装使用 pnpm（基于 Node.js v16.20.2）
鉴于笔者电脑上很多老旧项目使用的还是 Node.js v16.x，所以此项目搭建是基于 v16.20.2。pnpm 对于 Node.js 的版本要求较高，针对 Node.js v16.20.2 来说 pnpm 不能使用 v9.x。

```shell
$ npm uninstall -g yarn pnpm
$ corepack prepare pnpm@8.15.7
```

关于 Corepack 的知识可以参考文章：[[../../../Node.js后端开发/Node.js基础与进阶/构建工具篇/Corepack使用教程|Corepack使用教程]]。
## 使用 Vite 初始化项目
具体可以参考 Vite 官方文档：[开始 | Vite 官方中文文档 (vitejs.dev)](https://cn.vitejs.dev/guide/#scaffolding-your-first-vite-project)

初始化默认安装了 Vite 和 Vue 的最新版本（Vue3.4.x+Vite5.x），根绝需要选择是否安装 TypeScript，为了更好地开发效率和严谨度，笔者选择安装 TypeScript，最终 package.json 文件内容如下：

```json
{
  "name": "vue23-components",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "packageManager": "pnpm@8.15.7",
  "scripts": {
    "dev": "vite",
    "build": "vue-tsc && vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "vue": "^3.4.21"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5.0.4",
    "typescript": "^5.2.2",
    "vite": "^5.2.0",
    "vue-tsc": "^2.0.6"
  }
}
```

> [!NOTE] 提示
> 最终依赖项相对于 Vue2 开发环境来说简单得多了，如果你想要基于 Vue2 版本使用 Vite，可以参考文章：
> - [Vite 搭建 Vue2 项目（Vue2 + vue-router + vuex）-CSDN博客](https://blog.csdn.net/weixin_39415598/article/details/119106298)
> - [underfin/vite-plugin-vue2: Vue2 plugin for Vite (github.com)](https://github.com/underfin/vite-plugin-vue2)
> 而你如果想要基于 Vue2 从 vue/cli 升级到 Vite，可以参考文章：
> - [🖖 Vue2.x 改造 ⚡️ Vite - 掘金 (juejin.cn)](https://juejin.cn/post/6999466892373000199)
> - [🖖 Vue2 改造 ⚡️ Vite - 2.0 - 掘金 (juejin.cn)](https://juejin.cn/post/7012880929102233637)

## 常见问题
- [Cannot find name '__dirname' Error in TypeScript [Solved] | bobbyhadz](https://bobbyhadz.com/blog/typescript-cannot-find-name-dirname)

## 参考资料
- [使用 vue-demi 轻松解决 Vue2 和 Vue3 组件兼容性问题 - 掘金 (juejin.cn)](https://juejin.cn/post/7221147640489738297)
- [Build a universal Vue component library with Vue Demi - LogRocket Blog](https://blog.logrocket.com/build-universal-vue-component-library-vue-demi/)
- [基于vue-demi,支持sfc方式的vue2/3通用库开发指南 - 掘金 (juejin.cn)](https://juejin.cn/post/7134628175854141447)