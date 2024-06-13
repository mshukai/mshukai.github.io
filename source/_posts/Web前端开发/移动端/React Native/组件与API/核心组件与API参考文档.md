## [View 组件](https://reactnative.cn/docs/view)



## [Text 组件](https://reactnative.cn/docs/text)

### 常用组件属性

| 属性 | 描述 | 属性 | 描述 |
| ---- | ---- | ---- | ---- |
|      |      |      |      |
|      |      |      |      |

### 组件专属样式



### 注意事项

- Text 组件可嵌套使用

- 可设置宽高，类似于块级元素，但不能使用 margin 和 padding

## [Image 组件](https://reactnative.cn/docs/image)

### 常用组件属性

| 属性       | 描述                       | 属性          | 描述        |
| ---------- | -------------------------- | ------------- | ----------- |
| source     | 本地图片/{ uri: 远程图片 } | defaultSource | 值同 source |
| blurRadius | 一个数值，指定图片模糊度   | fadeDuration  |             |

### 常用组件事件

| 事件                                                         | 描述              | 事件                                                     | 描述               |
| ------------------------------------------------------------ | ----------------- | -------------------------------------------------------- | ------------------ |
| [onLoad](https://reactnative.cn/docs/image#onload)           | event.nativeEvent | [onError](https://reactnative.cn/docs/image#onerror)     | 加载失败时调用     |
| [onLoadStart](https://reactnative.cn/docs/image#onloadstart) | 开始加载时调用    | [onLoadEnd](https://reactnative.cn/docs/image#onloadend) | 仅在加载成功时调用 |

### 组件专属样式

| 属性       | 描述                                | 属性      | 描述                 |
| ---------- | ----------------------------------- | --------- | -------------------- |
| resizeMode | contain/center/cover/repeat/stretch | tintColor | png 图片染色（实用） |

### 常用组件事件

| 事件                                                         | 描述              | 事件                                                     | 描述               |
| ------------------------------------------------------------ | ----------------- | -------------------------------------------------------- | ------------------ |
| [onLoad](https://reactnative.cn/docs/image#onload)           | event.nativeEvent | [onError](https://reactnative.cn/docs/image#onerror)     | 加载失败时调用     |
| [onLoadStart](https://reactnative.cn/docs/image#onloadstart) | 开始加载时调用    | [onLoadEnd](https://reactnative.cn/docs/image#onloadend) | 仅在加载成功时调用 |

### 组件 API

| API                                                          | 描述 | API                                                          | 描述                             |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------------------------------- |
| [ImageRef.getSize()](https://reactnative.cn/docs/image#getsize) |      | [ImageRef.prefetch()](https://reactnative.cn/docs/image#prefetch) | 预加载图片到本地磁盘（性能优化） |

### 注意事项

- <mark>resizeMode 属性既可以作为常用组件属性使用，也可以作为组件专属样式使用</mark>

## [ImageBackground 组件](https://reactnative.cn/docs/imagebackground)（=View+Image）

### 常用组件属性

| 属性       | 描述           | 属性   | 描述          |
| ---------- | -------------- | ------ | ------------- |
| imageStyle | 设置图片样式   | source | 同 Image 组件 |
| imageRef   | Image 组件引用 |        |               |

### 组件专属样式

<mark>该组件的样式由 View 和 Image 两个组件分别控制，具体体现在组件的 style 属性和 imageStyle 属性上。</mark>

### 注意事项

该组件中的 Image 组件作为背景使用，其 resizeMode 组件专属样式一般选择 cover 进行不变形全覆盖。

## TextInput 组件

#### 常用组件属性

| 属性         | 描述                                                   | 属性          | 描述                                             |
| ------------ | ------------------------------------------------------ | ------------- | ------------------------------------------------ |
| autoFocus    | 会否自动聚焦，表现为键盘自动弹出                       | blurOnSubmit  | 点击键盘中的提交是否隐藏键盘                     |
| defaultValue | 默认内容                                               | editabls      | 是否可编辑                                       |
| keyboardType | number-pad/decimal-pad/numeric/email-address/phone-pad | returnKeyType | 表明输入框的的操作类型：done/go/next/search/send |
| maxLength    |                                                        | multiline     | 是否允许多行                                     |

## 组件公共属性

| 属性  | 描述         | 属性 | 描述     |
| ----- | ------------ | ---- | -------- |
| style | 组件样式控制 | ref  | 组件引用 |

