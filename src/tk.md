# 关于 Tk

现在，我们要进入 Tcl 的图形领域 - Tk。如果咱们曾经尝试过用 C++ 编写图形程序，那么当看到用 Tk 制作图形程序是如此简单时，咱们一定会愤怒地尖叫起来。咱们会为自己以前没有发现这种语言而感到非常生气。以及发出了警告。


现在我们回到一开始所给出的 `Hello World` 程序。


```tcl
#!/usr/bin/env -S wish -encoding utf-8
#Make a label "Hello World"
label .hello -text "Hello World"
pack .hello
```

这里是第二次给出这部分内容 -- 我（作者）想确保咱们知道，这是如何完成的。


{{#include ./hello_world.md:16:57}}


现在，咱们进一步了解各个小工具......
