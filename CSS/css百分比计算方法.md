# margin&padding
padding也是根据应用该属性的父元素的宽来计算的，跟margin表现一致。(再插一句：当按百分比设定一个元素的宽度时，它是相对于父容器的宽度计算的,元素竖向的百分比设定也是相对于容器的宽度，而不是高度。)
# 定位元素

```
<div style="height: 100px; width: 50px">
    <div id="temp1" style="position: relative; top: 50%">Test top</div>
    <div id="temp2" style="position: relative; right: 25%">Test right</div>
    <div id="temp3" style="position: relative; bottom: 75%">Test bottom</div>
    <div id="temp4" style="position: relative; left: 100%">Test left</div>
</div>
```

对于定位元素，这些值也是相对于父元素的，但与非定位元素不同的是，它们是相对于父元素的高而不是宽。
