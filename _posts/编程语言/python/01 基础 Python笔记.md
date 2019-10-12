---
title: article
toc: true
date: 2019-10-07 02:32:43
tags: [python,语法]
categories:  
- 编程语言
- python
---

[TOC]

## 概论

### 计算机编程概述

算法(algorithm)：描述了为了解决某个问题需要采取的动作以及这些动作的顺序，可以用自然语言或者伪代码（pseudocode，自然语言混杂着一些程序代码）的形式描述

程序：程序是用于控制计算机的一系列指令

程序语言：描述这些指令的语言，是“程序员”与“机器”对话的语言。

语法（syntax）: 哪些符号或文字的组合方式是正确的

语义（semantics） : 描述程序的意义，当代码运行时计算机干什么。

**低级语言**   

* 机器语言（Machine code）:CPU所执行的指令，由多个数字组成，比如 05  01 23

* 汇编语言（Assembly Language）: 以人可读的方式描述机器代码，如add EAX, 1，mov [ESP+4], EAX

**解释和编译**

如何将使用高级语言编写的程序（源代码source code）转换为目标代码（机器码）？

* 解释器（Interpreter）：将语句翻译成机器码，并且执行，Python、Javascript、Perl、PhP等。不需编译，但是每次运行需要翻译。如python的代码必须在python内运行。

* 编译器（Compiler）：将语句翻译成机器码，形成目标代码文件，C、C++等编译时相比解释可以作更多的优化。需要编译，但是运行中不需要翻译。如C的代码编译后可在个平台运行。

有些语言将解释和编译结合在一起

* Java语言：源代码首先通过编译器（javac）转换为中间的Java字节码（Byte Code），然后在目标机器上通过解释器（java虚拟机）来运行

* Python也支持伪编译，即将.py程序转换为.pyc字节码来优化程序和提高执行速度

### 预备知识

**现代计算机的部件**  
  
CPU( Central Processing Unit )  =运算器 + 控制器

辅存(Secondary Storage):硬盘、闪存（U盘、TF卡、SD卡等）、DVD：数据和指令首先从外存读到内存后才能被CPU使用

![](https://i.loli.net/2019/10/12/EVrsgWSfLcNDCtF.png)

**数据表达：Bit、Byte(K/M/G/T)**

一个字节=8个比特（1B=8b)，一个字节可以表示0到255的整数，或者也可表示一个ASCII字符

二进制00101011对应十进制43，即〖0∗2〗^7+〖0 ∗2〗^6+〖1 ∗2〗^5+〖0 ∗ 2〗^4+〖1 ∗2〗^3+〖0 ∗2〗^2+〖1 ∗2〗^1+〖1 ∗2〗^0  =43

Kilobyte (kB)、Megabyte (MB)、Gigabyte (GB)、Terabyte (TB)

**Python版本**

查看已安装版本的方法（在所启动的IDLE界面也可以直接看到）：

```
import sys
sys.version
sys.version_info
```

**IDLE快捷键**

|  快捷键   |                                       功能说明                                        |
| --------- | ------------------------------------------------------------------------------------- |
| Ctrl+A    | 全选                                                                                  |
| Ctrl+\]   | 增进代码块                                                                             |
| Ctrl+\[   | 取消代码块缩进                                                                         |
| Ctrl+F6   | 重启shell，之前定义的对象和导入的模块全部失效                                            |
| Ctrl + \  | (show calltip)显示函数的参数使用方式                                                    |
| **Alt+p** | **浏览历史命令（上一条）**                                                             |
| **Alt+n** | **浏览历史命令（下一条）**                                                             |
| Alt+/     | （Expand word）自动补全前面曾经出现过的单词，如果之前有多个单词具有相同前缀，则在多个单词中循环选择 |
| **Alt+3** | **注释代码块**                                                                        |
| **Alt+4** | **取消注释代码块**                                                                    |
| ALT+ \    | (show completions)显示自动完成                                                         |
| F1        | 打开帮助文档                                                                           |
| F5        | 运行当前代码                                                                           |
| Tab       | 智能缩进或者自动完成（即输入前缀后会列出相关的关键字和属性）                              |

**python打开方法**

windows+r打开`cmd`，输入以下代码

```
python

python helloworld.py

helloworld.py
```

### Python基础知识

#### 对象（Object）

**对象：Python中各种数据的抽象**

标识ID(identity): 对象一旦创建其ID不再改变，可以看成该对象在内存中的地址，

`id(x) `返回对象x的ID，`a is b`判别 a和b是否同一个对象（ID是否相同 ）

**类型(type)**：决定了对象可能取值的范围以及支持的操作。对象的类型不可变，强类型语言

`type(x) `返回对象x的类型

**对象是类型的一个实例（instance）**

**python内置对象类型**

|   对象类型   |                   示例                   |
| ----------- | ---------------------------------------- |
| 数字        | 1234,    3.14,  3+4j                     |
| 字符串       | 'swfu',   "I'm student",   '''Python ''' |
| 列表        | \[1,   2, 3\]   \[‘a’,’b’,\[‘c’,2\]\]    |
| 字典        | {1:'food'   ,2:'taste', 3:'import'}      |
| 元组        | (2,   -5, 6)                             |
| 文件        | f=open('data.dat',   'r')                |
| 集合        | set('abc'),   {'a', 'b', 'c'}            |
| 布尔型       | True,   False                            |
| 空类型       | None                                     |
| 编程单元类型 | 函数(def)、模块、类(class)                |

**如何描述和引用对象？** 

Literal(字面值)：表示某个内置对象类型的固定不变的值，在词法和语法分析时识别其类型

* 字符串字面值: 'Hello World'

* 整数字面值:  2016    0o177  0xda80  0b10010111  

* 浮点数字面值:   3.14   10.   .001  3.14e-10  1.0e100 

* 复数字面值:  3.14j      10j  

表达式(expression): 各个对象通过运算符(operator)运算之后的结果(3\*4+5)\*6 

**对象删除**

Python具有自动内存管理功能，解释器会跟踪所有的对象的引用情况，一旦发现某个对象不再有任何变量引用，垃圾回收机制在适当的时候会回收该对象，释放内存资源

`del`语句可显式解除变量与所指向对象之间的绑定，也可解除列表list等可变序列中的元素的绑定，即删除该元素。

**可变与不可变对象**

不可变(immutable)对象：有些对象一旦创建其值不可变，比如数字、字符串、元组等

可变(mutable):对象的值可以改变，比如列表、字典等

两个变量分别赋值为两个可变对象，值即便相同，也会有两个可变对象存在。

而对于不可变对象，由于其值不变，为了性能方面的考虑，Python实现中可能仅仅分配一个对象，多个变量指向同一个对象。

整数为不可变对象，而且注意只有在[-5,256]间的整数才有这样的行为，而且不排除以后实现可能不再适用。

`help(thing)`: 查看对象thing相关的帮助

`dir([object])`: 查看object相关的属性和方法列表，其中_开头的名字表示内部使用

`[n for n in dir([object]) if not n.startswith('_')] `过滤掉以_开头的属性


#### 变量

变量(variable): 表示对于某个对象的引用（reference）

* 在使用之前无需声明变量及其类型,而是自动判断其类型 ,支持的运算由类型决定

* 通过赋值语句来给变量赋值:  `variable = expression  (LHS = RHS)`    

* 变量出现在RHS(Right Hand Side) 处时表示引用该变量所指向对象的值

* 变量出现在LHS，表示给该变量赋值，即保存RHS所对应对象的引用（地址）

* 由于变量表示对于某个对象的引用，因此Python允许多个变量指向同一个对象

* Python是一种动态类型语言：变量的类型是可以随时变化的

* 在python语言中，类型是对象的一部分，变量保存的是对象的引用

```python
endFlag = 'yes'
s = 0
while endFlag.lower() ==' yes':
    x = input("请输入一个正整数: ")
    x = int(x)
    if isinstance(x, int) and 0<=x<=100:
        s = s + x
    else:
        print('不是数字或不符合要求')
    endFlag = raw_input('继续输入？(yes or no)')
print('整数之和=', s)
```

**全局变量与局部变量**

当你在函数定义内声明变量的时候，它们与函数外具有相同名称的其他变量没有任何关系，即变量名称对于函数来说是局部的。这称为变量的作用域 。所有变量的作用域是它们被定义的块，从它们的名称被定义的那点开始。

如果你想要为一个定义在函数外的变量赋值，那么你就得告诉Python这个变量名不是局部的，而是全局的。我们使用global语句完成这一功能。没有global语句，是不可能为定义在函数外的变量赋值的。

局部变量的引用比全局变量速度快。

global语句被用来声明x是全局的——因此，当我们在函数内把值赋给x的时候，这个变化也反映在我们在主块中使用x的值的时候。

你可以使用同一个global语句指定多个全局变量。例如global x, y, z。

```python
def func2():
    global x
    x = 2
    print('global x is',x)

x = 50
func2()
print('x is still', x)
>>> global x is 2
>>> x is still 2
```

**变量名规范**

* 标识符是变量、函数、类、模块和其他对象的名字

* 必须以**字母或下划线**开头，其后的字符可以是字母、下划线或数字

* 以下划线开头的变量在Python中有特殊含义

* 变量名中**不能有空格以及标点符号**（括号、引号、逗号、斜线、反斜线、冒号、句号、问号等等）

* 标识符对英文字母的大小写敏感，例如student和Student是不同的变量。

* 一些特殊的标识符保留为Python关键字，不能用作变量名

* 不建议使用系统内置的模块名、类型名或函数名以及已导入的模块名及其成员名作变量名，这将会改变其类型和含义，可以通过`dir(__builtins__)`查看所有内置模块、类型和函数；

* 建议使用有意义的名字，i,j,k仅仅用在较短的循环等结构，比如area、keys等

* 建议使用小写字母表示变量名,多个单词时以下划线隔开: lower_case_with_underscores

#### 数字类型

* 数字为不可变对象

* 包括整数(int)、浮点数(float)、复数(complex)、布尔（bool）

* 与有些语言不同，整数可以表示任意大的数值

* 整数字面值（integer literal）

    * 十进制整数: 0、-1、9、123， 注意007不可以

    * 十六进制整数: 0x开头后面为十六进制数字，可接[0-9]以及[a-f]，如0x10、0xfa、0xabcdef,注意这些数字的大写字母(包括前缀0X)也可以

    * 八进制整数:以0o开始后面为八进制数字，接[0-8]，比如0o35、0o11

    * 二进制整数:以0b开头如，0b101、0b100 、 0b10010111

* （有限精度）浮点数（float）

    * 浮点数字面值：浮点数用于表示实数，在内部采用科学计数法表示，因此称为浮点数；小数表示：3.14；科学计数法：$15E-2 =15*10^{-2} = 0.15$， $3.14E-10$ ，$1.0E100$

    * 需要说明的是由于计算机内部采用二进制表示，与其他语言一样，采用IEEE 574双精度表示浮点数时，有精度误差。a= 0.1 + 0.1 + 0.1，a == 0.3 结果为 False。

    * Python提供了decimal模块（高精度浮点数Decimal）用于十进制数学计算，来保证用户指定的精度

    * fractions模块用于表示分数

```python
from decimal import Decimal

Decimal(0.1)

>>>Decimal('0.1000000000000000055511151231257827021181583404541015625')

from fractions import Fraction

Fraction('3/7')

>>>Fraction(3, 7)
```

* 复数（Complex）:一个复数包括实部（real）和虚部（imaginary），即实部+虚部，如3+4j， 2.5j+3 4j，0j，注意j、 4*j 都不是复数。复数也支持常用的数学运算（加减乘除）。

```python
c.real #查看复数实部
c.imag #查看复数虚部
a.conjugate() #返回共轭复数
```

* 布尔（bool）：整数类型的特例，取值为True、False，分别对应整数1和0，实际上所有非0的整数转变为bool时都是True，True 等价于 非0，False等价于0

#### 算术运算符

| **运算符** |         **名称**         |                          **说明**                          |                                             **例子**                                              |
| ---------- | ------------------------ | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| +         | 加                       | 加法，列表、元祖、字符串合并                                                             | 3 + 5得到8。'a' + 'b'得到'ab'。                                                                   |
| -          | 减                       | 减法，集合差集                                              | -5.2得到一个负数。50 - 24得到26。                                                                  |
| *          | 乘                       | 乘法或是返回一个被重复若干次的字符串                                                      | 2 * 3得到6。'la' * 3得到'lalala'。                                                                |
| **         | 幂                       | 返回x的y次幂                                               | 3 ** 4得到81（即3 * 3 * 3 * 3）                                                                   |
| /          | 除                       | 真除法                                                                                  | 4/3得到1（整数的除法得到整数结果）。4.0/3或4/3.0得到1.3333333333333333                              |
| //         | 取整除                   | 返回商的整数部分                                            | 4 // 3.0得到1.0                                                                                   |
| %         | 取模                     | 返回除法的余数，字符串格式化                                                             | 8\%3                        得到2。-25.5   \%2                                              .25得到1.5 |
| <<        | 左移                     | 把一个数的比特向左移一定数目（每个数在内存中都表示为比特或二进制数字，即0和1）               | 2 << 2得到8。——2按比特表示为10                                                                     |
| >>        | 右移                     | 把一个数的比特向右移一定数目                                                             | 11 >> 1得到5。——11按比特表示为1011，向右移动1比特后得到101，即十进制的5。                             |
| &         | 按位与                   | 数的按位与；集合交集                                        | 5 & 3得到1。                                                                                      |
| \|         | 按位或                   | 数的按位或；并集                                            |                                                                                                  |
| ^         | 按位异或                  | 数的按位异或；差集                                          | 5 ^ 3得到6                                                                                        |
| ~         | 按位翻转                  | x的按位翻转是-(x+1)                                         | ~5得到6。                                                                                         |
| <         | 小于                     | 返回x是否小于y。所有比较运算符返回1表示真，返回0表示假。这分别与特殊的变量True和False等价。注意，这些变量名的大写。 | 5 < 3返回0（即False）而3 < 5返回1（即True）。比较可以被任意连接：3 < 5 < 7返回True。                                                    |
| >         | 大于                     | 返回x是否大于y                                                                          | 5 > 3返回True。如果两个操作数都是数字，它们首先被转换为一个共同的类型。否则，它总是返回False。          |
| <=        | 小于等于                  | 返回x是否小于等于y                                                                       | x = 3; y = 6; x <= y返回True。                                                                    |
| >=        | 大于等于                  | 返回x是否大于等于y                                                                       | x = 4; y = 3; x >= y返回True。                                                                    |
| ==        | 等于                     | 比较对象是否相等                                                                         | x = 2; y = 2; x == y返回True。x = 'str'; y = 'stR'; x == y返回False。x = 'str'; y = 'str'; x == y返回True。  |
| !=         | 不等于                   | 比较两个对象是否不相等                                                                   | x = 2; y = 3; x != y返回True。                                                                    |
| not        | 布尔“非”                 | 如果x为True，返回False。如果x为False，它返回True。           | x = True; not y返回False。                                                                        |
| and       | 布尔“与”                 | 如果x为False，x and y返回False，否则它返回y的计算值。        | x = False; y = True; x and y，由于x是False，返回False。在这里，Python不会计算y，因为它知道这个表达式的值肯定是False（因为x是False）。这个现象称为短路计算。  |
| or         | 布尔“或”                 | 如果x是True，它返回True，否则它返回y的计算值。               | x = True; y = False; x or y返回True。短路计算在这里也适用。                                         |
| Is;is not  | 对象实体统一性测试（地址） | X is y ; x is not y                                        |                                                                                                   |
| In;not in  | 成员测试运算符            |                                                            |                                                                                                   |

**注：**

按位运算符是把数字看作二进制来进行计算的。Python中的按位运算法则如下：

* 按位与 ( bitwise and of x and y ) & 举例： 5&3 = 1 解释： 101 11 相同位仅为个位1 ，故结果为 1

* 按位或 ( bitwise or of x and y ) | 举例： 5|3 = 7 解释： 101 11 出现1的位是 1 1 1，故结果为 111

* 按位异或 ( bitwise exclusive or of x and y ) ^ 举例： 5^3 = 6 解释： 101 11 若相同位不一致时为1，一致时为0，故结果为 110

* 按位反转 (the bits of x inverted ) ~ 举例： ~5 = -6 解释：  将二进制数+1之后乘以-1，即~x = -(x+1)，-(101 + 1) = -110。按位反转仅能用在数字前面。所以写成 3+~5 可以得到结果-3，写成3~5就出错了

* 按位左移  （ x shifted left by n bits ）<< 举例: 5<<2 = 20 解释：101 向左移动2位得到 10100 ，即右面多出2位用0补

* 按位右移  （ x shifted right by n bits ） >> 举例： 5>>2 = 1 解释：101 向右移动2位得到 1，即去掉右面的2位

优先级顺序，通过小括号改变运算顺序 ，可嵌套，注意：**中括号[ ]和大括号{}不用于数学计算**

上述运算符支持两个不同的数字类型的对象之间的运算，即混合运算，比如浮点数+整数

如果其中包含complex对象，则其他数字类型转换为complex对象，结果为complex对象，如果其中包含float对象，则其他数字类型转换为float对象，结果为float对象。即：bool int→float→ complex

 **内置数学函数**

|           **函数**            |                    **含义**                    |                **实例**                |      **结果**       |
| ----------------------------- | --------------------------------------------- | -------------------------------------- | ------------------- |
| abs(x)                        | x的绝对值。如果x为复数，则返回其模              | abs(-1.2)abs(1-2j)                     | 1.22.23606797749979 |
| **divmod(a,b)**               | **返回a除以b的商和余数**                       | **divmod(5,3)**                        | **(1,2)**           |
| **pow(x,y\[,z\])**            | **返回x**y。如果z有，则为pow(x,y)%z**          | **pow(2,10)****pow(2,10,10)**          | **1024****4**       |
| **round(number\[,ndigits\])** | **四舍五入取整，如果ndigits则保留ndigits小数** | **round(3.14159)****round(3.14159,4)** | **3****3.1416**     |
|                               |                                               |                                        |                     |
| min(arg1,arg2,*args)          | 取最小值                                       | min(1,7,3,15,14)                       | 1                   |
| sum(iterable\[,start\])       | 求和，start如果有，表示加上start                | sum((1,2,3))sum((1,2,3),44)            | 650                 |

#### Python代码编写规范

（1）缩进

* python程序是依靠代码块的缩进来体现代码之间的逻辑关系的

* 类定义、函数定义、选择结构、循环结构等，行尾出现`: `(后面可以包括空格等)表示后面应该紧跟缩进的代码块，行尾的冒号表示缩进的开始。缩进结束表示代码块的结束

* 同一个级别的代码块的缩进量必须相同

* 建议以4个空格为基本缩进单位，不建议采用制表符来缩进

* IDLE缩进和反缩进的快捷键为 Ctrl + [ 和 Ctrl + ]

（2）必要的空格与空行

* 运算符两侧建议使用空格分开

* 建议在逗号后面添加一个空格

* 不同功能的代码块之间、不同的函数定义之间建议增加一个空行以提高可读性。

* 如果一行语句太长，可以在行尾加上\来换行分成多行，但是更建议使用**括号来包含多行内容**。

* 一个好的、可读性强的程序一般包含30%以上的注释。

* 以#开始，表示本行#之后的内容为注释

* 不属于任何语句的字符串为注释，经常在函数体开始处添加长注释（三引号），作为docstring

* 在spyder中，注释和解除注释的快捷键为：Ctrl + 4/5

（3）每个import只导入一个模块

* 首先导入Python标准库模块，如os、sys、re

* 导入第三方扩展库，如numpy、scipy

* 导入自己定义和开发的本地模块

（4）适当使用异常处理结构进行容错，后面将详细讲解。

（5）软件应具有较强的可测试性，测试与开发齐头并进

（6）__name__属性

* 每个Python程序在运行时都有一个“__name__”属性。

* 如果程序作为模块被导入，则其“__name__”属性的值被自动设置为模块名

* 如果程序独立运行,称为脚本(script)，则其“__name__”属性值被自动设置为“__main__”。

```python
if __name__ == '__main__':
    main()

### 例如，假设文件nametest.py中只包含下面一行代码：
print(__name__)
### 直接运行时：
__main__
### 而将该文件作为模块导入时得到如下执行结果：
import nametest
>>> Nametest
```

（7）代码编写规范示例

```python
def function1(para1, para2):
    return conse1

def function2(para1, para2):
    return conse2

def main():                 # 设定一个总函数，包含其他分函数
    constant = a
    ness_list = function1(constant)
    print_consequence = function2(ness_list, constant)

if __name__ == '__main__':  # 作为一个独立的脚本运行
    main()
```

### 常见函数

**内置函数**

`isinstance(object, classinfo)`

判断实例是否是这个类或者object是变量

`range([start,] stop[, step])`，创建一个整数列表

**基本输入与输出**

input(prompt)函数：首先输出prompt，等待用户输入，直到用户按回车结束，返回用户输入的字符串（不包括最后的回车）

print(value1,value2,…,sep=‘ ’,end=‘\n’,file=sys.stdout)：将多个值转换为字符串并且输出到相应的文件file，这些值之间以sep分隔，最后以end结束，sep缺省为空格，end缺省为换行，file缺省为标准输出(屏幕)

### 常见内置模块

相互之间有相应联系的一些函数以及变量组织在一起，放到同一个Python源文件（.py)，这个.py文件就是一个模块（module），提高了代码的可维护性和可重用性，不同模块属于不同的名字空间，可以避免函数名和变量名冲突。

