# 一些常见的小部件选项


必须用任何的粗体字，替换其中大写字母。请查阅手册，了解所有选项。同时确保咱们正使用的小部件，支持正使用的选项。

- `-anchro POSITION`，将小部件置于相对位置：`n`、`ne`、`nw`、`s`、`se`、`sw`、`e`、`w` 或 `center`；

- `-background COLOR`，背景色；

- `-bitmap BITMAP`，显示一张小图片。`BITMAP` 必须是 `error`、`gray12`、`gray25`、`gray50`、`gray75`、`hourglass`、`info`、`questhead`、`question`、`warning` 或 `@filename`；

- `-borderwidth WIDTH`，边框宽度。选择 `0` 将隐藏边框；

- `-command SCRIPT`，在调用时执行 `SCRIPT`；

- `-cursor CURSOR`，当鼠标在该部件中时，要显示的鼠标光标；

- `-disabledforeground COLOR`，当该小部件被禁用时的前景色；

- `-font FONTNAME`，用于文本样式的字体名称。以这种格式给出：`FONTNAME SIZE STYLE`。比如：`-font "fixed 12 bold"`；

- `-geometry WIDTHXHEIGHT`，可用于设置水平（同时可选的垂直）方向上的小部件尺寸；

- `-height VALUE`，设置小部件的垂直高度；

- `-image IMAGE`，显示在小部件中的图片；

- `-justify JUSTIFICATION`，**多行**（文本）的对齐方式：`left`、`right` 或 `center`；

- `-orient ORIENTATION`，针对诸如刻度盘或滚动条这样的对象。必须是 `horizontal` 或 `vertical`（或 `h`/`v`）；

- `-padx NUMBER`，水平填充。给定小部件顶部与底部的空间。例如：`-padx 5`；

- `-pady NUMBER`，垂直填充。这是指定小部件两侧的空间。例如，`-pady 2`；

- `-relief RELIEF`，3D 的斜面边框 - `RELIEF` 必须是 `flat`（屏幕）、`groove`（凹槽）、`raised`（凸起）、`ridge`（脊）、`solid`（实心）或 `sunken` （凹陷）。用到框架时非常有用；

- `-state STATE`，将小部件设置为：`normal`、`disabled` 或 `active`；

- `-text STRING`，显示文本字符串；

- `-variable VARNAME`，显示文本变量。如果对小部件进行了操作，那么变量的值将会自动改变，如果该变量的值发生变化，小部件也会随之改变，以反映变量变化；

- `-underline CHAR`，字符串中要加下划线的字符位置。这必须是一个数字 -- `0` 表示第一个字符，`1` 表示第二个字符，以此类推；

- `-width WIDTH`，设置小部件的水平尺寸；

- `-wraplength LENGHT`，单词换行的最大字符长度，word wrapping maximum string length；
