# 文件处理

与所有其他优秀语言一样，Tcl 也可以打开、读取及写入文件。和其他所有优秀的教程一样，本教程也会教大家如何做到这一点。首先让我们看看如何打开文件。


## `open` 命令

*语法*：

```tcl
open fileName ?access? ?permission?
```

`fileName` 是文件名。`access` 参数（如果存在），指定出访问文件的方式。他可以有以下任意值：

- `r`，打开文件仅供读取；文件必须已经存在。在未指定访问权限 `access` 参数时，这是默认值；

- `r+`，打开文件供读写；文件必须已经存在；

- `w`，打开文件，仅供写入。如果存在该文件名的文件，则会删除该文件的所有内容。如果不存在，则创建一个新文件；

- `w+`，打开文件进行读写。如果存在该文件名的文件，则删除该文件的所有内容。如果不存在，则创建一个新文件；

- `a`，打开文件，仅供写入。如果文件不存在，则创建一个新的空文件。会将初始访问位置，the initial access position，设置到文件末尾；

- `a+`，打开文件供读写。如果文件不存在，则创建一个新的空文件。会将初始访问位置，设置到文件末尾。


咱们来看一个示例。


```tcl
#Open the file called "jokes.txt" for writing
open "jokes.txt" w
```

现在我们知道如何打开文件了。没什么用，不是吗？为了让这个函数发挥作用，我们需要写入文件。


## `puts` 命令

*语法*：

```tcl
puts ?-nonewline? ?channelId? string
```

只有在写入文件的字符串末尾，不需要换行时，才使用 `-nonewline` 选项。`channelID` 参数，表示必须要写入输出流的 ID（如果不明白是什么意思，不用担心，稍后会明白）。`string` 便是要写入文件的字符串。让我们看看示例。


```tcl
#Open the file called "jokes.txt" for writing
set out [open "jokes.txt" w]
puts $out "Computers make very fast, very accurate mistakes."
```

请注意，这里创建了一个名为 `out` 的变量。他将存储打开文件的 `ID`。一定要以这种方式打开文件，否则他们就没什么用了。然后，咱们使用 `puts` 命令，运用这个 `ID` 来写入文件。现在，名为 `jokes.txt` 的文件只有一行。接下来，咱们必须关闭文件。


## `close` 命令

*语法*：

```tcl
close ?channelId?
```

这条命令会关闭通道。一定要这样做，否则你会哭的。让我们继续举例说明......


```tcl
#Open the file called "jokes.txt" for writing
set out [open "jokes.txt" w]

puts $out "Computers make very fast, very accurate mistakes."

close $out
```

关闭文件后，我们决定要在文件中，添加更多行。于是，我们再次打开文件，这次是在追加模式下。这个例子变得更长了......


```tcl
#Open the file called "jokes.txt" for writing
set out [open "jokes.txt" w]

puts $out "Computers make very fast, very accurate mistakes."

close $out

set out [open "jokes.txt" a]

puts $out "Computers are not intelligent. They only think they are."
puts $out "My software never has bugs. It just develops random features."
puts $out {All computers wait at the same speed.
Best file compression around:  "DEL *.*" = 100% compression
DEFINITION: Computer - A device designed to speed and automate errors.
DEFINITION: Upgrade - Take old bugs out, put new ones in.}

close $out
```

完成这些后，我们就需要读取那些笑话，并将他们放回屏幕上。所以我们要学习新的指令。女士们，先生们，让我向你们介绍......


## `gets` 命令


*语法*：

```tcl
gets channelId ?varName?
```


`gets` 将从频道（或文件）中复制 **一行**，并将其放入 `varName` 中。如未指定 `varName`，则复制的行，就是该函数的结果。咱们回到示例，并获取文件的第一行。为此，我们要再次打开那个文件，这次采用读取模式。


```tcl
#Open the file called "jokes.txt" for writing
set out [open "jokes.txt" w]

puts $out "Computers make very fast, very accurate mistakes."

close $out

set out [open "jokes.txt" a]

puts $out "Computers are not intelligent. They only think they are."
puts $out "My software never has bugs. It just develops random features."
puts $out {All computers wait at the same speed.
Best file compression around:  "DEL *.*" = 100% compression
DEFINITION: Computer - A device designed to speed and automate errors.
DEFINITION: Upgrade - Take old bugs out, put new ones in.}

close $out

#Opening file in read mode
set in [open "jokes.txt" r]

gets $in line

label .line -text "First Line : $line"
pack .line
```


下面的命令，可用于逐行读取整个文件。请看下面的示例。请勿担心其中的行 `.txt insert end "$line\n---\n"` -- 稍后这里会作解释。


```tcl
text .txt
#Opening file in read mode
set in [open "jokes.txt" r]

while {[gets $in line] != -1} {
    #Do whatever you want with the $line variable
    .txt insert end "$line\n---\n"
}
close $in

pack .txt -expand 1 -fill both
```

这个命令用于逐行读取文件。现在咱们需要查看到整个文件。为此，我们需要使用下面的 `read` 命令。但请记住，如果咱们之前已经读取了一行，那么读取命令将只读取第二行。为了将通道重置到最初位置，我们需要使用下面的 `seek` 命令。


## `seek` 命令

*语法*：

```tcl
seek channelId offset ?origin?
```

`offset` 和 `origin` 参数，指定了 `channelId` 下一次读取或写入的位置。*偏移量，offset* 必须是整数（可以是负数），*原点，origin* 则必须是以下其中之一：`start`、`current` 或 `end`。

现在我们必须要读取文件内容了。因此，咱们要继续到......


## `read` 命令


*语法*：

```tcl
read channelId ?numChars?
```

`read` 会从通道中读取 `numChars` 个字符，并将其返回。如果没有指定 `numChars`，则会读取整个文件并返回其内容。咱们可以读取文件，然后将所有行放入一个列表，将每一行作为列表中的一个项目。这可以通过下面的代码完成：


```tcl
set in [open "file.txt" r]
set contents [read $in]
close $in

set lines [split $contents "\n"]
```

现在，名为 `$lines` 的列表中的每一项，都是名为 `file.txt` 文件中的一行。下面是这一小节的最后一次举例说明。


```tcl
#Open the file called "jokes.txt" for writing
set out [open "jokes.txt" w]
puts $out "Computers make very fast, very accurate mistakes."
close $out

#Now append more jokes at the end of the file
set out [open "jokes.txt" a]
puts $out "Computers are not intelligent. They only think they are."
puts $out "My software never has bugs. It just develops random features."
puts $out {All computers wait at the same speed.
Best file compression around:  "DEL *.*" = 100% compression
DEFINITION: Computer - A device designed to speed and automate errors.
DEFINITION: Upgrade - Take old bugs out, put new ones in.}
close $out

#Opening file in read mode
set in [open "jokes.txt" r]
gets $in line
label .line -justify left -text "First Line : $line"
pack .line

seek $in 0 start
set contents [read $in]
close $in

label .full-heading -text "Full file Contents... \n"
label .full -justify left -text "$contents"
pack .full-heading .full
```

就这样，文件处理到此为止。现在，让我们进入更有趣的话题。


（End）


