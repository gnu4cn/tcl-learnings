# 附录

## 附录 C：Unix 中的 Tcl/Tk

如果想要在 Unix 或 Linux 中使用 Tcl/Tk，那么咱们的选择是正确的。Tcl/Tk 是专为这些操作系统创建的，与 Windows 或 Mac 相比，在这些操作系统中使用更简洁。虽然本教程主要面向 Windows 用户，但我（作者）认为可以在此添加有关 Unix 的说明。


首先确保咱们同时拥有 `tcl` 和 `tk`。使用 `rpm -q tcl tk` 命令（在基于 Debian 的系统上，使用 `apt search tcl tk`），进行验证。大多数发行版都有 Tcl，但有些发行版没有 `tk`。如果没有 `tcl` 或 `tk`，请从发行版光盘或从 www.rpmfind.net 下载安装这些软件包（`apt install -y tcl tk`）。


现在确保第一行 -- `#!/usr/local/bin/wish`（例如）正确指向 `wish` 可执行文件。在不同的系统中，这可能会发生变化。因此，最好的办法是使用另一种方法。与其直接指向可执行文件，不如将脚本文件作为参数来执行 `wish`。这可以通过以下命令来实现...

```tcl
#!/bin/sh
#The next line executes wish - wherever it is \
exec wish "$0" "$@"
```


> **注意**：这种写法在 Ubuntu 20.04 上，会报出如下错误：

```bash
lenny.peng@sta-fpga-b:~/tk_demos$ ./hello_world.tcl
Error in startup script: can't read "0": no such variable
    while executing
"exec wish "$0" "$@""
    (file "./hello_world.tcl" line 4)
```

更好的写法，应是：`#!/usr/bin/env wish`。
