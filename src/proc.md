# 过程

有些语言称之为函数。另一些语言称之为子程序。还有一些语言称之为方法。在 TCL 中，我们称之为 **程序, Procedures**。我知道这些词之间有微妙的、人类无法区分的变化 -- 但谁在乎呢？

*语法*：

```tcl
proc procedureName arguments ?args? body
```

而我（作者）则更喜欢下面这种......

```tcl
proc procedureName { arguments ?args? } {
    body
}
```

`proc` 命令会以任意名字，创建出一个新的 Tcl 过程，a new Tcl procedure，并以那个名字，取代其下既有的任何命令或过程。每当调用这个新命令时，Tcl 解释器将执行 `body` 的内容。可以为过程指定参数。参数是由一个列表（可能为空）组成，每个元素指定一个参数。每个参数的指定符，argument specifier，也是包含了一或两个字段的列表。如果只有一个字段，则为参数名称；如果有两个字段，则首个字段为参数名称，第二个字段为该参数的默认值。


对于这条命令（`proc`），这里将给出一个 C++ 示例，和一个 TCL 示例......


**C++ 中**

```c++
int plus(int a, int b)
{
    int ans=a+b;
    return ans;
}
```


**Tcl 中**：


```tcl
proc plus {a b} {
    set ans [expr $a+$b]
    return $ans
}
```

给定的参数，可以是数字、字符串、列表、人类 -- 总之，任何东西都可以。我（作者）还不知道，如何将人作为参数，但我坚信这是可行的。

使用函数名，便可以调用已定义的函数。参数列在名称之后。使用上述函数的示例。

```tcl
# Function Plus
proc plus {a b} {
    set ans [expr $a+$b]
    return $ans
}

set sum [plus 1 2]

label .txt -text "Sum of 1 and 2 is $sum"
pack .txt
```


（End）


