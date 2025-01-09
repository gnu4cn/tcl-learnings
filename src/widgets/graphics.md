# 图形小部件

## `canvas`

画布小部件，是一个非常重要的部件，因为其上的所有点，都是可寻址的图形绘制区域。画布部件实现了结构化图形，structured graphics。画布可显示任意数量的项目，如矩形、圆形、线条及文本。可以对这些项目进行操作（如移动，或重新着色），也可以将命令与项目关联起来。因此，如果咱们不喜欢 Windows 中的绘画程序，就可以用这个这个小部件，制作自己的程序。


命令 `path create type options`，用于构造出一些不同结构。下面给出了几个例子。如需了解更多信息，请阅读 Tcl/Tk 附带的出色手册。


**示例**：


```tcl
canvas .cns -relief sunken -background "blue"

.cns create polygon 5 100   50 5   150 5   200 100   5 100 \
	-joinstyle bevel -fill "red" -outline "white" -width 5

.cns create oval 200 100 300 200 -fill "green"
.cns create oval 100 150 300 100 -fill "white" -width 0
.cns create rectangle 10 150 100 250 -dash {6 4 2 4 2 4}

pack .cns
```


（End）


