# 在 Vue2 项目中使用 Composition API

Composition API 的作用和优势就不必多说了，下面先说下升级前的场景：

- 老项目基于 Vue CLI 4.x
- Vue 版本 ^2.6.11

## 升级前准备

如果 Vue 的版本低于 2.7，需要手动引入组合式 API 的官方依赖 @vue/composition-api，当 Vue 版本为 2.7.x 时官方将该依赖内置为框架内部的 API，这时候无需做任何改动即可使用。如果不想升级 Vue 至 2.7.x 那就手动引入这个依赖即可，相关教程网上有很多，包括 @vue/composition-api 是怎么使用的，可以下面列出的这些参考来源：

- [在Vue2项目上怎么使用CompositionAPI ？它们之间到底能擦出怎样的火花？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/387632378)
- [@vue/composition-api 上手指南 - 掘金 (juejin.cn)](https://juejin.cn/post/6850418114111537159)
- [Vue 3.0--在Vue2.0中使用composition-api - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/382378466)

