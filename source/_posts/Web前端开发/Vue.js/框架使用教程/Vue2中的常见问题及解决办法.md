## 表格组件数据更新，UI 不更新问题

给表格添加 key 属性，遇见此问题时更新 key 的值即可解决，比 `$forceUpdate()` 好用。