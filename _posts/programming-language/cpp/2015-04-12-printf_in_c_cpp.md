---
title: C/C++中的格式化IO
author: Tao He
date: 2015-04-12
tag: C/C++
category: 编程语言
layout: post
---

C/C++中的格式化IO操作（输入、输出）使用非常灵活，但C/C++语言标准中复杂的关于格式化IO的定义也很让人头疼。接下来，将系统地讨论C/C++定义的格式化字符串，以及在使用格式化输出时容易出现错误的地方。

格式化字符串的定义
------------------

格式化参数以一个字符串的形式定义了输入/输出的格式，例如类型、宽度、进制，等等，标准格式化字符串的定义：

    %[flags][width][.precision][length]specifier

<!--more-->

科学计算法输出
---------------

`%e`和`%E`用于以科学计数法的格式来输出数字。`e`和`E`用来区分科学计数法输出中的字符`e`的大小写。

百分号
--------

在格式化输出中，不能直接输出`%`要使用`%%`来转义。

在标准定义中，对于`%n`有如下阐述：

> Nothing printed.
> The corresponding argument must be a pointer to a signed int.
> The number of characters written so far is stored in the pointed location.

也就是说，`%n`并不向`printf`函数传递输出内容相关的信息，而是要求`printf`函数把截止当前位置为止已经输出的**字符**总数写入相应变元(corresponding argument)指向的整形变量中。与`%n`相对应的变元必须是一个整形指针。

在格式化输入中，`%n`也有着类似的含义：

> No input is consumed.
> The number of characters read so far from stdin is stored in the pointed location.

输出指针值
----------

在C/C++中，指针占用四个字节，因此，可以使用`%d`来以输出`int`型整数的方式来输出指针。此外，格式化输出专门定义了输出指针变量的指定格式化字符标识`p`，可以通过`%p`的方式输出指针变量。

`g`/`G`的使用
-------------

`%g`和`%G`的含义是总是输出`%f`/`%F`、`%e`/`%E`中较短的形式(shortest representation)。

指定宽度
---------

对于每一组格式化输出，有两种方式来指定输出的宽度。

一种方式是在`%`和格式化字符（如`d`、`x`、`s`等等）之间用一个数字来指定宽度，这也是最常用的方式。例如：

    printf("%12d", 10);

另一种方式是使用%*和一个与之对应的数字参数来指定宽度，如下例：

    printf("%*%d", 12, 10);

则输出宽度为`12`。当然，也可以使用一个整型变量来指定这个宽度：

    int x = 12, y = 10;
    printf("%*%d", x, y);

同样，在输出浮点数，指定小数点后的位数是，也可以使用这种方式。

对齐和填充
----------

当指定的宽度大于要输出的宽度时，默认右对齐，并且以空白符填充。要想改变这种输出格式，可以在百分号`%`后，格式化字符前加一个`-`符号来使得输出左对齐。例如：

    printf("%-12d", 10);

当输出右对齐是，可以指定字符`0`来填充前面的空白，如：

    printf("%05d", 10);

得到的输出内容为：

    00010

如下语句也能得到与之相同的输出：

    printf("%.5d", 10);

输出结果为：

    00010

输出正负号(+/-)
----------------

在输出正数是，默认前面是没有一个加号`+`输出的，要想强制输出这个`+`符号，只需要在`%`后面加上一个`+`符号即可：

    printf("%+d", 20);

输出内容为

    +20

在MinGW g++ 4.8.1 的环境下测试是，使用这种方法输出`0`时，输出为：

    +0

可见，格式化输入/输出时，**`+`和`-`之间有着很大的区别！**

转义序列
-------

Table of escape sequences

| Escape sequence   | Hex value in ASCII  | Character represented                             |
|-------------------|:-------------------:|---------------------------------------------------|
| `\a`              | 07                  | Alarm (Beep, Bell)                                |
| `\b`              | 08                  | Backspace                                         |
| `\f`              | 0C                  | Formfeed                                          |
| `\n`              | 0A                  | Newline (Line Feed); see notes below              |
| `\r`              | 0D                  | Carriage Return                                   |
| `\t`              | 09                  | Horizontal Tab                                    |
| `\v`              | 0B                  | Vertical Tab                                      |
| `\\`              | 5C                  | Backslash                                         |
| `\'`              | 27                  | Single quotation mark                             |
| `\"`              | 22                  | Double quotation mark                             |
| `\?`              | 3F                  | Question mark                                     |
| `\nnn`            | any                 | The character whose numerical value is            |
|                   |                     | given by `nnn` interpreted as an **octal number** |
| `\xhh`            | any                 | The character whose numerical value is given      |
|                   |                     | by `hh` interpreted as a **hexadecimal number**   |

Each escape sequence in the above table maps to a single character, including `\n`. This is despite the fact that the platform may use more than one character to denote a newline, such as the MS-DOS/Windows CR-LF sequence, 0x0d 0x0a. The translation from 0x0a to 0x0d 0x0a on MS-DOS and Windows occurs when the character or string is written out to a file or to the console, but `\n` only creates a single character within the memory of the program itself.

参考
----

参考内容：

1. [cplusplus: scanf](http://www.cplusplus.com/reference/cstdio/scanf/)
2. [cplusplus: printf](http://www.cplusplus.com/reference/cstdio/printf/)
3. [Escape sequences in C](https://en.wikipedia.org/wiki/Escape_sequences_in_C)


