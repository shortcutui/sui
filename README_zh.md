# SUI

控制电脑和网页app的快捷键用户接口.

[English Version](./README.md)

## 简介

SUI全称(Shortcut User Interface)是一个快捷键用户接口, 它吸收了emacs和vim的快捷键设计思想,
提取出一些在日常使用软件中各个软件常用且共有的操作, 并给这些操作设计了一个易于学习,易于理解, 易于按下的快捷键.

SUI目前在三大主流操作系统和各主流浏览器上都易于实现. 能够实现SUI的软件和网站称为SUI兼容的.

## 动机

我之前是一个GUI用户, 在某一天发现右手摸鼠标的时候手指有点发麻, 同时左手的小拇指也感觉按ctrl有些发麻,因此不得不想办法使用
全键盘来操作电脑, 现有的按键规范有3种主流的, 一种是emacs的ctrl+x开头跟一系列按键, 一种是vim的模式按键, 还有一种是有些软件
自带的菜单按键, 是alt+一个字母开头, 再跟一系列按键, 或者上下左右来浏览菜单.

这些按键都有些各自的缺点, emacs按键太过长, 稍微多一点操作都要3个按键, vim的模式编译很难应用在gui的软件, 软件带的菜单在各
软件不通用, 并无法方便的应用在窗口管理器和浏览器中.

通过一些研究和思考, 在日常使用软件的过程中, 不管是gui的还是tui的, 或者是网站, 我发现绝大多数情况,
不得不用鼠标的原因都是由于没有办法通过键盘去定位到某个窗口或者某个菜单. 如果能够通过快捷键方便的切换窗口, 那么app的其它大部分功能都能通过上下左右或者一些其他的按键来完成.

## SUI相关的仓库(TODO)

下面的仓库是实现了sui的操作系统或者应用软件, 或者是web应用. 能够实现sui基本接口的应用叫做sui兼容的.

这些应用有些是我日常重度使用的, 例如wezterm,browser,yazi还有neovim, 这些我后面会陆续脱敏放出来.


