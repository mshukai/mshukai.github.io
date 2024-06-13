# URL 与 URL API

##### 【参考资料】

1. [URL - Web API 接口参考 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/API/URL)
2. [URL.createObjectURL() - Web API 接口参考 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/createObjectURL_static)
3. 书籍《红宝书（第4版）》第 20.4.5 章节





### 应用案例一：为相对路径文件生成绝对路径

```
new URL('src/some-file.js', import.meta.url)
```

> `import.meta.url` 仅在现代浏览器中支持，返回 ESM 的 URL。

### 应用案例二：使用 URL.createObjectURL() 

## 更多参考资料

- [URL - Web API 接口参考 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/API/URL)
- [URL.createObjectURL() - Web API 接口参考 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/createObjectURL_static)

