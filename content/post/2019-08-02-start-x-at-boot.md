---
title: "登入后直接进入 X"
date: 2019-08-02T08:00:00+08:00
---

大概我没有办法完全活在 TTY 下吧。

那样的话每次登入后都要手动输入一次 `startx` 又有什么意思？

登录管理器？不行，有点浪费资源！

那我就用其它方法吧

## 原料
* `xinit`，`~/.xinitrc` 已配置好
* `bash` or `zsh` or `fish`

## 具体操作
对于 `bash`，需要修改 `~/.bash_profile`；而 `zsh` 则是 `~/.zlogin` 或 `~/.zprofile`。在上述文件中加入一行即可

``` shell
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx
```

`&&` 表示逻辑与；`[[ ]]` 为条件表达式，返回值为 0 或 1 。

此语句指：当 `$DISPLAY`（是否已打开显示）为零且 `$XDG_VTNR`（现在所处虚拟控制台号码）等于 1 时，（且）执行 `startx`

fish 中则是在 `~/.config/fish/config.fish` 中加入以下内容

``` shell
# start X at login
if status --is-login
  if test -z "$DISPLAY" -a $XDG_VTNR = 1
    exec startx
  end
end
```

`test` 和 `[[ ]]` 用法相似。

~~可以每次开机少打一行字了ww~~

## 参考
[Autostart X at login](https://wiki.archlinux.org/index.php/Xinit#Autostart_X_at_login) - Arch Wiki
