# 作用
<!DOCTYPE>声明位于位于HTML文档中的第一行，处于 <html> 标签之前。告知浏览器的解析器用什么文档标准解析这个文档。DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现。
# 各种doctype的区别
- HTML4.01Strict：这个DTD包含所有HTML元素以及属性，但是就不包括展示性的以及弃用的元素，比如说font，不允许框架集
- 
- HTML4.01Transitional：这个DTD包含全部deepHTML元素以及属性，包括展示性的和弃用的元素，比如font，不允许框架集。
- HTML4.01Frameset：这个DTD相当于HTML4.01Transitional，但是允许框架集内容。
- <!DOCTYPE html>

# 怪异模式（不写Doctype头部）
- 盒模型为IE盒模型，IE盒模型的width = boder + padding + content,标准盒模型width = content
- 图片元素的垂直对齐方式,对于inline元素和table-cell元素，标准模式下vertical-align属性默认取值是baseline；在怪异模式下，table单元格中的图片的vertical-align属性默认取值是bottom。因此在图片底部会有及像素的空间。
- 图片元素的垂直对齐方式,对于inline元素和table-cell元素，标准模式下vertical-align属性默认取值是baseline；在怪异模式下，table单元格中的图片的vertical-align属性默认取值是bottom。因此在图片底部会有及像素的空间。
- 内联元素的尺寸,标准模式下，non-replaced inline元素无法自定义大写；怪异模式下，定义这些元素的width、height属性可以影响这些元素显示的尺寸。
- 元素的百分比高度,CSS中对于元素的百分比高度规定：百分比为元素包含块的高度，不可为负值；如果包含块的高度没有显示给出，该值等同于auto，所以百分比的高度必须是在元素有高度声明的情况下使用。 当一个元素使用百分比高度是，标准模式下，高度取决于内容变化，怪异模式下，百分比高度被准确应用 
- 元素溢出的处理,标准模式下，overflow取值默认为visible；在怪异模式在，该溢出会被当做扩展box来对待，即元素的大小由内容决定，溢出不会裁剪，元素框自动调整，包含溢出内容
# 参考文章
[浏览器标准模式和怪异模式之间的区别是什么？](https://blog.csdn.net/qq_31059475/article/details/78010601)