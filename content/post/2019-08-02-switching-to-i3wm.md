---
title: "再见，Xmonad；你好，i3wm"
date: 2019-08-02T16:00:00+08:00
---

![void desktop or wallpaper](/images/2019/08/02/wallpaper.png)
在用了一段时间 Xmonad 以后，我还是决定将 i3wm，确切说是 i3-gaps 作为了我的窗口管理器。

Xmonad 是个相当理想的窗口管理器，其配置相当灵活强大，囊括众多细节，然而也就是这点让我离开了它。

**对我来讲，过于复杂，学习成本太高了…**

不得不承认，Haskell 是一门十分优秀的语言，从 Xmonad —— 由它写作的应用之一中也可见一般，然而，我并不希望做一点很小的事（或者说，已知可用其它应用很简单就实现）就需要查阅大量的文档——这对于我本来就很缺乏的精力来讲无疑是一种“毁灭”。

相较而言，i3wm 更加容易上手一些（尽管没有那么灵活强大）：对配置文件无须再有多余的学习，几乎是一眼就能看懂；不需要各种引入功能，直接在很“宏观”的层面上去做就是了。i3-gaps 是 i3wm 的一个 fork，带有窗口间隔的功能（其实这也说明了 i3wm 的缺点：功能不足，自认为，Xmonad 的配置过程像是在“创作”，因为可以利用的东西太多，而 i3wm 的配置过程更像是对着图纸搭积木）。这里是我的[配置文件](https://gist.github.com/rakino/b9f8f0fe1126f7c70d454c4e9f23bb47)。

这次试着使用 KiTTY 作为终端模拟器，它在键盘操作方面十分不错，不久以后我就能登入一台服务器了，有这样一个完美的本地终端模拟器 + 远程终端连接器还是十分不错的。（update: KiTTY 使用 ssh 存在某些问题，也许以后会讲解决方案）

配合着 pywal 自动根据桌面背景更改 shell 配色，~~我就再也不用担心自己搞的瞎了眼的配色了。~~

大概就是这样，以下附图！~~（图片可点击）~~（已关闭 Fancybox）

![single terminal](/images/2019/08/02/single-terminal.png)

![multiple terminal](/images/2019/08/02/multiple-terminal.png)

![editing i3 config file under vim](/images/2019/08/02/editing-i3-config-file-under-vim.png)

![ranger previewing image](/images/2019/08/02/ranger-previewing-image.png)

![firefox](/images/2019/08/02/firefox.png)
