# 文本输入小部件

## `entry`

输入小部件，the entry，是一个显示单行文本字符串的部件，用户可以在其中输入和编辑文本。当输入焦点在条目上时，他就会显示一个插入光标，an insertion cursor，指示新字符将插入的位置。下面使用 HTML，给出了一个输入元素。


<input type="text" value="Text can be inputed here." />


**部分选项**

| 选项 | 描述 |
| :-- | :-- |
| `-width NUMBER` | 这个输入字段的宽度。其中的 `NUMBER` 应是整数。 |
| `-textvariable VARIABLE` | 变量 `VARIABLE` 的内容，将显示在该小部件中。在小部件中的文本被编辑时，变量也将自动被编辑。在给到 `VARIABLE` 时，前面应 **不带** `$` 符号。 |
| `-state STATE` | 这个输入字段的状态。可以是 `normal`、`disabled` 或 `readonly`。如果是 `readonly` 状态，则无法编辑文本。 |


**一些命令**

| 命令 | 描述 |
| :-- | :-- |
| `path get` | 输入字段内的文本，可以通过此命令提取。 | `set name [.ent get]` |
| `path delete FIRST ?LAST?` | 删除该输入部件的一或多个元素。`FIRST` 是要删除的第一个字符索引，`LAST` 是要删除的最后字符之后字符的索引。如果没有指定 `LAST`，则其默认为 `FIRST+1`，即只删除一个字符。此命令将返回空字符串。 | `.ent delete 0 end` |
| `path insert index STRING` | 将 `STRING` 中的字符，插入索引所表示字符之前。第一个字符的索引为 `0`。最后一个字符可以使用 `end`（结束）。 | `.ent insert end {Hello}` |

**示例**：


```tcl
set input {World}

proc push_button {} {
	.ent insert 0 {Hello, }
}

entry .ent -textvariable input
button .but -text "Push Me" -command "push_button"

pack .ent .but
```

## `text`

文本小部件显示一或多行文本，并允许对文本进行编辑。与 [输入小部件](#entry) 类似，但尺寸更大。


**部分选项**

| 选项 | 描述 |
| :-- | :-- |
| `-xscrollcommand COMMAND` | 这是为了实现文本小部件和滚动条小部件之间的通信。还有一个 `-yscrollcommand` 与之类似。 |
| `-font FONTNAME` | 指定在 `text` 小部件内，绘制文本时使用的字体。 |
| `-width NUMBER` | 指定 `text` 小部件的宽度。 |
| `-height NUMBER` | 指定 `text` 小部件的高度，猜对了。 |


**一些命令**

| 语法 | 描述 | 示例 |
| :-- | :-- | :-- |
| `path get index1 ?index2 ...?` | 返回该文本输入框的某个字符范围。返回值将是文本中从索引为 `index1` 的字符开始，到索引为 `index2` 字符之前的所有字符（不会返回索引为 `index2` 的字符）。如果省略 `index2`，则返回 `index1` 处的单个字符。<br />请注意，文本的索引与输入 `entry` 部件的索引不同。文本输入框部件的索引格式为 `LINE_NO.CHARECTER_NO`。这意味着 `1.0` 表示第一行第一个字符。 | `set contents [.txt get 1.0 end]` |
| `path insert index DATA` | 在索引处的字符前，插入所有参数字符。如果索引指向文本输入框的末尾（最后一个换行符之后的字符），那么新文本将插入到最后一个换行符之前。 | `.txt insert end "Hello World"` |


**示例**


```tcl
proc push_button {} {
    set name [.ent get]
    .txt insert end "Hello, $name"
}

frame .frm -relief groove
label .lab -justify left -text {Enter name:}
entry .ent
button .but -text {Push Me} -command "push_button"
text .txt -width 20 -height 10

pack .lab -in .frm
pack .ent -in .frm

pack .frm
pack .but
pack .txt
```


## `scrollbar`

滚动条是一种显示出两个箭头的小部件，箭头位于滚动条的两端，滑块位于滚动条的中间部分。他提供了显示着某种文档（如正在编辑的文件或绘图）的相关视窗中，可见内容的信息。滑块的位置和大小，表示文档哪一部分，在关联窗口中可见。例如，如果竖直滚动条中的滑块，覆盖了两个箭头之间区域的顶部三分之一，就表示滚动条关联的窗口，显示了其文档顶部的三分之一。他可以与文本输入框等，其他部件一起使用。


**部分选项**


| 选项 | 说明 |
| :-- | :-- |
| `-orient DIRECTION` | 对于可按水平，或垂直方向布局的那些小部件（如滚动条），该选项指定了应使用的方向。`DIRECTION` 必须是 `horizontal` 或 `vertical`，或者是其中之一的缩写, an abbreviation of one of these。 |
| `-command COMMAND` | 在滚动条被移动时，这条命令会被执行。该选项的值几乎总是 `.t xview` 或 `.t yview`，由小部件部件的名称和 `xview`（当滚动条是在水平滚动时）或 `yview`（用于垂直滚动）组成。所有可滚动部件，都有着 `xview` 和 `yview` 命令，并会取与由滚动条所附加的，完全相同的额外参数。 |


**示例**


```tcl
proc push_button {} {
    set name [.ent get]
    .txt insert end "Hello, $name."
}

frame .frm -relief groove
label .lab -text "Enter name:"
entry .ent
button .but -text "Push Me" -command "push_button"

frame .textarea
text .txt -width 20 -height 10 \
    -yscrollcommand ".srl_y set" -xscrollcommand ".srl_x set"

scrollbar .srl_y -command ".txt yview" -orient v
scrollbar .srl_x -command ".txt xview" -orient h

pack .lab -in .frm
pack .ent -in .frm
pack .frm
pack .but

grid .txt -in .textarea -row 1 -column 1
grid .srl_y -in .textarea -row 1 -column 2 -sticky ns
grid .srl_x -in .textarea -row 2 -column 1 -sticky ew
pack .textarea
```




（End）


