# 控制流

**The Control Flow**


## `if` 条件

*语法*：

```tcl
if { test1 } {
    body1
} elseif { test2 } {
    body2
} else {
    bodyn
}
```

如果不喜欢大括号，咱们也可以去掉他们。但这样一来，咱们就必须在一行中给出完整内容。我知道，当咱们看完这些语法之后，还在想这到底是怎么回事。别担心，一个例子就能让咱们明白。



```tcl
#The marriage status script...
#Change the status please
set marital_status "After"

label .thesis -text "Marriage is a three ring circus..."

if { $marital_status=="Before" } {
    set ring "Engagement"
} elseif { $marital_status=="During" } {
    set ring "Wedding"
} else {
    set ring "suffe -"
}

label .proof -text "$marital_status Marriage: $ring ring"

pack .thesis
pack .proof
```

运行此脚本，并将 `marital_status` 设为 `"Before"`、`"During"` 及 `"After"`，看看不同的结果。


### 运算符

**Operators**

咱们需要运算符，来进行（条件）检查。幸运的是，Tcl 中的运算符，与其他语言中的运算符相同。因此，只要对任何一种语言有一点经验，就能保证咱们对所有运算符了如指掌。


Tcl 有两种运算符。


- *关系运算符，Relational Operators*：`<`、`<=`、`>`、`>=`、`==` 及 `!=`，他们会返回 `0`（`false`）或 `1`（`true`）。

| Tcl 中的运算符 | 意义 | 示例 |
| :-- | :-- | :-- |
| `==` | 等于 | `5 == 6` |
| `!=` | 不等于 | `5 != 6` |
| `<` | 小于 | `5 < 6` |
| `<=` | 小于等于 | `5 <= 6` |
| `>` | 大于 | `5 > 6` |
| `>=` | 大于等于 | `5 >= 6` |


- *逻辑运算符，Logical Operators*：`&&`、`!` 及 `||` 运算符，与（`AND`）、非（`NOT`）及或（`OR`）运算符。


| 运算符 | 逻辑等价物 | 示例 |
| :-- | :-- | :-- |
| `! expression` | 非（`NOT`） | `!$a` |
| `expression1 && expression2` | 与（`AND`） | `$a > 6 && $a < 10` |
| <code>expression1 &#124;&#124; expression2</code> | 或（`OR`） | <code>$a != 6 &#124;&#124; $a != 5</code> |

## `for` 循环

最常用的循环，是 `for` 循环。当咱们必须在很少或没有变化的情况下，执行一组给定指令时，这个循环非常有用。


*语法*：

`for init test next body`

我（作者）更喜欢下面这种语法：

```tcl
for { init } { test } { next } {
    body
}
```

现在，咱们要第一次编写脚本，来做一些有用的事情 -- 构造一个乘法表。想知道这有什么用吗？当你像我（作者）一样忘记数学时，就会发现他非常有用。


```tcl
# 乘法表...
set n 4 ;# 咱们要的是 4 的乘法表
set table ""

for { set i 1 } { $i <= 10 } { incr i } {
# 这将把 n 的所有数相乘，追加到名为
# table 的变量
	set table "$table $i x $n = [expr $i \* $n]\n"
}

label .mul -text [encoding convertto utf-8 "Multiplication table for $n\n\n$table"]
pack .mul
```

> **注意**：以下是完整的乘法表（需在 Linux 系统上运行，否则会出现乱码）：

```tcl
#!/usr/bin/env wish

# 乘法表...
set table ""

for { set i 1 } { $i < 10 } { incr i } {
# 这将把 n 的所有数相乘，追加到名为
# table 的变量
	for { set j 1 } { $j <= $i } { incr j } {
		set tmpExp  "$j x $i = [expr $j \* $i]"
		set table [ expr [string length $tmpExp] <= 9 ? { "$table$tmpExp\t\t" } : { "$table$tmpExp\t" } ]
	}
	set table "$table\n"
}

label .mul -justify left -text "乘法表\n\n$table"
pack .mul
```

