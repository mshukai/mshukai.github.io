# 微信小程序中使用 Windi CSS

### 使用 Windi CSS



### 命令行（CLI）执行监听

```shell
windicss **/*.wxml -o windi.wxss -d -f windi.config.js
```

> <font color="red">注意：上述命令中的选项及值都不能缺，顺序也不能乱！</font>

### 问题记录（模板中使用）

- 如何使用负值，如 -left-20
- 如何使用动态值，如 h-[20px]
- 如何使用百分比
- 如何使用 important 声明类
- 如何使用 tree-shaking，去除无用代码
- 如何去掉浏览器兼容性代码并压缩代码，减少代码体积