# 概念
移动设备上的viewport就是设备的屏幕上能用来显示我们的网页的那一块区域，在具体一点，就是浏览器上(也可能是一个app中的webview)用来显示网页的那部分区域，但viewport又不局限于浏览器可视区域的大小，它可能比浏览器的可视区域要大，也可能比浏览器的可视区域要小。
# layout viewport
移动端浏览器的默认宽度，通过document.documentElement.clientWidth可获得
#  visual viewport
可视视口，可通过window.innerWidth获取
#  ideal viewport
先不需要用户缩放和横向滚动条就能正常的查看网站的所有内容；第二，显示的文字的大小是合适，比如一段14px大小的文字，不会因为在一个高密度像素的屏幕里显示得太小而无法看清，理想的情况是这段14px的文字无论是在何种密度屏幕，何种分辨率下，显示出来的大小都是差不多的
# 参考
[移动前端开发之viewport的深入理解](https://www.cnblogs.com/2050/p/3877280.html)