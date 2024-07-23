# 数字输入小部件

## `scale`

构造出一个可由用户调整的滑块，用于输入变量。


**部分选项**

| 选项 | 说明 |
| :-- | :-- |
| `-from NUMBER` | 开始数字。 |
| `-to NUMBER` | 结束数字。 |
| `-tickinterval NUMBER` | 确定在滑块下方或左侧，所显示数字刻度线之间的间距。 |
| `-varable NAME` | 指定了链接到刻度盘的全局变量名称。每当变量值发生变化时，刻度盘就会更新以反映该值。无论何时对刻度盘进行交互式操作，该变量都将被修改，以反映刻度盘的新值。 |


**部分命令**

| 语法 | 说明 | 示例 |
| `path get` | 获取刻度盘的当前值。 | `set age [.scl get]` |
| `path set value` | 给刻度盘一个新值。 | `.scl set 20` |


**示例**


```tcl
#This function will be executed when the button is pushed
proc push_button {} {
	global age
	set name [.ent get]
	.txt insert end "Hello, $name.\nYou are $age years old."
}

#Global Variables
set age 10

#GUI building
frame .frm -relief groove
label .lab -text "Enter name:"
entry .ent -width 48

button .but -text "Push Me" -command "push_button"

#Age
scale .scl -label "Age :" -orient h -digit 1 -from 10 -to 50 \
	-variable age -tickinterval 5 -length 640

#Text Area
frame .textarea
text .txt -yscrollcommand ".srl_y set" -xscrollcommand ".srl_x set" \
	-width 48 -height 10
scrollbar .srl_y -command ".txt yview" -orient v
scrollbar .srl_x -command ".txt xview" -orient h

#Geometry Management
pack .lab -in .frm
pack .ent -in .frm
pack .frm

pack .scl
pack .but

grid .txt   -in .textarea -row 1 -column 1
grid .srl_y -in .textarea -row 1 -column 2 -sticky ns
grid .srl_x -in .textarea -row 2 -column 1 -sticky ew
pack .textarea
```

现在，我们的小例子越来越像一个程序。因为他变得越来越大，难以理解，咱们已经添加了注释。现在我们添加了一个滑块，可以输入年龄。咱们可能也注意到了，这里增加了一行 `global age`。这不是地球的年龄，也不是每个人类年龄的总和。他表示变量 `age` 应从全局作用域，移至那个 `push_button` 函数的作用域。

## `spinbox`

这个小工具就像右侧有两个，用于增加或减少输入区域显示数字的按钮的 [输入 `entry` 小部件](#entry)。请看下面的示例 -- 在这个示例中，我（作者）尝试用 HTML 创建一个起作用的输入小部件。这不是一张精确的图片，但却是他在 HTML 中能做到的最好的。单击右侧的任一箭头，便可增加或减少数字。

<table>
    <tr>
        <td rowspan="2"><input name="txt" id="txt" type="text" value="1" /></td>
        <td class="button_type" onClick="incr()">^</td>
    </tr>
    <tr>
        <td class="button_type" onClick="decr()">v</td>
    </tr>
</table>

<script language="Javascript" type="text/javascript">
<!--
function incr() {
	var txt=document.getElementById('txt');
	var val = txt.value;
	val++;
	txt.value = val;
}
function decr() {
	var txt=document.getElementById('txt');
	var val = txt.value;
	val--;
	if(val >= 0) txt.value = val;
}
//-->
</script>


**部分选项**


| 选项 | 说明 |
| :-- | :-- |
| `-from NUMBER` | 起始数字。输入字段中的数值，不能低于该数字。 |
| `-to NUMBER` | `NUMBER` 是上限。输入字段中的值，不能超过该数值。 |
| `-increment NUMBER` | 与 `-from` 和 `-to` 一起使用时，当按下旋转按钮时，小部件中的值，将以 `-increment` 方式进行调整（向上增加值，向下减少值）。默认为 `1`。 |


**示例**

```tcl
set number 5

spinbox .spn -from 0 -to 100 -increment 5 -textvariable number
scale .scl -label {Number:} -orient h -digit 1 -from 0 -to 100 \
	-variable number -tickinterval 10 -length 640

pack .spn .scl
```

