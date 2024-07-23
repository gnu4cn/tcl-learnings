# 清单/列表

Tcl 列表包含着一个元素序列，a sequence of elements，每个元素则可以是数字、字符串或其他列表。咱们来构造一个列表：


```tcl
set list_name "To Do List"

# Create an Empty list using the list command. Not very nessary
set to_do [list]

#Add items to our to do list
lappend to_do "Buy Groceries"
lappend to_do "Tame Nature"
lappend to_do "Split Atom"

# lappend to_do "Buy Groceries" "Tame Nature" "Split Atom" 250 true

#Display all things
label .desc -text "The $list_name\n$to_do"

label .one -text "First thing to do : [lindex $to_do 0]"; # Get first element
label .second -text "Second thing to do : [lindex $to_do 1]" ;#Get second element
label .third -text "Third thing to do : [lindex $to_do 2]" ;#and so on

pack .desc .one .second .third

#Insert a new Item in the second place
set to_do [linsert $to_do 1 "Capture Osama Bin Laden" "Learning Tcl/Tk"]
label .list -text "New List\n$to_do"

#Change an item
set to_do [lreplace $to_do 2 3 "Someone already did that" "New task I" "Making food"]
label .latest -text "Latest List\n$to_do"

label .total -text "Total number of jobs to do = [llength $to_do]"

pack .list .latest .total
```

此处用于列表的命令，及其说明：


| 命令 | 语法 | 描述 |
| :-- | :-- | :-- |
| `list` | `list ?value value value...?` | 该命令返回一个包含所有参数的列表，在没有指定参数时，返回一个空字符串。|
| `lappend` | `lappend listName ?value value value...?` | 此命令将 `listName` 所给到变量，视为一个列表，并将各个值参数作为独立元素，追加到该列表中，这些元素之间用空格隔开。如果 `listName` 不存在，则会创建包含那些值参数所给元素的一个列表。 |
| `lindex` | `lindex list ?index...?` | `lindex` 命令会取某个 Tcl 列表，并返回其第 `index` 个索引元素。请记住，列表从 `0` 开始，第一个元素便是其第 `0` 个。 |
| `linsert` | `linsert list index element ?element element...?` | 该命令将所有元素参数，插入第 `index` 个元素之前，从而从列表生成一个新的列表。 |
| `lreplace` | `lreplace list first last ?element element...?` | 通过以元素参数，替换列表的一个或更多元素，`lreplace` 会返回由此构成的一个新的列表。语法中的 `first` 和 `last`，分别指定出要替换元素范围的第一个和最后一个索引。 |
| `llength` | `llength list` | 将 `list` 视为列表，并返回一个十进制字符串，表示其中元素的个数。 |

> **注意**：
>
> 1. Tcl 列表中可以存储不同类型的数据。如上面示例中就存储了字符串、数字和布尔值；
>
> 2. `llength` 可传入字符串参数。如：

```tcl
#!/usr/bin/env tclsh
set str "The quick brown fox jumps over the lazy dog."

puts [llength $str]
```

> 将输出：`9`，表示这个字符串有 9 个单词。

还有更多与列表相关的命令，如 `lsort`、`lset`、`lrange`、`lsearch` 以及 `split`、`join` 等。有关这些命令的详细信息，请参阅 [手册](https://tcl.tk/man/tcl8.6.13/TclCmd/list.html)。


## **`split`** 命令

`split` 是一条非常有用的命令，用于从字符串创建出列表。如果要在字符串中的任意字符处，将字符串拆分成若干项，可以使用 ...嗯... `split` 命令。在要将句子中的每个单词都放入列表中时，该命令非常有用。

```tcl
set words [split $sentence " "]
```


在这里，名为 `$sentence` 的变量中的每一个空格，都会被剪切 -- 实质上就是将其分割成单词。现在有了一个名为 `$words` 的新列表。`[lindex $words 0]` 的结果，将是第一个单词，`1` 将是第二个单词，以此类推。这条命令的另一个用途，是用 `read` 命令读取文件，然后用 `\n` 对该命令的结果字符串加以分割，从而得到文件中所有行的列表。要了解这一点，需要前往 [文件处理](./file.md)。


## 数组/字典

> **注**：原文为 “数组”，根据下面的内容，这种数据结构实为字典。

使用 `array` 命令，咱们可以在 Tcl 中创建出另一种数组。这会给到数组中的每个值一个名字，而可以用名字访问这些值。


*语法*：

```tcl
array option arrayName ?arg arg ...?
```

示例：

```tcl
#Make the array
array set star_trek {
	location	"Bridge of the Enterprise"
	problem		"Power surge"
	solution	"a fuse"
}

#Access the variables
label .sol1 -text "The $star_trek(problem) at $star_trek(location) \
	could have been avoided if they had $star_trek(solution)."

#Change the variable
set star_trek(solution)	"Wesley"

#Access the changed variables
label .sol2 -text "The $star_trek(problem) at $star_trek(location) \
	could have been avoided if they had $star_trek(solution)."

#Show the solutions
pack .sol1 .sol2
```

> **注意**：与列表一样，Tcl 的字典也可以存储不同类型的值，如字符串、数字与布尔值等。

命令 `array set star_trek` 会创建出字典 `star_trek`，并给到随后的参数，作为其内容。可以用以下代码，访问这个字典。

```tcl
$<ARRAY_NAME>(<ELEMENT_ID>)
```

移除 `$` 符号后，就可以像访问其他变量一样，轻松地修改变量。例如：

```tcl
set <ARRAY_NAME>(<ELEMENT_ID>) <VALUE>
```

一些 `array` 相关的命令，及其描述：

| 命令 | 语法 | 描述 |
| :-- | :-- | :-- |
| `array set` | `array set arrayName { list }` | 设置 `arrayName` 中一个或多个元素的值。*列表，list* 的形式必须与数组 `get` 返回的形式相同，由偶数个元素组成。列表中各个奇数元素，都会被视为 `arrayName` 中的元素名，而列表中的下一元素，会被用作该数组元素的新值。 |
| `array size` | `arrary size arrayName` | 返回一个十进制字符串，表示数组中元素的个数。如果 `arrayName` 不是某个数组的名称，则返回 `0`。 |
| `array names` | `array names arrayName ?mode? ?pattern?` | 返回一个列表，其中包含了字典中，与模式匹配的所有元素名称。其中模式可以是 `-exact`、`-glob` 或 `-regexp`。 |
