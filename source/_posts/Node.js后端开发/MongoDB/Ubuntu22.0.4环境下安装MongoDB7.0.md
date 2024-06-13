Ubuntu 中安装软件时，如果软件库中找不到就需要自己进行添加到软件库中再进行安装。MongoDB 就是如此，所以会有以下步骤：

- 第一步：导入 MongoDB 的 GPG 公钥

```shell
$ curl -fsSL https://pgp.mongodb.com/server-7.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
   --dearmor
```

- 第二步：创建 MongoDB list file

```shell
$ echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
```

- 第三步：更新软件库

```shell
$ sudo apt-get update
```

- 第四步：执行安装

```shell
$ sudo apt-get install mongodb-org
```

安装结果可能会失败，失败信息如下：

```shell
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 mongodb-org-mongos : Depends: libssl1.1 (>= 1.1.1) but it is not installable
 mongodb-org-server : Depends: libssl1.1 (>= 1.1.1) but it is not installable
E: Unable to correct problems, you have held broken packages.
```

<font color="red">根据信息提示，很明显是因为 MongoDB 服务需要 lissl1.1 以上版本的支持，而系统并未满足，所以还需要安装 libssl1.1 库：</font>

```shell
$ echo "deb http://security.ubuntu.com/ubuntu focal-security main" | sudo tee /etc/apt/sources.lis
t.d/focal-security.list
$ sudo apt-get update
$ sudo apt-get install lib-ssl1.1
```

libssl1.1 库安装成功以后再执行 mongodb-org 的安装就没有问题了。最后可通过一下命令查看是否安装成功：

```shell
$ mongod --version
```