> **注意**：`-justify` 选项只有当小部件中有着多行文本时，才生效。参考链接：["Justify=LEFT" NOT WORKING on Tkinter Label Widget](https://stackoverflow.com/a/62233664)。


## `foreach`

*语法*：

`foreach varName list body`

> **注意**：同 `for` 循环一样，更具可读性的写法为：

```tcl
foreach varName list {
    body
}
```

这是一种可以让编程变得更简单的循环。主要用于列表。例如......


```tcl
#Make the list
set list [list "Item 1" {Item 2} Last]

set text ""
foreach item $list {
	#Append the every item to $text
	set text "$text\n$item"
}

#Shows the result
label .lab -text "$text"
pack .lab
```


> **注意**：这里会显示出 4 个行，其中第一个是空行，因为 `list` 列表中第一个元素为 `list`，是个空列表。


通过下面这样一个普通的 `for` 循环，也能达到同样的效果。

```tcl
#Make the list
set list [list "Item 1" {Item 2} Last]

set text ""
for { set i 0 } { $i < [llength $list] } { incr i } {
	#Append the every item to $text
	set text "$text\n[lindex $list $i]"
}

label .lab -text "$text"
pack .lab
```

## `while` 循环

只要满足条件，就重复执行脚本。在给到的语法中，`test` 是条件，`body` 是脚本。只要 `test` 为真，脚本就会重复执行。


*语法*：

```tcl
while test body
```

而我（作者）更喜欢下面这种......

```tcl
while { test } {
    body
}
```

与我们在 `for` 循环中，用到的程序相同。现在介绍 -- `while` 循环：


```tcl
#Multiplication table...
set n 4 ;# We want the multiplication table of 4

set table ""
set i 1
while { $i <= 10 } {
# This will append all multiples of all numbers for the number n
#		into a variable called table
	set table "$table $i x $n = [expr $i \* $n]\n"
	incr i
}

label .mul -text "Multiplication table for $n\n\n$table"
pack .mul
```

> **注意**：使用 Tcl 的 `while` 循环，打印完整乘法表的代码如下：

```tcl
#!/usr/bin/env wish

# 乘法表...
set table ""
set i 1

while { $i < 10 } {
# 这将把 n 的所有数相乘，追加到名为
# table 的变量
	set j 1
	while { $j <= $i } {
		set tmpExp  "$j x $i = [expr $j \* $i]"
		set table [ expr [string length $tmpExp] <= 9 ? { "$table$tmpExp\t\t" } : { "$table$tmpExp\t" } ]
		incr j
	}

	incr i
	set table "$table\n"
}

label .mul -justify left -text "乘法表\n\n$table"
pack .mul
```

![Tcl `while` 循环打印的完整乘法表](images/multiplication_table.png)


## `switch` 循环

根据给定值，执行多个脚本中之一。

*语法*：

```tcl
switch ?options? string { pattern body ?pattern body ...? }
```

而我（作者）更喜欢下面这种......


```tcl
switch ?options? { string } {
    pattern  { body }
    ?pattern { body }
    ...?
}
```

其中 `?options?` 可以是下面任何一项：


- `-exact`，在将字符串与模式匹配时，使用精确匹配。这是默认设置；

- `-glob`，在匹配字符串与模式时，使用 `glob` 风格的匹配（即与字符串匹配命令的实现方式相同）；

- `-regexp`，将字符串与模式匹配时，使用正则表达式匹配。


`switch` 与 `if-else` 命令非常相似。因此，这里将使用刚才的例子。


```tcl
#The marriage status script...
#Change the status please
set marital_status "After"

label .thesis -text "Marriage is a three ring circus..."

switch $marital_status {
    "Before" { set ring "Engagement" }
    "During" { set ring "Wedding" }
    default { set ring "suffe -" }
}

label .proof -text "$marital_status Marriage: $ring ring"

pack .thesis
pack .proof
```

{{#include ./control_flow.md:45}}


（End）


