# 消息小部件

## `label`


这个小部件显示文本消息。


**示例**：

```tcl
proc push_button {} {
	.ent insert 0 {Hello }
}

label .lab -justify left -text {Enter name:}
entry .ent
button .but -text {Push Me} -command "push_button"

pack .lab .ent .but
```

## `message`

所谓消息，是一种显示文本字符串的小部件。与标签小部件很相似，但消息小部件，可以用来构造多行文本。


`-justify`（对齐）选项，用于指定文本行的对齐方式。必须是 `left`（左对齐）、`center` （居中）或 `right` （右对齐）之一。默认为 `left`。该选项与 `anchor`、`aspect`、`padX`、`padY` 和 `width` 选项配合使用，可在该视窗中，提供多种文本排列方式。



（End）


