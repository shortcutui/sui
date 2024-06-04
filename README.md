# SUI

Shortcut User interface for controlling computer and web app shortcuts.

[中文版本](./README_zh.md)

## Introduction

SUI (Shortcut User Interface) is a shortcut user interface, which absorbs the shortcut design ideas of emacs and vim.
It extracts some common and shared operations in daily use of software, and designs an easy-to-learn, easy-to-understand and easy-to-press shortcut key for these operations.

SUI is currently easy to implement in the three major operating systems and major browsers. Software and Web sites that implement SUI are called SUI-compatible.

## Motivation

I was a GUI user before, and one day I realized that my right hand was numb when I touched the mouse, and my left hand's pinky felt numb when I pressed ctrl, so I had to find a way to use the full keyboard to operate the computer.
Full keyboard to operate the computer, the existing key specification there are three mainstream, one is emacs ctrl + x with a series of keys at the beginning, one is vim mode key, and the other is the menu button that comes with some software, which is alt+letter to goto a menu, followed by a series of buttons, or up and down to navigate the menu.

These ways have their own drawbacks, emacs buttons are too long, a little more operations require three buttons, vim's mode compilation is difficult to apply to current gui software, software with the menu in the various software is not common, and  can not be easily applied to the window manager and browser.

Through some research and thinking, in the process of daily use of software, whether gui or tui, or website, I found that in most cases, the reason why I have to use the mouse is because there is no way to locate a window or a menu via the keyboard in some app. If you can switch between windows with shortcuts, then most of the rest of the app's functionality can be accomplished with up, down, left, right, or some other keystroke.

## SUI-related repositories (TODO)

The following repositories are operating systems, applications, or web applications that implement sui. Applications that implement the basic sui interface are called sui-compatible.

Some of these applications are heavily used by me, such as wezterm, browser, yazi, and neovim, which I will desensitize later.


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

## Terminology and Key conventions

In this document, a sequence of keystrokes is enclosed in parentheses, e.g. (a) means that key a was pressed on the keyboard, and (a b) means that key a was pressed first, and key b was pressed a short time later.
A plus sign means that both keys were pressed at the same time, e.g. (ctrl+a) means that both ctrl and a were pressed at the same time, (ctrl+alt+a) means that both ctrl and alt were pressed at the same time, and a was pressed at the same time. Except in vim
scenario, (leader+a) might mean pressing the leader key first, then pressing the a key for a short period of time.

The leader key represents different keys in different applications, and the SUI categorizes them according to the characteristics of the application, with different types of applications using different keys as leader keys.
The following is an example of a leader setup. The leader keys in parentheses represent the leader keys used by them

- Window manager (ctrl)
- Normal GUI apps (alt)
- Browser or other terminal app that can connect to ssh remotely (ctrl+alt or none)
- Window manager on remote terminal(alt)
- Normal TUI app (none, or leader in vim mode).

SUI recommends mapping right ctrl to ctrl+alt by pressing ctrl and ctrl+alt with both left and right hand palms, and mapping Capslock to one of the key combinations when pressed in conjunction with other keys. Depending on the layout of your keyboard and the distribution of your hands, you are free to choose what the leader is and how you want to press it.

All SUI shortcuts are (leader+character character character character), so if the leader key is a ctrl or alt key, then when you press the character after it, the leader should be mapped to a key combination if it is released or not.
If the leader key is a ctrl or alt key, then pressing the next character and releasing the leader should be mapped to the same action. In addition to the leader key, the SUI should only use numbers 0-9 and letters a-z plus a few other characters, and should avoid using uppercase letters as much as possible.
It should also avoid the use of uppercase letters, and if it is necessary to use uppercase letters, it must be a natural variant of lowercase letters that have a similar or related function.

Currently SUI uses only three non-alphabetic symbols in addition to the editor interface, that is comma for recently, period for arbitrary, and slash for search.

