---
title: "更加丰富多彩的 ls 输出"
date: 2019-07-11T08:00:00+08:00
draft: true
---

作为一个 ls 高度依赖者, 我的 shell 历史记录里总是充满 “ls” 的字样，我甚至还在思想放空的时候不由自主敲着 “ls”，显然 ls 已经成了我生活中的一部分了。

即便有 --color=auto 的加成, 在图形界面下却总是面对着纯文本的环境多少还是有些叫人乏味；当我了解到还有更加多彩（没错, 我喜欢鲜艳颜色）并且能同时输出与文件相对应的图标 (由一个字符充当) 时, 我立刻心动了。

最开始我找到了 [colorls](https://github.com/athityakumar/colorls#installation), 但由于安装 colorls 需要同时安装一些 ruby 依赖，我就放弃了尝试（我不希望安装一些不一定用得上的软件）。

![lsd](images/2019/07/11/screen_lsd.png)

随后我发现了一个相似项目，[lsd](https://github.com/Peltoche/lsd)（上图），它是受到了 colorls 启发的，据称相较于 colorls 速度更快，且没有多余的依赖，这对我而言是很好的。

在安装了 lsd 后，我在显示图标上遇到了麻烦；这是字体不足造成的，只需安装相应字体即可。

我选择了一个十分齐全的字体集合 `nerd-fonts-complete`（[AUR](https://aur.archlinux.org/packages/nerd-fonts-complete/) 及 [Github](https://github.com/ryanoasis/nerd-fonts)，在 Arch Linux CN 源中也有包括该包），这样我就不必再遇到更多麻烦了。

接下来就是替代 ls 了（其实也不算替代）， 只需要在 shell 配置文件中写下这行设置 ls 的别名即可：
    alias ls='lsd'

另外一些有用的别名：
    alias l='ls -l'
    alias la='ls -a'
    alias lla='ls -la'
    alias lt='ls --tree'
