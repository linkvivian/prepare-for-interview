# 合成事件的setState
## 合成事件
首先得了解一下什么是合成事件，react为了解决跨平台，兼容性问题，自己封装了一套事件机制，代理了原生的事件，像在jsx中常见的onClick、onChange这些都是合成事件
![image](https://pic3.zhimg.com/80/v2-225868f3e3e590bbab45336a6f3af9e6_hd.jpg)
这个方法中把 isBatchingUpdates 设为了 true , 导致在 requestWork 方法中， isBatchingUpdates 为 true ，但是 isUnbatchingUpdates 是 false，而被直接return了。

那return完的逻辑回到哪里呢，最终正是回到了 interactiveUpdates 这个方法，仔细看一眼，这个方法里面有个 try finally 语法，前端这个其实是用的比较少的，简单的说就是会先执行 try代码块中的语句，然后再执行 finally 中的代码，而 fn(a, b) 是在try代码块中，刚才说到在 requestWork 中被return掉的也就是这个fn（上文提到的 从dispatchEvent到 requestWork 的一整个调用栈）。

所以当你在increment中调用 setState 之后去 console.log 的时候，是属于try代码块中的执行，但是由于是合成事件，try 代码块执行完 state 并没有更新，所以你输入的结果是更新前的 state 值，这就导致了所谓的"异步"，但是当你的 try 代码块执行完的时候（也就是你的increment合成事件），这个时候会去执行 finally 里的代码，在 finally 中执行了 performSyncWork 方法，这个时候才会去更新你的 state并且渲染到UI上。
# 生命周期函数中的setState
其实还是和合成事件一样，当componentDidmount执行的时候，react内部并没有更新，执行完componentDidmount后才去commitUpdateQueue更新。这就导致你在componentDidmount中setState完去console.log拿的结果还是更新前的值
# 原生事件中的setState
原生事件的调用栈就比较简单了，因为没有走合成事件的那一大堆，直接触发click事件，到requestWork ,在 requestWork 里由于 expirationTime === Sync 的原因，直接走了 performSyncWork 去更新，并不像合成事件或钩子函数中被return，所以当你在原生事件中setState后，能同步拿到更新后的state值。
# setTimeout中的setState
在 setTimeout 中去 setState 并不算是一个单独的场景，它是随着你外层去决定的，因为你可以在合成事件中 setTimeout，可以在钩子函数中 setTimeout，也可以在原生事件setTimeout，但是不管是哪个场景下，基于event loop的模型下，setTimeout 中里去 setState 总能拿到最新的state值
# 参考
[你真的理解setState吗？](https://zhuanlan.zhihu.com/p/39512941/)
