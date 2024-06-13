Window系统安装 MongoDB 7.0，也是一路波折，安装过程中就会遇见类似以下错误：

![img](https://img-blog.csdnimg.cn/a1ef00b16792498c979ec7efee21e86c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56eL6Zuo6ZuB5Y2X6aOe,size_13,color_FFFFFF,t_70,g_se,x_16)

有时候会提供 ignore 选项，先略过，安装完成后再手动安装并启动服务即可（如果想要自定义各类配置文件路径请参考网络博客）：

```shell
$ mongod --install --serviceName "MongoDB"
$ net start mongod
```

在启动服务时可能会报错内部错误码 100，这时候删除 data/db 目录重新创建，给予读写权限就好了。

有时候（Window 11 中安装 MongoDB7.0）执行完服务安装命令之后，启动服务时仍然提示：服务名无效。这时候可以尝试指定配置文件进行安装服务：

```shell
mongod --config "C:\Program Files\MongoDB\Server\7.0\bin\mongod.cfg" --install
```

除了指定配置文件，有时候想要修改数据及日志的存放位置，也可以通过 --dbpath 和 --logpath 选项指定到某个文件路径（略）。

新版 MongoDB 安装以后没有自带 shell 工具 mongosh，可以在[这里](https://www.mongodb.com/try/download/shell)下载进行安装即可。

> 要全局执行 mongod 命令当然先要设置环境变量，另外，mongosh 工具使用是通过 mongosh 命令进入的。

> 上面安装过程中出现的问题是在 Window 10 上出现的，Window 11 上安装 MongoDB7.0 没有出现问题，且服务自动启动。

```javascript
console.log('hello Obsidian')
```