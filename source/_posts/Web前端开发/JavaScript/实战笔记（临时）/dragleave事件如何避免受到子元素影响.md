# dragleave事件如何避免受到子元素影响

##### 【参考资料】

1. [拖拽过程触碰到子元素会触发dragleave事件_vue drag 子元素冒泡连续触发dragenter问题_-老頭子-的博客-CSDN博客](https://blog.csdn.net/weixin_45380966/article/details/127447108#:~:text=有两种办法： 1.粗暴版：当你的子元素没有hover、active或者点击事件这些情况 (就是无需对子元素进行操作的情况)的时候.content *{ pointer-events%3A none%3B,} 1 2 3 直接加样式穿透就可以了 (如果对子元素有操作的话，加了这个属性就无法触发了))

---

