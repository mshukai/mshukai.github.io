# 【案例说知识】事件循环

JavaScript 事件循环涉及程序异步执行逻辑，为了模拟程序阻塞执行过程，可以封装以下方法：

```javascript
// 模拟任务同步执行过程
function simulationExec(task, during = 1) {
    let then = Date.now()
    const s = document.createElement('p')
    s.textContent = `[${task}] 任务处理开始`
    document.body.appendChild(s)
    while (true) {
        // 使用 Performance API 能精确到微秒，以浮点值返回（单位仍是 ms）
        if (performance.now() + performance.timeOrigin - then >= during) {
            const e = document.createElement('p')
            e.textContent = `[${task}] 任务处理完成，历时 ${(performance.now() + performance.timeOrigin - then).toFixed(3)}ms`
            document.body.appendChild(e)
            break
        }
    }
}
```



### 案例一：同时含有宏任务与微任务的代码执行顺序

- 代码清单

```javascript
<body>
    <button id="firstButton">按钮一</button>
    <button id="secondButton">按钮二</button>
    <script>

        const firstButton = document.querySelector('#firstButton')
        const secondButton = document.querySelector('#secondButton')
        firstButton.addEventListener('click', function () {
            Promise.resolve().then(() => {
                simulationExec('按钮一点击回调中 Promise', 4)
            })
            simulationExec('按钮一点击回调', 8)
        })
        secondButton.addEventListener('click', function () {
            simulationExec('按钮二点击回调', 5)
        })
        simulationExec('全局代码执行', 15)
        setTimeout(() => firstButton.click(), 5)
        setTimeout(() => secondButton.click(), 12)
    </script>
</body>
```

- 程序执行结果

```
[全局代码执行] 任务处理开始
[全局代码执行] 任务处理完成，历时 15.000ms
[按钮一点击回调] 任务处理开始
[按钮一点击回调] 任务处理完成，历时 7.900ms
[按钮一点击回调中 Promise] 任务处理开始
[按钮一点击回调中 Promise] 任务处理完成，历时 4.000ms
[按钮二点击回调] 任务处理开始
[按钮二点击回调] 任务处理完成，历时 5.000ms
```

- 执行原理分析

按照事件的触发顺序，应该先执行按钮二的单击事件才算公平，但是实际上先执行了“按钮一点击回调中 Promise任务”，==这是因为执行完一个宏任务以后会优先检查微任务队列并全部执行，而后再执行下一个宏任务，而不是按照任务添加顺序来执行的！==另外也可以从执行结果中发现无论宏任务还是微任务，包括全局代码一旦开始执行，不会被其它任务中断，直至完成，然后按照事件循环机制执行下一个任务。

- 问题思考

1. 本案例中为什么不能使用 `setTimeout()` 模拟任务执行过程，结果会怎样？
2. 点击事件触发时机为什么可以通过 `setTimeout()` 来模拟？像下面这样：

```javascript
setTimeout(() => console.log(`任务处理完成，历时 10ms`), 10)
```

> 更多案例分析详情可参考书籍《JavaScript忍着秘籍》第2版第 13.1.2 章节，不喜欢看书的欢迎评论区留言。

### 案例二：同时含有延时计时器和间隔计时器的代码执行顺序

- 代码清单

```html
<body>
    <button id="firstButton">按钮一</button>
    <button id="secondButton">按钮二</button>
    <script>
        setTimeout(function () {
            simulationExec('延迟 10ms 执行', 6)
        }, 10)

        const interval = setInterval(function () {
            simulationExec('间隔 10ms 执行', 8)
        }, 10)
        // 100ms 后中断计时器
        setTimeout(() => clearInterval(interval), 100);

        const myButton = document.querySelector("#myButton");

        myButton.addEventListener("click", function () {
            simulationExec('按钮点击回调', 10)
        });

        simulationExec('全局代码执行', 18)

        setTimeout(() => myButton.click(), 6)
    </script>
</body>
```

- 执行原理分析

