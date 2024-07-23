# 你好世界

**Hello World**

让我们像其他教程一样，从 `Hello World` 程序开始。创建一个名为 `Hello.tcl` 的文件，并输入以下内容。


```tcl
#!/usr/bin/env wish
# 构造出一个 "Hello World" 的标签

label .hello -text "Hello World"
pack .hello
```

第一行 -- `#!/usr/bin/env wish` 在 windows 中是不需要的。在 Linux 中，他告知的是脚本语言处理器的名称。不明白这是什么意思？不用担心。把他放在文件顶端就可以了。但如果咱们打算制作一个良好可移植的脚本，就不要使用这一行。请使用下面这一行。


```tcl
#!/bin/sh
#The next line executes wish - wherever it is \
exec wish "$0" "$@"
```

为什么？原因请参见 [Unix 中的 Tcl/Tk]()。

{{#include ./appendix.md:20:30}}

第二行 -- 这是一条注释。任何以 `#` 字符开头的行，都是注释。注释在程序中没有任何作用。他是程序员用来自言自语的。程序员不可能记住脚本所做的每一件事。因此他便使用注释将其写下来。下次编辑脚本时，他便可以阅读注释，了解程序的用途。尽可能多地编写注释，是一种很好的做法。


第三行 -- `label .hello -text "Hello World"`，创建了一个标签，并在其中写入 "Hello world"。咱们可以将文本，改成任何咱们喜欢的内容。请注意该命令的结构：

- `label` -- 小部件，the widget，的名称。小部件是 X 图形用户界面中，一个用户界面对象。不明白吗？不明白？我也是。只能说他是出现在屏幕上对象的名称。还有很多其他小部件。如果要显示一个按钮，咱们可以使用按钮部件。如果要显示文本，则使用文本部件。要显示条目，你猜对了，就是条目部件。若咱们想要，咱们就会发现更多的图形用户界面的 [小部件](widgets_part_I.md)；


> **注**：小部件，widget，实际上是一个小的视窗。是视窗化桌面管理系统的组成元素。

- `.hello` - 赋予给这个视窗小组件的名称。每个部件都必须有个唯一的名称。当必须要访问这个视窗部件时，将使用该名称。这就是所谓的路径；

- `-text "Hello World"` - 这个视窗组件的选项。该选项表示，必须为该部件提供 "Hello World" 文本。选项会根据部件的不同而改变 -- 按钮部件不会拥有标签部件的所有选项，反之亦然。但各种不通部件之间，会有很多共同选项。咱们还可以在这里，继续编写其他选项。例如，咱们来制作一个，下面这样的显示文本 "Hell World" 的标签。其他行与 `Hello World` 程序相同。

```tcl
label .hell -text "Hell World" -font courierfont -relief raised
```

在这个示例中，用到了更多选项。`font` 字体选项，用于说明必须使用哪种字体来制作文字，`relief` 选项则用于说明文字应显示为凸起、凹陷还是扁平的等等。要了解特定小部件的所有选项，请阅读 Tcl 随附的手册。手册中列出了各个部件及其选项。如果咱们打算用 Tcl 编程，就会发现自己每隔几分钟，就会翻看一下手册。那里列出了最重要、最常用的选项。


这样，咱们便有了小部件命令的最终语法。


```tcl
<NameOfWidget> <path> ?<option 1> <option 2> ...?
```

第四行 -- `pack .hello` - 这一行告诉咱们，如何打包这个小部件。这一行请求解释器，打包名为 `.hello` 的部件。解释器比一般孩子都听话，他照做了。现在，`pack` 是个几何管理器，a geometry manager。另一个几何管理器是 [`grid`](widgets.md#grid)。我个人更喜欢 `grid`。


现在，Tcl 的清教徒们，Tcl puritans，会大声疾呼，说这不是打印 "Hello World" 的方法。“纯粹” 方法如下......


```tcl
#!/usr/bin/env tclsh
#Print "Hello World"
puts "Hello World"
```

> **注意**：这里的第一行，原本也是 `#!/usr/bin/tclsh`，为更加正式，修改为了 `#!/usr/bin/env tclsh`。

客观地讲，这里是在教 Tcl/Tk，而不是 Tcl。以上是 Tcl 的操作方法。这里是 Tcl/Tk 的方法。我（作者）知道，正在阅读本教程的人会大叫：“等一下，你是说 Tcl 和 Tk 是两种不同的语言？！！”

现在，Tk 本身，并不是一种语言 -- 怎么说呢，他是 Tcl 的附加组件，an add-on to Tcl。创建 Tk 的目的，是为某些应用程序提供图形工具包，a graphical ToolKit。然而 Tcl 本身，则是一门完整的语言。如果咱们说 Tcl 与 Tcl/Tk，是两种不同的语言，那就大错特错了。

上述脚本是在 UNIX 环境下，使用 Tcl 打印 "Hello World" 的方法。在 Windows 中，如果使用 `wish` 执行该脚本，则什么也看不到。

> **注意**：实际上，使用 Windows 上的 `wish` 执行该脚本，是可以打开一个窗口，并显示出那个标签的。