使用模块：

`import 模块名 [as 别名]`

可以使用`sys.modules.items()`显示所有预加载模块的相关信息。

`sys.builtin_module_names`给出了Python解释器内置的模块

可以使用`dir`函数查看任意模块中所有的对象列表，如果调用不带参数的`dir()`函数，则返回当前脚本的所有对象列表。

可以使用`help`函数查看任意模块或函数的使用帮助。

访问模块中的对象，采用模块名.对象或者别名.对象方式，

`from 模块名 import 对象名[ as 别名]`

仅仅从模块中导入特定的对象，访问对象时不再需要包括模块名，可以减少查询次数，提高执行速度

例子：

```python
import math
math.sin(0.5)       #求0.5的正弦
from math import sin as f #别名
f(3)
>>> 0.1411200080598672
sin(30) # 不带模块名
-0.9880316240928618
```

导入的模块保存在字典sys.modules中

`from math import *`从模块中导入所有的对象

多个模块中有同样的对象名时造成混乱，因此谨慎使用

**寻找要导入的模块文件**

导入模块时会从sys.path给出的目录列表中查找

```python
import sys
sys.path
>>>['', 'C:\\Program Files (x86)\\Python35\\python35.zip', 'C:\\Program Files (x86)\\Python35\\DLLs', 'C:\\Program Files (x86)\\Python35\\lib', 'C:\\Program Files (x86)\\Python35', 'C:\\Program Files (x86)\\Python35\\lib\\site-packages']
```

* 通过`append`自定义的目录到sys.path可以扩展搜索路径

* 注意搜索顺序可能导致没有导入正确的模块

* 在导入模块时，会优先导入相应的pyc文件，如果相应的pyc文件与py文件时间不相符，则导入py文件并重新编译该模块。

#### math模块

`import math` 或者 `from math import *`

`math.pi`: 数学常量 𝜋 print(math.pi) = 3.141592653589793

`math.e`: 数学常量e math.e = 2.718281828459045

|   **函数**   |       **含义**       |        **实例**        |      **结果**       |
| ------------ | ------------------- | ---------------------- | ------------------ |
| fabs(x)      | 绝对值，返回float     | fabs(-3)               | 3.0                |
| ceil(x)      | 大于等于x的最小的整数 | ceil(1.2),ceil(-1.6)   | (2,-1)             |
| floor(x)     | 小于等于x的最大的整数 | floor(1.8),floor(-2.1) | (1,-3)             |
| trunc(x)     | 截取为最接近0的整数   | trunc(1.2),trunc(-2.8) | (1,-2)             |
| factorial(x) | 整数x(>=0)的阶乘     | factorial(5)           | 120                |
| sqrt(x)      | x(>=0)的平方根       | sqrt(2)                | 1.4142135623730951 |
| exp(x)       |        e\*\*x             |     exp(5)                   | 148.4131591025766                   |
| log(x\[,base\]) | 以base为底的对数，base没有则为以e为底的自然对数 | log(math.e**2), log(4,2) | (2.0,2.0)    |                     |                        |                    |
| sin(x)       | x的正弦              | sin(pi/2)              | 1.0                |
| cos(x)       | x的余弦              | cos(2*pi)              | 1.0                |
| tan(x)       | x的正切              | tan(pi/4)              | 0.9999999999999999 |
| asin(x)      | x的反正弦            | asin(1)                | 1.5707963267948966 |
| acos(x)      | x的反余弦            | acos(1)                | 0.0                |
| atan(x)      | x的反正切            | atan(1)                | 0.7853981633974483 |
| degrees(x)   | x从弧度转换为角度     | degrees(pi)            | 180.0              |
| radians(x)   | x从角度转换为弧度     | radians(90)            | 1.5707963267948966 |

#### Random模块

```python
import random
r=random.randint(0,25)
print("The character is",chr(r+ord('a'))) # 随机小写英文字母
```

|        **函数**         |                **含义**                 |
| ----------------------- | -------------------------------------- |
| random()                | 返回在[0,1]区间的随机实数                |
| uniform(a,b)            | 返回在[a,b]区间的随机实数                |
| randint(a,b)            | 返回在[a,b]区间的随机整数                |
| choice(seq)             | 返回序列seq中的随机一个元素              |
| sample(seq,n)           | 从序列seq中随机选择 n个不同的元素         |
| shuffle(list)           | 将列表随机排序                          |
| normalvariate(mu,sigma) | 生成服从均值为mu，方差为sigma的随机浮点数 |

使用方法：`random.random()`;`random.choice(alist)`

```python
生成指定数量随机数
[random.randint(0,100) for _ in range(10)]
```

设定种子，加入代码`random.seed(n)`，n是整数，即可，设定种子后，随机生成的数字将会一样.

> 貌似normalvariate不受种子影响

`random.seed(random.random())`

#### time 和 calendar

**基础语法：**

```python
import time  # 引入time模块
ticks = time.time()  # 获取时间戳，只能用于1970-2038年，结果如1568425413.2062666
localtime = time.localtime(time.time()) # 时间戳转化为时间元组
# 结果如time.struct_time(tm_year=2019, tm_mon=9, tm_mday=14, tm_hour=9, tm_min=46, tm_sec=59, tm_wday=5, tm_yday=257, tm_isdst=0)
# 其中tm_wayday表示周几（0-6，0是周一），tm_yday表示一年中第几天，tm_isdst表示是否夏令时（0否1是-1未知）
# getime()返回格林威治天文时间下的时间元组
localtime = time.asctime( time.localtime(time.time()) ) # 时间元组格式化，结果如'Sat Sep 14 09:50:12 2019'

time.perf_counter()  # 返回系统运行时间
time.process_time()  # 返回进程运行时间
time.spleep(secs)        # 推迟调用线程的运行，secs指秒数。
```

**时间格式化：**

```python
import time
time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())
# 格式化成2019-09-14 09:56:28的格式

a = "Sat Mar 28 22:24:24 2016"
time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y"))
# 将格式字符串转换为时间戳
# 字符串放在前面，元组放在后面
```

日期格式化符号

- %y 两位数的年份表示（00-99）
- %Y 四位数的年份表示（000-9999）
- %m 月份（01-12）
- %d 月内中的一天（0-31）
- %H 24小时制小时数（0-23）
- %I 12小时制小时数（01-12）
- %M 分钟数（00=59）
- %S 秒（00-59）
- %a 本地简化星期名称
- %A 本地完整星期名称
- %b 本地简化的月份名称
- %B 本地完整的月份名称
- %c 本地相应的日期表示和时间表示
- %j 年内的一天（001-366）
- %p 本地A.M.或P.M.的等价符
- %U 一年中的星期数（00-53）星期天为星期的开始
- %w 星期（0-6），星期天为星期的开始
- %W 一年中的星期数（00-53）星期一为星期的开始
- %x 本地相应的日期表示
- %X 本地相应的时间表示
- %Z 当前时区的名称
- %% %号本身

**calendar**

```python
import calendar
calendar.month(year,month[,w=2,l=1])
# 返回一个多行字符串格式的year年month月日历，两行标题，一周一行。每日宽度间隔为w字符。每行的长度为7* w+6。l是每星期的行数。
calendar.calendar(year[,w=2,l=1,c=6])
# 返回一个多行字符串格式的year年年历，3个月一行，间隔距离为c。 每日宽度间隔为w字符。每行长度为21* W+18+2* C。l是每星期行数。
calendar.firstweekday( )
# 返回当前每周起始日期的设置。默认情况下，首次载入caendar模块时返回0，即星期一。
calendar.setfirstweekday(weekday)
# 设置每周的起始日期码。0（星期一）到6（星期日）。
calendar.isleap(year)
# 是闰年返回 True，否则为 false。
calendar.leapdays(y1,y2)
# 返回在Y1，Y2两年之间的闰年总数。
calendar.monthcalendar(year,month)
# 返回一个整数的单层嵌套列表。每个子列表装载代表一个星期的整数。Year年month月外的日期都设为0;范围内的日子都由该月第几日表示，从1开始。
calendar.monthrange(year,month)
# 2. 返回两个整数。第一个是该月的第一天是星期几，第二个是该月有几天。星期几是从0（星期一）到 6（星期日）。
calendar.weekday(year,month,day)
# 2. 返回给定日期的星期码。
```

## python 序列

### 序列

序列：是一系列连续值（对象），它们通常是相关的，并且按一定顺序排列。

序列中每个组成部分称为“元素”。

Python中常用的序列结构有列表、元组、字典、字符串、集合以及range等等。

|     |    可变    |       不可变        |
| --- | --------- | ------------------- |
| 有序 | 列表       | 元组*、字符串 |
| 无序 | 字典、集合 |                     |

\* 元组的元素如果可变，则元组也可变。

有序序列（列表、元组、字符串）支持双向索引，第一个元素下标为0，第二个元素下标为1，以此类推；最后一个元素下标为-1，倒数第二个元素下标为-2，以此类推。

**scipy.optimize**

* leastsq：可求任意多项式的最小二乘

```python
leastsq(func, x0, [args=(), Dfun=None, full_output=0, col_deriv=0, ftol=1.49012e-08, xtol=1.49012e-08, gtol=0.0, maxfev=0, epsfcn=0.0, factor=100, diag=None, warning=True])
# func 是我们自己定义的一个计算误差的函数，
# x0 是计算的初始参数值
# args 是指定func的其他参数
import numpy as np
import scipy as sp
from scipy.optimize import leastsq
 
##样本数据(Xi,Yi)，需要转换成数组(列表)形式
Xi=np.array([160,165,158,172,159,176,160,162,171])
Yi=np.array([58,63,57,65,62,66,58,59,62])
 
##需要拟合的函数func :指定函数的形状y = k*x + b
def func(p,x):
    k,b=p
    return k*x+b 
##偏差函数：x,y都是列表:这里的x,y和上面的Xi,Yi中是一一对应的
def error(p,x,y):
    return func(p,x)-y
#k,b的初始值，可以任意设定,经过几次试验，发现p0的值会影响cost的值：Para[1]
p0=[1,20]
#把error函数中除了p0以外的参数打包到args中(使用要求)
Para=leastsq(error,p0)
```

* fmin：求某函数在某点附近的极小值。`fmin(func, x0)`，x0值或数组

#### 常用内置函数

* 序列大小比较：可以直接使用关系运算符来比较数值或序列（列表、元组、字符串）的大小，也可以使用对象的“__le__()”及其相关方法。

```python
'ABC' < 'C' < 'Pascal' < 'Python'
>>> True
a = [1, 2]
b = [1, 2, 3]
a.__le__(b)
>>> True
a.__gt__(b)
>>> False
```

* len(列表)：返回列表中的元素个数，同样适用于元组、字典、字符串等等。

* max(列表)、 min(列表)：返回列表中的最大或最小元素，同样适用于元组、range。

* sum(列表)：对数值型列表的元素进行求和运算，对非数值型列表运算则出错，同样适用于元组、range。

#### 序列解包(sequence unpacking)

序列解包用来对多个对象引用(变量等)同时赋值 LHS= RHS，对象引用可以是变量名，可以是通过下标或者切片描述的多个list元素。 对象引用可以通过圆括号、方括号来组织，通过逗号来分割。RHS可以是任何可迭代对象，包括tuple、list、dict、range、str等，逐个取该序列的元素赋予左边对应位置的对象引用

除了在有带星号的对象引用（*seq）外，要求RHS为与LHS对应的相同数量元素的可迭代对象。**带星号的对象引用应该最多只出现一次**，该引用前后的变量一一对应赋值后，剩余的变量转变为list然后赋予该引用

```python
(x, y, z) = (False, 3.5, 'exp')
x
>>> False
x,y,z
>>> (False, 3.5, 'exp')
a,*b,c = range(1,7)
a,b,c
>>> (1, [2, 3, 4, 5], 6)
```

* 序列解包对于字典同样有效：后面再讲

```python
b, c, d={'a':1,'b':2,'c':3}
b, c, d
>>> ('a', 'b', 'c')
```

* 序列解包可以嵌套

```python
a,[b,(c,d)] = 1,['hello', ('Steve','Lee')]
a,b,c,d
>>> (1, 'hello', 'Steve', 'Lee')
```

* 序列解包中，变量引用可以是元素或者切片

```python
list1 = list(range(12))  
x, y, list1[-1], list1[0:5] = 3,4,0,range(-5,0)
list1
>>> [-5, -4, -3, -2, -1, 5, 6, 7, 8, 9, 10, 0]
```

* zip(列表1,列表2,…):将多个列表对应位置元素组合为元组，并返回包含这些元组的zip对象。Zip对象可以进一步用list()函数转换为列表对象。

```python
aList = [1, 2, 3]
bList = [4, 5, 6]
cList = zip(aList, bList)
cList
>>> <zip object at 0x0000000003728908>
list(cList)			
>>> [(1, 4), (2, 5), (3, 6)]
```

```python
keys=['a','b','c']
values=[1,2,3]
for k,v in zip(keys,values):
	print(k,v)
>>> a 1
>>> b 2
>>> c 3
```

* enumerate(列表)：枚举列表元素，返回枚举对象，其每个元素为包含下标和值的元组。该函数对元组、字符串同样有效。

```python
dList = [5, 6, 7]
for item in enumerate(dList):
	print(item)
>>> (0, 5)
>>> (1, 6)
>>> (2, 7)
```

```python
aList = [1,2,3]
bList = [4,5,6]
cList = [7,8,9]
dList = zip(aList, bList, cList)
for index, value in enumerate(dList):
	print(index, ':', value)
>>> 0 : (1, 4, 7)
>>> 1 : (2, 5, 8)
>>> 2 : (3, 6, 9)
```

注：枚举对象（如enumerate对象）只能用一次，再用时需要再创建一次，zip也是

#### 可迭代对象、迭代器和生成器、yield

* iterable（可迭代对象）: iterable对象包括：str, list, tuple, dict, set, range。其特征是可以多次访问，一般而言能多次使用for语句的都是iterable对象。可迭代对象所有值均存储在内存中，不管你需要与否。

* iterator（迭代器）: 包含__next__()方法，调用其获得下一个元素。iterator包括：reversed(), zip(), enumerate()，map()，另外生成器推导式也会生成iterator。可通过内置函数 iter(iterable)将iterable对象转换成iterator。你仅仅能迭代一次（也即只能使用一次for语句），因为它们并不存储所有值，而是运行时才生成值，且会释放前一个运行值。

* for var in iterator 循环相当于每次取可迭代对象或者迭代器的下一个元素，执行一系列语句，然后取下一个元素执行，直到遍历结束抛出异常StopIteration。 

* 生成器(generator)给出了更方便的创建iterator的手段，在函数中加入关键词`yield`，该函数即变为生成器。

```python
# Yield类似return，但是它返回的是iterator
def createGenerator():
    mylist = range(3)
    for i in mylist:
        yield i*i

print(createGenerator())
>>> <generator object createGenerator at 0x000001485E3C47D8>
for i in createGenerator():
    print(i)
>>> 0
    1
    4

# 注意当你调用createGenerator()时它是不运行的，只会返回generator object
# 只有使用这个generator object时才会运行，而且是一次性产品，必须要再次调用函数才能继续用
```

注意：如果有循环的话，当你第一次调用函数产生的generator object时，它会从头运行代码到yield，然后返回循环的第一个值，接着第二次调用返回循环第二个值……直到所有值均迭代完后，继续下一块代码。

```python
def demoIterator():
    print("I'm in the first call of next()")
    for i in range(3):
        yield i**i
    print("I'm in the second call of next()")
    yield 3

for i in demoIterator():
    print(i)

>>> I'm in the first call of next()
    1
    1
    4
    I'm in the second call of next()
    3
```

