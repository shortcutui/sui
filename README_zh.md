# SUI

Shortcut User Interface to control apps with keyboard.

[English Version](./README.md)

## 简介

SUI全称(Shortcut User Interface)是一个快捷键用户接口, 它吸收了emacs和vim的快捷键设计思想,
提取出一些在日常使用软件中各个软件常用且共有的操作, 并给这些操作设计了一个易于学习,易于理解, 易于按下的快捷键.

SUI目前在三大主流操作系统和各主流浏览器上都易于实现. 能够实现SUI的软件和网站称为SUI兼容的.

## 动机

我之前是一个普通的GUI用户, 在某一天发现右手摸鼠标的时候手指有点发麻, 同时左手的小拇指也感觉按ctrl有些发麻,因此不得不使用
全键盘来操作电脑, 现有的按键规范有3种主流的, 一种是emacs的ctrl+x开头跟一系列按键, 一种是vim的模式按键, 还有一种是有些软件
自带的菜单按键, 是alt+一个字母开头, 再跟一系列按键, 或者上下左右来浏览菜单.

这些按键都有些各自的缺点, emacs按键太过长, 稍微多一点操作都要3个按键, vim的模式编译很难应用在gui的软件, 软件带的菜单在各
软件不通用, 并无法方便的应用在窗口管理器和浏览器中.

## SUI相关的仓库

下面的仓库是实现了sui的操作系统或者应用软件, 或者是web应用.

