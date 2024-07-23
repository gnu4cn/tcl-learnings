# 对话框

所谓对话框，可被叫做程序中脱离主窗口的一些元素。这是一个非常笼统的定义，存在很多问题。但就目前而言，这个定义是可行的。Tk 提供了许多种对话框。


## `tk_messageBox`

这个程序，this procudure, `proc`，会创建并显示出一个消息窗口，其中包含了应用程序所指定的消息、图标及一组按钮。消息窗口中的每个按钮，都有一个唯一的符号名称，a unique symbolic name（参见 `-type` 选项）。消息窗口弹出后，`tk_messageBox` 会等待用户，选择其中一个按钮。请点击下面的按钮，查看消息框的示例。


<input type="button" value="Message" onClick="alert('This is a message box')" />



**部分选项**

| 选项 | 说明 |
| :-- | :-- |
| `-default name` | `name` 给到该消息窗口，默认按钮的符号名称（`ok`、`cancel` 等）。有关符号名称的清单，请参阅 `-type`。如未指定这个选项，对话框中的第一个按钮，将作为默认按钮。 |
| `-icon iconImage` | 指定出要显示的图标。`IconImage` 必须是下列图标之一：`error`、`info`、`question` 或 `warning`。如未指定这个选项，则将显示 `info` 图标。 |
| `-message string` | 指定要在此消息框中显示的消息。 |
| `-title string` | 指定作为消息框标题，而要显示的字符串。默认值为空字符串。 |
| `-type predefinedType` | 安排下要显示的一组预定义按钮。`predefinedType` 可有以下值：<br /><li> `abortretryignore`，显示三个按钮，其符号名称分别为中止（`abort`）、重试（`retry`）和忽略（`ignore`）；</li><li> `ok`，显示一个按钮，其符号名称为 `ok`；</li><li> `okcancel`，显示两个按钮，符号名称分别为 `ok` 和 `cancel`；<li></li> `retrycancel`，显示两个按钮，符号名称分别为重试（`retry`）和取消（`cancel`）；</li><li> `yesno`，显示两个按钮，符号名称分别为 `yes` 和 `no`；</li><li> `yesnocancel`，显示三个按钮，符号名称分别为 `yes`、`no` 和 `cancel`。</li> |


**示例**


```tcl
set answer [tk_messageBox -message "Really quit?" -type yesno -icon question]

switch -- $answer {
    yes exit
    no {tk_messageBox -message "I know you like this application!" -type ok}
}
```


## `tk_chooseColor`


`tk_chooseColor` 小部件，会弹出一个对话框，供用户选择颜色。


**部分选项**


| 选项 | 说明 |
| :-- | :-- |
| `-initialcolor COLOUR` | 指定弹出颜色对话框时，要显示的颜色。 |


**示例**

```tcl
set color [tk_chooseColor -title {请选择你偏好的颜色}\
    -initialcolor {black}]


set answer [tk_messageBox -message "Your favorite color: $color Really quit?"\
    -type yesno -icon question]

switch -- $answer {
    yes exit
    no {tk_messageBox -message {I know you like this application!} -type ok}
}
```


## `tk_chooseDirectory`


`tk_chooseDirectory` 命令，会弹出一个对话框，供用户选择目录。


**部分选项**

| 选项 | 说明 |
| :-- | :-- |
| `-initialdir DIRNAME` | 指定弹出对话框时，要显示目录中的目录。如果未指定此参数，则显示当前工作目录下的目录。如果参数指定了相对路径，返回值将把相对路径转换为绝对路径。 |
| `-mustexist BOOLEAN` | 指定用户是否可以指定不存在的目录。如果该参数为 `true`，则用户只能选择已存在的目录。默认值为 `false`。 |


**示例**

```tcl
set dir [tk_chooseDirectory -mustexist true]

set answer [tk_messageBox -message "选择的目录为：$dir。真的要退出吗？"\
    -type yesno -icon question]

switch -- $answer {
    yes exit
    no {tk_messageBox -message {I know you like this application!} -type ok}
}
```

## `tk_getOpenFile`


程序，the procudure, `proc`，`tk_getOpenFile` 和 `tk_getSaveFile`，均会弹出一个对话框，让用户选择要打开或保存的文件。`tk_getOpenFile` 命令，通常与文件菜单中的打开命令相关联。其目的是让用户只选择一个现有文件。如果用户输入了一个不存在的文件，对话框就会给出错误提示，并要求用户给出其他选择。如果应用程序允许用户创建新文件，则应提供单独的 “新建” 菜单命令。

`tk_getSaveFile` 命令，则通常与文件菜单中的另存为命令相关联。如果用户输入的文件已经存在，对话框会提示用户，确认是否要覆盖现有文件。


**部分选项**


| 选项 | 说明 |
| :-- | :-- |
{{#include ./dialogs.md:80}}
| `-defaultextension EXTENSION` | 指定出一个字符串，如果用户输入的文件名，没有扩展名，则该字符串将被附加到文件名中。默认值为空字符串，即在任何情况下都不会在文件名后添加扩展名。 |
| `-filetypes filePatternList` | 在特定平台，the particular platform，的文件对话框中，存在文件类型列表框时，则该选项会给到列表框中的文件类型。当用户在列表框中，选择文件类型时，只会列出该类型的文件。如果未指定该选项，或该选项被设置为空列表，或特定平台不支持文件类型列表框，则会列出所有文件，无论其类型如何。这有点麻烦，请参阅手册了解相关信息。 |
| `-initialfile FILENAME` | 指定弹出对话框时，要显示的文件名。 |
| `-multiple` | 允许用户在 “打开” 对话框中，选择多个文件。 |


## `toplevel`

`toplevel` 是一个小部件。他可用于创建自定义的对话框。`toplevel` 与框架 `frame` 类似，但他是作为顶层视窗创建的：它的 `X` 父视窗，是屏幕的根视窗，而不是路径名中的逻辑父视窗。顶层视窗的主要用途，是作为对话框和其他视窗小部件集合的容器。顶层视窗的唯一可见特征，the only visible features，是其背景颜色，和一个可选的三维边框，用于使其看起来凸起或凹陷。


咱们可以使用 `toplevel`，来创建出新窗口。一些视窗小部件，可以打包其中，就像视窗部件打包在框架 `frame` 中一样。例如......


```tcl
#A procedure to make a toplevel window
proc makeTop {} {
    toplevel .top ;#Make the window

    #Put things in it
    label .top.lab -text "This is Toplevel Window" -font "ansi 12 bold"

    text .top.txt
    .top.txt insert end "Widgets can be packed in this window."

    #An option to close the window.
    button .top.but -text "Close" -command { destroy .top }

    #Pack everything
    pack .top.lab .top.txt .top.but
}

label .lab -text "This is the root window." -font "ansi 12 bold"
button .but -text "Click to Create Toplevel" -command { makeTop }
pack .lab .but
```

> **注意**：这里在 `.top.lab`、`.top.text` 与 `.top.but` 中，使用了不同于以往 `-in` 参数的新语法，来表示小部件之间的从属关系。
