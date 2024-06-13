## 第一步：下载安装

`nvm-windows` 下载地址：[NVM for Windows](https://github.com/coreybutler/nvm-windows)、https://sourceforge.net/projects/nvm-for-windows.mirror/（安装过程略）。

## 第二步：修改镜像地址

```shell
$ nvm node_mirror https://npm.taobao.org/mirrors/node/
$ nvm npm_mirror https://registry.npmmirror.com	# 旧地址：https:/npm.taobao.org/mirrors/npm/
```

> 镜像地址配置结果可以通过 `nvm` 安装目录下的 `settings.txt` 文件进行查看。

## 第三步：查看并安装/卸载 `Node.js`

- 查看远程可安装版本

```shell
$ nvm ls available
```

- 安装/卸载 `Node.js` 指定版本

```shell
$ nvm install <node_version>
$ nvm uninstall <node_version> # 卸载
```

- 查看本地可使用版本

```shell
$ nvm ls
```

## 第四步：切换、使用 `Node.js` 版本

```shell
$ nvm use <node_version>
```

> 切换 Node.js 版本的执行命令可能需要管理员权限。<mark>另外 nvm 列出的远程可安装版本比较新，如果需要安装较低版本，可以到 https://nodejs.org/en/download/releases/ 网站进行自行下载，然后进行解压手动放入 nvm 安装目录（版本号作为子目录名程）即可作为本地安装版本进行切换使用。</mark>

## 第五步：验证安装、切换结果

```shell
$ node -v && npm -v
```

> 安装使用不同的 `Node.js` 版本，`npm` 版本会自动跟随切换。

## 参考资料

[nvm文档手册 - nvm是一个nodejs版本管理工具 - nvm中文网 (uihtm.com)](https://nvm.uihtm.com/)