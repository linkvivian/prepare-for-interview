# <script src="script.js"></script>
没有 defer 或 async，浏览器会立即加载并执行指定的脚本，“立即”指的是在渲染该 script 标签之下的文档元素之前，也就是说不等待后续载入的文档元素，读到就加载并执行。，所以在没有async和defer的情况下，<script>标签最好放到<body>底下
# <script async src="script.js"></script>
有 async，加载和渲染后续文档元素的过程将和 script.js 的加载与执行并行进行（异步）。
# <script defer src="myscript.js"></script>
有 defer，加载后续文档元素的过程将和 script.js 的加载并行进行（异步），但是 script.js 的执行要在所有元素解析完成之后，DOMContentLoaded 事件触发之前完成。
# 结论
defer和async在网络读取是一样的。区别在于执行的时机，async在脚本加载完会立即执行，defer在所有元素都解析完才会执行。并且它们还有一个区别就是async在脚本执行顺序是不可预测的，因为它们都是一旦加载完就会执行，但是defer执行的顺序是按照它们在文档声明的顺序决定的。明显看出，defer更适用于平时我们的开发。async 对于应用脚本的用处不大，因为它完全不考虑依赖（哪怕是最低级的顺序执行），不过它对于那些可以不依赖任何脚本或不被任何脚本依赖的脚本来说却是非常合适的