`?` represents all characters in the sui that are not defined in that section, e.g., in [space-interface](#space-interface), `(space+?)` represents all characters not defined in the SUI's space interface. Generally these characters are left to be customized by the user.

The keys in SUI are defined using qwerty's keyboard layout, there are a few special keys that are defined based on their position, jlik(left, right, up, down)
and sfed (home, end, pageup, pagedown). For other letters, an effort is made to find the corresponding words to help memorize them. The same letter should mean the same thing in different applications.

Unless otherwise specified, after pressing the first key combination, the SUI will enter a key combination mode, either briefly or permanently, which can be exited by pressing esc or q.
If the mode is permanent, then ({x mode} a) means that key a is pressed in x mode, and without explanation, pressing a will perform the corresponding action without exiting x mode.

SUI works well with the standard qwerty layout and the norman layout I'm using, other layouts may require some modification.

## Video Demo

I recorded a [video](https://www.bilibili.com/video/BV14w4m1q7YQ/) on bilibili to illustrate some of the ways SUI works on my computer now.

## SUI interface

The SUI is categorized into different interfaces depending on what the interface does, and uses a different key as the first button. The same type of interface often serves the same purpose.

All interfaces are represented as (key) = value, where (key) represents the sequence of keys pressed at the keyboard, and value represents the actual output of a key or an action.

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

The space interface is used to map common up, down, left, right and function keys to the main keyboard area.

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

(space+?) = Any keystroke or action you want to customize
```

### backup interface

The backup interface is mainly used by apps that can use sui in most cases, and in some cases when sui is not available and you don't want to use the [fallthrough interface](#fallthrough-interface).

```clojure
(ctrl+b j) = move to the left window or tab
(ctrl+b l) = move to the right window or tab
(ctrl+b i) = move to the upper window or tab
(ctrl+b k) = move to the lower window or tab
(ctrl+b .) = Open the application's own shortcut command window
(ctrl+b q) = exit the current window
(ctrl+b r) = Reload the current window

(ctrl+b ?) = Any keystroke or action you customize
```

### mouse interface

This interface simulates mouse operations, and is used for special apps that don't have sui adaptations.

```clojure
(ctrl+n) = enter mouse mode
({mouse mode} q) = leave mouse mode
({mouse mode} esc) = leave mouse mode

({mouse mode} j) = mouse left (mouse movement slows down and is constant when ctrl is held down)
({mouse mode} l) = mouse right (slow and constant when ctrl is held down)
({mouse mode} i) = mouse up (slow and constant speed when ctrl is held down)
({mouse mode} k) = mouse down (slow and constant speed when ctrl is held down)
({mouse mode} s) = left mouse button
({mouse mode} f) = click right mouse button
({mouse mode} e) = mouse wheel up
({mouse mode} d) = mouse wheel down

({mouse mode} n) = mouse click on the center of the window of interest, to prevent some loss of focus, then leave mouse mode
({mouse mode} x) = [click] center mouse button
({mouse mode} w) = [click] forward  mouse button
({mouse mode} r) = [click] backward mouse button
({mouse mode} c) = mouse wheel left
({mouse mode} v) = mouse wheel right
({mouse mode} h) = hide mouse
({mouse mode} o) = show mouse
```
### editline interface

This interface is used to edit the contents of a line.

```clojure
(ctrl+e) = enter edit mode
({edit mode} j) = delete a word forward
({edit mode} J) = move one word forward
({edit mode} l) = delete a word backward
({edit mode} L) = move backward one word
({edit mode} s) = delete forward to the beginning of the line, then leave edit mode
({edit mode} f) = delete backward to the beginning of the line, then leave edit mode
({edit mode} d) = delete the entire line and leave edit mode
({edit mode} y) = copy the line and leave edit mode
({edit mode} u) = undo
({edit mode} U) = reverse undo
({edit mode} q) = quote the word before it
({edit mode} Q) = quote the entire line
({edit mode} ,) = switch to another editline mode, when you realize that the current action doesn't work
({edit mode} ?) = user defined by self or print char then leave edit mode
```

### zxcva interface

```clojure
(ctrl+zxcva) works according to windows rules
(alt+z ?) = (ctrl+?) For mac it is (cmd+?)
(alt+x ?) = (alt+?)
(alt+c) = Mouse wheel to the left
(alt+v) = mouse wheel right
(alt+a .) = Display a menu of application-level user-defined shortcuts
(alt+a ?) = Application-level user-defined shortcuts
```

### uniq interface

This interface is intended for applications that have some frequently used functions that can't be categorized, or that need to be pressed all the time and aren't conveniently designed as a sequence of keys.Some shortcuts can be defined in alt a, but if you want them to be faster you can set them to the uniq interface.
```clojure
(ctrl+u) = the most common, I currently give it to tts
(ctrl+alt+u) = most used or unique
(alt+u) = most used or unique
```

### fallthrough interface

In fallthrough mode, all keystrokes starting with the leader are output as is. That is, in window manager, after pressing ctrl+f, all shortcuts starting with control are sent to the app as is, unless control+shift+f is pressed to unlock them. This interface is designed for apps that don't yet have a sui implementation.

```clojure
(leader+f) = enter fallthrough mode
(leader+shift+f) = exit fallthrough mode.
```

### open interface

```clojure
(leader+o .) = Open command panel or menu
(leader+o o) = most common open operations
(leader+o r) = Reload configuration or restart the App
(leader+o v) = open a resource in a vertical window
(leader+o h) = open a resource in a horizontal window(leader+o t) = open a resource in a new tab
(leader+o s c) = open app configuration
(leader+o s m) = open app shortcuts
(leader+o s h) = open app help
(leader+o s i) = open app info panel
(leader+o ?) = open user-defined resource
```

### quit interface

```clojure
(leader+q .) = Search for quit
(leader+q q) = Quit current window (caps force quit)
(leader+q t) = quit current tab (force quit with capitalization)
(leader+q a) = exit app
(leader+q u) = undo exit
(leader+q s) = exit window other than the current one
(leader+q S) = exit tab other than current tab

(leader+q j) = quit left window
(leader+q l) = quit right window
(leader+q i) = quit upper window
(leader+q k) = quit lower window
```

### Focus interface

```clojure
(leader+j) = focus to the left window (if there is only one window in the current tab, you can focus to the left tab or not)
(leader+l) = focus on right window (if current tab has only one window, you can focus on right tab or no action)
(leader+i) = focus on upper window (if current tab has only one window, focus on floating layer or no action)
(leader+k) = focus on lower window (if there is only one window in the current tab, you can focus on the tiled layer or do nothing)
(leader+w left) = focus on left window (if the current tab has only one window, you can focus on the left tab or nothing)
(leader+w right) = focus on right window (if current tab has only one window, focus on right tab or no action)
(leader+w up) = focus on upper window (if there is only one window in the current tab, you can focus on the floating layer or nothing)((leader+w down) = focus on lower window (if the current tab has only one window, you can focus on the tiled layer or no action)
(leader+left) = focus on left tab
(leader+right) = focus on right tab
(leader+up) = focus on floating layer
(leader+down) = Focus on tiled layer
(leader+t left) = Focus on left tab
(leader+t right) = focus on right tab
(leader+w .) = search window and focus
(leader+w ,) = focus on the recently window
(leader+w ?) = focus on user-defined window
(leader+t .) = search for tabs and focus
(leader+t ,) = focus on recently tab
(leader+t ?) = focus on user-defined tab
(leader+d .) = search for tabs and move the current window to that tab
(leader+d ?) = move the current window to the user-defined tab
(leader+d left) = move the current window to the left tab
(leader+d right) = move the current window to the right tab

(ctrl+/) = window manager find widgets
(alt+/) = app find some thing

; In many cases where there are three windows at the same time, when my focus is on one of the main windows, I can work on the other two at the same time.
(shift+up) moves the cursor or window up in the second window.
(shift+down) moves the cursor or window down in the second window
(shift+left) moves the cursor in the second window to the left.
(shift+right) Moves the cursor or window in the second window to the right.
(shift+pageup) Puts the cursor or window in the third window up.
(shift+pagedown) Moves the cursor or window down in the third window.
(shift+home) Moves the cursor or window left in the third window.
(shift+end) Turns the cursor or window in the third window to the right.
```

### goto interface

Whereas the previous operations were mainly for windows or tabs, the goto interface operates on the resource that the app is manipulating. This goto interface works on the resource that the app is working on, or the current location of the app.

```clojure
(leader+g .) = Search for a resource and jump to it.
(leader+g ,) = jump to the recently resource
(leader+g j) = Cursor jumps back.
(leader+g l) = jump forward with the cursor
(leader+g d) = jump to definition
(leader+g r) = jump to reference
(leader+g t ?) = jump to specific user-defined resource
```

### move interface

```clojure
(leader+m j) = move the window to the left
(leader+m l) = window moves to the right
(leader+m i) = window moves up
(leader+m k) = window moves down
(leader+m left) = tab moves to the left
(leader+m right) = tab moves to the right
(leader+m up) = move window to floating level
(leader+m down) = move window to tiled layer

(leader+m f) = Toggle window to floating state
```

### size interface

```clojure
(leader+s j) = increase window to the left or decrease window to the right
(leader+s j) = window decreases left or increases right
(leader+s l) = window increases to the right or decreases to the left
(leader+s L) = window decreases to the right or increases to the right
(leader+s i) = window increases up or decreases to the right
(leader+s I) = window decreases upwards or increases to the right
(leader+s k) = window increases down or decreases to the right
(leader+s K) = window decreases down or increases to the right

(leader+s m) = toggle the window maximization state
(leader+s z) = toggle window zen mode
(leader+s h) = hide or minimize the window
(leader+s w) = change the window name
(leader+s t) = change tab name
(leader+s u) = increase font or sound size
(leader+s d) = decrease font or sound size
(leader+s s) = resize font or sound to default size

(leader+s ?) = User-defined window modification related operations
```

### copy&paste interface

f represents the resource or file associated with the current cursor or window, all resources are files. A resource or file has a path, a name and a directory.

```clojure
; General principles
(leader+y y) = most common copy
(leader+y n) = copy of the resource name
(leader+y p) = Copy the full path of the resource.
(leader+y d) = Copy the directory where the resource is located.
(leader+y i) = copy all information of the resource
(leader+y f) = copy resource
(leader+y b) = Bookmark resource, add to bookmarks, etc.

; Window manager
(ctrl+y r) = Rectangle screenshot
(ctrl+y w) = Screenshot of a window.
(ctrl+y l) = long screenshot (long)
(ctrl+y a) = screen shot (all)
(ctrl+y g) = gif screenshot (gif)
(ctrl+y v) = record video
(ctrl+y .) = take a screenshot of any area ()

; Terminal
(ctrl+alt+y w) = copy a word
(ctrl+alt+y l) = copy a url
(ctrl+alt+y p) = copy a path
(ctrl+alt+y c) = copy a command

; Browser
(ctrl+alt+y n) = copy the title
(ctrl+alt+y p) = copy the URL
(ctrl+alt+y d) = copy the domain name of the website
(ctrl+alt+y i) = copy all information of the site

(ctrl+alt+y e) = copy edit box information
(ctrl+alt+y t) = copy image address

(ctrl+Y t) = translate message
(ctrl+Y o) = ocr processing message
(ctrl+Y i) = send to im chat tool
(ctrl+Y e) = send to file manager open
(ctrl+Y s ?) = search for copied information (web or docs)
(ctrl+Y b) = Bookmark the copied information

```
### editor interface(TODO)

## SUI CheatSheet


| top level character (usually pressed with ctrl or alt) | meaning                    | call                      |
| -------------                                          | --------------             | --------------            |
| ,                                                      | recently                   | comma                     |
| .                                                      | arbitrary                  | dot                       |
| /                                                      | search                     | slash                     |
| ikjl                                                   | up,down,left,right         | small(up,down,left,right) |
| edsf                                                   | pgup, pgdn, home, end      | big(up,down,left,right)   |
| ctrl+azxcv                                             | Remain unchanged           |                           |
| alt+zx                                                 | Equivalent to ctrl and alt |                           |
| alt+a                                                  | Shortcuts at the app level |                           |
| y                                                      | yank/copy                  |                           |
| Y                                                      | paste                      |                           |
| e                                                      | edit                       |                           |
| q                                                      | quit                       |                           |
| o                                                      | open/new                   |                           |
| w                                                      | window                     |                           |
| t                                                      | tab                        |                           |
| s                                                      | size,change                |                           |
| m                                                      | move                       |                           |
| d                                                      | deliver                    |                           |
| b                                                      | backup                     |                           |
| n                                                      | mouse                      |                           |
| g                                                      | goto                       |                           |
| u                                                      | unique                     |                           |

| second level character | meaning         |
| -------------          | --------------  |
| v                      | vertical        |
| h                      | horizontal/hide |
| m                      | maximize        |
| z                      | zen             |
| u                      | up              |
| d                      | down            |
| s/S                    | single          |
| n                      | name/new        |
| p                      | path            |
| d                      | dir             |
| i                      | info            |
| r                      | reset/reload    |

