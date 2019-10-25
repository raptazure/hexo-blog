---
title: Vim基本命令
categories: Linux
---



#### 进入普通模式：

- VS Code Vim修改键盘映射 Setting->Normal Mode Key Bindings ,添加：

```json
   "vim.insertModeKeyBindings": [
 {
    "before": ["j", "j"],
	"after": ["<Esc>"]
 }
],
```

- 实现按两次 j 键进入普通模式。

  <!-- more-->

#### 插入模式：

- i  -insert

- I - insert before line

- a - append 

- A - append after line

- o - open a line below

- O - open a line above

- u - undo

- 快速删除字符: 这几个快捷键也可用于Linux终端

  crtl+h 删除上一个字符 ctrl+w 删除上一个单词 ctrl+u 删除当前行
  
- 在normal模式下使用`gi`快速跳转至最后一次编辑的位置并进入插入模式

- Manjaro 里可以直接交换大写锁定与ctrl


#### 命令模式：
- :w 保存 :q 退出
  
- :vs - vertical split    :sp - split
  
- :%s/foo/bar/g 全局替换 
  
#### 可视模式:

- 快速选择文本 - hjkl选择S
- V 选择行  - 执行各种命令,比如 d - 删除  y - 复制
- crtl+v 进入块状选择模式 - hjkl选择

#### Vim快速移动: Normal/Visual

- h  j(下)  k(上)  l

- 在单词间移动: w/W 移动到下一个word/WORD开头, e/E 下一个word/WORD末尾

- b/B回到上一个word/WORD开头, 可以理解为backword

  此处word指以非空白符分隔的单词, WORD是以空白符分隔的词

- **行间**搜索移动：使用`f{char}`可以移动到字符char上，使用t移动到char的前一个字符。可以使用`; ` / ` ,`继续搜该行下一个/上一个字符。`F{char}`表示反过来搜前面的字符。

- 非空白字符(可用0  w组合来替代)，**$移动到行尾**，g_移动到行尾非空白字符。

- 垂直移动：()在句子中移动，{}在段落之间移动。

- 页面移动：`gg` / `G`移动到文件开头/结尾，可用ctrl+o返回光标的上个位置。H/M/L跳转到屏幕开头Head，中间Middle，结尾Lower。crtl+u   crtl+f上下翻页upward/forward。zz把屏幕置为中间。

#### Vim快速增删改查：Normal

- 增加：a/i/o  A/I/O

- 删除：`x`删除一个字符，使用`d`配合文本对象快速删除一个单词

  `daw` delete around word   删除单词及周围空格

  `diw` 删除单词但不删除周围空格

  `dd` 删除当前行

  `dt` delete to + 符号  比如`dt)`删除光标到右括号的所有内容（清空括号）

  `d$` 删除光标到行尾的内容

  `d0` 删除光标到行首的内容

  `d`和`x`可搭配数字实现多次执行，比如`4x`删除四个字符，`2dd`删除两行
  
- 修改：`r` - replace 替换一个字符，比如`ra`将当前字符改为a

   `R` - 进入Replace模式，可以连续替换，Esc退回Normal模式

   `c` - change 配合文本对象进行快速修改 （结合d的操作组合）

   `caw`   `cw`   删除单词并进入插入模式   `C`删除整行并进入插入模式   

   `ct"` 删除光标到后引号中的内容并进入插入模式

   `s` - substitute 替换并进入插入模式    `4s`删除四个字符并进入插入模式

   `S` - 删除整行并进入插入模式
   
- 查询：`/` 或 `？` 进行前向或反向搜索，`n`或`N`跳转到下一个或上一个匹配。

   `*`或者`#`进行当前光标所处单词的前向和后向匹配。
