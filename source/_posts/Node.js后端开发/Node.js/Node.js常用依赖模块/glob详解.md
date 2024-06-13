- [前端工程化之强大的glob语法 - 掘金 (juejin.cn)](https://juejin.cn/post/6876363718578405384)

glob 的作用类似于正则表达式，但是主要针对文件路径的匹配，当然包括文件后缀名。具体的语法可以参考上述【参考资料】，下面通过实用的案例进行记录学习。

### 其它

在尤大大创建的构建工具 Vite 中对 `import.meta` 这个特殊的对象进行了扩展，添加了 glob() 方法，以支持批量导入模块，更多信息可以参考：

- [功能 | Vite 官方中文文档 (vitejs.dev)](https://cn.vitejs.dev/guide/features.html#glob-import-as)；
- [从 v2 迁移 | Vite 官方中文文档 (vitejs.dev)](https://cn.vitejs.dev/guide/migration-from-v2.html#importmetaglob)；