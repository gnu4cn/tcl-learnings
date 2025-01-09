# 字符串操作

**String Manipulation**

构造了一些数学脚本后，咱们移步到字符串。字符串，顾名思义，就是一串字符，a string of characters。现在，咱们来试着构造一些脚本，熟悉字符串的用法。


将字符串赋值给变量，与将数字赋值给变量一样简单。

```tcl
set str "This is a string"
```

咱们可以在其中加入一些特殊字符，以格式化输出结果。

```tcl
set str "Tcl/tk\nis\na\ngood\nlanguage"
```

这将给到变量 `str` 以下文本：

```console
Tcl/tk
is
a
good
language
```

`\n` 表示新行。还有其他一些替换。详情请阅读 [手册](https://tcl.tk/man/tcl8.2.3/TclCmd/string.html)。字符串变量的使用非常简单。请看下面的脚本。

```tcl
set joke1 "There are two ways to write error-free programs. Only the third one works."
set joke2 "A bug in the code is worth two in the documentation."

label .jokes -text "Joke 1 : $joke1 \nJoke 2 : $joke2"
pack .jokes
```

赋值字符串的另一方法，是使用 `{...}`（使用花括号）。举例如下。


```tcl
set price {$20}
```

花括号（大括号）确保在其内不进行任何替换。如果咱们不使用大括号，而是使用 `""`（双引号），设置价格为 `"$20"`，脚本将给出一个错误，提示 Tcl 无法读取名为 `20` 的变量。在双引号中可以进行替换。因此 Tcl 认为 `20` 是一个变量，因为他跟在 `$` 符号后面。这在大括号内是不会发生的。之前也解释过这个问题。



## 一些基本的字符串操作技巧

`string` 函数，是几乎所有字符串操作技巧的基础。下面给出了一些最常用的函数。请注意，在所有情况下，结果都会返回。而要将结果存入变量，就必须使用下面这样的代码：

```tcl
set result [string index "Binny" 0]
```

现提供几个例子。


### 获取某个字符串的第 `n` 个字母

`[string index <string> <character index>]`


示例：


```tcl
set quest "What is at the beginning of the end and at the end of all time?"
set ans [string index $quest 32]
label .question -text "Question : $quest"
label .answer -text "Answer : \"$ans\" OR \"[string index $quest end-1]\""
pack .question
pack .answer
```



### 获取从字符数 `n` 到字符数 `m` 的字符串

`[string range <string> <first character index> <last character index>]`


示例：

```tcl
set common "marriage, a man"
set end "for the women he loves"
set verb "yearns"

label .before -text "Before...\nBefore $common $verb $end\n"
label .afterm -text "After...\nAfter $common [string range $verb 1 end] $end"

pack .before
pack .afterm
```

> **注意**：这里只能在 `last character index` 参数处，使用 `end` 关键字，而不能在 `<first character index>` 处，使用 `start/begin` 这样的关键字。


### 获取字符串中某个字符（字符串）的第一和最后一个实例

- `[string first <string1> <string2> ?startIndex?]` - 用于获取第一个 `string1` 的位置索引；

- `[string last <string1> <string2> ?startIndex?]` - 用于获取最后一个 `string2` 的位置索引。

示例：

```tcl
#!/usr/bin/env tclsh
set str "The quick brown fox jumps over the lazy dog."

puts "First o's index: [string first "o" $str]"
puts "Last o's index: [string last "o" $str]"
```

输出为：

```console
First o's index: 12
Last o's index: 41
```

### 获取字符串长度

`[string lenght <string>]`


示例：

```tclsh
#!/usr/bin/env tclsh
set str "The quick brown fox jumps over the lazy dog."

puts [string length $str]
```

输出为：


```console
44
```

还有许多其他字符串的函数。完整列表请参见 [手册](https://tcl.tk/man/tcl8.2.3/TclCmd/string.htm#M8)。


## `utf-8` 与 `cp936` 字符编码问题

Windows 系统上，使用 Vim 编辑器编写带有中文字符串的 Tk 脚本，会显示为乱码。而在 Linux 系统上，却没有这样的问题（Windows 中的终端 Tcl 脚本，也不会显示乱码）。这是因为 Tk 默认使用 UTF-8 编码，而 Windows 系统上，中文使用了 GB2312(cp936) 的编码。参见：

- [关于TCL中的编码问题](https://blog.csdn.net/lights_joy/article/details/1748448)。

- [How to Use Tcl 8.1 Internationalization Features](https://www.tcl.tk/doc/howto/i18n.html)


Windows 系统上，因为这两种字符编码，会造成 Tcl/Tk 程序处理中文等文字时，显示为乱码。在运行 `tclsh` 或 `wish` 解释器时，使用 `-encoding utf-8` 选项可解决这个问题。如：

```powershell
PS C:\tools\msys64\home\Lenny.Peng\tcl-scripts> wish -encoding utf-8 .\tk_gui_demo.tcl
```

会打开如下窗口：

![在 Windows 上 Tk `while` 实现的完整乘法表](images/multiplication_table_win.png)

> *参考链接*：[Working with UTF-8 encoded TCL files on windows](https://stackoverflow.com/a/29004123)


进一步，可在 Tcl/Tk 脚本顶部的 Shebang/Hashbang （`#!`） 行，写下 `#!/usr/bin/env -S wish -encoding utf-8`，便可在赋予脚本执行属性（`chmod +x`）后，直接以参数 `-encoding utf-8` 执行所编写的 Tk 脚本了。

> *参考链接*：[Multiple arguments in shebang](https://unix.stackexchange.com/a/477651)

类似地，也可以写这样的 Shebang：`#!/usr/bin/env -S tclsh -encoding utf-8`。


（End）