- [shortcutui/windows](https://github.com/shortcutui/windows)
- [shortcutui/macos](https://github.com/shortcutui/macos)
- [shortcutui/wezterm](https://github.com/shortcutui/wezterm)
- [shortcutui/tmux](https://github.com/shortcutui/tmux)
- [shortcutui/browser](https://github.com/shortcutui/browser)
- [shortcutui/yazi](https://github.com/shortcutui/yazi)
- [shortcutui/neovim](https://github.com/shortcutui/neovim)
- [shortcutui/vscode](https://github.com/shortcutui/vscode)
- [shortcutui/idea](https://github.com/shortcutui/idea)

## 名词解释和按键约定

在SUI中, 在圆括号中括起来的代表一个按键序列, 例如(a)代表按下了键盘上的a键, (a b)代表先按下a键, 并在较短的时间内按下b键.
加号代表同时按下, 比如(ctrl+a)代表同时按下ctrl键和a键, (ctrl+alt+a)代表同时按下ctrl键和alt键和a键. 除了在vim这种模式编辑
的场景, 这时的(leader+a)可能代表先按下leader键, 然后短时间内按下a键.

leader键在不同的应用中代表不同的按键, SUI根据应用的特性将其分成几类, 不同类型的应用使用不同的按键作为leader键.

- 窗口管理器(ctrl)         这个每个操作系统只有一个, 是最普遍的接口
- 普通GUI的app(alt)
- 浏览器或者其它可以远程连接ssh的终端app(ctrl+alt)
- 远程终端上的窗口管理器(ctrl+alt)
- 普通TUI的app(无, 或者vim模式中的leader)

SUI推荐通过用左右手的手掌来按ctrl和ctrl+alt, 把右ctrl映射给ctrl+alt, 并且Capslock如果和其它按键一起按的时候也推荐将其
映射为某一个组合键. 这个依据您的键盘布局和手掌分布, 您可以自由选择leader是什么以及怎么按leader.

SUI所有的快捷键都是(leader+字符 字符 字符)这种按键形式, 如果leader键是ctrl或者alt这种按键, 那么按后面的字符时,leader有
没有松开都应该映射为同一个操作. 并且除了leader键以外, SUI应该只使用0-9的数字和a-z的字母加上少量的其它字符, 并应尽量避免
使用大写字母, 如果需要使用大写字母, 那么必须保证大写字母和小写字母的功能类似或者相关, 是其中的一个很自然的变体.

目前SUI只使用了3个字符, 分别为逗号代表最近的, 句号代表任意的, 斜杆代表搜索.

? 代表所有sui中该章节未定义的字符, 比如在[space接口]中, (space+?)代表所有未在SUI的space接口中定义的字符.

SUI可以很好的在标准的qwerty布局和我正在使用的norman布局上工作, 其它布局可能需要稍微修改一下.

## SUI接口导航

- [space接口](#space接口)

## space接口

```clojure
(space+j) = (left)
(space+l) = (right)
(space+i) = (up)
(space+k) = (down)
(space+s) = (home)
(space+f) = (end)
(space+e) = (pageup)
(space+d) = (pagedown)

(space+h) = (enter)
(space+o) = (backspace)
(space+.) = (delete)

(space+?) = any other key or operation what you like
```

## backup interface

```clojure
(ctrl+b j) = 移动到左边的窗口或者tab
(ctrl+b l) = 移动到右边的窗口或者tab

(ctrl+b .) = 打开应用自身的快捷命令窗口
(ctrl+b q) = quit current window
(ctrl+b r) = reload current window
```

## mouse interface

```clojure
(ctrl+n)  = enter mouse mode
({mouse mode q}) = leave mouse mode
({mouse mode esc}) = leave mouse mode

({mouse mode j}) = mouse move left
({mouse mode l}) = mouse move right
({mouse mode i}) = mouse move up
({mouse mode k}) = mouse move down
({mouse mode s}) = mouse left button
({mouse mode f}) = mouse [click] right button
({mouse mode e}) = mouse wheel up
({mouse mode d}) = mouse wheel down

({mouse mode n}) = focus current window, mouse click current window then leave mouse mode
({mouse mode x}) = mouse [click] middle button
({mouse mode w}) = mouse [click] forward button
({mouse mode r}) = mouse [click] backword button
({mouse mode c}) = mouse wheel left
({mouse mode v}) = mouse wheel right
({mouse mode h}) = hide cursor
({mouse mode o}) = show cursor
({mouse mode space}) = move to screen center
```

## editline interface

```clojure
(ctrl+e)    =  enter edit mode

({edit mode j}) = delete backword word
({edit mode J}) = move backword word
({edit mode l}) = delete forward word
({edit mode L}) = move forward word
({edit mode s}) = delete to home then leave edit mode
({edit mode f}) = delete to end then leave edit mode

({edit mode d}) = delete hole line then leave edit mode
({edit mode y}) = copy line then leave edit mode
({edit mode u}) = undo
({edit mode U}) = redo
({edit mode q}) = quote a word
({edit mode Q}) = quote hole line
({edit mode * except predefined}) = user defined by self or print char then leave edit mode
```

## misc interface

```clojure
ctrl zxcva  按照windows平台的规则, 不变
(alt+z *) = (alt+*)
(alt+x *) = (ctrl+*)
(alt+c)   = mouse wheel scroll left
(alt+v)   = mouse wheel scroll right
(alt+a *) = application layer user defined operation
(alt+a .) = show application layer user defined operation

(ctrl+u) = user defined favorite
(ctrl+alt+u) = user defined app favorite
(alt+u) = user defined app favorite
```


## 分层接口

### fallthrough interface

```clojure
(leader+f) = enter fallthrough mode
(leader+shift+f) = leave fallthrough mode
```

### launch interface

```clojure
(leader+l .) = launch command palette or launch menu
(leader+l l) = launch user favorite
(leader+l r) = launch reload (if config change, some app need restart)
(leader+l v) = launch anything in vertical window
(leader+l h) = launch anything in horizontal window
(leader+l t) = launch anything in other tab
(leader+l s c) = launch system config
(leader+l s m) = launch system keymap
(leader+l s h) = launch system help
(leader+l s i) = launch system info
```

### quit interface

```clojure
(leader+q .) = search to quit
(leader+q q) = quit current window (Upper case will force quit)
(leader+q t) = quit current tab (Upper case will force quit)
(leader+q a) = quit all (Upper case will force quit)
(leader+q u) = undo quit
(leader+q s) = let current window single (quit other windows)
(leader+q S) = let current tab single (quit other tabs)

(leader+q j) = quit left window
(leader+q l) = quit right window
(leader+q i) = quit up window
(leader+q k) = quit down window
```

### focus interface

```clojure
(leader+j) = focus left
(leader+l) = focus right
(leader+i) = focus up
(leader+k) = focus down
(leader+w space+j) = focus left (if only one window, user can focus prev tab)
(leader+w space+l) = focus right (if only one window, user can focus next tab)
(leader+w space+i) = focus up (if only one window, user can focus prev tab)
(leader+w space+k) = focus down (if only one window, user can focus next tab)
(leader+space+j) = focus left tab
(leader+space+l) = focus right tab
(leader+space+i) = focus(toggle) float layer
(leader+space+k) = focus(toggle) tiled layer
(leader+t space+j) = focus left tab

(leader+t space+k) = focus(toggle) tiled layer

(leader+w .) = search to focus
(leader+w ,) = focus recent window
(leader+w ?) = focus user defined window
(leader+t .) = search to focus
(leader+t ,) = focus recent tab
(leader+t ?) = focus user defined tab
(leader+d .) = search to deliver
(leader+d ?) = deliver current window to user defined tab
(leader+d left) = deliver current window to left tab
(leader+d right) = deliver current window to right tab

(ctrl+/) = window manager find widgets
(alt+/) = app find some thing

(shift+up)       操作第二个窗口里的光标向上
(shift+down)     操作第二个窗口里的光标向下
(shift+left)     操作第二个窗口里的光标向左
(shift+right)    操作第二个窗口里的光标向右
(shift+pageup)   操作第三个窗口里的光标向上
(shift+pagedown) 操作第三个窗口里的光标向下
(shift+home)     操作第三个窗口里的光标向左
(shift+end)      操作第三个窗口里的光标向右
```

### goto interface

```clojure
(leader+g .) = search to go
(leader+g ,) = go recent
(leader+g j) = go back
(leader+g l) = go forward
(leader+g d) = goto define
(leader+g r) = goto reference
(leader+g t ?) = goto user defined resource
```

### move interface

```clojure
(leader+m j) = move window left
(leader+m l) = move window right
(leader+m i) = move window up
(leader+m k) = move window down
(leader+m space+j) = move tab left
(leader+m space+l) = move tab right
(leader+m space+i) = move window to float layer
(leader+m space+k) = move window to tiled layer

(leader+m f) = toggle window float
```

### size interface
```clojure
(leader+s j) = window size inc left
(leader+s l) = window size inc right
(leader+s i) = window size inc up
(leader+s k) = window size inc down

(leader+s m) = toggle window maximize
(leader+s z) = toggle window zenmode
(leader+s h) = set window hide
(leader+s w) = change window name
(leader+s t) = change tab name
(leader+s u) = change some thing up
(leader+s d) = change some thing down
(leader+s s) = change some thing default

(leader+s * except predefined) = user defined window or change related operation
```

## 极简模式

| 顶层字符(一般和ctrl或者alt一起按下) | 意义                  | 叫法                |
| -------------                       | --------------        | --------------      |
| ,                                   | 最近                  | comma/逗号          |
| .                                   | 任意                  | dot/句号            |
| /                                   | 搜索                  | slash/斜杆          |
| ikjl                                | 上下左右              | 小上,小下,小左,小右 |
| edsf                                | pgup, pgdn, home, end | 大上,大下,大左,大右 |
| ctrl+azxcv                          | 保持不变              |                     |
| y                                   | yank/拷贝             |                     |
| e                                   | edit/编辑             |                     |
| q                                   | quit/退出             |                     |
| l                                   | launch/启动,新建      |                     |
| w                                   | window/窗口           |                     |
| t                                   | tab/标签              |                     |
| s                                   | size,change/大小变化  |                     |
| m                                   | move/移动             |                     |
| d                                   | deliver/投递          |                     |
| b                                   | backup/备份           |                     |
| n                                   | 鼠标                  |                     |
| g                                   | goto, 粘贴            |                     |

第二层字母的意义
| 第二层字符    | 意义            |
| ------------- | --------------  |
| v             | vertical        |
| h             | horizontal/hide |
| m             | maximize        |
| z             | zen             |
| u             | up              |
| d             | down            |
| s/S           | single          |
| n             | name/new        |
| p             | path            |
| i             | info            |
| r             | reset/reload    |

## 编辑器相关接口

TODO sui
