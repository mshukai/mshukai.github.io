Node.js 16.9+ 版本中默认包含了一个实验性工具：[Corepack 核心包 | Node.js v16 文档 (nodejs.cn)](https://nodejs.cn/api/v16/corepack.html)，类似于 nvm 用于管理 Node.js 版本一样，该工具用于管理依赖管理工具的选择及版本。下面是一些常用命令（对应版本 Node.js v16.x），更多使用教程可以参考文章：[Node.js Corepack - 掘金 (juejin.cn)](https://juejin.cn/post/7111998050184200199)。

```shell
# 启用/禁用 Corepack
$ corepack enable
$ corepack disable
# 使用 pnpm 并指定版本（会下载对应版本）
$ corepack prepare pnpm@8.15.7 --activate
```

如果想要限制项目中只能使用哪一种构建工具，可以在 package.json 文件中添加 packageManager 字段，指定构建工具及其版本，之后如果使用的构建工具不是该字段指定的就会进行提示而阻止操作：

```json
{
	"packageManager": "pnpm@8.15.7"
}
```

> [!NOTE] 注意事项
> 如果启用 Corepack，需要现将之前自行安装的 Yarn 和 pnpm 卸载。另外，Corepack 是随着 Node.js 一起发布的，使用方法可能随着 Node.js 版本的升级发生变化，比如在高版本 Node.js 18+ 之后 `corepack prepare` 命令就被替换成为 `corepack use`。

## 参考资料
- [nodejs/corepack: Zero-runtime-dependency package acting as bridge between Node projects and their package managers (github.com)](https://github.com/nodejs/corepack)
- [Corepack 核心包 | Node.js v16 文档 (nodejs.cn)](https://nodejs.cn/api/v16/corepack.html)
- [Node.js Corepack - 掘金 (juejin.cn)](https://juejin.cn/post/7111998050184200199)