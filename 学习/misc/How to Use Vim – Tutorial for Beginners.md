# [How to Use Vim – Tutorial for Beginners](https://www.freecodecamp.org/news/vim-beginners-guide/)

## Vim Modes

1. Command Mode

   使用 vim 打开文件后的默认模式

2. Command-Line Mode

   在命令模式下按 : 进入底行模式

3. Insert Mode

   在命令模式下按 i、o、A 等进入编辑模式

4. Visual Mode

   在命令模式下按 v 进入

## 常用命令

1. vim filename

   使用 vim 打开文件

2. :w

   命令行模式下保存文件

3. :q

   命令行模式下关闭文件并退出 vim 编辑器

4. :wq

   命令行模式下保存并关闭文件

5. :wq!

   命令行模式下保存并强制关闭文件

6. i

   在当前光标前编辑文本

7. a

   在当前光标后编辑文本

8. o

   在当前光标下一行开始处编辑文本

9. Shift+o

   在当前光标上一行开始处编辑文本

10. dw

    命令模式下删除单字

## 拷贝、剪切、粘贴文本

有两种方式

Visual mode

按 v 进入，选中文本，按 y 复制，按 d 剪切，按 p 在光标后粘贴，按 P 在光标前粘贴。

Keyboard

nyy 复制

ndd 剪切

np 粘贴

## 查找并替换文本

语法

```vim
:[range]s/{pattern}/{string}/[flags]
```

- `[range]` indicates that you can pass the range of lines. Pass % to find and replace in all lines. The range is separated by a comma. To find and replace between lines 5 to 10, pass 5,10. Use `.` to represent the current line and `$` the last line of the file.
- `{pattern}` indicates the pattern to find the text. You can pass regex patterns here.
- `{string}` is the string to replace in the found text.  
- `[flags]` indicates if you wish to pass any additional flags (for example, the flag `c` is passed to confirm before replacing the text). By default, this does a case-sensitive search. You can change it to do a case-insensitive search by passing a `i` flag.

## 撤销和重做

撤销：命令模式下按 u

重做：命令模式下按 Ctrl+R

2u 撤销2次