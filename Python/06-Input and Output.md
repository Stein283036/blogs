# Input and Output

程序输出有几种显示方式；数据既可以输出供人阅读的形式，也可以写入文件备用。本章探讨一些可用的方式。

## 更复杂的输出格式

到目前为止我们已遇到过两种写入值的方式: *表达式语句* 和 [`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print) 函数。 （第三种方式是使用文件对象的 [`write()`](https://docs.python.org/zh-cn/3/library/io.html#io.TextIOBase.write) 方法；标准输出文件可以被引用为 `sys.stdout`。）。

对输出格式的控制不只是打印空格分隔的值，还需要更多方式。格式化输出包括以下几种方法。

- 使用 格式化字符串字面值 ，要在字符串开头的引号/三引号前添加 `f` 或 `F` 。在这种字符串中，可以在 `{` 和 `}` 字符之间输入引用的变量，或字面值的 Python 表达式。

  ```
  >>> year = 2016
  >>> event = 'Referendum'
  >>> f'Results of the {year} {event}'
  'Results of the 2016 Referendum'
  ```

- 字符串的 [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format) 方法需要更多手动操作。该方法也用 `{` 和 `}` 标记替换变量的位置，虽然这种方法支持详细的格式化指令，但需要提供格式化信息。

  ```
  >>> yes_votes = 42_572_654
  >>> no_votes = 43_132_495
  >>> percentage = yes_votes / (yes_votes + no_votes)
  >>> '{:-9} YES votes  {:2.2%}'.format(yes_votes, percentage)
  ' 42572654 YES votes  49.67%'
  ```

- 最后，还可以用字符串切片和合并操作完成字符串处理操作，创建任何排版布局。字符串类型还支持将字符串按给定列宽进行填充，这些方法也很有用。