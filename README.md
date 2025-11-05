## 其他人构建的Windows 版本的 ffs
https://github.com/abcdec/MinFFS/

.

.

.

.

第一类（公开能拿到的）

来自 wxWidgets 的：

wx/bitmap.h, wx/scrolwin.h, wx/panel.h, wx/window.h, wx/artprov.h, wx/combobox.h, wx/frame.h, wx/image.h
→ 解决方案：在 GitHub Actions 的 Windows runner 上安装 wxWidgets 对应版本，并在 VS 工程里设置好 include/lib 路径。

来自 FreeFileSync 官方 Source 里的：

zen/serialize.h, zen/zstring.h, zen/i18n.h, zen/file_error.h, zen/xml_io.h, zen/optional.h, zen/time.h, zen/error_log.h, zen/async_task.h

wx+/grid.h
→ 解决方案：确保你的 FreeFileSync.vcxproj 的 Additional Include Directories 把 FreeFileSync_7.0_Source.zip 解出来的 zen\ 和 wx+\ 加进去（路径正确对上）。

这批东西是“你已经合法拥有，只是 VS 没看到”的。

.

.

.

.

第二类（官方 7.0 Source 包里根本没有的）

头文件：

dll.h

源码：

..\..\zen\dst_hack.cpp（通过 /zen/dst_hack.cpp）

..\..\zen\privilege.cpp（通过 /zen/privilege.cpp）

..\..\wx+\mouse_move_dlg.cpp（通过 /wx+/mouse_move_dlg.cpp）

lib\shadow.cpp（通过 /lib/shadow.cpp、\lib\shadow.cpp）

lib\xml_base.cpp（通过 /lib/xml_base.cpp、\lib\xml_base.cpp）

ui\dir_name.cpp（通过 /ui/dir_name.cpp、\ui\dir_name.cpp）

ui\exec_finished_box.cpp（通过 /ui/exec_finished_box.cpp、\ui\exec_finished_box.cpp）

对于这批东西，基于目前能看到的情况，现实就是：

官方公开的 7.0 源码里没有这些文件；

你的 easybuild 工程里却把它们当成源码引用了；

所以它们要么：

曾经存在于作者的私有 Windows 代码里，从未随 Source 放出；

要么是很老版本的遗留文件名，后来被删/合并了，但工程文件没清理干净。

这就正好对应你说的第二类：

要么找原作者，要么去挖别的第三方移植（他们可能自己写过一份实现），再要么就自己读现在的代码，手搓一个功能等价的替代实现。
