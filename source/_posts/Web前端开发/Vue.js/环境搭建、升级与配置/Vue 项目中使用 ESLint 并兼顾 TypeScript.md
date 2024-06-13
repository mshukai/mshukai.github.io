## 通过这篇文章你能学到什么
- ESLint 核心概念：规则、共享配置、插件、解析器
- Vue 项目中如何使用 ESLint，以及 eslint-plugin-vue 插件的原理
- 基于Vue CLI + TypeScript 的项目如何使用 ESLint，以及 @vue/typescript-eslint 插件的原理

>这篇文章假设 Vue 的运行环境基于 Vue CLI 4.5 以上，ESLint 配置文件以 js 文件（.eslintrc.js）的形式进行配置，版本不高于 9.0。

## Vue 项目中使用 ESlint

Vue 官方提供了一个 eslint 插件 [eslint-plugin-vue](https://eslint.vuejs.org/user-guide/)，看起来只是在配置项 extends 中新增了 eslint:recommended 和 plugin:vue/vue3-xxx（如下所示）就可以直接使用了，其实每一项都对应着某一个 ESLint 共享配置或插件下面的某一项共享配置（故以 plugin: 打头），也就是说共享配置可以被自定义插件包含，也可以独立引用，当然 ESLint 内置配置肯定要引入 eslint 依赖，而且以 plugin: 打头的配置必须要先引入该插件以及该插件下面的（以 npm 包的形式）。<font color="red">关于 ESLint 中的核心概念：[配置](https://eslint.nodejs.cn/docs/latest/use/core-concepts#可共享的配置)和[插件](https://eslint.nodejs.cn/docs/latest/use/core-concepts#插件)也可参考[这篇文章](https://blog.csdn.net/letterTiger/article/details/113748741)。</font>

```javascript
module.exports = {
    extends: [
        "eslint:recommended",
    	"plugin:vue/vue3-essential"
    ],
    rules: {}
## }
```

对于插件 eslint-plugin-vue，通过引入共享配置 plugin:vue/vue3-essential（插件源码 configs 目录下的一个文件而已），ESLint 核心配置项 parser 会被设置成为 [vue-eslint-parser](https://github.com/vuejs/vue-eslint-parser#readme) 用于解析 vue SFC，当然还要依赖 vue 框架本身（同样作为插件引入），而不用自己亲自配置。下面展示了 eslint-plugin-vue 源码中的 lib/configs/base.js 文件内容：

```javascript
// node_modules/eslint-plugin-vue/lib/configs/base.js
module.exports = {
  parser: require.resolve('vue-eslint-parser'),
  parserOptions: {
    ecmaVersion: 2020,
    sourceType: 'module'
  },
  env: {
    browser: true,
    es6: true
  },
  plugins: ['vue'],
  rules: {
    'vue/comment-directive': 'error',
    'vue/experimental-script-setup-vars': 'error',
    'vue/jsx-uses-vars': 'error'
  }
}
```

对于配置文件中的 rules 选项，并不是让我们去定义，而是让我们去覆盖 extends 中引入的共享配置 eslint:recommended 和 plugin:vue/vue3-essential 中所有设定好的规则（[Rules](https://eslint.nodejs.cn/docs/latest/use/core-concepts#%E8%A7%84%E5%88%99)）。

>  使用 Vue 框架引入 ESLint 使用起来很简单，我们当然也要知道其中的 ESLint 知识，如果哪天脱离了框架需要自己配置 ESLint 时就不会手忙脚乱了。当然笔者也是通过参考网络文章、查看 ESLint 官网等，特别是查看了 eslint-plugin-vue 插件源码之后才懂得。<font color="red">所以说开源的项目能看就看，免费看还涨知识，何乐而不为？！</font>

关于没有使用 TypeScript 的项目中 package.json 文件新增 ESLint 相关依赖如下所示：

```json
{
    "devDependencies": {
        "@vue/cli-plugin-eslint": "~4.5.0",
        "eslint": "^6.7.2",
        "eslint-plugin-vue": "^7.0.0",
    }
}
```

> ESLint 版本不要升级到 v9+，此版本改动过大，后期有时间笔者会尝试升级配置。

## ESLint 解析器 parser

上面讲述 Vue3 如何引入 ESLint 用于解析 vue SFC 时，eslint-plugin-vue 插件其实有一个关键的配置项，那就是[解析器 parser](https://eslint.nodejs.cn/docs/latest/use/core-concepts#解析器)。

ESLint 内置解析器定义了一系列的规则，默认对齐的是 JavaScript 标准，是没办法解析 Vue SFC 这种独特的语法从而进行错误提示，所以这时候就需要引入自定义 parser 来覆盖默认的解析器，从能实现 vue SFC 语法错误提示。这时候就和 ESLint 默认提供的规则一样，自定义 parser 的内部也会定义一系列规则作用于 vue SFC，从而实现 ESLint 的规则扩展（自定义解析器  parser 一般都是最大程度兼容 ESLint 内置规则）。

## 如何让 ESLint 兼顾 TypeScript

Vue 项目中如果使用了 TypeScript，就和 ESLint 不识别 vue SFC 的语法一样，也是需要一个新的解析器来解析 ts/tsx 这类文件的语法，可是上面在 eslint-plugin-vue 插件中的配置已经覆盖了 ESLint 的内置解析器，难道还能配置第二个解析器不成？答案是的确是能配置第二个解析器，那就是 [parserOptions.parser 选项](https://github.com/vuejs/vue-eslint-parser#readme)！

<font color="red">该选项允许指定第二个解析器用于解析 script 标签下面的 ts 代码（如果没有使用 TypeScript，只用 eslint-plugin-vue 插件就可以进行解析和 vue SFC 错误语法提示），而这个解析器就是 [@typescript-eslint/parser](https://typescript-eslint.io/packages/parser)，新的解析器自然就对应着一系列新的规则，和解析 vue SFC 语法只需要引用一个插件一样（插件依赖也是需要安装的），也有一个专门的插件 [@typescript-eslint/eslint-plugin](https://typescript-eslint.io/packages/eslint-plugin) 用于解析 ts 文件，该插件也提供了一系列的共享配置和规则，然后被别的共享配置或插件引用，对于 Vue 项目来说就有一个官方共享配置： @vue/eslint-config-typescript，然后同样在 extends 中新增该共享配置即可。</font>

```javascript
module.exports = {
    extends: [
        "eslint:recommended",
    	"plugin:vue/vue3-essential",
        "@vue/typescript/recommended"
    ],
    rules: {}
}
```

最终在基于 Vue CLI v4.5+ 的项目中使用 ESLint + TypeScript 的话，需要 package.json 文件新增如下依赖：

```json
{
    "devDependencies": {
        "@typescript-eslint/eslint-plugin": "^4.5.0",
		"@typescript-eslint/parser": "^4.5.0",
    	"@vue/cli-plugin-typescript": "~4.5.0",
	    "@vue/eslint-config-typescript": "^5.0.0",
        "eslint": "^6.7.2",
        "eslint-plugin-vue": "^7.0.0",
    }
}
```

> 如果是基于 Vue CLI v5.0+ 的话，@vue/cli 相关的依赖，也包括 @vue/cli-plugin-typescript 都需要升级到 ~5.0.8，包括 typescript-eslint 相关的两个依赖插件都需要升级到 ^5.0.0（@vue/eslint-config-typescript 维持在 ^5.0.0 就可以），否则会出现兼容性问题（见下文）。

## 常见问题

### 问题一：因为版本不兼容报错，导致 ESLint 对 ts 文件检测无效

<font color="red">当项目升级到 Vue CLI v5.0+ 时 typescript-eslint 相关插件也需要升级到 ^5.0.0，否则会报兼容性错误而导致 ESLint 对 ts 文件检测无效！</font>

<font color="red">有人遇见过（包括我自己）@typescript-eslint 插件无论如何也无法消除 vue SFC 的 script 标签中定义的事件函数名提示“未使用的变量”的错误（非事件方法未报错），这时候也可以尝试升级**这两个插件**到更高版本进行解决！</font>

### 问题二：'defineProps' is not defined.eslint（no-undef）

在配置文件中添加 globals 选项进行全局声明即可：

```javascript
globals: {
    defineProps: "readonly",
    defineEmits: "readonly",
    defineExpose: "readonly",
    withDefaults: "readonly",
},
```

### 问题三：vue 文件中通过

### 路径别名引入模块时提示 Cannot find module

一切就绪以后，终于可以在 Vue 项目中使用 TypeScript 了，没想到在 Vue 组件中通过路径别名引入组件或其它模块时总是提示 Connot find module "@/xxx/xxx.vue" 一类的错误，在 tsconfig.json 文件中我也配置了 baseUrl 和compilerOptions.paths 选项，排查到最后发现 include 选项中没有囊括 vue 类型文件……加上去就好了（其实不算是问题）。

### 问题四：vue.config.js 中 require() 方法调用提示错误

```
ESLint: Require statement not part of import statement.(@typescript-eslint/no-var-requires)
```

typescript-eslint

### require 提示错误问题……

<font color="red">未完待续……</font>

## 其它参考资源

- [ESLint 的 parser 是个什么东西 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/295291463)
- [Vue.js ESLint配置中的”parser”和”parserOptions.parser”的区别是什么|极客教程 (geek-docs.com)](https://geek-docs.com/vuejs/vue-js-questions/441_vuejs_what_the_difference_between_parser_and_parseroptionsparser_in_eslint_config.html)
- [Vue + TypeScript 项目放弃 TSLint，拥抱 ESLint - 掘金 (juejin.cn)](https://juejin.cn/post/6844904074534453261)
- [eslint报错Parsing error: "parserOptions.project" has been set for @typescript-eslint/parser. The fi... - 简书 (jianshu.com)](https://www.jianshu.com/p/f95d54ec6994)
- [Eslint配置（vue3+ts项目） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/552925831)
- [解决：使用 Vue 3 Script Setup 时 ESLint 报错 ‘defineProps‘ is not defined_defineprops' is not defined-CSDN博客](https://blog.csdn.net/m0_54850604/article/details/123398753)