### 列表

* 列表是Python中内置可变序列，是若干元素的有序集合。

* 列表中的每一个数据称为元素，列表的所有元素放在一对中括号“[”和“]”中，并使用逗号分隔开；

* 在Python中，一个列表中的数据类型可以各不相同，可以同时分别为整数、实数、字符串等基本类型，甚至是列表、元素、字典、集合以及其他自定义类型的对象。

* 列表元素的访问：第一个元素下标为0，第二个元素下标为1，以此类推；最后一个元素下标为-1，倒数第二个元素下标为-2，以此类推。二维数组的访问：aList[0][0]。

* 列表对象的修改：当为对象修改值时，并不是真的直接修改变量的值，而是使变量指向新的值，这对于列表变量也是一样的。

```python
id(li=[100, "123"])
>>> 46614248
li[0]='200'
id(li)
>>> 46614248
```

|       **方法**        |             **说明**             |
| --------------------- | ------------------------------- |
| list.append(x)        | 将元素x添加至列表尾部             |
| list.extend(L)        | 将列表L中所有元素添加至列表尾部    |
| list.insert(index, x) | 在列表指定位置index处添加元素x    |
| list.remove(x)        | 在列表中删除首次出现的指定元素     |
| list.pop(\[index\])   | 删除并返回列表对象指定位置的元素   |
| list.clear()          | 删除列表中所有元素，但保留列表对象 |
| list.index(x)         | 返回值为x的首个元素的下标         |
| list.count(x)         | 返回指定元素x在列表中的出现次数    |
| list.reverse()        | 对列表元素进行原地逆序            |
| list.sort()           | 对列表元素进行原地排序            |
| list.copy()           | 返回列表对象的浅拷贝              |

#### 列表创建与删除

* 使用等号`=`创建

* 或者，也可以使用list()函数将元组、range对象、字符串或其他类型的可迭代对象类型的数据转换为列表。例如：

```python
list('hello world')
>>> ['h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd']
```

* 当不再使用时，**使用del命令删除整个列表**，如果列表对象所指向的值不再有其他对象指向，Python将同时删除该值。

#### 列表元素的增加

（1） 可以使用“+”运算符来实现将元素添加到列表中的功能。

虽然这种用法在形式上比较简单也容易理解，但严格意义上来讲，这并不是真的为列表添加元素，而是创建一个新列表，并将原列表中的元素和新元素依次复制到新列表的内存空间。**所相加的必须也为列表**。

由于涉及大量元素的复制，该操作速度较慢，在涉及大量元素添加时不建议使用该方法。

```python
aList = aList + [7]
```

（2）使用列表对象的append()方法，**原地修改列表**，是真正意义上的在列表尾部添加元素，速度较快，也是推荐使用的方法。

```python
aList.append(9)
```

（3）使用列表对象的extend()方法，在该列表对象尾部**增加另一列表**。通过extend()方法来增加列表元素也不改变其内存地址，属于原地操作。

```python
aList.extend([4,5,6])
```

（4）使用列表对象的**insert()**方法将元素添加至列表的指定位置。

**注意：**

1.insert()方法会涉及到插入位置之后所有元素的移动，这会影响处理速度。

2.列表删除方法remove()和pop()弹出非尾部元素时，也有类似问题。

**建议：**除非有必要，否则应尽量避免在列表中间位置插入和删除元素的操作，而是优先考虑使用前面介绍的append()方法和下一小节介绍的pop()方法。

（5）使用**乘法**来扩展列表对象，将列表与整数相乘，生成一个新列表，新列表是原列表中元素的重复。

该操作实际创建一个新列表，而不是原地修改。当使用“*”运算符将包含列表的列表重复并创建新列表时，并不创建元素的复制，而是创建已有对象的引用。每个重复元素所指向对象（地址）是相同的。

“*”运算符还可以用来创建多维数组，但需要注意的是通过乘法复制并不创建元素值的复制，而是创建已有元素对象的引用复制。因此，**当修改其中一个值时，相应的引用也会被修改**

例如：

```python
[1,2,3] * 3
>>> [1, 2, 3, 1, 2, 3, 1, 2, 3]
x = [[1,2,3]]*3
x
>>> [[1, 2, 3], [1, 2, 3], [1, 2, 3]]
x[0][0] = 10
x
>>> [[10, 2, 3], [10, 2, 3], [10, 2, 3]]
```

**各种列表元素增加方法的比较**

           

|     | 列表元素增加方法 | 别名 |   效果   |
| --- | --------------- | ---- | ------- |
| 1   | +               | 拼接 | 新建列表 |
| 2   | append          | 附加 | 原地修改 |
| 3   | extend          | 扩展 | 原地修改 |
| 4   | insert          | 插入 | 原地修改 |
| 5   | *               | 复制 | 新建列表 |

#### 列表元素的删除

（1）使用**del命令**删除列表中的指定位置上的元素。前面已经提到过，del命令也可以直接删除整个列表，这里不再赘述。`del alist[1]`

（2）使用列表的**pop()方法**删除并返回指定（默认为最后一个）**位置**上的元素，如果给定的索引超出了列表的范围则抛出异常。`a_list.pop(1)`


（3）使用列表对象的**remove()方法**删除首次出现的指定**元素**，如果列表中不存在要删除的元素，则抛出异常。`a_list.remove('a')`

在使用循环进行列表元素删除时，需要使用正确的方法。例如大家会很自然地想到使用“循环+remove()”的方法 删除列表中指定元素的所有重复。例如，下面的代码成功地删除了列表中的重复元素，执行结果是完全正确的。

```python
x = [1,2,1,2,1,2,1,2,1]
for i in x:
    if i == 1:
    x.remove(i)      
x
>>> [2, 2, 2, 2]
```
然而，上面这段代码的逻辑是错误的，尽管执行结果是正确的。因为每当插入或删除一个元素之后，该元素位置后面所有元素的索引就都改变了。

**怎么办？**

1. 在循环的判断条件部分，使用列表的切片替代原始列表，这样即使原始列表因元素删除或增加而变化，切片不会变化。

2. 使用正确的顺序，例如从后往前依次判断。

正确的代码：

```python
# 代码1：
x = [1,2,1,2,1,1,1]
for i in x[::]:
	if i == 1:
		x.remove(i)

# 看着类似于新设一个y，然后令y=x，但不是这样的。切片是浅拷贝，操作x不影响x的原始切片，但是会影响y（因为=是深拷贝）

# 代码2：
x = [1,2,1,2,1,1,1]
for i in range(len(x)-1,-1,-1):
	if x[i]==1:
		del x[i]
```

#### 列表元素访问与计数

（1）使用下标直接访问列表元素。`alist[3]``alist[i][j]`

（2）使用列表对象的index方法获取指定元素首次出现的**下标**

语法：L.index(value, [start, [stop]])

（3）使用列表对象的count方法统计指定元素在列表对象中出现的次数。`aList.count(0)`

#### 成员资格判断

判断列表中是否存在指定的值

（1）可以使用前面介绍的count()方法，如果存在则返回大于0的数，如果返回0则表示不存在。

（2）或者，使用更加简洁的“in”关键字来判断一个值是否存在于列表中，返回结果为“True”或“False”。关键字in也可用于其他可迭代对象，包括元组、字典、range对象、字符串、集合等。常在循环中使用关键字in对可迭代对象的元素进行遍历。

#### 切片操作

切片是Python序列的重要操作之一，适用于列表、元组、字符串、range对象等类型。

参数：切片使用2个冒号分隔的3个数字来完成，第一个数字表示切片开始位置（默认为0），第二个数字表示切片截止（但不包含）位置（默认为列表长度），第三个数字表示切片的步长（默认为1），当步长省略时可以顺便省略最后一个冒号。

返回值：切片返回的是列表元素的浅拷贝。

功能：可以使用切片来截取列表中的任何部分，得到一个新列表，也可以通过切片来修改和删除列表中部分元素，甚至可以通过切片操作为列表对象增加元素。

**切片返回的是列表元素的浅拷贝**

```python
aList = [3, 5, 7]

bList = aList 	#bList与aList指向同一个内存
bList[1] = 8
aList
>>> [3, 8, 7]
aList == bList
>>> True
aList is bList
>>> True

bList = aList[::]
aList == bList
>>> True
aList is bList
>>> False
bList[1] = 8
bList
>>> [3, 8, 7]
aList
>>> [3, 5, 7]

a[-2:] # 截取最后两位
a[:-3] # 截取开头到倒数第三位之前
a[-1]  # 截取最后一位
```

（1）功能1：可以使用切片来截取列表中的任何部分，得到一个新列表。

```python
a[100:]
>>> []
```

与使用下标访问列表元素的方法不同，切片操作不会因为下标越界而抛出异常，而是简单地在列表尾部截断或者返回一个空列表，代码具有更强的健壮性。

（2）功能2：可以使用切片来原地修改列表内容

```python
aList = [3, 5, 7]
aList[len(aList):] = [9]
aList
>>> [3, 5, 7, 9]
aList[:3] = []
aList
>>> [9]
```
切片操作确实是返回原列表的副本，但是如果把切片作为左值使用的话（在赋值号左边出现），内核会对原件进行修改。

（3）功能3：del与切片结合来删除列表元素

```python
aList = [3,5,7,9]
del aList[:3]
aList
>>> [9]
```

#### 列表排序

（1）使用列表对象的**sort方法**进行**原地排序**，支持多种不同的排序方法

```python
list.sort([key=None], [reverse=False]) # 默认升序

aList = [3, 4, 5, 6, 7, 9, 11, 13, 15, 17]
aList.sort(key = lambda x:len(str(x)))
aList
>>> [9, 7, 6, 5, 4, 3, 17, 15, 13, 11]
```

（2）使用**内置函数sorted**对列表进行排序并返回**新列表**，`sorted(aList,reverse = True)`

（3）使用列表对象的**reverse方法**将元素**原地逆序**，`aList.reverse()`

（4）使用**内置函数reversed方法**对列表元素进行逆序排列并返回迭代对象，`reversed(aList)`

```python
aList = [3, 4, 5, 6, 7, 9, 11, 13, 15, 17]
newList = reversed(aList)
newList
>>> <list_reverseiterator object at 0x0000000003624198>
list(newList)    # 第二次list(newList)时返回空值，代表已经结束迭代
[17, 15, 13, 11, 9, 7, 6, 5, 4, 3]
for i in newList:
	print(i)
# 无输出内容，迭代对象已遍历结束，需要重新创建迭代对象
print(list(reversed(aList)))
>>>[17, 15, 13, 11, 9, 7, 6, 5, 4, 3]
```

#### 列表推导式

列表推导式（list comprehension）是利用其他列表创建新列表的一种方法。

语法： [表达式 for 变量 in 列表]    或者  [表达式 for 变量 in 列表 if 条件] 

使用列表推导式来快速生成包含多个随机数的列表，可以看出，列表推导式使用非常简洁的方式来快速生成满足特定需求的列表，代码具有非常强的可读性。例如：

```python
aList = [x*x for x in range(10)]
# 相当于
aList = []
for x in range(10):
	aList.append(x*x)
```

* 过滤不符合条件的元素——if子句

```python
aList = [-1,-4,6,7.5,-2.3,9,-11]
[i for i in aList if i>0]
>>> [6, 7.5, 9]
```

* 列出当前文件夹下所有Python源文件——if子句

```python
[filename for filename in os.listdir('.') if filename.endswith('.py')]
```

* 使用列表推导式实现嵌套列表的平铺——for子句嵌套(从外向里套)

```python
vec = [[1,2,3], [4,5,6], [7,8,9]]
[num for elem in vec for num in elem] 
# 目标元素 for 一级元素[列表] in 顶级列表 for 二级元素（目标元素） in 一级列表
>>> [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

* 在列表推导式中**使用多个循环**，实现多序列元素的任意组合，并且可以结合条件语句过滤特定元素

```python
 [(x, y) for x in range(3) for y in range(3)]
