# 部分 Tk 命令


## `bind`

`bind` 将 Tcl 脚本与事件关联起来。如果咱们想在用户双击列表框中的某个项目，或按下任何按钮（如 `F1`）时执行某些操作，那么 `bind`，就是咱们所需要的。咱们来在下一个示例中，绑定一些东西。


*语法*：


```tcl
bind path <sequence> script
```

`<sequence>` 表示按下按钮/鼠标的顺序。应按这样的模式给出：`<modifier-modifier-type-detail>`。比如：

`<Ctrl-Alt-Key-t>` 便是 `Ctrl+Alt+T`。

其中的 `Ctrl` 和 `Alt` 便是修饰符，而 `Key` 则为类型，`t` 便是细节了。参阅下一示例，咱们就会明白。


```tcl
#The helping function
proc help {} {
	tk_messageBox -message {Did you ask of help?
You ain't getting any.
Ha Ha Ha!}
}

#This happens at double-click
proc double {} {
	tk_messageBox -message {You double clicked something.
This script is simple - so it won't display what you clicked on.
But if you want a sript that is able to do that,
write to me at binnyva(at)gmail(dot)com
and I will send you a better script.}
}

label .lab -text " The Bind command " -font {ansi 12 bold}

listbox .lst
.lst insert end "Don't double-click this."
.lst insert end "Don't double-click this either."
.lst insert end "Don't even think of double-clicking this."
.lst insert end "You may double-click this."
.lst insert end "No. Negative. Nay. Nope. Get the message?"

#Bind the double click event to the list box
bind .lst <Double-ButtonPress-1> { double }

label .keys  -justify left -text {Press any of the following...
Ctrl+A
Ctrl+Shift+A
Ctrl+Alt+T
Right click
Ctrl+Alt+E}

pack .lab .lst .keys -expand 1 -fill x ;#Pack everything

#Exit when the escape key is pressed
bind . <Key-Escape> { exit }
#Shows a helping dialog box when F1 is pressed
bind . <Key-F1> { help }
#Binds misc keys.
bind . <Control-Key-a> \
 { tk_messageBox -message "You pressed Ctrl+A, didn't you?" } ;#Ctrl+A
bind . <Control-Key-A> \
 { tk_messageBox -message "Ctrl+Shift+A, right?" } ;#Ctrl+Shift+A
bind . <Control-Alt-Key-t> \
 { tk_messageBox -message "Control, Alt and T" } ;#Ctrl+Alt+T
bind . <ButtonPress-3> \
 { tk_messageBox -message "The right way to click." } ;#Right click
bind . <Control-Alt-Key-e> \
 { tk_messageBox -message {You must be a married man.
What you pressed remindes married men of what they never will have
 - Ctrl Alt e.}
} ;#Ctrl+Alt+e
```

> **注意**：
>
> 1. 最后一个绑定为 `Control-Key-Escape`，但 `Ctrl+Esc` 快捷键，在 Windows 10 上已被系统使用，按下时会弹出开始菜单，故会先被系统拦截，导致咱们的程序无法拦截到此快捷键绑定；
>
> 2. 当 `Ctrl` 出现在 `modifier-modifier-type-detail` 中时，不能写 `Ctrl`，而必须写出 `Control` 这样的完整形式。
