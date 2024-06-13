我是在接触 [vueuse/vue-demi](https://github.com/vueuse/vue-demi) 这个工具库的时候才认识到 peerDependencies 这个属性的作用。

## peerDependencies 属性的作用
---
该属性的作用简短描述为：

> 开发的 package（一般是工具包）如果同样依赖宿主环境中的某些核心依赖（比如：开发的某个 React UI 库肯定是基于 React 环境并同样依赖 react-dom 这个核心库）就可以通过在 peerDependencies 属性中声明这些核心依赖的版本要求。

就拿下面 vue-demi  的配置来说，由于该工具包的工作同样依赖 Vue 环境的核心依赖 vue（如果 vue 版本低于 2.7，同样依赖 @vue/composition-api 这个核心库来实现 Composition API）且要求 vue 的版本不能低于 2.0（最终结果来看），否则 vue-demi 就无法使用。

```json
{
  "dependencies": {
    "vue-demi": "latest"
  },
  "peerDependencies": {
    "@vue/composition-api": "^1.0.0-rc.1",
    "vue": "^2.0.0 || >=3.0.0"
  },
  "peerDependenciesMeta": {
    "@vue/composition-api": {
      "optional": true
    }
  },
  "devDependencies": {
    "vue": "^3.0.0" // or "^2.6.0" base on your preferred working environment
  },
}
```

很多网友将这个属性中声明的依赖称为**对等依赖**，我觉得根据其作用描述称为**同等依赖**更容易让人理解。
## 关于 peerDependenciesMeta 属性
---
peerDependenciesMeta 属性，顾名思义是对 package 中声明的同等依赖的补充说明，具体就是它允许对其中声明的依赖标记为可选，就像上面关于 vue-demi 的案例中那样。<mark>在最新版的 npm（v7+）中恢复了对 package.json 文件中声明的同等依赖的自动安装，如果标记为可选则不会自动安装也不会报错，但用户需要根据实际情况自行安装！</mark>

关于该属性定义可参考：[peerDependenciesMeta - npm 中文文档 (nodejs.cn)](https://nodejs.cn/npm/cli/v7/configuring-npm/package-json/~/peerdependenciesmeta/)
## 写在最后
---
更多关于 peerDependencies 和 peerDependenciesMeta 属性的案例可以参考以下文章：

1. [一文搞懂peerDependencies - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/562343488)
2. [将 Vue 插件升级到同时支持 Vue2 和 3 的实践小结 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/476861141)
3. [前端 - dependencies 和 devDependencies 和 peerDependencies - 个人文章 - SegmentFault 思否](https://segmentfault.com/a/1190000041855828)