>>> [(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2)]
[(x, y) for x in [1, 2, 3] for y in [3, 1, 4] if x != y]
>>> [(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

* 列表推导式中可以使用函数或复杂表达式——复杂表达式

```python
def f(v):
    if v%2 == 0:
        v = v**2
    else:
        v = v+1
    return v
print([f(v) for v in [2, 3, 4, -1] if v>0])
>>> [4, 4, 16]
print([v**2 if v%2 == 0 else v+1 for v in [2, 3, 4, -1] if v>0])
>>> [4, 4, 16]
```

* 使用列表推导式实现矩阵转置

```python
matrix = [ [1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]] 
[[row[i] for row in matrix] for i in range(4)] 
>>> [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

* 也可以使用内置函数来实现矩阵转置

```python
list(zip(*matrix)) # *参见序列解包
>>> [(1, 5, 9), (2, 6, 10), (3, 7, 11), (4, 8, 12)] 
```

* 列表推导式支持文件对象迭代

```python
fp = open('C:\install.log', 'r')
print([line for line in fp]) 
fp.close()
```

例：使用列表推导式生成100以内的所有素数

```python
[p for p in range(2, 100) if 0 not in [ p% d for d in range(2, int(math.sqrt(p))+1)] ]
>>> [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]
```

### 元组

元组和列表类似，但属于不可变序列。元组一旦创建，用任何方法都不可以修改其元素。

元组的定义方式和列表相同，但定义时所有元素是放在一对圆括号“（”和“）”中，而不是方括号中。

注意：如果创建只有一个元素的元组，需要在元素后面加上一个逗号“,”。

```python
a=(3)
a
>>> 3
a=3,	#在不引起歧义时，括号可省略。
a
>>> (3,)
```

#### 元组创建与删除

* 使用tuple函数将其他序列转换为元组

```python
s = tuple() #空元组
```

* 使用del删除元组对象，不能删除元组元素

#### 元组访问

与list、str一样，可以通过`[下标]`访问某个元素，也可以使用切片操作

tuple的元素可以是可变对象，**tuple不可变，指的是其元素不可变，但是元素指向的对象的可变并没有限制。比如元祖中的列表不可删掉，但因为其本身就是可变对象，所以可以修改元祖中列表的元素**

**即：元组中的元素不可变，但当元素所指向的对象可变，则该对象的值是可变的。**

```python
x = (1,2,[4,5]) 
x[2] = [5,5] 
>>> TypeError: 'tuple' object does not support item assignment
x[2][0] = 5 
x 
>>> (1, 2, [5, 5])
```

除了索引（下标）和切片访问外，还支持其他序列的基本操作：+，*，in，not in，count(x)，index(value,[start,[stop]])，<   <=   ==   !=  >=   >，sorted(iterable)，len(iterable)、max(iterable)、min(iterable)、sum(iterable)，enumerate(iterable)，zip(iter1,iter2…)

#### 元组与列表的区别

* 元组中的元素一旦定义就不允许更改。

* 元组没有append()、extend()和insert()等方法，无法向元组中添加元素；

* 元组没有remove()或pop()方法，也无法对元组元素进行del操作，不能从元组中删除元素。

* 内建的tuple( )函数接受一个列表参数，并返回一个包含同样元素的元组，而list( )函数接受一个元组参数并返回一个列表。从效果上看，tuple( )冻结列表，而list( )融化元组。

* 元组的速度比列表更快。如果定义了一系列常量值，而所需做的仅是对它进行遍历，那么一般使用元组而不用列表。

* 元组对不需要改变的数据进行“写保护”将使得代码更加安全。

* 一些元组可用作字典键（特别是包含字符串、数值和其它元组这样的不可变数据的元组）。列表永远不能当做字典键使用，因为列表不是不可变的。


#### 生成器推导式(一次性对象)

* 生成器推导式与列表推导式非常接近，只是生成器推导式使用圆括号而不是列表推导式所使用的方括号。

* 生成器推导式的结果是一个iterator。

* 可将其转化为列表或元组，也可使用iterator的`__next__()`方法（Python 3.x）进行遍历，也可采用内置函数next(obj)

* iterator访问时元素指针会往前移动。所有元素访问结束时，下一个元素会抛出异常StopIteration

```python
g=((i+2)**2 for i in range(3))
g
>>> <generator object <genexpr> at 0x02B15C60>
tuple(g)
>>> (4, 9, 16,)
tuple(g)
>>> ()

g=((i+2)**2 for i in range(3))
next(g)     # g.__next__() 
>>> 4
next(g)
>>> 9
……
StopIteration
```

**补充： 

**生成器推导式：例子**

毕达哥拉斯三元数组：存在{x,y,z}, 0<x<y<z,使得x^2+y^2=z^2。求前10个毕达哥拉斯三元数组

```python
pyt = [(x,y,z) for z in range(100) for y in range(1,z) for x in range(1,y) if x*x + y*y == z*z ]
firstN_pyt = pyt[:10]
print(firstN_pyt)  #运行代码，找出结果

pyt = ((x,y,z) for z in range(1000) for y in range(1,z) for x in range(1,y) if x*x + y*y == z*z )   #记住命令，不运行，速度更快
firstN_pyt = [next(pyt) for x in range(10) ] 
print(firstN_pyt )
```

### 字典

* 字典是包含键-值对的无序的可变序列，也称为映射（map）类型。给出了键和值的映射关系

* 键(keys)不允许重复，==关系。不要求不同元素的key为同一种类型。

* keys可以为任意不可变对象（数据），比如整数、实数、复数、字符串、元组等。可变对象不能作为key

* 无序：不是按照key的大小顺序排列，实际上是按照key的hash值顺序

* 值(values)可以是任何对象，每个key对应着一个值，可以通过key查询到其对应的值

* Python环境中许多内置函数和变量使用了dict。如：sys.modules 返回当前已经加载的模块名与模块对象的映射；globals()返回包含当前作用域内所有全局变量和值的字典；locals()返回包含当前作用域内所有局部变量和值的字典

#### 字典创建与删除

* 大括号界定，元素用key:value表示，元素间用逗号分隔

{key1:value1 ,key2:value2, … ,keyN:valueN }

* 可以通过dict(iterable)函数来创建dict对象：新字典的元素来自于iterable，每个元素必须包括两个子元素

```python
adict = dict(enumerate(range(0,20,2)))
adict
>>> {0: 0, 1: 2, 2: 4, 3: 6, 4: 8, 5: 10, 6: 12, 7: 14, 8: 16, 9: 18}

dict(['one', 'two', 'three'], [1, 2, 3])
dict([['one',1],('two',2),['three',3]])
dict({'three': 3, 'one': 1, 'two': 2})
dict(one=1, two=2, three=3)
```

* 通过dict类方法创建新字典，每个元素的key来自于序列对象，值设置为value，缺省为None。`dict.fromkeys(seq[,value])`

```python
dict1=dict.fromkeys(['name','age','sex'])
dict1 
>>> {'age': None, 'name': None, 'sex': None}
dict2 = dict.fromkeys(range(5),10) 
dict2 
>>> {0: 10, 1: 10, 2: 10, 3: 10, 4: 10}
```

* 使用del删除整个字典: del dict2

* len(d): 返回字典中元素的个数

#### 字典元素的读取：下标

以**键（不能用下标值）**作为下标可以访问字典元素，若键不存在则抛出异常KeyError，`aDict['name']`           

|            方法             |                                说明                                |
| --------------------------- | ------------------------------------------------------------------ |
| d\[key\]                    | 返回key对应的value，key不存在raise KeyError                         |
| d.get(key\[,default\])      | 返回key对应的value，key不存在时返回default，缺省为None               |
| d.keys()                    | 返回可迭代对象，其中元素为字典中的所有key                             |
| d.values()                  | 返回可迭代对象，其中元素为字典中的所有value                           |
| d.items()                   | 返回可迭代对象，其中元素为包括了(key,value)的元组                     |
| key in d<br>key not in d    | 判断字典d中有没有键==key，返回True or False。相当于 key in d.keys()  |
| d\[key\] = value            | 设置字典中键=key的元素的值为value，如果不存在，则添加key:value        |
| setdefault(key\[,default\]) | 如果key不在字典里插入新元素，其值为default(缺省None)。如果在不更新。返回d\[key\] |
| update(other)               | 根据另一字典或元素为key/value对的可迭代对象更新字典，返回None          |
| del d\[key\]                | 删除元素，如果key不存在，raise KeyError                              |
| popitem()                   | 随机返回并删除字典中的一对键和值(一般删除末尾对)。                     |
| pop(key)                    | 如果key存在删除对应元素并返回值，否则raise KeyError                  |
| pop(key,fault)              | 如果key存在删除对应元素并返回值，否则返回fault                        |
| clear()                     | 清除所有元素                                                        |
| copy()                      | 返回shallow copy后的新字典                                          |


#### 字典元素的读取: get()，可用来添加

* d.get(key\[,default\]) ： 返回key对应的value，key不存在时返回None，若想设定不存在时返回特定值，则可以加上default（比如‘SDIBT’），key不存在时可以返回SDIBT（key存在则无影响）.

* 另外，key不存在时会自动往字典中添加这个key！

```python
aDict['score'] = aDict.get('score',[])
aDict['score'].append(98)
aDict['score'].append(97)
aDict
>>> {'age': 37, 'score': [98, 97], 'name': 'Dong', 'sex': 'male'}
```

下面代码实现了统计字符串各个字符数量的功能：

```python
chars = "abcefghiacscaf"
cntdict = dict()
for ch in chars:
    cntdict[ch] = cntdict.get(ch,0) + 1
```

这串代码创建了一个字符为key,数量为value的字典，非常值得学习

#### 字典元素的添加与修改：d[key]=value

当以指定键为下标为字典赋值时，若键存在，则可以修改该键的值；若不存在，则表示添加一个键、值对。

**更新多个键值，d.update(another)**，将另一个字典another的键、值对添加到当前字典对象

```python
d= {'age': 37, 'score': [98, 97], 'name': 'Dong', 'sex': 'male'}
d.update({'age':38,'city':'shanghai'})
d
{'age': 38, 'score': [98, 97], 'name': 'Dong', 'city': 'shanghai', 'sex': 'male'}
```

#### 字典应用案例

**例一：**下面的代码首先生成包含1000个随机字符的字符串，然后统计每个字符的出现次数。

```python
import string
import random

def generateChars(N=100):
    global charset
    charset = string.ascii_letters + string.digits + string.punctuation
    g = (random.choice(charset) for _ in range(N))
    chars= ''.join(g)
    return chars

def process(chars):
    cntdict = dict()
    #for ch in charset:
    #    cntdict[ch] = 0
    for ch in chars:
        cntdict[ch] = cntdict.get(ch,0) + 1 #不存在则返回零，存在则加1 #
    return cntdict

def output(cntdict,N=20):
    #print(cntdict)
    mlist = [(value,key) for key,value in cntdict.items()]
    mlist.sort() #reverse=True
    for idx in range(20):
        print("{}: {}  ".format(mlist[idx][1],mlist[idx][0]),end="")
        if((idx+1)%6==0):  # 每隔6个换行
            print()
    #print(mlist)

def main():
    chars = generateChars(100)
    countdict = process(chars)
    output(countdict)

if __name__ == "__main__":
    main()
```

* 也可以使用collections模块的defaultdict类（提供缺省值的dict）来实现该功能。

```python
import string
import random

x = string.ascii_letters + string.digits + string.punctuation
y = [random.choice(x) for i in range(1000)]
z = ''.join(y)

from collections import defaultdict
frequences = defaultdict(int)

'''
括号里可以是list、set、str等等，作用是当key不存在时，返回的是工厂函数的默认值，比如list对应[ ]，str对应的是空字符串，set对应set( )，int对应0
'''

for item in z:
    frequences[item] += 1

print(frequences.items())
```

* 使用collections模块的Counter类可以快速实现这个功能，并且能够满足其他需要，例如查找出现次数最多的元素。下面的代码演示了Counter类的用法：

```python
from collections import Counter
frequences = Counter(z)
frequences.items()
print(frequences.most_common(1))
>>> [('e', 21)]
print(frequences.most_common(3))
>>> [('e', 21), ('(', 19), ('S', 17)]
```

**例二：输入一段文本，统计高频词汇**

```python
import string

text = '''
SCARLETT O'HARA was not beautiful, but men seldom realized it when caught by her charm as the Tarleton twins were. In her face were too sharply blended the delicate features of her mother, a Coast aristocrat of French de?scent, ………
'''

def generateWords():
    global text
    for punc in ":,.'\"-!?;":
        text = text.replace(punc,'')
    for spec in "\n()":                     #去掉换行符#
        text = text.replace(spec,' ')
    text = text.lower()                     #全部转换为小写#
    return text

def process(words):
    cntdict = dict()
    for word in words.split():
        cntdict[word] = cntdict.get(word,0) + 1 
    return cntdict

def output(cntdict,N=20):
    #print(cntdict)
    mlist = [(value,key) for key,value in cntdict.items()]
    mlist.sort(reverse=True) 
    for idx in range(20):
        info = "{:6s}: {:2d}  ".format(mlist[idx][1],mlist[idx][0])
        print(info,end="")
        if((idx+1)%6==0):
            print()
    #print(mlist)

def main():
    words = generateWords()
    countdict = process(words)
    output(countdict)

if __name__ == "__main__":
    main()
```

### 集合

#### 集合(set)的创建与删除

* 集合是无序可变集合，使用一对大括号界定，元素间以逗号分隔。集合中的元素必须是可hash对象，即不可变对象，不能是可变对象

* **元素不重复，且无序**

* 可通过set(literal)创建集合对象，定义时可以包含重复的对象，但只会保留一个 。**另外 a={}产生的空字典对象而不是空集合**

* 使用del删除整个集合

#### 集合的运算


|                  方法                  |                           说明                           |
| -------------------------------------- | -------------------------------------------------------- |
| s1 \| s2 \| …<br>s1.union(s2,…)        | 并集                                                     |
| s1 & s2 & …<br>s1.intersection(s2,…)   | 交集，s1 ∩ s2 ∩…在所有集合出现                            |
| s1 – s2<br>s1.difference(s2)           | 差集，s1 – s2 在s1但不在 s2                               |
| s1 ^ s2<br>s1.symmetric_difference(s2) | 对称差集, s1 ⊕ s2只属于其中一个但不属于其中另一个= (s1 ∪ s2) -s1 ∩ s2 |
| s1.isdisjoint(s2)                      | 没有共同元素为True                                        |
| s1.issubset(s2) s1 <= <s2              | s1是否为s2的子集或真子集                                         |
| s1.issuperset(s2) s1>= >s2             | s1是否为s2的超集或真超集                                          |
| ==   !=                                | 判断两个集合是否相等                                      |
| x in s  或者 x not in s                | 判断元素x是否在集合s中                                    |
| len(s)                                 | 集合的元素个数                                            |
| max(s)/min(s)/sum(s)                   | 集合中元素最大值、最小值和求和                             |

**集合元素的更改**

|                 方法                 |                 说明                  |                  例子                   |
| ------------------------------------ | ------------------------------------- | --------------------------------------- |
| s.add(x)                             | 将x添加到集合s                         | s1.add('a') # s1 = {1,2,3,'a'}                      |
| s1.update(s2)                        | 并集 s1 =s1 ∪ s2                     | s1.update(s2) # s1 = {1,2,3,4}                     |
| s1.intersection_update(s2)           | 交集 s1 = s1 ∩ s2                     | s1.intersection_update(s2) # s1 = {2,3} |
| s1.difference_update(s2)             | 差集 s1 = s1 – s2                     | s1.difference_update(s2) # s1 = {1}     |
| s1.symmetric\_difference\_update(s2) | 对称差集 s1 = s1 ⊕ s2                | s1.symmetric\_difference\_update(s2) \# s1 = {1,4}                            |
| s.remove(x)                          | 从集合s中移除x，不存在抛异常KeyError    | s1.remove(1) \# s1 = {2,3}                      |
| s.discard(x)                         | 从集合s中移除x                         | s1.discard(1) \# s1 = {2,3}                       |
| s.pop()                              | 从集合s移除一个元素并返回，空时KeyError | s1.pop() \# return 1, s1 = {2,3}                      |
| s.clear()                            | 清空集合s                             | s1.clear() \# s1 = set()                     |

**集合操作:去除list重复元素**

### 再谈内置方法sorted()

* 列表对象提供了sort()方法支持原地排序，内置函数sorted()返回新的列表，可对元组、列表、字典等进行排序，借助于其key参数可以实现自定义的的排序。

```python
persons = [{'name': 'Dong', 'age': 43}, {'name': 'Dong', 'age': 37}, {'name': 'Li', 'age': 50}, {'name': 'Zhang', 'age': 40}]
print(sorted(persons, key=lambda x:(x['name'], -x['age'])))

def sort_by_name_age(x):
    return x['name'],-x['age'] 
print(sorted(persons, key=sort_by_name_age))
```

* operator模块的itemgetter函数：itemgetter(item) itemgetter(*items)，返回的是一个函数对象，该函数对象在被调用(参数为obj)时将调用对应对象obj的__getitem__(item)方法，即obj[item]

```python
f = itemgetter(2)       # f(obj)将返回 obj[2] 
g=itemgetter(2,5,3)     # g(obj)将返回 (obj[2],obj[5],obj[3]) 
phonebook = {'Linda':'7750', 'Bob':'9345', 'Carol':'5834'}
from operator import itemgetter
sorted(phonebook.items(), key=itemgetter(1)) 
#按字典中元素的值进行排序
>>> [('Carol', '5834'), ('Linda', '7750'), ('Bob', '9345')]
sorted(phonebook.items(), key=itemgetter(0)) 
#按字典中元素的键进行排序
>>> [('Bob', '9345'), ('Carol', '5834'), ('Linda', '7750')]
```

## 选择与循环

### 条件表达式

算术运算符：+、-、\*、/、//、%、\*\*、~

关系运算符：>、<、==、<=、>=、!=，可以连续使用，如`print(1<2<3)`

测试运算符：in、not in、is、is not

逻辑运算符：and、or、not，注意**短路求值**

位运算符：~、&、|、 ^、 <<、>>

条件表达式的运算结果（值）只有两种：True、False，条件表达式的值只要不是相当于0或者空、False，Python解释器均认为与True等价。从这个意义上来讲，几乎所有的Python合法表达式都可以作为条件表达式，包括含有函数调用的表达式。 

比较特殊的运算符还有逻辑运算符“and”和“or”，这两个运算符具有短路求值或惰性求值的特点，简单地说，就是只计算必须计算的表达式的值。在设计条件表达式时，在表示复杂条件时如果能够巧妙利用逻辑运算符“and”和“or”的短路求值或惰性求值特性，可以大幅度提高程序的运行效率，减少不必要的计算与判断。

以“and”为例，对于表达式“表达式1 and 表达式2”而言，如果“表达式1”的值为“False”或其他等价值时，不论“表达式2”的值是什么，整个表达式的值都是“False”，此时“表达式2”的值无论是什么都不影响整个表达式的值，因此将不会被计算，从而减少不必要的计算和判断。

例如，下面的函数根据用户指定的分隔符将多个字符串连接成一个字符串，如果用户没有指定分隔符则使用逗号。

```python
def Join(chList, sep=None):
	return (sep or ',').join(chList)
```

另外，在Python中，条件表达式中不允许使用赋值运算符“=”，避免了其他语言中误将关系运算符“==”写作赋值运算符“=”带来的麻烦，例如下面的代码，在条件表达式中使用赋值运算符“=”将抛出异常，提示语法错误。

### 选择结构

#### 单分支选择结构

```python
if 表达式:
    语句块

# 下例按升序打印两个输入的数：
a,b=input('Input two number:')
if a>b:
   a,b=b,a
print(a,b)

# a,b=input('Input two number:')只能接受‘12’这样的输入，结果a=‘1’,b=‘2’
# 要接受‘1 2’这样的输入，可以写为：
a,x,b=input('Input two number:') 
# 2. 或者
a,b=input('Input two number:').split(' ')
```

#### 双分支结构

```python
if 表达式:
    语句块1
else:
    语句块2

a = 5
print(6) if a>3 else print(5)
print(6 if a>3 else 5)
b = 6 if a>13 else 9
```

#### 多分支结构

```python
if 表达式1:
    语句块1
elif 表达式2:
    语句块2
elif 表达式3:
    语句块3
else:
    语句块4
# 3. 其中，关键字elif是else if的缩写。
```

#### 选择结构的嵌套

```python
def func(score):
	degree = 'DCBAAF'
	if score > 100 or score < 0:
		return 'wrong score.must between 0 and 100.'
	else:
		index = (score - 60)//10
		if index >= 0:
			return degree[index]
		else:
			return degree[-1]
```

#### 选择结构应用

例1：自动判定求职者条件

```python
age=24
subject="计算机"
college="非重点"
if (age > 25 and subject=="电子信息工程") or (college=="重点" and subject=="电子信息工程" ) or (age<=28 and subject=="计算机"):
    print("恭喜，你已获得我公司的面试机会!")
else:
    print("抱歉，你未达到面试要求")
```

例2：用户输入若干个分数，求所有分数的平均分。每输入一个分数后询问是否继续输入下一个分数，回答“yes”就继续输入下一个分数，回答“no”就停止输入分数。

```python
endFlag = 'yes'
sum,count = 0,0
while endFlag.lower() == 'yes':
    x = input("请输入一个正整数: ")
    x = int(x)
    if isinstance(x, int) and 0<=x<=100:
        sum += x
        count += 1
    else:
        print('不是数字或不符合要求')
    endFlag = input('继续输入？(yes or no)')
if count > 0:
    print('平均数=', sum/count)
else:
    print("No input number!")
```

### 循环结构

**注：循环除了可以用for、while外，还可以用列表推导式**

**for循环与while循环**

* while循环一般用于循环次数难以提前确定的情况，也可以用于循环次数确定的情况；

* for循环一般用于循环次数可以提前确定的情况，尤其是用于枚举序列或迭代对象中的元素；

* 一般优先考虑使用 for循环 \+ 序列。

* 相同或不同的循环结构之间都可以互相嵌套，实现更为复杂的逻辑。

**while循环语法**

```python
while 表达式:
    循环体

while 表达式:
	循环体
else:   #当循环自然结束（不是因为执行了break而结束）时执行else结构中的语句
	else子句
```

![](https://i.loli.net/2019/10/12/Wbsu14VqiGEmprY.png)

**for循环语法**

```python
for 变量 in 序列或迭代对象:
    循环体

for 变量 in 序列或迭代对象:
    循环体
else:    #当循环自然结束（不是因为执行了break而结束）时执行else结构中的语句
    else子句
```

**例1：由用户输入一个正整数n，求从1到n各数平方和。**

```python
def inputinteger():
    while True:
        instr = input('please input a positive integer:')
        positive = int(instr)
        if(positive<=0):
            print("wrong input")
        else:
            return int(instr)
    
def process(num):
    sum = 0
    for idx in range(1,num+1):
        sum += idx*idx
    return sum

def outputResult(sum):
    print('the result is ',sum)

def main():
    num = inputinteger()
    sum = process(num)
    outputResult(sum)


if __name__=='__main__':
    main()
```

**例2：输入一个字符串，输出以空格间隔的字符序列**

```python
a = input("please enter a string:")

for i in range(len(a)):
    print(a[i],end = " ")
```

**例3：查找一个最小正整数，要求满足以下条件：被3除余2，被5除余3，被7除余4。**

```python
num = 4
while not(num%3==2 and num%5==3):
    num += 7
print(num)
```

### break 和 continue

**break和continue语句**

* break语句在while循环和for循环中都可以使用，一般放在if选择结构（if嵌套于while或for内）中，一旦break语句被执行，将使得当前整个循环提前结束。

* continue语句的作用是终止当前循环，并忽略continue之后的语句，然后回到循环的顶端，提前进入下一轮循环。

* 除非break和continue语句让代码更简单或更清晰，否则不要轻易使用。

```python
import math

def inputInteger():
    while True:
        instr = input("Please enter an Positive Integer:")
        try:
            n = int(instr)
            if(n>0):
                break
            else:
                print("Wrong param range")
        except:
            print("Wrong param type")
        #end try
    return n

def computePrime(N):
    rlist = []
    if N>=2: rlist.append(2)

    for n in range(3,N+1,2):
        for k in range(3,n,2):  #(int)(math.sqrt(n))+1):
            if k*k <= n and n%k==0:
                break
        else:
            rlist.append(n)
    return rlist

def printResult(rlist):
    for idx in range(len(rlist)):
        print("{0:5d}".format(rlist[idx]),end="")
        if((idx+1)%6==0):
            print()
    #end for

if __name__ == "__main__":
    N = inputInteger()
    rlist = computePrime(N)
    printResult(rlist)
```

### 循环嵌套

**乘法表**

```python
def printmultiply2():
    for i in range(1,10):
        for j in range(1,i+1):
            item = "%dx%d=%d\t" %(i,j,i*j)
            print(item,end="")
        print()

if __name__ == "__main__":
    printmultiply()
```

**水仙花数**

水仙花数是指1个3位的十进制数，其各位数字的立方和等于该数本身。例如：153是水仙花数，因为153 = 1^3 + 5^3 + 3^3

输出全部的“水仙花数”。

```python
def solve():
    prereckon = [i**3 for i in range(0,10)]
    for hundred in range(1,10):
        h1 = 100*hundred
        for ten in range(0,10):
            t1 = 10*ten
            for digit in range(0,10):
                realvalue = h1 + t1 + digit
                tulip = prereckon[hundred] + prereckon[ten] + prereckon[digit]
                if(realvalue == tulip):
                    print("%d=%d^3+%d^3+%d^3"%(realvalue,hundred,ten,digit))

if __name__ == "__main__":
    solve()
```

**循环作业（1）输入任意一个正整数，显示相应大小的菱形。**

```python
def printstar(N,space='  ',star='* '):
    for k in list(range(1,N+2))+list(range(N,0,-1)):
        content =space *(N+1-k) + star*(2*k-1)
        print(content)

if __name__ == "__main__":
    printstar(5,'  ','* ')
```

**循环作业（2）**

K数定义为：若正整数n可以分割为二个数(不一定是在中间位分割)，而这二个数相加之和的平方恰好等于n，那么n就是K数。

例如：3025可以分割为30和25，而30+25=55，并且55的平方等于3025；再88209可以分割为88和209，而88与209之和为297，其平方正好等于88209。

请找出100000以内的全部K数。

```python
def process(N):
    rlist = []
    rlist.append((1,0,1))
    for k in range(1,N):
        strk = str(k)
        for idx in range(1,len(strk)):
            head,tail = int(strk[0:idx]) , int(strk[idx:len(strk)])
            value = (head+tail)**2
            if(value == k):
                rlist.append((k,head,tail))
    return rlist

def printResult(rlist):
    for k,head,tail in rlist:
        print("{}=({}+{})**2".format(k,head,tail))
    #end for

if __name__ == "__main__":
    N = 100000
    result = process(N)
    printResult(result)
```

### 两维列表 与 循环嵌套

**示例 —— 给学生答案评分**

假设有8名学生和10道选择题，他们的答案存储在一个表格中，每一行记录了一位学生对这些问题的答案，如下图所示：每题1分，程序显示评分结果。

![](https://i.loli.net/2019/10/12/MCqNwlT47QgsHAe.png)

```python
answers = [
    ['A','B','A','C','C','D','E','E','A','D'],
    ['D','B','A','B','C','A','E','E','A','D'],
    ['C','B','A','E','D','C','E','E','A','D']
]

keys = ['D','B','D','C','C','D','A','E','A','D']

def grade():
    for row in range(len(answers)):
        correctcount = 0
        for col in range(len(answers[row])):
            if answers[row][col] == keys[col]:
                correctcount += 1
        print("student: {0}  score:{1}".format(row,correctcount))

if __name__ == "__main__":
    grade()
```

**循环结构代码优化（兼测试）**

为了优化程序以获得更高的效率和运行速度，在编写循环语句时，应尽量减少循环内部不必要的计算，将与循环变量无关的代码尽可能地提取到循环之外。对于使用多重循环嵌套的情况，应尽量减少内层循环中不必要的计算，尽可能地向外提。

```python
import time

def f1():
    result = []
    digits = (1,2,3,4)
    for i in digits:
        for j in digits:
            for k in digits:
                result.append(i*100+j*10+k)
    #end for
    return result

def f2():
    result = []
    digits = (1,2,3,4)
    for i in digits:
        i = i*100
        for j in digits:
            j = j*10
            for k in digits:
                result.append(i+j+k)
    #end for
    return result

def measure(f,N,name="f"):
    start = time.time()
    for i in range(N):
        f()
    end = time.time()
    print("{}: {} {}ms".format(name,N,end-start))
    return end-start

if __name__ == "__main__":
    delta1 = measure(f1,10000,"f1")
    delta2 = measure(f2,10000,"f2")
    speedup = (delta1-delta2)/delta2
    print("speedup is : {0:.2f}%".format(speedup*100))
```

## 字符串与正则表达式

### 字符串

#### 定义

字符串是由字符(字母、数字、汉字、其他符号)组成的一个序列。

与其他语言一般用双引号来定义字符串字面值不同，Python可以使用单引号和双引号，一般建议采用单引号定义，如果字符串中有双引号，则使用单引号定义，反之亦然。单引号和双引号定义的字符串不能跨越多行，字符串中想要有换行需要使用字符转义。三引号`'''`或`"""`表示的字符串可以换行，用于长字符串，也用于在程序中表示较长的注释。

字符串属于不可变序列。空串表示为`''`或 `""`

无论数字、字母、汉字，都按一个字符对待，也可以**使用中文作为变量名**。

**字符编码**

* ASCII：1个字节；128个字符组成，包括大小写字母、数字0-9、标点符号、非打印字符（换行符、制表符等4个）以及控制字符（退格、响铃等）组成

* UTF-8：；1～6个字节，对世界上所有国家需要用到的字符进行了编码

* GB2312：中国制定的中文编码，1个字节表示英文，2个字节表示中文

* GBK：对GB2312的扩充

* CP936：微软在GBK基础上完成的编码

Python3的字符串默认为Unicode字符串，从而可以包含中文字符串

| ASCII值 | 控制字符 | ASCII值 | 控制字符 | ASCII值 | 控制字符 | ASCII值 | 控制字符 |
| ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- |
| 0       | NUT      | 32      | (space)  | 64      | @       | 96      | 、       |
| 1       | SOH      | 33      | !       | 65      | A       | 97      | a       |
| 2       | STX     | 34      | "       | 66      | B       | 98      | b       |
| 3       | ETX     | 35      | #       | 67      | C       | 99      | c       |
| 4       | EOT      | 36      | $       | 68      | D       | 100     | d       |
| 5       | ENQ      | 37      | %       | 69      | E       | 101     | e       |
| 6       | ACK      | 38      | &       | 70      | F       | 102     | f       |
| 7       | BEL     | 39      | ,       | 71      | G       | 103     | g       |
| 8       | BS      | 40      | (       | 72      | H       | 104     | h       |
| 9       | HT      | 41      | )       | 73      | I       | 105     | i       |
| 10      | LF      | 42      | *       | 74      | J       | 106     | j       |
| 11      | VT      | 43      | +       | 75      | K       | 107     | k       |
| 12      | FF      | 44      | ,       | 76      | L       | 108     | l       |
| 13      | CR      | 45      | -       | 77      | M       | 109     | m       |
| 14      | SO      | 46      | .       | 78      | N       | 110     | n       |
| 15      | SI      | 47      | /       | 79      | O       | 111     | o       |
| 16      | DLE     | 48      | 0       | 80      | P       | 112     | p       |
| 17      | DCI     | 49      | 1       | 81      | Q       | 113     | q       |
| 18      | DC2      | 50      | 2       | 82      | R       | 114     | r       |
| 19      | DC3      | 51      | 3       | 83      | S       | 115     | s       |
| 20      | DC4      | 52      | 4       | 84      | T       | 116     | t       |
| 21      | NAK      | 53      | 5       | 85      | U       | 117     | u       |
| 22      | SYN      | 54      | 6       | 86      | V       | 118     | v       |
| 23      | TB      | 55      | 7       | 87      | W       | 119     | w       |
| 24      | CAN      | 56      | 8       | 88      | X       | 120     | x       |
| 25      | EM      | 57      | 9       | 89      | Y       | 121     | y       |
| 26      | SUB     | 58      | :       | 90      | Z       | 122     | z       |
| 27      | ESC     | 59      | ;       | 91      | \[      | 123     | {       |
| 28      | FS      | 60      | <       | 92      | /       | 124     |         |
| 29      | GS      | 61      | =       | 93      | \]      | 125     | }       |
| 30      | RS      | 62      | >       | 94      | ^       | 126     | `       |
| 31      | US      | 63      | ?       | 95      | _       | 127     | DEL     |

**特殊字符解释**

|    NUL空     |  VT 垂直制表  | SYN 空转同步 |
| ----------- | ------------ | ------------ |
| STX 正文开始 | CR 回车       | CAN 作废      |
| ETX 正文结束 | SO 移位输出   | EM 纸尽       |
| EOY 传输结束 | SI 移位输入   | SUB 换置      |
| ENQ 询问字符 | DLE 空格      | ESC 换码      |
| ACK 承认     | DC1 设备控制1 | FS 文字分隔符 |
| BEL 报警     | DC2 设备控制2 | GS 组分隔符   |
| BS 退一格    | DC3 设备控制3 | RS 记录分隔符 |
| HT 横向列表  | DC4 设备控制4 | US 单元分隔符 |
| LF 换行      | NAK 否定      | DEL 删除      |

**字符串驻留机制string interning**

* 将其赋值给多个不同的对象时，内存中只有一个副本，多个对象共享该副本。

* 保护.pyc文件不会被错误代码搞的过大。

* 数值-5~256也遵循驻留机制

**判断一个变量是否为字符串**

使用内置函数isinstance(s,str)

**字符串属于不可变序列类型**

支持序列通用方法，包括切片操作，支持特有的字符串操作方法。

例：把一个字符串分m行输出，m由用户指定

```python
s = input("请输入一行字符：")
m = eval(input("请输入行数："))
n = len(s)//m if len(s)%m==0 else len（s）//m+1
for i in range(o,len(s),n)：print(s[i:i+n])
```

#### 字符串转义

如果一个字符串内容有单双引号，则需要通过在引号前加上转义字符（\表示需要后面的字符需要特别对待)表示为字符串的一部分，而不是字符串的结束

回车换行以及其他控制字符也可以通过转义来描述：

| 特殊字符 |         含义         | 特殊字符 |          含义          |
| ------- | ------------------- | ------- | --------------------- |
| \'      | 一个单引号           | \"      | 一个双引号             |
| \\      | 一个\                | \t      | 制表符                 |
| \n      | 换行符               | \r      | 回车                   |
| \ddd    | 3位八进制数对应的字符 | \xhh    | 2位十六进制数对应的字符 |

**原始字符串**

字符串界定符前面加字母r或R表示原始字符串，其中的特殊字符不进行转义，但字符串的最后一个字符不能是\。例：

```
a=r'C:\\Program Files (x86)\\Python35\\Lib'
a
>>> 'C:\\\Program Files (x86)\\\Python35\\\Lib'
print(a)
>>> C:\\Program Files (x86)\\Python35\\Lib
```

交互式console在计算表达式时：如果表达式obj的值不为None时调用`print(repr(obj))` 。对于字符串而言，输出结果为转义的字符串

`repr(obj)`: 内部表示字符串，一般可通过eval(repr(obj))得到原来的对象obj

`print(obj)`: 用户友好的输出，对于字符串而言，一串字符

**字符串前加u**

例：u"我是含有中文字符组成的字符串。"

　　作用：后面字符串以 Unicode 格式 进行编码，一般用在中文字符串前面，防止因为源码储存格式问题，导致再次使用时出现乱码。

**字符串前加b**

python3.x里默认的str是(py2.x里的)unicode, bytes是(py2.x)的str, b”“前缀代表的就是bytes。python2.x里, b前缀没什么具体意义， 只是为了兼容python3.x的这种写法

#### 相关转换函数

|     **函数**     |                                 **含义**                                  |                           **实例**                            |              **结果**               |
| ---------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------- | ----------------------------------- |
| bin(x)           | 把数字x转换为二进制字符串                                                  | bin(4)                                                        | '0b100'                             |
| oct(x)           | 把数字x转换为八进制字符串                                                  | oct(25)                                                       | '0o31'                              |
| hex(x)           | 把数字x转换为十六进制字符串                                                | hex(75)                                                       | '0x4b'                              |
| str(obj)         | 把对象obj转换为字符串                                                      | str(16),str(1/2)                                              | ('16','0.5')                        |
| int(x\[,d\])     | 把数字x截取为整数，或将基数为d的数字型字符串x转换为整数，如果d没有缺省为十进制 | （int(3.14), int('314')）<br>int('ff',16)                     | (3,314)<br>255                      |
| float(x)         | 将对象(数字或字符串)x转换为浮点数                                           | float(3),float('3.14')<br>float('12e-2')                      | (3.0,3.14)<br>0.12                  |
| len(obj)         | 返回序列类对象obj包含的元素个数                                            | len('Hello World'),len('')                                    | (11, 0)                             |
| ord(s)           | 返回长度为1的字符串s中的字符对应的Unicode码（ASCII码是其子集）               | ord('a'),ord('A'),ord('你')<br>ord('0'), ord('\\n')           | (97, 65, 20320)<br>(48, 10)         |
| chr(x)           | 返回Unicode编码为x的字符串(len=1)                                          | chr(65),chr(10),chr(20320)<br>chr(ord('d')-ord('a')+ord('A')) | ('A','\\n', '你')<br>'D'                |
| strip(\[chars\]) | 用于移除字符串**头尾**指定的字符（默认为空格）                              | str = "000this is string 000 wow!!!000";print str.strip( '0' )                                                           | this is string 000 wow!!!           |
| 访问值           | 访问字符串某一特定的值                                                     | var1 = 'Hello World!'<br>var2 = "Python Runoob"               | var1\[0\] =  H<br>var2\[1:5\]= ytho |

例：列出1000以内所有回文数

```python
palist=[]
for i in range(1000):
    s = str(i)
    if s == s[::-1]:
        palist.append(i)
print(palist)
```

**转换大小写**

和其他语言一样，Python为string对象提供了转换大小写的方法：`upper()` 和` lower()`。还不止这些，Python还为我们提供了首字母大写，其余小写的`capitalize()`方法，以及所有单词首字母大写，其余小写的`title()`方法，`swapcase()`大小写互换。

**获取字符串表达式值**

内置函数`eval(.)`，可以将字符串转为数值

```python
eval("3+4")
eval("__import__('os').system('md testtest')")  # 运行notepad.exe程序，打开一个记事本窗口
```

#### 对齐与格式化

**字符串对齐**

* str.center(width[, fillchar])：返回指定宽度的新字符串，原字符串居中，并使用指定字符(默认空格)填充

* str.ljust(width[, fillchar])：返回指定宽度的新字符串，原字符串左对齐，并使用指定字符(默认空格)填充

* str.rjust(width[, fillchar])：返回指定宽度的新字符串，原字符串右对齐，并使用指定字符(默认空格)填充

例：打印三角形

![](https://i.loli.net/2019/10/12/Hk3PxqO2BzQsNCT.png)

```python
lines = eval(input("请输入行数："))

for i in range(lines//2):
    stars = ["*"] * (i+1)
    stars = " ".join(stars)
    online = stars.center(lines," ")
    print(online)

for i in range(lines//2-1,0,-1):
    stars = ["*"] * (i)
    stars = " ".join(stars)
    online = stars.center(lines," ")
    print(online)
```

**字符串格式化**

`format_string % obj`把对象obj按格式要求format_string转换为字符串。

简单来说，这些格式字符相当于占位符，作用就是将后面的字符串替换上来，基本格式是`'xx %s' % 'xx'`（如果是数字就不用引号了，如果只替换一个内容就不用括号）


| **格式字符** |               **说明**               |        **格式字符**        |          **说明**           |
| ------------ | ------------------------------------ | ------------------------- | -------------- |
| %[width]s   | 字符串(采用str()的显示)               | %[width]x                 | 十六进制整数    |
| %[width]r    | 字符串(采用repr()的显示)              | %[width]e                 | 指数(基底写为e) |
| %c           | 单个字符（给出asscia值，打印相应字符） | %[width]E                 | 指数(基底写为E) |
| %[width]b    | 二进制整数                           | %[width].[precision]f、%F | 浮点数          |
| %[width]d   | 十进制整数                           | %g                        | 指数(e)或浮点数(根据显示长度) |
| %[width]i    | 十进制整数                           | %G                        | 指数(E)或浮点数(根据显示长度)       |
| %[width]o    | 八进制整数                           | %%                        | 字符”%”        |

**字符串格式化例子**

如果格式化字符串中有多个占位符，则obj应该是元组tuple对象，格式为(var1,var2…,varN) 

```python
a = 3.6674
'%7.3f' % a
>>> ' 3.667'
"%d:%c"%(65,65)
>>> '65:A'
"""My name is %s, and my age is %d"""%('Dong Fuguo',38)
>>> 'My name is Dong Fuguo, and my age is 38'
```

另外width有大用，如下，可以自定义格式，左对齐为负数，字符串s类似

```python
'%d'%2
>>> '2'
'%2d'%2
>>> ' 2'
'%02d'%2
>>> '02'
'%-2d'%2
>>> '2 '
```

**高级字符串格式化**

`“{n:3s}”.format(a)`

N是第n+1个元素，3s是其占用字符长度，可以随意增加元素，比如：”x={}”.format(x)

`^`,`<`,`-`, `>` 分别是居中、左对齐、左对齐、右对齐，后面带宽度， `:` 号后面带填充的字符，只能是一个字符，不指定则默认是用空格填充。

`+` 表示在正数前显示 +，负数前显示 -；` ` （空格）表示在正数前加空格

```python
Print("{{a}}".format())                   #{a}
Print("{a}".format())                     #error,里面没有为a的参数
Print("{a} - {b}".format(a = 100,b = 200))#100 - 200
Print("{0},{0}".format(11,22))            #11,11
Print("{0},{0},{1},{2}".format(11,22,33)) # 11,11,22,33  中括号里面的数代表第几个参数
Print("{0:3d},{1:4s},{1:5s},{2}".format(11,"a",33)) # ' 11,a   ,a    ,33'
Print("{0:=>+011.3f}".format(12.12345))  #====+12.123;用=来填充,右对齐,因为已经用=来填充了,0无效,宽度11,小数点精度后精度为3,类型为浮点数
Print("{0:>+011.3f};".format(12.12345))   #0000+12.123;
a = "test"
print("{0:^10}".format(a))                #test
print("{0!s:^10}".format(a))              #test
print("{0!r:^10}".format(a))              #'test'

#通过下标也行
a=[1,2]
print('{0[0]},{0[1]}'.format(a))          #1,2
```

```python
weather = [("Monday","rain"),("Tuesday","sunny"),("Wednesday", "sunny"),("Thursday","rain"),("Friday","Cloudy")]
formatter = "Weather of '{0[0]}' is '{0[1]}'".format  #方法对象
for item in map(formatter,weather):
    print(item)
```

#### 查找与替换

* str.find(str[,beg,end])、str.rfind(str[,beg,end])：find()和rfind()方法分别用来查找一个字符串在另一个字符串指定范围（默认是整个字符串）中首次和最后一次出现的位置，如果不存在则返回-1；

* str.index(str[,beg,end])、str.rindex(str[,beg,end])：index()和rindex()方法用来返回一个字符串在另一个字符串指定范围中首次和最后一次出现的位置，如果不存在则抛出异常；

* str.count(str[,beg,end])：count()方法用来返回一个字符串在另一个字符串中出现的次数。

* str.replace(old, new[, max])：替换字符串，max为替换最大次数。

#### 拼接与分割

**str.join(sequence)**

sequence要连接的字符串

例：

```python
li=\["apple", "peach", "banana", "pear"\]
sep=","
s=sep.join(li)
s
>>> "apple,peach,banana,pear"
a,b = "ABC","xyz"
a.join(b)
>>> 'xABCyABCzABC'
```

* 不推荐使用 **+**  连接字符串，优先使用join()方法

* 效率原因。每做一次+，需要新建一个字符串，而join()一次性计算出总串长度。

例：输入一个字符串，输出以空格间隔的字符序列

**split()方法**

`str.split(str="", num=string.count(str))`，`str.rsplit()`

str -- 分隔符，默认为所有的空字符，包括空格、换行(\\n)、制表符(\\t)等。

num -- 分割次数，默认分隔所有分隔符。

返回列表。

**partition()、rpartition()**

`str.partition(str)`和`strrpartition(str)`用来以指定字符串为分隔符将原字符串分割为3部分**元组**，即**分隔符前的字符串、分隔符字符串、分隔符后的字符串**，如果指定的分隔符不在原字符串中，则返回原字符串和两个空字符串。

```python
s="apple,peach,banana,pear"
s.partition(',')
>>>('apple', ',', 'peach,banana,pear')
s.rpartition('banana')
>>>('apple,peach,', 'banana', ',pear')
```

#### 转换与消减

* 生成映射表函数`str.maketrans(intab, outtab)`和按映射表关系转换字符串函数`str.translate(table)`

`bytes.translate(table[, delete])`、`bytearray.translate(table[, delete])`

table -- 翻译表。

delete -- 字符串中要过滤的字符列表，使用该参数时，要用b来声明。

```python
intab = "aeiou"
outtab = "12345"
trantab = str.maketrans(intab, outtab)   # 制作翻译表
 
sentence = "this is string example....wow!!!"
print (sentence.translate(trantab))
```

```python
trantab = bytes.maketrans(b"aeiou", b"12345")
sentence = b"this is string example....wow!!!"
print(sentence.translate(trantab,b"o"))   # 删除字母o并转换
```

* `str.strip([chars])`、rstrip()、lstrip()

这几个方法分别用来删除两端、右端或左端的空格或连续的指定字符`chars`。


#### 常量与成员判断

**字符串常量**

`string.ascii_letters`是生成所有字母，从a-z和A-Z；

`string.digits`是生成所有数字0-9；

`string.punctuation`：包含所有标点的字符串

`string.ascii_letters`：英文字母（大小写）

`string.printable` 可打印字符

'0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'

`string.ascii_lowercase` 小写字母

`string.ascii_uppercase` 大写字母

**成员判断**

```python
"a" in "abcde"
```

**判断字符串是否以指定字符串开始或结束**

s.startwith(t)、s.endswith(t)

```python
import os
[filename for filename in os.listdir(r'c:\\') if filename.endswith(('.bmp','.jpg','.gif'))]
```

**检验字符串是否为字母、数字等**

* str.isalnum() —— 检验字符串是否为数字或字母

* str.isalpha() —— 检验字符串是否为字母

* str.isdigit() —— 检验字符串是否为数字字符

* str.isspace() —— 检验字符串是否为空白字符

* str.isupper() —— 检验字符串是否为大写字母

* str.islower() —— 检验字符串是否为小写字母

例：连续输入若干行字符串（以空行结束），输出最长的那些行

统计文章的单词个数。约定单词由英文字母组成，其他字符只是用来分隔单词。

#### 一种简单的加密和解密

加密：对明文每m位提取其字符，到达末尾则回至头部，已经提取的不再提取

如：“abcde”，m=3， 密文为： “caebd”

解密：已知密文和m，如何恢复明文？

例：报数出圈。设有编号为1~n的n个人按顺时针站成一个圆圈。首先从第1个人开始，按顺时针从1开始报数，报到第m个人，令其出列。然后再从出列的下一个人开始，按顺时针从1开始报数，报到第m个人，再令其出列，……。如此下去，直到圆圈不再有人为止。求这n个人出列的顺序。

解题思路

假设此圈共有rest个人，对应x[0], x[1], x[2], …, x[rest-1]。假设这一轮报1的人对应的元素下标为 curIndex (0 <= curIndex < rest)，则报m的人对应的数组元素下标为 (curIndex + m - 1) % rest 。把报m的人对应的元素从列表中删除(元素删除导致 rest 自动减1)。把curIndex赋值为刚才被删除元素的下标，之后进行下一轮报数。

![](https://i.loli.net/2019/10/12/PAXOfloMjNLkRD6.png)

报数出圈代码

```python
n,m = 20,7
x = list(range(1,n+1))
y = []
curindex = 0
while x:
    curindex = (curindex + m - 1) % len(x)
    y.append(x.pop(curindex))
print(y)
```

明文加密

```python
m = 7
x = input("请输入一串明文字符：")
x = list(x)
y = []

curindex = 0
while x:
    curindex = (curindex + m - 1) % len(x)
    y.append(x.pop(curindex))

y = "".join(y)
print(y)
```

秘文解密

```python
m = 7
y = input("请输入一串密文字符：")
y = list(y)
x = [None]*len(y)       # 如果用[]*len(y)的话，结果是[]，长度依然是1
z = list(range(len(y)))

curindex = 0
for each in y:
    curindex = (curindex + m -1) % len(z)
    x[z.pop(curindex)] = each

x = "".join(x)
print(x)
```

### 正则表达式

* 快速分析大量文本以找到特定的符合某些复杂规则（亦称模式）的字符串

* 提取、编辑、替换或删除文本子字符串

* 将提取的字符串添加到集合以生成报告

#### 普通字符（包括转义字符）

* 最基本的正则表达式由单个或多个普通字符组成，用以匹配字符串中对应的单个或多个普通字符，普通字符包括ASCII字符，Unicode字符和转义字符

* 由于`^$.*?+-\{}[]| ()`被正则表达式用作**元字符**，如作为普通字符使用则需要转义（**加个\就行**）

| **正则表达式** |              **字符串**               |          **说明**          |
| -------------- | ------------------------------------ | ------------------------- |
| fo             | ‘The quick brown fox jumps for food’ | 匹配其中3个含有’fo’的字符串 |
| 1+1=2          | ‘1+1=2’                              | +为元字符，无法匹配         |
| 1\+1=2        | ‘1+1=2’                              | [‘1+1=2’]                 |
| (note)         | ‘please(note)’                       | ()为元字符, 配”note”       |
| \(note\)       | ‘please(note)’                       | 匹配“(note)”               |

#### Python中的正则表达式引擎

Python中，**re**模块提供了正则表达式操作所需要的功能。`re.findall(pattern, string)`：以列表形式列出字符串中模式的所有匹配项

|                    **Python语句**                     |    **匹配结果**    |
| ----------------------------------------------------- | ----------------- |
| re.findall('fo','The quick brown fox jumps for food') | ['fo', 'fo','fo'] |
| re.findall('1+1=2','1+1=2')                           | []                |
| re.findall('1\\+1=2','1+1=2')                         | ['1+1=2']         |
| re.findall('(note)','please(note)')                   | ['note']          |
| re.findall('\\(note\\)','please(note)')               | ['(note)']        |

#### 元字符

如：`\b . * ＋ () `都是元字符

正则表达式**元字符**分类： 字符类、预定义字符类、边界匹配符、重复限定符、分组符()、选择符|

**字符类**

| **元字符** |         **说明**          |
| ---------- | ------------------------ |
| []         | 匹配位于[]中的任意一个字符 |
| -          | 用在[]之内用来表示范围     |
| ^          | 用在[]之内用来表示否定    |

```
[xyz]:枚举字符集，匹配括号中任意字符，'[pjc]ython'可以匹配'python'、'jython'、'cython'
[^xyz]:否定枚举字符集，匹配不在括号中任意字符，'[^abc]'可以匹配一个任意除'a'、'b'、'c'之外的字符	
[a-z]:指定范围的字符，匹配指定范围的任意字符，'[a-zA-Z0-9]'可以匹配一个任意大小写字母或数字	
[^m-z]:指定范围以外的字符，匹配指定范围以外的任意字符
```

**预定义字符类**：正则表达式将常常用到的一些特定字符类形成了若干预定义字符类

| **元字符** |                             **说明**                             |
| ---------- | ---------------------------------------------------------------- |
| .          | 匹配除换行符以外的任意单个字符                                     |
| \d        | 匹配任何数字，相当于[0-9]                                         |
| \D        | 与\d含义相反,非数字，相当于`[^0-9]`                                |
| \s        | 匹配任何空白字符，包括空格、制表符、换页符等等。相当于`[\t\n\r\f\v]` |
| \S        | 与\s含义相反，相当于`[^\t\n\r\f\v] `                              |
| \w        | 匹配任何字母、数字以及下划线，相当于`[a-zA-Z0-9_]`                  |
| \W        | 与\w含义相反,相当于`[^a-zA-Z0-9_]`                                 |
| [\s\S]*    | 匹配包括换行符之内的任意字符                                       |

**边界匹配符**：字符串匹配往往涉及从某个位置开始匹配，例如行的开头或结果、单词边界等，边界匹配符用于匹配字符串的位置

| 元字符 |                                          说明                                           |
| ------ | --------------------------------------------------------------------------------------- |
| ^      | 匹配行首，匹配以^后面的字符开头的字符串如：“^a”匹配“abc”中的“a”,不匹配“bat”中的“a”          |
| $      | 匹配行尾，匹配以\$之前的字符结束的字符串如：“c\$”匹配“abc”中的“c”,不匹配“acb”中的“c”        |
| \\b    | here is a word 那么，这句中有好几个\\b, 每个单词的前后都有一个\\b. 所以你用 \\bhere\\b 可以匹配上面这个here,但如果here 不是一个单词，而是一个单词的一部分，如 adheread, 这样的话，用here 可以匹配，用\\bhere\\b就不能区配了，因为ad后面没有\\b. 所以 adhere 中的here 不会被匹配。总结： \\b 就是用在你匹配整个单词的时候。 如果不是整个单词就不匹配。 你想匹配 I 的话，你知道，很多单词里都有I的，但我只想匹配I，就是“我”，这个时候用 \\bI\\b\\B就是反过来，代表非字间。 类似\\d代表数字， \\D代表非数字。注意:’\\b’在正则表达式表示单词边界，而在字符串中’\\b’表示退格字符，所以这些与标准转义字符重复的元字符必须使用两个\\\字符，在python中也可以使用原始字符串r””或r’’，即“\\\bfoo\\\b” 或 r“\bfoo\\b” |
| \\B    | 与\\b含义相反如：’py\\B’ 匹配 ”python” “py3” “py2”,但不匹配”happy” ”sleepy” ”py!”，即含有py但py不在结尾 |

**重复限定符**：指定重复的次数（默认最大匹配）

简单说，就是要找到几个连到一起的值，比如’fooood’,o{2}，要找两个连在一起的o，可以看出正好四个o，可输出两个，如果o{3}，那么找3个o，前三个匹配成功后，只剩最后一个，不能匹配，故只输出一个；如果是o{1,3}，先找三个o，再找3个，找不到，就退一步找两个，两个也没有，就找一个，成功输出两个。

| 正则表达式 |                                      说明                                       |
| --------- | ------------------------------------------------------------------------------- |
| X{n,m}    | X重复n到m次如：“o{1,3}”匹配“fooooood”中的前3个“o”和后3个“o”                              |
| X{n,}     | X至少重复n次如：“o{2,}”匹配“fooooood”中的所有的“o”,不匹配“bob”中的“o”            |
| X{n}      | X重复n次如：“\\\b\[0-9\]{3}”匹配”000” ~ “999”, “o{2}”匹配“food”中的两个”o”,不匹配“bob”中的“o” |
| X+        | X重复1次或多次，等价于X {1,}如：’zo+’ 匹配 ”zo” ,“zoo”,但不匹配 ”z”               |
| X*        | X重复0次或多次，等价于X {0,}如：’zo*’ 匹配 ”zo” ,“zoo”, ”z”                      |
| X?        | X重复0次或1次，等价于X{0,1}如：’colou?r’ 匹配 ”color” ,”colour”；                 |

**匹配算法：贪婪性匹配算法**

Python针对重复限定符，默认采用贪婪性匹配算法，**贪婪性匹配算法**是指重复限定符会导致正则表达式引擎**尽可能多**地重复前导字符，只有当这种重复引起整个正则表达式匹配失败的情况下，引擎会进行回溯

```python
import re                   
re.findall('<.+>','<book><title>Python</title><author>Dong</author></book>')
>>> ['<book><title>Python</title><author>Dong</author></book>']
```

贪婪算法返回了一个最左边的最长匹配！

**匹配算法：懒惰性匹配算法**

如果在限定符后面加后缀”**?**”，正则表达式引擎则使用懒惰性匹配算法。**懒惰性匹配算法**是指重复限定符会导致正则表达式引擎**尽可能少**地重复前导字符，只有当这种重复引起整个正则表达式匹配失败的情况下，引擎会进行回溯

| **符号** |           **说明**            |
| -------- | ----------------------------- |
| *?       | 重复任意次，但尽可能少重复      |
| +?       | 重复1次或更多次，但尽可能少重复 |
| ??       | 重复0次或1次，但尽可能少重复    |
| {n,m}?   | 重复n到m次，但尽可能少重复      |
| {n,}?    | 重复n次以上，但尽可能少重复     |

```python
import re                   
re.findall('<.+?>','<book><title>Python</title><author>Dong</author></book>')
>>> ['<book>', '<title>', '</title>', '<author>', '</author>', '</book>']
```

**分组符**

分组符”()”：重复限定符重复前导字符，如果需要重复的符合某种模式的多个字符，则需要将描述该模式的正则表达式放在()内，()表示一个分组（子模式），即()内的内容作为一个整体出现

例如’(red)+’可以匹配’redred’、’redredred‘等多个重复’red’的情况

re. findall(pattern,string[,flags]):返回匹配结果列表，若pattern含有子模式，同时返回子模式的列表

| **正则表达式** |       **说明**       |
| -------------- | ------------------- |
| (pattern)？    | 允许模式重复0次或1次 |
| (pattern)*     | 允许模式重复0次或多次 |
| (pattern)+     | 允许模式重复1次或多次 |
| (pattern){m.n} | 允许模式重复m~n次     |

```python
telNumber = '''Suppose my Phone No. is 0535-1234567, yours is 010-12345678, his is 025-87654321.'''
pattern = re.compile(r'(\d{3,4})-(\d{7,8})')
pattern.findall(telNumber)
>>> [('0535', '1234567'), ('010', '12345678'), ('025', '87654321')]
re.findall(r'(\d{3,4})-(\d{7,8})',telNumber)
>>> [('0535', '1234567'), ('010', '12345678'), ('025', '87654321')]
re.findall(r'((\d{3,4})-(\d{7,8}))',telNumber)
>>> [('0535-1234567', '0535', '1234567'), ('010-12345678', '010', '12345678'), ('025-87654321', '025', '87654321')]
```

例如，我想把一个html标签替换为markdown格式，需要保留原链接

`<img src="http://cimg.fx361.com/images/2019/10/05/201910051418036954801.jpg">`

只需要`<img src="(http://.+.jpg)">`替换为`[]($1)`即可，其中`$1`表示引用第一个括号内的内容

正则表达式测试网站还有蓝天采集器都可以这样做，但是python好像不行，只能写循环了

```python
for each in pattern.findall(content):
    content = pattern.sub(each[0],content,count = 1)
```

**选择符”|”**

用于选择匹配多个可能的正则表达式中的一个，优先级最低，如果需要使用()来限制选择符的作用范围

|                                Python语句                                 |      匹配结果      |
| ------------------------------------------------------------------------- | ----------------- |
| `re.findall('red|green|blue','pink red ,green and blue')`                 | ['red','green', 'blue']  |
| `re.findall('\\b(red|green|blue)\\b','bluesky,pink red ,green and blue')` | ['red', 'green', 'blue']                        |

 **例子：电话号码一般形式为“区号-电话号码”，区号为3位或4位，电话号码为6位或8位数字。**

```python
import re
re.findall('((0\d{2}|\d{3})-(\d{8}|\d{6}))','复旦大学总机021-65642222')
>>> [(‘021-65642222’, ‘021’, ‘65642222’)]
```

#### re模块主要方法

既可以直接使用re模块的方法进行字符串处理，也可以将模式编译为正则表达式对象，然后使用正则表达式的方法来操作字符串

re模块的主要方法列表，pattern:匹配模式，string：要匹配的字符串，flag：匹配选项

|               **方法**                |                          **说明**                          |
| ------------------------------------ | ---------------------------------------------------------- |
| findall(pattern,string\[,flags\])    | 列出字符串中模式的所有匹配项返回匹配结果列表，若pattern含有组(子模式)，同时返回组的列表，或空列表  |
| search(pattern,string\[,flags\])     | 在字符串中寻找模式，若匹配，返回Match对象（参4.2.5），否则返回None |
| match(pattern,string\[,flags\])      | 从字符串的开始处匹配模式，若匹配，返回Match对象，否则返回None  |
| split(pattern,string\[,maxsplit=0\]) | 根据模式匹配项（匹配分割符）分割字符串，返回分割后的字符串列表，maxsplit为分割的最大次数    |
| sub(pat,repl,string\[,count=0\])     | 将字符串中所有pat的匹配项用repl替换；并返回替换后的**字符串**，count为替换的最大次数    |
| subn(pat,repl,string\[,count=0\])    | 将字符串中所有pat的匹配项用repl替换；并返**回元组**：(替换后的字符串,替换次数），count为替换的最大次数  |
| **escape(string)**                   | **将字符串中所有特殊正则表达式字符转义**                    |

**flag：匹配选项（可以使用|进行组合）**

|    **匹配选项**    |                  **说明**                  |
| ------------------ | ------------------------------------------ |
| re.l re.IGNORECASE | 忽略大小写                                 |
| re.L re.lOCALE     | \\w \\W \\b \\B \\s \\S与本地字符集有关     |
| re.M re.MULTILINE  | 多行匹配模式                                |
| re.S re.DOTALL     | 使元字符，也匹配换行符                      |
| re.U re.UNICODE    | 匹配Unicode字符                            |
| re.X re.VERBOSE    | 忽略模式中的空格，并可以使用#注释，提高可读性 |

#### 直接使用re模块方法

**示例：匹配搜索、分割**

```python
import re
text = 'alpha. beta....gamma delta '
pat = '[a-zA-Z]+'

re.findall(pat,text) # 查找所有单词
>>> ['alpha', 'beta', 'gamma', 'delta']
re.match('done|quit','done') # 匹配成功
>>> <_sre.SRE_Match object; span=(0, 4), match='done'>
print(re.match(‘done|quit’,‘doe!’) ) # 不成功
>>> None
print(re.match('to',"To be,\nor not to be")) # 不成功，只匹配开始处
>>> None
re.search('to',"To be,\nor not to be")
>>> <_sre.SRE_Match object; span=(14, 16), match='to'>
re.search('to',"To be,\nor not to be").group()
>>> to
re.split(‘[\. ]+',text)
>>> ['alpha', 'beta', 'gamma', 'delta']
re.split('[. ]+',text,maxsplit=2)
>>> ['alpha', 'beta', 'gamma delta']
re.split('[. ]+',text, 1)  # 分割1次
>>> ['alpha', 'beta....gamma delta']
```

**示例：替换，转义**

```python
import re
pat = '{name}'
text = 'Dear {name}...'
re.sub(pat,'Mr.Dong',text) #字符串替换
>>> 'Dear Mr.Dong...'
s = 'a s d'
re.sub('a|s|d','good',s) #字符串替换
>>> 'good good good'
re.escape('http://www.python.org') #字符串转义
>>> 'http\\:\\/\\/www\\.python\\.org'
```

**示例：删除字符串中重复的空格**

```python
import re
s='aaa      bb      c d e   fff    '
re.split('[\s]+',s)
>>> ['aaa', 'bb', 'c', 'd', 'e', 'fff', '']
re.split('[\s]+',s.strip())
>>> ['aaa', 'bb', 'c', 'd', 'e', 'fff']
' '.join(re.split('[\s]+',s.strip()))
>>> 'aaa bb c d e fff'
re.sub('\s+',' ',s.strip())
>>> 'aaa bb c d e fff'
s
>>> 'aaa      bb      c d e   fff    '
s.split()     #也可以不使用正则表达式
>>> ['aaa', 'bb', 'c', 'd', 'e', 'fff']
' '.join(s.split())
>>> 'aaa bb c d e fff'
```

**示例：使用以'\'开头的元字符**

```python
import re
example = 'ShanDong Institute of Business and Technology'
re.findall('\\ba.+?\\b',example) # 以a开头的完整单词
>>> ['and']
re.findall('\\Bo.+?\\b',example) # 不以o开头且含有o字母的单词剩余部分
>>> ['ong', 'ology']
re.findall('\\b\w.+?\\b',example) # 所有单词
>>> ['ShanDong', 'Institute', 'of', 'Business', 'and', 'Technology']
re.findall(r'\b\w.+?\b',example) # 使用原始字符串，减少需要输入的符号数量
>>> ['ShanDong', 'Institute', 'of', 'Business', 'and', 'Technology']
re.findall('\d\.\d\.\d','Python 2.7.8,Python 3.4.2')  # 查找并返回x.x.x的数字形式
>>> ['2.7.8', '3.4.2'] 
re.split('\s',example) # 使用任何空白字符分割字符串
>>> ['ShanDong', 'Institute', 'of', 'Business', 'and', 'Technology']
```

## 函数设计与使用

函数：可能需要反复执行的代码封装为函数，实现代码的复用,保证代码的一致性，Python提供了许多常用的内置函数如print()、len()、sum()等

函数和方法的区别。

区别一所处的位置：函数是直接写文件中而不是class中，方法是只能写在class中。

区别二定义的方式：

1.函数定义的方式 def关键字  然后接函数名 再是括号 括号里面写形参也可以省略不写形参 

```python
def functionName():
    """这里是函数的注释"""
    print("这一块写函数的内容")
```

2.方法定义的方式 首先方法是定义在类中的其他他大体和函数定义差不多，这里需要注意的一点就是方法必须带一个默认参数(相当于this)，静态方法除外

```python
class className(super):    
    def methodName(self):
        """这里是方法的注释
        self相当于this；
        """
        print("这里是方法的内容")
```

区别三调用的方式：

1.函数的调用：函数的调用是直接写  函数名(函数参数1,函数参数2,......) 

```python
def functionName():
    print("这是一个函数")
#调用
functionName()
```

2.方法的调用：方法是通过对象点方法调用的（这里是指对象方法）

```python
class className:    
    def method(self):
        print("这是一个方法") 
#调用---------------------
#实例化对象
c=className() 
c.method()
```

### 函数定义与调用

#### def

函数定义（声明）格式：

```python
def 函数名([形参列表]):
	'''注释''' 
	函数体
```

函数调用：`函数名([实参列表])`

* 函数名命名规则为第一个单词小写，第二个单词大写……

* 括号后面的冒号必不可少,然后换行

* 在定义函数时，开头部分的注释并不是必需的，但是如果为函数的定义加上这段注释的话，可以为用户提供友好的提示和使用帮助。

* 参数（形参）可没有，如果有以逗号(,)隔开，但括号必须有

* 可以有缺省值参数，相应位置没有参数传递时使用缺省值

* 支持可变长度参数` *args`，调用时相应位置可以传递0个或者多个参数

* 通过return语句返回值，如果没有return，返回的值为None，其类型为NoneType（只有一个值即None）

* 实参：应该与形参（函数定义时的参数）对应，表示传递实参给出的对象引用到相应的形参

* 支持关键字参数：即相应参数采用`形参名=value`

#### lambda

python 使用 lambda 来创建匿名函数。其主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。lambda 函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。

> lambda [arg1 [,arg2,.....argn]]:expression

```python
# 可写函数说明
sum = lambda arg1, arg2: arg1 + arg2
 
# 调用sum函数
print ("相加后的值为 : ", sum( 10, 20 ))
>>> 相加后的值为 :  30

map(lambda  x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10]) 
>>> [3, 7, 11, 15, 19]

# 3. 同样的，也可以把匿名函数作为返回值返回
def build(x, y):
    return lambda: x * x + y * y
```

### 形参与实参

* 绝大多数情况下，在函数内部直接修改形参的值不会影响实参

```python
def addOne(a):
	print(a)
	a += 1
	print(a)
a=3
addOne(a)
>>> 4
a
>>> 3
```

* 在有些情况下，可以通过特殊的方式在函数内部修改实参的值

```python
def modify(v):
    v[0] = v[0] + 1
v = [10]
modify(v)
>>> [11]
v
>>> [11]
```

**当参数为数值类型时，传值(id不同)，当参数类型为列表（字典）时，传引用(id相同)**

### 参数类型

在Python中，函数参数有很多种：普通参数、默认值参数、关键参数、可变长度参数等等。

Python函数的定义非常灵活，在定义函数时不需要指定参数的类型，形参的类型完全由调用者传递的实参类型以及Python解释器的理解和推断来决定，类似于重载和泛型；

函数编写如果有问题，只有在调用时才能被发现，传递某些参数时执行正确，而传递另一些类型的参数时则出现错误。

#### 默认值参数

```python
def 函数名(……，形参名=默认值)
    函数体
```

调用带有默认值参数的函数时，可以不对默认值参数进行赋值，也可以赋值，具有较大的灵活性。

使用“**函数名.__defaults__**”以元组的形式查看函数所有默认值参数的当前值

```python
def say( message, times =1 ):
	        print (message * times)
	        
say('hello')    #不为默认值参数传值
>>> hello
say('hello',3)  #使用调用者显示传递的值
>>> hellohellohello
say.__defaults__
>>> (1,)
```

**默认值参数必须出现在函数参数列表的最右端，且任何一个默认值参数右边不能有非默认值参数。**

例：使用指定分隔符将列表中所有字符串元素连接成一个字符串，默认空格。

```python
def Join(List,sep=None):
    return (sep or ' ').join(List)
```

**默认值参数如果使用不当，会导致很难发现的逻辑错误。**

```python
def demo(newitem,old_list=[]):
    old_list.append(newitem)
    return old_list

print (demo('a') )  #right
>>> ['a']
print (demo('b'))
>>> ['a', 'b']
print (demo.__defaults__)
>>> (['a', 'b'],)
```

注意：多次调用函数并且不为默认值参数传递值时，默认值参数值用在第一次调用时进行解释，可以使用函数名.__defaults__查看默认参数的当前值

修改程序如下：

```python
def demo(newitem,old_list=None):
    if old_list is None:
        old_list=[]
    old_list.append(newitem)
    return old_list
```

#### 关键参数

**关键参数**主要指实参，即调用函数时的参数传递方式。

通过**关键参数可以按参数名字**传递值，实参顺序可以和形参顺序不一致，但不影响传递结果，避免了用户需要牢记位置参数顺序的麻烦。

```python
def demo(a,b,c=5):
    print (a,b,c)
	
demo(3,7)
>>> 3 7 5
demo(a=7,b=3,c=6)
>>> 7 3 6
demo(c=8,a=9,b=0)
>>> 9 0 8
```

#### 可变长度参数

**可变长度参数**在定义函数时主要有两种形式：

`*parameter`：接收多个实参并将其放在一个元组中

`**parameter`，接收字典形式的实参。

```python
def demo(*p):
	print (p)
>>> demo(1,2,3)
(1, 2, 3)
# *parameter无论调用该函数时传递了多少实参，一律将其放在元组中。
```

```python
def demo(**p):
	for item in p.items():
		print (item)
		
demo(x=1,y=2,z=3)
>>> ('z', 3)
>>> ('y', 2)
>>> ('x', 1)
# 4. **parameter调用该函数时自动将接收的参数转换为字典。
```

几种不同类型的参数可以混合使用,但是不建议这样做,易导致代码混乱而严重降低可读性，可能导致查错非常困难

#### 参数传递的序列解包

为含有多个变量的函数传递参数时，可以使用Python列表、元组、集合、字典以及其他可迭代对象作为实参，并在实参名称前加一个**星号***，Python解释器将自动进行解包。

```python
def demo(a,b,c):
	print (a+b+c)	
seq=[1,2,3]
demo(*seq)
>>> 6

dic={1:'a',2:'b',3:'c'}
demo(*dic.values())
>>> abc
```

### return语句

* return语句用于从一个函数中返回并结束函数的执行，同时还可以通过其从函数中返回一个值。

* 无论return语句出现在函数的什么位置，一旦得到执行将直接结束函数的执行。

* 函数的返回值类型由return语句返回值的类型来决定

* 如果函数没有return语句或者没有执行return语句，执行了不带任何值的return语句，则函数都默认为返回空值None。

```python
def maximum( x, y ):
	if x>y:
		   return x
	else:
		   return y
```

#### 返回函数

return除了返回常数外，还可以返回一个函数。它和`yield`类似，都是只有使用的时候才运行，否则只返回一个函数。

```python
def lazy_sum(*args):
    def sum():
        ax = 0
        for n in args:
            ax = ax + n
        return ax
    return sum

f = lazy_sum(1, 3, 5, 7, 9)
f           # 调用lazy_sum()时只会返回函数
>>> <function lazy_sum.<locals>.sum at 0x101c6ed90>
f()         # 调用f()时才会返回值，这是因为，第一个f调用的是laze_sum()，返回的是sum函数，第二个f()即调用sum函数，这次就能返回值了
>>> 25
```

#### 闭包

返回函数时，相关参数和变量都保存在返回的函数中，这种程序结构称为“闭包（Closure）”

注意返回的函数并不会立刻执行，只有调用f()时才会执行

```python
def count():
    fs = []
    for i in range(1, 4):
        def f():
             return i*i
        fs.append(f)
    return fs

f1, f2, f3 = count()  # count()的返回值fs虽然是一个列表，但其中元素是函数
```

这个例子中，我们调用的f1()，f2()，f3()结果都是9，这是因为每个返回的函数都引用了参数i，但是它只会以最后一个函数调用的i为准，然后再进行运算，f3使i变为了3，因此调用f()都会返回9

因此，不要在循环内写函数，或者做其他任意可能导致返回函数所引用参数变化的行为

上面的代码可以改写如下：

```python
def count():
    def f(j):
        def g():
            return j*j
        return g
    fs = []
    for i in range(1, 4):
        fs.append(f(i)) # f(i)立刻被执行，因此i的当前值被传入f()
    return fs
```

### 高级函数

#### map/reduce/filter

**map(function, iterable, ...)**

map() 会根据提供的函数对指定序列做映射。第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的**Iterator**。

```python
def square(x) :            # 计算平方数
    return x ** 2
list(map(square, [1,2,3,4,5]))   # 计算列表各个元素的平方
>>> [1, 4, 9, 16, 25]
list(map(str, [1, 2, 3, 4, 5, 6, 7, 8, 9]))  # 将数值类型转换为字符串
>>> ['1', '2', '3', '4', '5', '6', '7', '8', '9'] 
```

**reduce(function，iterable, ...)**

函数将一个数据集合（列表，元组等）中的所有数据进行下列操作：用传给 reduce 中的函数 function（有两个参数）先对集合中的第 1、2 个元素进行操作，得到的结果再与第三个数据用 function 函数运算，最后得到一个结果。

即：`reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)`

```python
from functools import reduce   # python3中该函数已被移除，只能通过模块引用

def fn(x, y):
    return x * 10 + y

reduce(fn, [1, 3, 5, 7, 9])      # 将几个数字拼成一串整数
>>> 13579
```

**filter(function，iterable, ...)**

和map()类似，filter()也接收一个函数和一个序列。和map()不同的是，filter()把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素。

```python
'''
背景：埃氏筛法选素数，首先取从2开始的所有素数，用2把所有2的倍数删去
从新序列中取第一个数3，用3把所有3的倍数删去
从新序列中取第一个数5，用5把所有5的倍数删去
……
'''
def _odd_iter():  # 生成从3开始的奇数数列
    n = 1
    while True:
        n = n + 2
        yield n

def _not_divisible(n):        # 判定是否能被n整除
    return lambda x: x % n > 0  # 返回True/False
    # 上面这个匿名函数有些难以理解，实际上是这样的：它有两个函数，一个def定义的函数，一个lambda匿名函数
    # n传入的其实是def函数，x传入的是匿名函数
    # 结合下面的filter函数，可以理解为：先将it序列传入n，比如现在n是2，那么该函数就变成了filter(lambda x: x % 2 > 0,it)，接着再把it序列传入x，相当于两层循环？

def primes():
    yield 2
    it = _odd_iter() # 初始序列
    while True:
        n = next(it) # 返回序列的第一个数
        yield n
        it = filter(_not_divisible(n), it) # 构造新序列
```

#### 偏函数

偏函数即新定义一个函数，其各参数分别是原函数、原函数第一个参数、原函数第二个参数……（当然，如果指定了原函数的参数名，则可不按顺序），接着调用原函数并输入这些参数，这样可以为原函数预先设定参数，从而简化原函数的复杂程度

```python
import functools
int2 = functools.partial(int, '50')
int2()
>>> 50
int2 = functools.partial(int, base = 2)  # int(x[，base])，base即进制
int2('10111')     # 好像有进制的情况下不能输入数值型
>>> 23
max2 = functools.partial(max, 100)
max2(1,2,3,4)
>>> 100
```

### 案例精选

**例1：编写函数计算圆的面积。**

```python
import math

def calcCircleArea(radius):
    '''
    return the area of a circle with radius value.
    '''
    if isinstance(radius,int) or isinstance(radius,float):
        return math.pi * radius * radius
    else:
        print("Parameter radius need int or float value!")
```

**例2：编写函数，输出一组列表中的最小数以及ID**

```python
import random

def searchminindex(lst):
    if lst:
        minvalue = min(lst)
        result = (minvalue,)
        for idx, value in enumerate(lst):
            if value == minvalue:
                result = result + (idx,)
        #end for
        return result
    else:
        return (None,)

if __name__ == "__main__":
    lst = [random.randint(0,100) for idx in range(10)]
    print("lst: {}".format(lst))
    ret = searchminindex(lst)
    print("ret: {}".format(ret))
```

**例3：编写函数，接收字符串参数，返回一个元组，其中第一个元素为大写字母个数，第二个元素为小写字母个数。**

```python
def demo(s):
    result = [0,0]
    for ch in s:
        if 'a'<=ch<='z':
            result[1] += 1
        elif 'A'<=ch<='Z':
            result[0] += 1
    return result
print(demo('aaaabbbbC'))
```

**例4：编写函数，接收包含20个整数的列表lst和一个整数k作为参数，返回新列表。处理规则为：将列表lst中下标k之前的元素逆序，下标k之后的元素依序，然后将整个列表lst中的所有元素逆序。**

```python
def demo(lst,k):
    x = lst[:k]
    x.reverse()
    y = lst[k:]
    y.reverse()
    r = x+y
    r.reverse()
    return r
```

**例5：编写函数，接收整数参数t，返回斐波那契数列中大于t的第一个数。**

```python
def demo(t):
    a, b = 1, 1
    while b<t:
        a, b = b, a+b
    else:
        return b
print(demo(50))
```

**例6：编写函数，接收一个整数t为参数，打印杨辉三角前t行。**

```python
def printtriangle(t):
    if t>=1:
        print([1])
    if t>=2:
        print([1,1])

    line = [1,1]
    for i in range(2,t):
        r = []
        for j in range(0,len(line)-1):
            r.append(line[j] + line[j+1])
        line = [1] + r + [1]
        print(line)
    #end for

if __name__ == "__main__":
    t = 10
    print("Triangle t = {} :".format(t))
    printtriangle(t)
```


**例7：编写函数，接收一个正偶数为参数，输出两个素数，并且这两个素数之和等于原来的正偶数。如果存在多组符合条件的素数，则全部输出。**

```python
import math

def isprime(n):
    for k in range(2,int(math.sqrt(n))+1):
        if n % k == 0:
            return False
    return True

def decompose(n):
    if isinstance(n,int) and n>0 and n%2 == 0:
        for a in range(2, n//2 + 1):
            if isprime(a) and isprime(n-a):
                print("{} = {} + {}".format(n,a,n-a))

if __name__ == "__main__":
    for n in (10, 200, 2, 4, 11):
        print("Decompose {}".format(n))
        decompose(n)
```

例8：编写函数，接收两个正整数作为参数，返回一个数组，其中第一个元素为最大公约数，第二个元素为最小公倍数。

```python
def solvegcd(n,m):
    if isinstance(n,int) and n>0 and isinstance(m,int) and m>0:
        if m>n:
            m, n = n, m
        p = m*n
        while m != 0:
            r = n % m
            n = m
            m = r
            #print("{} {} {}".format(m, n, r))
        return (p//n, n)
    else:
        return (None,None)


if __name__ == "__main__":
    print(solvegcd(36,12000))
```

## 类和实例

### 相关名词介绍

- **类(Class):** 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。
- **方法**：类中定义的函数。
- **类变量**：类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体之外。类变量通常不作为实例变量使用。
- **数据成员**：类变量或者实例变量用于处理类及其实例对象的相关的数据。
- **方法重写**：如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。
- **局部变量**：定义在方法中的变量，只作用于当前实例的类。
- **实例变量**：在类的声明中，属性是用变量来表示的。这种变量就称为实例变量，是在类声明的内部但是在类的其他成员方法之外声明的。
- **继承**：即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。例如，有这样一个设计：一个Dog类型的对象派生自Animal类，这是模拟"是一个（is-a）"关系（例图，Dog是一个Animal）。
- **实例化**：创建一个类的实例，类的具体对象。
- **对象**：通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法。

### 类的定义与调用

```python
class MyClass():  # 括号内是该类的父类，不填的话默认是object类，也即所有类的父类，也可省略括号
    """一个简单的类实例"""
    name = 'Dong Xing'  
    # 这样是绑定一个属性到类上，可以通过x.name访问也可以直接通过MyClass.name访问
    def f(self):    
    # 类中的方法第一个参数表示的永远是self，即它本身，不需要为它传实参。可以写成其他参数如caly，如def f(caly)等价于def f(self)
        return 'hello world'
 
# 实例化类
x = MyClass()
 
# 访问类的属性(类中的常量)和方法(类中的函数)
print("MyClass 类的属性 name 为：", x.name)        # Dong Xing
print("MyClass 类的方法 f 输出为：", x.f())   # 'hello world'

x.id = 'caly'
# 添加类的属性，也可对已有属性进行修改
x.name = 'Li'  # 实例的优先级高于类，所以访问x.name变成了Li，但是类属性不变，MyClass.name仍然是DongXing
```

类有一个名为 __init__() 的特殊方法（构造方法），该方法在类实例化时会自动调用，可利用该方法绑定默认属性

```python
class Complex():
    def __init__(self, name, age):
        self.name = name
        self.age = age
x = Complex('Dong Xing', 22)      # 一旦类中定义了__init__方法，实例化时就必须要填参数了
print(x.name, x.age)   # 输出结果：Dong Xing 22
```

**数据封装**：我们可以通过函数来访问类的属性，比如`print(x.name)`，但如果我们把`print()`写在类的内部，这样就可以直接通过类来访问这些数据了，也叫数据封装。

```python
class Complex():
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def print_info(self):
        print(self.name,self.age)

x = Complex('Dong Xing', 22) 
x.print_info()     # Dong Xing 22
```

类似地，可以将所有常用的函数写为方法。

### 访问限制

如前所示，你可以对类的属性自由修改，如果我们想要限制这点，可以定义私有属性，只要在属性前加上`__`即可，方法类似

```python
class Complex():
    __name = 'Dong Xing'
    def __init__(self, age):
        self.__age = age
    # 这样，你就无法在外部访问x.__name和x.__age了
    def get_age(self):
        return self.__age
    # 如果你想在外部访问的话，可以定义一个get_age方法
    def set(self, age):
        self.__age = age
    # 如果你想在外部修改的话，可以定义一个set_age方法
    # 这样的话，可以限制修改属性，避免无效输入（比如set方法加个判定条件）
    def __foo(self):
        print("这是一个私有方法")
    # 类似地，可以构造私有方法
```

### 继承和多态

基本语法是`class ClassName(Base1, Base2, Base3)`，是的，可以继承多个父类。

继承最大的用处就是可以使用父类的方法，如果存在多个父类，则依次从左到右进行搜寻该方法。但如果子类本身就有该方法，则直接调用子类的方法。

另外，如果某个实例的数据类型是某个子类，那么它同样也是父类，但反过来不行。

```python
class people:
    name = ''
    age = 0
    __weight = 0
    def __init__(self,n,a,w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print("%s 说: 我 %d 岁。" %(self.name,self.age))
 
#单继承示例
class student(people):
    grade = ''
    def __init__(self,n,a,w,g):
        #调用父类的构函
        people.__init__(self,n,a,w)
        self.grade = g
    #覆写父类的方法
    def speak(self):
        print("%s 说: 我 %d 岁了，我在读 %d 年级"%(self.name,self.age,self.grade))
```

### 类的专有方法

- **\_\_init\_\_ :** 构造函数，在生成对象时调用
- **\_\_del\_\_ :** 析构函数，释放对象时使用
- **\_\_repr\_\_ :** 打印，转换
- **\_\_setitem\_\_ :** 按照索引赋值
- **\_\_getitem\_\_:** 按照索引获取值
- **\_\_len\_\_:** 获得长度
- **\_\_cmp\_\_:** 比较运算
- **\_\_call\_\_:** 函数调用
- **\_\_add\_\_:** 加运算
- **\_\_sub\_\_:** 减运算
- **\_\_mul\_\_:** 乘运算
- **\_\_truediv\_\_:** 除运算
- **\_\_mod\_\_:** 求余运算
- **\_\_pow\_\_:** 乘方

注意，这些方法都是内置类才能用的，而且可以省略`____`，比如`len('ABC')`等价于`'ABC'.__len__()`

我们自己写的类，如果也想用len(myObj)的话，就自己写一个__len__()方法：

```python
class MyDog(object):
    def __len__(self):
        return 100
dog = MyDog()
len(dog)
>>> 100
```

如果要获得一个对象的所有属性和方法，可以使用`dir()`函数，它返回一个包含字符串的list，比如，获得一个str对象的所有属性和方法：

```
>>> dir('ABC')
['__add__', '__class__',..., '__subclasshook__', 'capitalize', 'casefold',..., 'zfill']
```

## 文件操作

### 文件对象

文件对象的操作遵循特定的流程：三步

* 打开：使用open()；

* 操作：读、写、删除等操作；

* 关闭：使用close()。

#### 文件打开详解

* 文件对象名 = open（文件名\[，访问模式\[，缓冲区\]\])

访问模式：

|    值     |    说明    |
| -------- | --------- |
| r（默认） | 读模式     |
| w         | 写模式     |
| a         | 追加模式   |
| b         | 二进制模式 |
| +         | 读写模式   |

缓冲区：读写文件的缓存模式；0表示不缓存，1表示缓存，大于1则表示缓冲区的大小，小于0这表示使用默认的缓冲区大小；默认值为1

```python
# 4. 以读写模式打开文件（文件不存在则创建文件，否则置文件指针到文件尾）：
f = open('b.csv','a+')
```

#### 文件对象的属性

|    属性    |          说明          |
| ---------- | ---------------------- |
| f.closed   | 若文件关闭则为真，否则假 |
| f.encoding | 文件所使用的编码        |
| f.mode     | 文件访问模式            |
| f.name     | 文件的名称              |

#### 文件对象的常用操作

<table>
<tr>
    <td>分组</td>
    <td>方法</td>
    <td>说明</td>
</tr>
<tr>
    <td rowspan='3'>读</td>
    <td>f.read([size])</td>
    <td>从文件中读取size个字节，默认读取所有</td>
</tr>
<tr>
    <td>f.readline</td>
    <td>从文本中读取一行内容</td>
</tr>
<tr>
    <td>f.readlines</td>
    <td>把文本文件中的每行作为字符串插入列表中返回列表</td>
</tr>
<tr>
    <td rowspan='2'>写</td>
    <td>f.write(s)</td>
    <td>把字符串s写入文件</td>
</tr>
<tr>
    <td>f.writelines</td>
    <td>把字符串列表s写入文件，不添加换行符</td>
</tr>
<tr>
    <td rowspan='5'>其他操作</td>
    <td>f.flush()</td>
    <td>把缓冲区内容写入文件，不关闭文件</td>
</tr>
<tr>
    <td>f.close()</td>
    <td>把缓冲区内容写入文件，关闭文件，释放对象</td>
</tr>
<tr>
    <td>f.tell()</td>
    <td>返回当前文件指针的位置</td>
</tr>
<tr>
    <td>f.truncate([size])</td>
    <td>删除从当前指针位置到文件末尾的内容。如果指定了size，则不论指针在什么位置都只留下前size个字节，其余的删除</td>
</tr>
<tr>
    <td>f.seek(offset[,whence])</td>
    <td>把文件指针移动到新的位置。offset表示相对于 Whence的位置；Whence为0表示从文件头开始计算，1表示从当前位置开始计算，2表示从文件尾开始计算，默认为0</td>
</tr>
</table>

#### 文件操作模式

```python
lines=[]
with open(”sample.txt”，”rb”) as handler:
  lines = handler.readlines()
print(lines)
# 5. 为了防止格式不对，最好用rb模式打开，否则会报错
```

### OS模块

```python
import os
os.listdir(org_url) # 列出某一路径下所有文件名

for root, dirs, files in os.walk(r'E:\python'):  
# os.walk生成一个三元组，分别是所有目录（包括子目录）及文件地址，所有文件的列表，所有文件的列表
    print(root) 
```

### shutil模块

```python
import shutil
shutil.copy(file_url,copy_url)  # 将file文件复制到指定文件夹下
```

### 例

**例1 向文本文件写入内容。**

 注意s1和s2中都有行结束标记。

```python
def write(filename):
    s1='1\tfudan\t复旦大学\t中国上海\t200433\n' 
    s2='2\tsjtu\t交通大学\t中国上海\t200240\n' 
    with open(filename,"a+") as handler:
        #handler.truncate(0)
        handler.write(s1)
        handler.write(s2)

if __name__ == '__main__':
    write("sample.txt")
```

**例2 排序10KI.txt中的整数，并按升序排列写入10KI_asc.txt中。**

```python
def sort10ki():
    with open('10KI.txt','r') as f:
        data = f.readlines()
    data = [int(line.strip()) for line in data]
    data.sort()
    data = [str(i)+'\n' for i in data]
    with open('10KI_asc.txt','a+') as f:
        f.truncate(0)
        f.writelines(data)

sort10ki()
fa('10KI_asc.txt')
```

**例3 把T76.py中的代码，在行首加上行号，保存为文件T76_n.py**

```python
def comment(fname):
    with open(fname,'r') as f:
        lines = f.readlines()

    lines = [ str(idx)+") "+line for idx,line in enumerate(lines)]
  
    with open(fname[:-3]+'_n.py','a+') as f:
        f.truncate(0)
        f.writelines(lines)
```

## 异常处理结构与程序调试

### 什么是异常（exception）

* 简单地说，异常是指程序运行时引发的错误。引发错误的原因有很多，例如除零、下标越界、文件不存在、网络异常、类型错误、名字错误、字典键错误、磁盘空间不足，等等。语法错误和逻辑错误不属于异常，但有些语法错误往往会导致异常，例如由于大小写拼写错误而访问不存在的对象。

* 如果这些错误得不到正确的处理将会导致程序终止运行，而合理地使用异常处理结果可以使得程序更加健壮，具有更强的容错性，不会因为用户不小心的错误输入或其他运行时原因而造成程序终止。

* 也可以使用异常处理结构为用户提供更加友好的提示。

* 异常分为两个阶段：第一个阶段是引起异常发生的错误；第二个阶段是检测并处理阶段。

* 不建议使用异常来代替常规的检查，如if...else判断。

* 应避免过多依赖于异常处理机制。

* 当程序出现错误，python会自动引发异常，也可以通过raise显式地引发异常。

### 异常类

|       异常        |                      描述                       |
| ----------------- | ----------------------------------------------- |
| Nameerror         | 尝试访问一个没有申明的变量                       |
| ZeroDivisionError | 除数为0                                         |
| SyntaxError       | 语法错误                                        |
| IndexError        | 索引超出序列范围                                 |
| KeyError          | 请求一个不存在的字典关键字                       |
| IOError           | 输入输出错误(例:读取不存在的文件)                  |
| Attribute Error   | 尝试访问未知的对象属性                           |
| ValueError        | 传给函数的参数类型不正确(例:给int()函数传入字符串) |
| AssertionError    | 断言异常                                        |

**抛出异常raise语句**

主动抛出异常：定义自己的异常类时或者需要抛出异常时。

raise语法：`raise [SomeException [, args [,traceback]]`

SomeException：必须是一个异常类，或异常类的实例；

Args：传递给SomeException的参数，必须是一个元组；

Traceback：很少用，主要是用来提供一个traceback对象。

**自定义异常类**

下面的例子演示了自定义的异常类，必须继承Exception类：所有异常类的基类（demon01）；

```python
class MyError(Exception):
  def __init__(self, value):
    self.value = value
  def __str__(self):
    return repr(self.value)

try:
    raise MyError(2*2)
except MyError as e:
    print('My exception occurred, value:', e.value)
>>> My exception occurred, value: 4
raise MyError('oops!')

>>> Traceback (most recent call last):
        File "<stdin>", line 1, in ?
        __main__.MyError: 'oops!'
```

### 异常处理结构

常见的异常处理结构：

* try.......except结构

* try.......except .......else结构

* 带有多个except的try结构

* try.......except .......finally结构

#### try.......except结构

```python
try:
    try_block #被监控的代码
except Exception[,reason]:
    except_block #异常处理代码
```

**代码处理形式二**

```python
try:
  ...
except BaseException,e:
  except_block
```

**优势：能够处理所有的异常**

**建议**

尽量显式捕捉可能会出现的异常，并编写具有针对性的代码；最后一个except用来捕捉BaseException。

My error 是exception的子类型；Exception是所有例外的父类型

**示例1**

```python
while True:
    try:
        x = int(input("Please enter a number: "))
        break
    except ValueError:
        print("That was no valid number.  Try again...")
```

**示例2**

```python
try:
    raise Exception('spam', 'eggs')
except Exception as inst:
    print(type(inst))    # the exception instance
    print(inst.args)     # arguments stored in .args
    print(inst)         
# __str__ allows args to be printed directly,but may be overridden in exception subclasses
    x, y = inst.args     # unpack args
    print('x =', x)
    print('y =', y)
<class 'Exception'>
('spam', 'eggs')
('spam', 'eggs')
>>> x = spam
>>> y = eggs
```

#### try.......except .......else

示例1：

```python
a_list = ['China', 'America', 'England', 'France']
while True:
    print('请输入字符串的序号')
    n = int(input())
    try:
        print(a_list[n])
    except IndexError:
        print('列表元素的下标越界，请重新输入字符串的序号')
    else:
        break
```

**示例2**

```python
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except IOError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```

#### 带有多个except的try结构

**示例1**

```python
try:
    x=int(input('请输入被除数: '))
    y=int(input('请输入除数: '))
    z=float(x) / y
except ZeroDivisionError:
    print('除数不能为零')
except TypeError:
    print('被除数和除数应为数值类型')
except NameError:
    print('变量不存在')
else:
    print(x, '/', y, '=', z)
```

**示例2**

```python
import sys
try:
    f = open('sample.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise

import sys
try:
    f = open('sample.txt')
    s = f.readline()
    i = int(s.strip())
except (OSError, ValueError, RuntimeError, NameError):
    pass
```

#### try.......except .......finally结构

Finally中的语句总会执行，可以用于清理工作，以便释放资源。

```python
try:
  try_block         #被监控的代码
except:
  except_block      #例外处理程序块
finally:
  finally_block     #无论如何都会执行
```

**示例1：文件的读取**

```python
try:
    f = open('sample.txt', 'r')
    line = f.readline( )
    print(line)
finally:
    f.close()
```
例外产生之后，需要有相应的处理。如果没有相应的except处理块，代码的执行顺序会发生改变，直到找到相应的except处理块或者程序退出为止。

```python
def divide(x, y):
    try:
        result = x / y
    except ZeroDivisionError:
        print("division by zero!")
    else:
        print("result is", result)
    finally:
        print("executing finally clause")
```

**示例3**

**finally代码中：返回值要慎重！**

```python
def demo_div(a, b):
    try:
        return a/b
    except:
        pass
    finally:
        return -1 
```

### 断言与上下文处理

两种特殊的异常处理形式；形式上比通常的异常处理简单；

#### 断言

断言语句的语法：`assert expression[, reason] `

当判断表达式expression为真时，什么都不做；如果表达式为假，则抛出异常。

assert语句用途：一般用于开发程序时对特定必须满足的条件进行验证，仅当__debug__为True时有效。当Python脚本以-O选项编译为字节码文件时，assert语句将被移除以提高运行速度。

**断言：示例1**

```python
try:
    assert 1 == 2 , "1 is not equal 2!"
except AssertionError as reason:
    print("%s:%s"%(reason.__class__.__name__, reason))
>>> AssertionError:1 is not equal 2!
```

**断言：示例2**

```python
def RecursiveSum(n):
  	#precondition: n >= 0
    assert(n >= 0)
    if n == 0: return 0
    return RecursiveSum(n - 1) + n
  	#postcondition: returned sum of 1 to n

def SumToN(n):
    if n <= 0:
        raise ValueError("N must be greater than or equal to 0")
    else:
    	return RecursiveSum(n)

SumToN('a')
>>> Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "<stdin>", line 2, in SumToN
    TypeError: unorderable types: str() <= int()
SumToN(-1)
>>> Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "<stdin>", line 3, in SumToN
    ValueError: N must be greater than or equal to 0
```

例程中assert作用：调用函数使用的参数符合要求；不符合要求时：提示用户存在的问题。

#### 上下文管理

使用with语句进行上下文管理，With语句的语法

```python
with context_expr [as obj]:
    with_block 

obj = context_expr
obj.__enter__()
try:
    with_block
finally:
    obj.__exit__()
```

with语句的作用：解决try…finally结构中的资源释放问题；提供了一种简单的方法。

with语句的实现：依赖于python语言的magic method，需要实现__enter__()和__exit__()两个方法：上下文管理协议；或者通过引用contextlib，并使用@contextlib.contextmanager方式实现。

**示例1**

```python
import time
class Timer(object):
    def __init__(self):
        pass
 
    def __enter__(self):
        self.start = time.time()
 
    def __exit__(self, exception_type, exception_val, trace):
        print("elapsed:", time.time() - self.start)
with Timer():
    [i for i in range(10000)]
>>> elapsed: 1.7445049285888672
```

**with语句：示例2**

```python
import contextlib
import time
 
@contextlib.contextmanager
def time_print(task_name):
    t = time.time()
    try:
        yield
    finally:
        print(task_name, "took", time.time() - t, "seconds.")
with time_print("processes"):
    [i for i in range(10000)]
```

代码和前面(1)中的代码功能相同；通过使用@contextlib.contextmanager实现