- [shortcutui/windows](https://github.com/shortcutui/windows)
- [shortcutui/macos](https://github.com/shortcutui/macos)
- [shortcutui/wezterm](https://github.com/shortcutui/wezterm)
- [shortcutui/browser](https://github.com/shortcutui/browser)
- [shortcutui/yazi](https://github.com/shortcutui/yazi)
- [shortcutui/neovim](https://github.com/shortcutui/neovim)
- [shortcutui/vscode](https://github.com/shortcutui/vscode)
- [shortcutui/idea](https://github.com/shortcutui/idea)
- [shortcutui/lazygit](https://github.com/shortcutui/lazygit)
- [shortcutui/lazydocker](https://github.com/shortcutui/lazygit)
- [shortcutui/tmux](https://github.com/shortcutui/tmux)

## 名词解释和按键约定

在本文中, 在圆括号中括起来的代表一个按键序列, 例如(a)代表按下了键盘上的a键, (a b)代表先按下a键, 并在较短的时间内按下b键.
加号代表同时按下, 比如(ctrl+a)代表同时按下ctrl键和a键, (ctrl+alt+a)代表同时按下ctrl键和alt键和a键. 除了在vim这种模式编辑
的场景, 这时的(leader+a)可能代表先按下leader键, 然后短时间内按下a键.

leader键在不同的应用中代表不同的按键, SUI根据应用的特性将其分成几类, 不同类型的应用使用不同的按键作为leader键.
下面是一个leader设置的例子. 后面括号中代表它们所使用的leader键

- 窗口管理器(ctrl)
- 普通GUI的app(alt)
- 浏览器或者其它可以远程连接ssh的终端app(ctrl+alt或者无)
- 远程终端上的窗口管理器(alt)
- 普通TUI的app(无, 或者vim模式中的leader)

SUI推荐通过用左右手的手掌来按ctrl和ctrl+alt, 把右ctrl映射给ctrl+alt, 并且Capslock如果和其它按键一起按的时候也推荐将其映射为某一个组合键. 这个依据您的键盘布局和手掌分布, 您可以自由选择leader是什么以及怎么按leader.

SUI所有的快捷键都是(leader+字符 字符 字符)这种按键形式, 如果leader键是ctrl或者alt这种按键, 那么按后面的字符时,leader有
没有松开都应该映射为同一个操作. 并且除了leader键以外, SUI应该只使用0-9的数字和a-z的字母加上少量的其它字符, 并应尽量避免
使用大写字母, 如果需要使用大写字母, 那么必须保证大写字母和小写字母的功能类似或者相关, 是其中的一个很自然的变体.

目前SUI除了编辑器接口以外只使用了3个非英文字母的符号, 分别为逗号代表最近的, 句号代表任意的, 斜杆代表搜索.

? 代表所有sui中该章节未定义的字符, 比如在[space接口](#space-interface)中, (space+?)代表所有未在SUI的space接口中定义的字符. 一般这些字符是留给用户自定义的.

SUI的按键定义是用qwerty的键盘布局来定义的, 其中有几个按键比较特殊, 它们是根据位置来定义的,分别是jlik(左右上下)
和sfed(home,end,pageup,pagedown). 其它的字母, 会努力找到对应的英文单词来帮助记忆. 并且同一个字母在不同的应用中应该代表相近的意思.

没有特殊说明, SUI按下第一个组合按键以后, 会短暂或者永久的进入到一个组合按键的模式, 按esc或者q可以退出该模式,
如果按下sui中定义的按键, 都会退出该组合模式, 如果该模式是永久的, 那么({x mode} a)代表在x模式下按下按键a, 并且无说明的
情况下, 按下a会执行对应操作并不会退出x模式.

SUI可以很好的在标准的qwerty布局和我正在使用的norman布局上工作, 其它布局可能需要稍微修改一下.

## 视频演示

我在bilibili录制了一个[视频](https://www.bilibili.com/video/BV14w4m1q7YQ/)来说明一些sui现在在我电脑上的使用情况.

## SUI接口

SUI根据接口的作用不同将其分为不同的接口, 并使用不同的按键作为第一个按键.相同类型的接口往往有相同的作用.

所有的接口表示为(key) = value, 其中 (key) 代表在键盘按下的按键序列, value表示实际输出的按键或者某一个操作.

- [space interface](#space-interface)
- [backup interface](#backup-interface)
- [mouse interface](#mouse-interface)
- [editline interface](#editline-interface)
- [zxcva interface](#zxcva-interface)
- [uniq interface](#uniq-interface)
- [fallthrough interface](#fallthrough-interface)
- [open interface](#open-interface)
- [quit interface](#quit-interface)
- [focus interface](#focus-interface)
- [goto interface](#goto-interface)
- [move interface](#move-interface)
- [size interface](#size-interface)
- [copy&paste interface](#copy&paste-interface)
- [eidtor interface](#editor-interface)

### space interface

space接口主要用于把常用的上下左右键和功能键映射到主键盘区域.

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

(space+?) = 任意你自定义的按键或者操作
```

### backup interface

backup接口主要用于那些能够在大部分情况下用sui来操作的app, 小部分情况下无法使用sui, 此时确又不希望用fallthrough接口时使用.

```clojure
(ctrl+b j) = 移动到左边的窗口或者tab
(ctrl+b l) = 移动到右边的窗口或者tab
(ctrl+b i) = 移动到上边的窗口或者tab
(ctrl+b k) = 移动到下边的窗口或者tab
(ctrl+b .) = 打开应用自身的快捷命令窗口
(ctrl+b q) = 退出当前窗口
(ctrl+b r) = 重新加载当前窗口

(ctrl+b ?) = 任意你自定义的按键或者操作
```

### mouse interface

这个接口模拟鼠标操作, 用在特殊的没适配sui的app.

```clojure
(ctrl+n)  = 进入 mouse mode
({mouse mode} q) = 离开 mouse mode
({mouse mode} esc) = 离开 mouse mode

({mouse mode} j) = 鼠标左移(按住ctrl时鼠标移动变慢并且恒速)
({mouse mode} l) = 鼠标右移(按住ctrl时鼠标移动变慢并且恒速)
({mouse mode} i) = 鼠标上移(按住ctrl时鼠标移动变慢并且恒速)
({mouse mode} k) = 鼠标下移(按住ctrl时鼠标移动变慢并且恒速)
({mouse mode} s) = 鼠标左键
({mouse mode} f) = 点击鼠标右键
({mouse mode} e) = 鼠标滚轮上
({mouse mode} d) = 鼠标滚轮下

({mouse mode} n) = 鼠标点击当前关注的窗口的中央,防止某些丢失焦点的情况,然后离开mouse mode
({mouse mode} x) = [点击]鼠标中键
({mouse mode} w) = [点击]鼠标前进键
({mouse mode} r) = [点击]鼠标后退键
({mouse mode} c) = 鼠标滚轮左
({mouse mode} v) = 鼠标滚轮右
({mouse mode} h) = 隐藏鼠标
({mouse mode} o) = 显示鼠标
```

### editline interface

这个接口就是用来编辑某一行的内容.

```clojure
(ctrl+e)    =  enter edit mode

({edit mode} j) = 向前删除一个单词
({edit mode} J) = 向前移动一个单词
({edit mode} l) = 向后删除一个单词
({edit mode} L) = 向后移动一个单词
({edit mode} s) = 向前删除到行首,然后离开 edit mode
({edit mode} f) = 向后删除到行首,然后离开 edit mode

({edit mode} d) = 删除整行，然后离开 edit mode
({edit mode} y) = 拷贝整行，然后离开 edit mode
({edit mode} u) = 撤销
({edit mode} U) = 反撤销
({edit mode} q) = 给前面的单词加上引号
({edit mode} Q) = 给整行加上引号
({edit mode} ,) = 切换到另一个 editline mode, 在你发现当前的操作不起作用的时候
({edit mode} ?) = user defined by self or print char then leave edit mode
```

### zxcva interface


```clojure
(ctrl+zxcva)  按照windows平台的规则起作用
(alt+z ?) = (ctrl+?) 如果是mac平台是 (cmd+?)
(alt+x ?) = (alt+?)
(alt+c)   = 鼠标滚轮向左
(alt+v)   = 鼠标滚轮向右
(alt+a .) = 显示应用层用户自定义的快捷键的菜单
(alt+a ?) = 应用层用户自定义的快捷键

```
### uniq interface

这个接口给某些应用, 有一些不好归类又用的比较经常的功能按键, 或者需要一直按着不方便设计成按键序列的功能.
或者叫做快捷键的快捷键, 有些快捷键你可以定义在 alt a 里面, 但是你还想要它更加的快可以设置成 uniq interface.
```clojure
(ctrl+u) = 最常用的, 我目前是给了 tts
(ctrl+alt+u) = 最常用的或者唯一的
(alt+u) = 最常用的或者唯一的
```

### fallthrough interface

在fallthrough mode, 所有该leader开头的按键都会原样输出. 也就是说, 在窗口管理出去中, 摁下 ctrl+f 以后, 所有的以 control 开头的快捷键，都是原样的发送给 App,除非摁下 control+shift+f 才能够解除    这个接口主要设计给还没有实现 sui 的应用.

```clojure
(leader+f) = 进入 fallthrough mode
(leader+shift+f) = 离开 fallthrough mode
```

### open interface

```clojure
(leader+o .) = 打开命令面板或者菜单
(leader+o o) = 最常用的打开操作
(leader+o r) = 重新加载配置或者重启 App
(leader+o v) = 在垂直窗口打开某个资源
(leader+o h) = 在水平窗口打开某个资源
(leader+o t) = 在新的 tab 打开某个资源
(leader+o s c) = 打开app配置
(leader+o s m) = 打开app快捷键
(leader+o s h) = 打开app帮助
(leader+o s i) = 打开app信息面板
(leader+o ?) = 打开用户自定义的资源
```

### quit interface

```clojure
(leader+q .) = 搜索退出
(leader+q q) = 退出当前窗口(大写强制退出)
(leader+q t) = 退出当前 tab(大写强制退出)
(leader+q a) = 退出app
(leader+q u) = 撤销退出
(leader+q s) = 退出除当前窗口以外的其他窗口
(leader+q S) = 退出除当前 tab 以外的其他 tab

(leader+q j) = 退出左边窗口
(leader+q l) = 退出右边窗口
(leader+q i) = 退出上边窗口
(leader+q k) = 退出下边窗口
```

### focus interface

```clojure
(leader+j) = 聚焦到左边窗口(如果当前tab只有一个窗口,可以聚焦到左边tab也可以无操作)
(leader+l) = 聚焦到右边窗口(如果当前tab只有一个窗口,可以聚焦到右边tab也可以无操作)
(leader+i) = 聚焦到上边窗口(如果当前tab只有一个窗口,可以聚焦到浮动层也可以无操作)
(leader+k) = 聚焦到下边窗口(如果当前tab只有一个窗口,可以聚焦到平铺层也可以无操作)
(leader+w left) = 聚焦到左边窗口(如果当前tab只有一个窗口,可以聚焦到左边tab也可以无操作)
(leader+w right) = 聚焦到右边窗口(如果当前tab只有一个窗口,可以聚焦到右边tab也可以无操作)
(leader+w up) = 聚焦到上边窗口(如果当前tab只有一个窗口,可以聚焦到浮动层也可以无操作)
(leader+w down) = 聚焦到下边窗口(如果当前tab只有一个窗口,可以聚焦到平铺层也可以无操作)
(leader+left) = 聚焦到左边 tab
(leader+right) = 聚焦到右边 tab
(leader+up) = 聚焦到浮动层
(leader+down) = 聚焦到平铺层
(leader+t left) = 聚焦到左边 tab
(leader+t right) = 聚焦到右边 tab

(leader+w .) = 搜索窗口并聚焦
(leader+w ,) = 聚焦到最近的窗口
(leader+w ?) = 聚焦到用户定义的窗口
(leader+t .) = 搜索 tab 并聚焦
(leader+t ,) = 聚焦到最近的 tab
(leader+t ?) = 聚焦到用户定义的 tab
(leader+d .) = 搜索 tab 并把当前窗口移动到该 tab
(leader+d ?) = 把当前窗口移动到用户定义的 tab
(leader+d left) = 把当前窗口移动到左边的 tab
(leader+d right) = 把当前窗口移动到右边的 tab

(ctrl+/) = window manager find widgets
(alt+/) = app find some thing

; 下面的操作适用于很多，同时存在3个窗口的情况, 当我的焦点在其中一个主窗口时，我可以同时操作另外两个窗口
(shift+up)       操作第二个窗口里的光标或窗口向上
(shift+down)     操作第二个窗口里的光标或窗口向下
(shift+left)     操作第二个窗口里的光标或窗口向左
(shift+right)    操作第二个窗口里的光标或窗口向右
(shift+pageup)   操作第三个窗口里的光标或窗口向上
(shift+pagedown) 操作第三个窗口里的光标或窗口向下
(shift+home)     操作第三个窗口里的光标或窗口向左
(shift+end)      操作第三个窗口里的光标或窗口向右
```

### goto interface

前面的操作主要是针对窗口或者 tab，这个 goto interface 的操作主要针对于 App 所操作的资源. 或者是当前所在的位置.

```clojure
(leader+g .) = 搜索资源并跳转
(leader+g ,) = 跳转到最近的资源
(leader+g j) = 光标往回跳转
(leader+g l) = 光标往前跳转
(leader+g d) = 跳转到定义
(leader+g r) = 跳转到引用
(leader+g t ?) = 跳转到用户定义的特定资源
```

### move interface

```clojure
(leader+m j) = 窗口向左移动
(leader+m l) = 窗口向右移动
(leader+m i) = 窗口向上移动
(leader+m k) = 窗口向下移动
(leader+m left) = tab 向左移动
(leader+m right) = tab 向右移动
(leader+m up) = 移动窗口到浮动层
(leader+m down) = 移动窗口到平铺层

(leader+m f) = 切换窗口的浮动状态
```

### size interface

```clojure
(leader+s j) = 窗口往左增加或往右减少
(leader+s J) = 窗口往左减少或往右增加
(leader+s l) = 窗口往右增加或往左减少
(leader+s L) = 窗口往右减少或往右增加
(leader+s i) = 窗口往上增加或往右减少
(leader+s I) = 窗口往上减少或往右增加
(leader+s k) = 窗口往下增加或往右减少
(leader+s K) = 窗口往下减少或往右增加

(leader+s m) = 切换窗口最大化状态
(leader+s z) = 切换窗口zen mode
(leader+s h) = 隐藏或者最小化窗口
(leader+s w) = 修改窗口名字
(leader+s t) = 修改 tab 名字
(leader+s u) = 增加字体或声音大小
(leader+s d) = 减少字体或声音大小
(leader+s s) = 把字体或声音调整到默认大小

(leader+s ?) = 用户定义的窗口修改相关的操作
```

### copy&paste interface

用f代表当前光标或者窗口所关联的资源或者文件, 所有的资源都是文件. 资源或者文件都有路径,名字还有目录

```clojure
; 大原则
(leader+y y) = 最常用的拷贝
(leader+y n) = 拷贝资源名字
(leader+y p) = 拷贝资源全路径
(leader+y d) = 拷贝资源所在目录
(leader+y i) = 拷贝资源全部信息
(leader+y f) = 拷贝资源
(leader+Y b) = 收藏资源,添加到书签等

; 窗口管理器
(ctrl+y r) = 矩形截图(rectangle)
(ctrl+y w) = 窗口截图(window)
(ctrl+y l) = 长截图(long)
(ctrl+y a) = 屏幕截图(all)
(ctrl+y g) = gif截图(gif)
(ctrl+y v) = 录制视频(video)
(ctrl+y .) = 任意区域截图()

; 终端
(ctrl+alt+y w) = 拷贝某个单词
(ctrl+alt+y l) = 拷贝某个url
(ctrl+alt+y p) = 拷贝某个路径
(ctrl+alt+y c) = 拷贝某个命令

; 浏览器
(ctrl+alt+y n) = 拷贝标题
(ctrl+alt+y p) = 拷贝网址
(ctrl+alt+y d) = 拷贝网站域名
(ctrl+alt+y i) = 拷贝网站所有信息

(ctrl+alt+y e) = 拷贝编辑框信息
(ctrl+alt+y t) = 拷贝图片地址

(ctrl+Y t) = 翻译信息
(ctrl+Y o) = ocr处理信息
(ctrl+Y i) = 发送给im聊天工具
(ctrl+Y e) = 发送给文件管理器打开
(ctrl+Y s ?) = 搜索拷贝的信息(web or docs)
(ctrl+Y b) = 收藏拷贝的信息

```
### editor interface(TODO)


## SUI接口字母含义速记表

| 顶层字符(一般和ctrl或者alt一起按下) | 意义                     | 叫法                |
| -------------                       | --------------           | --------------      |
| ,                                   | 最近                     | comma/逗号          |
| .                                   | 任意                     | dot/句号            |
| /                                   | 搜索                     | slash/斜杆          |
| ikjl                                | 上下左右                 | 小上,小下,小左,小右 |
| edsf                                | pgup, pgdn, home, end    | 大上,大下,大左,大右 |
| ctrl+azxcv                          | 保持不变                 |                     |
| alt+zx                              | 等价与ctrl和alt          |                     |
| alt+a                               | app层面的快捷键          |                     |
| y                                   | yank/拷贝                |                     |
| Y                                   | paste/粘贴               |                     |
| e                                   | edit/编辑                |                     |
| q                                   | quit/退出                |                     |
| o                                   | open/打开,新建           |                     |
| w                                   | window/窗口              |                     |
| t                                   | tab/标签                 |                     |
| s                                   | size,change/大小变化     |                     |
| m                                   | move/移动                |                     |
| d                                   | deliver/投递             |                     |
| b                                   | backup/备份              |                     |
| n                                   | 鼠标                     |                     |
| g                                   | goto                     |                     |
| u                                   | unique(唯一或者很常用的) |                     |


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
| d             | dir             |
| i             | info            |
| r             | reset/reload    |
