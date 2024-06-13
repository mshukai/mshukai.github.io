## 代码风格检查项

| 项目                   | Prettier 约束项 | 期望    |
| -------------------- | ------------ | ----- |
| 代码强制换行宽度             |              | 120   |
| 语句末尾是否使用分号           |              | 无分号   |
| 字符串使用单引号 or 双引号      |              | 单引号   |
| 句尾逗号                 |              | 有句尾逗号 |
| 花括弧两边空格              |              | 有空格   |
| 对象解构两边空格             |              | 有空格   |
| HTML 换行对齐方式          |              | 属性对齐  |
| JavaScript 何时换行、对齐方式 |              | 缩进对齐  |
| 匿名函数 function 关键字后空格 |              | 无空格   |
| 空的 [] 和 {} 边界强制换行    |              | 不换行   |
| 索引使用空格 or Tab        |              | Tab   |
|                      |              |       |
|                      |              |       |
|                      |              |       |

## ESLint 引入与配置



## Prettier 引入与配置



### 常见问题与解决方案

- 问题一：

```shell
error  in ./src/views/turnoverBasket/statisticsReport.vue?vue&type=template&id=fc8616b6&scoped=true&

Syntax Error: D:\MuYuan\my-slaughter-logistic-frontend\src\views\turnoverBasket\statisticsReport.vue: Unexpected token, expected "," (1:8)

> 1 | [object Promise]
    |         ^
  2 | export { render, staticRenderFns }

```

解决方案一：降低 prettier 版本 2.8.8 以下；

解决方案二：vue-loader 配置中关闭 prettify 选项。

参考来源：[报错SyntaxError: /xxxx.vue: Unexpected token, expected “,“，[object Promise\] - 掘金 (juejin.cn)](https://juejin.cn/post/7268554640938287104)
