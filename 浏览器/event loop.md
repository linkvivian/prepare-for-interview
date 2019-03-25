# 规范
- 从 task 队列（一个或多个）中选出最老的一个 task，执行它。
- 执行 microtask 检查点。简单说，会执行 microtask 队列中的所有 microtask，直到队列为空。如果 microtask 中又添加了新的 microtask，直接放进本队列末尾。
- 执行 UI render 操作
- 判断 document 在此时间点渲染是否会『获益』。浏览器只需保证 60Hz 的刷新率即可（在机器负荷重时还会降低刷新率），若 eventloop 频率过高，即使渲染了浏览器也无法及时展示。所以并不是每轮 eventloop 都会执行 UI Render。
- 执行各种渲染所需工作，如 触发 resize、scroll 事件、建立媒体查询、运行 CSS 动画等等
- 执行 animation frame callbacks
- 执行 IntersectionObserver callback
- 渲染 UI

# task
## 定义
一个 eventloop 有一或多个 task 队列。每个 task 由一个确定的 task 源提供。从不同 task 源而来的 task 可能会放到不同的 task 队列中。例如，浏览器可能单独为鼠标键盘事件维护一个 task 队列，所有其他 task 都放到另一个 task 队列。通过区分 task 队列的优先级，使高优先级的 task 优先执行，保证更好的交互体验。
## 源
- 事件回调
- XHR 回调
- IndexDB 数据库操作等 I/O
- setTimeout / setInterval
- history.back

# microtask
## 定义
每一个 eventloop 都有一个 microtask 队列。microtask 会排在 microtask 队列而非 task 队列中。
## 源
- Promise.then
Promise 规范中提及 Promise.then 的具体实现由平台把握，可以是 microtask 或 task。当前的共识是使用 microtask 实现。

- MutationObserver
- Object.observe

```
//步骤1： 开始执行首个 eventloop 的 task 阶段
console.log('A') // 步骤2：**输出 A**
setTimeout(() => {  // 步骤3：立刻将 callback（B） 放入 task 队列中
  console.log('B')
}, 0)
Promise.resolve().then(() => {  // 步骤4：立刻将 callback（C） 放入 microtask 队列中
  console.log('C')
}).then(() => {
  console.log('D')
})
console.log('E') // 步骤5：**输出 E**
// 步骤6：首个 eventloop 的 task 阶段执行完毕，开始执行 microtask，发现有一个 callback（C），执行之，**输出 C**，同时又将 callback（D）放入 microtask 队列中
// 步骤7：发现 microtask 队列不为空，执行 callback（D），**输出 D**
// 步骤8：microtask 队列为空，执行 UI render，（根据机器负荷等环境影响，综合浏览器策略，此步骤可能执行也可能不执行）
// 步骤9：首次 eventloop 结束。执行第二轮 eventloop，取出一个 task callback（B），执行之，**输出 B**
```
# 参考
[深入探究 eventloop 与浏览器渲染的时序问题](https://www.404forest.com/2017/07/18/how-javascript-actually-works-eventloop-and-uirendering/)
