---
title: numpy库
toc: true
date: 2019-10-24 00:17:23
tags: [numpy,python]
categories:  
- 编程语言
- python
---

## NumPy

### 数据类型

numpy 支持的数据类型比 Python 内置的类型要多很多，基本上可以和 C 语言的数据类型对应上，其中部分类型对应为 Python 内置的类型。下表列举了常用 NumPy 基本类型。

|    名称    |                                  描述                                  |
| ---------- | ---------------------------------------------------------------------- |
| bool_      | 布尔型数据类型（True 或者 False）                                       |
| int_       | 默认的整数类型（类似于 C 语言中的 long，int32 或 int64）                  |
| intc       | 与 C 的 int 类型一样，一般是 int32 或 int 64                             |
| intp       | 用于索引的整数类型（类似于 C 的 ssize_t，一般情况下仍然是 int32 或 int64） |
| int8       | 字节（-128 to 127）                                                    |
| int16      | 整数（-32768 to 32767）                                                 |
| int32      | 整数（-2147483648 to 2147483647）                                       |
| int64      | 整数（-9223372036854775808 to 9223372036854775807）                     |
| uint8      | 无符号整数（0 to 255）                                                  |
| uint16     | 无符号整数（0 to 65535）                                                |
| uint32     | 无符号整数（0 to 4294967295）                                           |
| uint64     | 无符号整数（0 to 18446744073709551615）                                 |
| float_     | float64 类型的简写                                                     |
| float16    | 半精度浮点数，包括：1 个符号位，5 个指数位，10 个尾数位                   |
| float32    | 单精度浮点数，包括：1 个符号位，8 个指数位，23 个尾数位                   |
| float64    | 双精度浮点数，包括：1 个符号位，11 个指数位，52 个尾数位                  |
| complex_   | complex128 类型的简写，即 128 位复数                                    |
| complex64  | 复数，表示双 32 位浮点数（实数部分和虚数部分）                            |
| complex128 | 复数，表示双 64 位浮点数（实数部分和虚数部分）                            |

numpy 的数值类型实际上是 dtype 对象的实例，并对应唯一的字符，包括 np.bool_，np.int32，np.float32，等等。

int8, int16, int32, int64 四种数据类型可以使用字符串 'i1', 'i2','i4','i8' 代替

```python
# 结构化数据类型
import numpy as np
student = np.dtype([('name','S20'), ('age', 'i1'), ('marks', 'f4')]) 
print(student)
>>> [('name', 'S20'), ('age', 'i1'), ('marks', '<f4')]
a = np.array([('abc', 21, 50),('xyz', 18, 75)], dtype = student) 
print(a)
>>> [('abc', 21, 50.0), ('xyz', 18, 75.0)]
```

### 数组属性

秩可以理解为索引一个多维数组中某个具体数所需要最少的坐标数量。

维度是指各维上具体的元素数量，维度不等于维。（维指的是某个方向，维度指的是某个方向上的元素数）。维的数量等于秩。

![](https://im.yanshu.work/article/20190915150207640_1747.png)

如图所示，它有两个方向，也就是两维，横向有两个元素，维度是2

* 0维，又称0维张量，数字，标量：1    # 不需要索引

* 1维，又称1维张量，数组，vector：[1, 2, 3]     # 需要一个坐标索引，有一个维（直线）

* 2维，又称2维张量，矩阵，二维数组：[[1,2], [3,4]]   # 需要两个坐标索引，有两个维（矩形）

轴（axis）是多维数组每个维的序号（从大到小）。为了方便理解，我们定义一个三维数组`[[[1,2],[3,4],[5,6]],[[5,6],[7,8],[9,10]]]`

图形化表示即：

![](https://im.yanshu.work/article/20190915151010551_11702.png)

```python
import numpy as np
a = np.array([[[1,2],[3,4],[5,6]],[[7,8],[9,10],[11,12]]])
a.shape
>>> (2,3,2)   
# 从外到里，最大级的矩阵有两个[[1,2],[3,4],[5,6]]和[[7,8],[9,10],[11,12]]
# 每个最大级的矩阵含有三个次一级的矩阵，比如[1,2],[3,4],[5,6]
# 每个次一级的矩阵含有两个元素
# 在图形上表示，即两个面，三行，两列（多维数组最后两个一定先行数再列数）
# 所谓的轴，也就是图形中的三个方向的次序，最大的z方向轴为0，y方向轴为1，x方向轴为2
print(np.sum(a,axis = 0))   # 沿着z方向相加，其结果的shape将会是(3,2)，即去掉第一个维度
>>> [[ 8 10]
    [12 14]
    [16 18]]
print(np.sum(a,axis = 1))
>>> [[ 9 12]                # 沿着y方向相加，其结果的shape将会是(2,2)，即去掉第二个维度
    [27 30]]
print(np.sum(a,axis = 2))   # 沿着x方向相加，其结果的shape将会是(2,3)，即去掉第三个维度
>>> [[ 3  7 11]
    [15 19 23]]

# 简而言之，最大级的矩阵轴为0，次级矩阵轴为1，再次级矩阵轴为2，以此类推
# 一个形状为(2,3,4)的数组，轴0上有2个元素，轴1上有3个元素……
# 实际中，按照axis而分别对不同等级的矩阵对应计算
```

|       属性       |                   说明                    |
| ---------------- | ----------------------------------------- |
| ndarray.ndim     | 秩，即维的数量                             |
| ndarray.shape    | 数组的维度，对于矩阵，n 行 m 列             |
| ndarray.size     | 数组元素的总个数，相当于 .shape 中 n*m 的值 |
| ndarray.dtype    | ndarray 对象的元素类型                     |
| ndarray.itemsize | ndarray 对象中每个元素的大小，以字节为单位  |
| ndarray.flags    | ndarray 对象的内存信息                     |
| ndarray.real     | ndarray元素的实部                         |
| ndarray.imag     | ndarray 元素的虚部                        |

### 创建数组

#### 基础方法

**array**

```python
numpy.array(object[, dtype = None, copy = True, order = None, subok = False, ndmin = 0])
```

|  名称  |                         描述                          |
| ------ | ----------------------------------------------------- |
| object | 数组或嵌套的数列                                       |
| dtype  | 数组元素的数据类型，可选                                |
| copy   | 对象是否需要复制，可选                                  |
| order  | 创建数组的样式，C为行方向，F为列方向，A为任意方向（默认） |
| subok  | 默认返回一个与基类类型一致的数组                        |
| ndmin  | 指定生成数组的最小维度                                  |

```python
import numpy as np 
a = np.array([[1,  2],  [3,  4]])   # 生成一个二维数组
print(a)
>>> [[1, 2] 
    [3, 4]]

a = np.array([1,  2,  3,4,5], ndmin =  2)   # 最小维度是2
print (a)
>>> [[1, 2, 3, 4, 5]]
```

**numpy.empty**：生成指定形状的随机数组

```python
numpy.empty(shape[, dtype = float, order = 'C'])
# shape，数组形状；dtype，数据类型，默认浮点数；
# order；有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序。
# 这种方法生成的数组中的数据都是随机的，多大多小都有可能
```

**numpy.zeros**：生成指定形状的0填充数组

```python
numpy.zeros(shape[, dtype = float, order = 'C'])
# 自定义类型
z = np.zeros((2,2), dtype = [('x', 'i4'), ('y', 'i4'),('z','float')])  
print(z)
>>> [[(0, 0, 0.) (0, 0, 0.)]
    [(0, 0, 0.) (0, 0, 0.)]]  # 参见结构化数据类型
```

**numpy.ones**：创建指定形状的数组，数组元素以 1 来填充

```python
numpy.ones(shape, dtype = None, order = 'C')
# 自定义类型
x = np.ones([2,2], dtype = int)
print(x)
>>> [[1 1]
    [1 1]]
```

#### 转换方法

**numpy.asarray**：将列表转为数组

```python
numpy.asarray(a, dtype = None, order = None)
# a可以是列表, 列表的元组, 元组, 元组的元组, 元组的列表，多维数组
```

**numpy.frombuffer**：将字符串转化为数组

```python
numpy.frombuffer(buffer, dtype = float, count = -1, offset = 0)
# 这个函数我也不懂是干啥的，好像buffer只能传入字符串，而且Python3 默认 str 是 Unicode 类型，所以要转成 bytestring，在原 str 前加上 b
# 另外，dtype = 'S1'这个条件必须加上
# count	读取的数据数量，默认为-1，读取所有数据。
# offset读取的起始位置，默认为0。
import numpy as np 
 
s =  b'Hello World' 
a = np.frombuffer(s, dtype =  'S1')  
print (a)
>>> [b'H' b'e' b'l' b'l' b'o' b' ' b'W' b'o' b'r' b'l' b'd']
```

**numpy.fromiter**：将iterator转化为数组

```python
numpy.fromiter(iterator, dtype, count=-1)

import numpy as np 
 
# 使用 range 函数创建列表对象  
list=range(5)
it=iter(list)
 
# 使用迭代器创建 ndarray 
x=np.fromiter(it, dtype=float)
print(x)
>>> [0. 1. 2. 3. 4.]
```

#### 范围创建

**numpy.arange**：生成一个range型数组

```python
numpy.arange(start, stop, step, dtype)

import numpy as np
x = np.arange(10,20,2)  
print (x)
>>> [10  12  14  16  18]
```

**numpy.linspace**：生成一个一维等差数列数组

```python
np.linspace(start, stop[, num=50, endpoint=True, retstep=False, dtype=None])
# num	要生成的等步长的样本数量，默认为50
# endpoint	该值为 ture 时，数列中中包含stop值，反之不包含，默认是True。
# retstep	如果为 True 时，生成的数组中会显示间距（即换行），反之不显示。

import numpy as np
a = np.linspace(1,10,10)
print(a)
>>> [ 1.  2.  3.  4.  5.  6.  7.  8.  9. 10.]
```

**numpy.logspace**：生成一个一维等比数列数组

```python
np.logspace(start, stop, num=50, endpoint=True, base=10.0, dtype=None)
# base	对数 log 的底数。
import numpy as np
a = np.logspace(0,9,10,base=2)
print (a)
>>> [  1.   2.   4.   8.  16.  32.  64. 128. 256. 512.]
```

### 数组操作

#### 修改数组形状

**reshape**

```python
import numpy as np 
 
a = np.array([[1,2,3],[4,5,6]]) 
a.shape =  (3,2)        # 原地修改  
print (a)
b = a.reshape(2,3)      # 新建修改
print (b)

numpy.reshape(arr, newshape, order='C')
# newshape：整数或者整数数组，新的形状应当兼容原有形状
# order：'C' -- 按行，'F' -- 按列，'A' -- 原顺序，'k' -- 元素在内存中的出现顺序。
```

**numpy.ndarray.flatten**和**numpy.ravel**：数组展开成一维数组，新建修改

```python
ndarray.flatten(order='C')
numpy.ravel(a, order='C')  # 也可写成a.ravel()
# order：'C' -- 按行，'F' -- 按列，'A' -- 原顺序，'K' -- 元素在内存中的出现顺序。

a = np.arange(8).reshape(2,4)
print (a.flatten())
>>> [0 1 2 3 4 5 6 7]
print (a.flatten(order = 'F'))
>>> [0 4 1 5 2 6 3 7]
print (a.ravel())
>>> [0 1 2 3 4 5 6 7]
```

#### 翻转数组

**数组转置**

```python
numpy.transpose(arr[, axes]) = numpy.ndarray.T
# arr：要操作的数组
# axes：整数列表，对应维度，通常所有维度都会对换。
```

**numpy.rollaxis**（）

```python
numpy.rollaxis(arr, axis[,start = 0])
# axis参数表示移动哪个轴
# start参数表示将这个轴移到那个轴前面，默认是最前面，也就是0轴之前
a = np.ones((1,2,3,4))   # 创建一个形状为(1,2,3,4)的4维数组
np.rollaxis(a, 1).shape
>>> (2, 1, 3, 4)   # 将1轴移动到最前面
np.rollaxis(a, 1,3).shape
>>> (1, 3, 2, 4)   # 将轴1移到轴3前面
```

**numpy.moveaxis**

貌似`numpy.rollaxis`过时了，现在一般都用`numpy.moveaxis`

```python
numpy.moveaxis(arr, source, destination)
# source表示原始轴，destination表示原始轴的目标位置
a = np.ones((1,2,3,4))
np.moveaxis(a,1,2).shape
>>> (1, 3, 2, 4)
np.moveaxis(a,1,-1).shape
>>> (1, 3, 4, 2)
```

**numpy.swapaxes（a，axis1，axis2 ）**

交换原始轴和目标轴的位置

```python
a = np.ones((1,2,3,4))
np.swapaxes(a,0,3).shape
>>> (4, 2, 3, 1)
```

#### 修改数组维度

* 广播机制

* numpy.expand_dims 函数通过在指定位置插入新的轴来扩展数组形状

```python
import numpy as np
 
x = np.array(([1,2],[3,4]))

# 在位置0插入轴
y = np.expand_dims(x, axis = 0)
print (y)
>>> [[[1 2]
    [3 4]]]
print (x.shape, y.shape)
>>> (2, 2) (1, 2, 2)
# 在位置 1 插入轴
y = np.expand_dims(x, axis = 1)
print (y)
>>> [[[1 2]]
    [[3 4]]]
print (x.shape, y.shape)
>>> (2, 2) (2, 1, 2)
```

* numpy.squeeze 函数从给定数组的形状中删除一个轴

```python
numpy.squeeze(arr[, axis=0])
```

#### 连接数组

* numpy.concatenate 函数用于沿指定轴连接相同形状的两个或多个数组

```python
numpy.concatenate((a1, a2, ...)[, axis = 0])
import numpy as np
 
a = np.array([[1,2],[3,4]])
b = np.array([[5,6],[7,8]])
# 两个数组的维度相同

print (np.concatenate((a,b)))
>>> [[1 2]
    [3 4]
    [5 6]
    [7 8]]

print (np.concatenate((a,b),axis = 1))
>>> [[1 2 5 6]
    [3 4 7 8]]
```

* numpy.stack 函数用于沿新轴连接数组序列

其方法是，首先加一层括号，然后将轴所对应的层级合并起来，比如`[[1,2],[3,4]]和[[5,6],[7,8]]`，加个括号就是`[[[1,2],[3,4]],[[5,6],[7,8]]]`

如果axis=0，`[[1,2],[3,4]]`和`[[5,6],[7,8]]`是同一级别的，该数组不用动

如果axis=1，其等级是`[1,2],[3,4],[5,6],[7,8]`这种，前两个下标分别是00和01，后两个下标是10和11，只看第二级别，0和0对应，1和1对应，那么最终数组为`[[[1,2],[5,6]],[[3,4],[7,8]]]`

如果axis=2，其等级是1,2,3,4,5,6,7,8这种，下标分别是000、001、010、011、100、101、110、111，只看后两个级别，00和00对应，01和01对应，依此类推就是`[[[1,5],[2,6]],[[3,7],[4,8]]]`

```python
numpy.stack(arrays, axis)

a = np.array([[1,2],[3,4]])
b = np.array([[5,6],[7,8]])
print (np.stack((a,b),0))
print (np.stack((a,b),1))
print (np.stack((a,b),2))
```

* numpy.hstack(a1,a2…) 是 numpy.stack 函数的变体，它通过水平堆叠来生成数组。相当于`np.concatenate((a,b))`

* numpy.vstack 是 numpy.stack 函数的变体，它通过垂直堆叠来生成数组。相当于`np.concatenate((a,b),axis = 1)`

如果想横向合并不同形状的数组，可以`np.column_stack((x_array,y_array))`

#### 分割数组

**numpy.split**

```python
numpy.split(ary, indices_or_sections[, axis=0])
# indices_or_sections：如果是一个整数，就用该数平均切分，如果是一个数组，为沿轴切分的位置（左开右闭）
# axis：沿着哪个维度进行切向，默认为0，横向切分。为1时，纵向切分
import numpy as np
 
a = np.arange(9)

b = np.split(a,3)
print (b)
>>> [array([0, 1, 2]), array([3, 4, 5]), array([6, 7, 8])]
b = np.split(a,[4,7])
print (b)
>>> [array([0, 1, 2, 3]), array([4, 5, 6]), array([7, 8])]
```

**numpy.hsplit 函数用于水平分割数组，通过指定要返回的相同形状的数组数量来拆分原数组**

```python
import numpy as np
 
harr = np.floor(10 * np.random.random((2, 6)))
print(harr)
 
print ('拆分后：')
print(np.hsplit(harr, 3))

'''
原array：
[[4. 7. 6. 3. 2. 6.]
 [6. 3. 6. 7. 9. 7.]]
拆分后：
[array([[4., 7.],
       [6., 3.]]), array([[6., 3.],
       [6., 7.]]), array([[2., 6.],
       [9., 7.]])]
'''       
```

**numpy.vsplit 沿着垂直轴分割，其分割方式与hsplit用法相同。**

```python
import numpy as np
 
a = np.arange(16).reshape(4,4)
print (a)

b = np.vsplit(a,2)
print (b)

'''
第一个数组：
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]
 [12 13 14 15]]
竖直分割：
[array([[0, 1, 2, 3],
       [4, 5, 6, 7]]), array([[ 8,  9, 10, 11],
       [12, 13, 14, 15]])]
'''
```

#### 数组元素的添加与删除

**numpy.resize** 函数返回指定大小的新数组。

```python
numpy.resize(arr, shape)
# 如果新数组大小大于原始大小，则包含原始数组中的元素的副本。

import numpy as np
a = np.array([[1,2,3],[4,5,6]])
b = np.resize(a, (3,2))
print (b)
>>> [[1 2]
    [3 4]
    [5 6]]

b = np.resize(a,(3,3))
# 要注意 a 的第一行在 b 中重复出现，因为尺寸变大了
print (b)
>>> [[1 2 3]
    [4 5 6]
    [1 2 3]]
```

**numpy.append** 函数在数组的末尾添加值。 

追加操作会分配整个数组，并把原来的数组复制到新数组中。 此外，输入数组的维度必须匹配否则将生成ValueError。

```python
numpy.append(arr, values, axis=None)
# values：要向arr添加的值，需要和arr形状相同（除了要添加的轴）
# axis：默认为 None。当axis无定义时，是横向加成，返回总是为一维数组！
# 当axis为0时，数组列数必须相等，纵向合并
# 当axis为1时，数组行数必须相等，横向合并。

import numpy as np
 
a = np.array([[1,2,3],[4,5,6]])
print (np.append(a, [7,8,9]))
>>> [1 2 3 4 5 6 7 8 9]
print (np.append(a, [[7,8,9]],axis = 0))
>>> [[1 2 3]
    [4 5 6]
    [7 8 9]]
print (np.append(a, [[5,5,5],[7,8,9]],axis = 1))
>>> [[1 2 3 5 5 5]
    [4 5 6 7 8 9]]
```

**numpy.insert** 函数在给定索引之前，沿给定轴在输入数组中插入值。

```python
numpy.insert(arr, obj, values, axis)
# obj：在其之前插入值的索引
# values：要插入的值
# axis：沿着它插入的轴，如果未提供，则输入数组会被展开
import numpy as np
 
a = np.array([[1,2],[3,4],[5,6]])
print (np.insert(a,3,[11,12]))
>>> [ 1  2  3 11 12  4  5  6]
print (np.insert(a,1,[11],axis = 0))  # 添加一行
>>> [[ 1  2]
    [11 11]
    [ 3  4]
    [ 5  6]]
print (np.insert(a,1,11,axis = 1))     # 添加一列
>>> [[ 1 11  2]
    [ 3 11  4]
    [ 5 11  6]]
```

**numpy.delete**返回从输入数组中删除指定子数组的新数组。 与 insert() 函数的情况一样，如果未提供轴参数，则输入数组将展开。

```python
Numpy.delete(arr, obj, axis)

a = np.array([1,2,3,4,5,6,7,8,9,10])
print (np.delete(a, np.s_[::2]))    # 包含从数组中删除的替代值的切片
>>> [ 2  4  6  8 10]
```

**numpy.unique** 函数用于去除数组中的重复元素。

```python
numpy.unique(arr[, return_index, return_inverse, return_counts])
# arr：输入数组，如果不是一维数组则会展开
# return_index：如果为true，返回新列表元素在旧列表中的位置（下标），并以列表形式储
# return_inverse：如果为true，返回旧列表元素在新列表中的位置（下标），并以列表形式储
# return_counts：如果为true，返回去重数组中的元素在原数组中的出现次数
import numpy as np
 
a = np.array([5,2,6,2,7,5,6,8,2,9])

u = np.unique(a)
print (u)
>>> [2 5 6 7 8 9]
u,indices = np.unique(a, return_index = True)
print (indices)
>>> [1 0 2 4 7 9]
u,indices = np.unique(a,return_inverse = True)
print (u)
>>> [2 5 6 7 8 9]
print (indices)
>>> [1 0 2 0 3 1 2 4 0 5]
print (u[indices])    # 使用下标重构原数组
>>> [5 2 6 2 7 5 6 8 2 9]
u,indices = np.unique(a,return_counts = True)
print (indices)
>>> [3 2 2 1 1 1]
```

### 切片和索引

#### 切片

两种方式，slice与[:]

```python
import numpy as np
 
a = np.arange(10)
s = slice(2,7,2)  # 从索引 2 开始到索引 7 停止，间隔为2
print(a[s])
b = a[2:7:2]  # b = a[s] = [2  4  6]

# 多维数组也可以切割
a = np.array([[1,2,3],[3,4,5],[4,5,6]])
print(a[1:])
>>> [[3 4 5]
    [4 5 6]]

# 使用,分隔维度
print(a[0:2,1:3])  # 0:2表示第1-2行，1:3表示2-3列，相交的部分即：
>>> [[2 3]
    [4 5]]

print (1:3,[1,2])  # 选择后两行，并在其中挑选第二、第三个元素

# 切片还可以包括省略号 …，它表示的是选择某维，举例说明比较清晰
a = np.array([[1,2,3],[3,4,5],[4,5,6]])  
print (a[...,1])   
# …在第一个位置，代表行，选择数组的每一行，1指的是选择每一行的第二个元素，也即第二列
print (a[2,...])   
# …在第二个位置，代表列，选择数组每一列，2指的是选择每一列的第三个元素，也就是第三行
print (a[...,1:])  # 选择每一行的第二、三个元素
>>> [[2 3]
    [4 5]
    [5 6]]
```

#### 索引

* 整数数组索引

```python
import numpy as np 
 
x = np.array([[1,  2],  [3,  4],  [5,  6]]) 
y = x[[0,1,2],  [0,1,0]]   # 获取数组中(0,0)，(1,1)和(2,0)位置处的元素
print (y)
>>> [1  4  5]

x = np.array([[  0,  1,  2],[  3,  4,  5],[  6,  7,  8],[  9,  10,  11]])  
# 获取四个角上的数组，其行索引是[0,0] 和 [3,3]，而列索引是 [0,2] 和 [0,2]。
rows = np.array([[0,0],[3,3]]) 
cols = np.array([[0,2],[0,2]]) 
y = x[rows,cols]  
# 当然，你也可以写成y = x[[[0,0],[3,3]],[[0,2],[0,2]]]
```

* 布尔索引

```python
import numpy as np 
 
x = np.array([[  0,  1,  2],[  3,  4,  5],[  6,  7,  8],[  9,  10,  11]])  
print (x[x >  5])
>>> [ 6  7  8  9 10 11]
a = np.array([np.nan,  1,2,np.nan,3,4,5])  
print (a[~np.isnan(a)])
>>> [ 1.   2.   3.   4.   5.]
```

* 花式索引

```python
# 使用一维整型数组作为索引，如果目标是一维数组，那么索引的结果就是对应位置的元素；如果目标是二维数组，那么就是对应下标的行。
# 花式索引跟切片不一样，它总是将数据复制到新数组中。
import numpy as np 
 
x=np.arange(32).reshape((8,4))
print (x[[4,2,1,7]])  # 分别选择第5行，第3行，第2行，第8行
print (x[[-4,-2,-1,-7]])  # 倒序

# 传入多个索引数组（要使用np.ix_）
print (x[np.ix_([1,5,7,2],[0,3,1,2])])  # 先选择第2、6、8、3行，接着在每行中分别打印第1、4、2、3个数据
```

### 广播机制

所谓广播机制，即当两个数组shape不一样时，自动将其扩展为shape一样的数组

注意，目前我只发现了`n*1`与`1*n`，`m*n`与`1*n`这两对数组能这样用

```python
# 如果a.shape == b.shape，那么a*b即ab对应位值相乘
import numpy as np 
 
a = np.array([1,2,3,4]) 
b = np.array([10,20,30,40]) 
c = a * b 
print (c)
>>> [ 10  40  90 160]

# 如果a.shape != b.shape，如：
a = np.array([[ 0, 0, 0],
           [10,10,10],
           [20,20,20],
           [30,30,30]])
b = np.array([1,2,3])
print(a + b)
>>> [[ 1  2  3]
    [11 12 13]
    [21 22 23]
    [31 32 33]]
```

可以这样理解：

![](https://im.yanshu.work/article/20190915185314901_3830.png)

以及

![](https://im.yanshu.work/article/20190916102419512_21806.png)

**numpy.broadcast**：产生模仿广播的形状，输入两个数组作为参数，返回一个广播后相应位置配对成元组的数组返，它是iterator


有两个属性：`index`指目前迭代的位置，`iters`则返回广播后数组的元素

```python
import numpy as np

x = np.array([[1], [2], [3]])
y = np.array([4, 5, 6])
b = np.broadcast(x, y)
print(b.index)         
>>> 0
print(next(b), next(b), next(b), next(b))
>>> (1, 4) (1, 5) (1, 6) (2, 4)
print(b.index)
>>> 4

row, col = b.iters
print(next(row), next(col))
>>> 2 5
print(next(col))
>>> 6
```

**numpy.broadcast_to**： 函数将数组广播到新形状。

```python
numpy.broadcast_to(array, shape[, subok])

import numpy as np
 
a = np.arange(4).reshape(1,4)
print ('调用 broadcast_to 函数之后：')
>>> [[0 1 2 3]
    [0 1 2 3]
    [0 1 2 3]
    [0 1 2 3]]
```

### 迭代数组

`numpy.nditer(a[,order='C',op_flags=['read-only']])`

```python
import numpy as np
 
a = np.arange(6).reshape(2,3)
for x in np.nditer(a):
    print (x, end=", " )
>>> 0, 1, 2, 3, 4, 5, 
```

`order='F'`:即是列序优先；一列一列读

`op_flags=['readwrite']`和`op_flags=['write-only']`分别是读写模式和只写模式

```python
import numpy as np
 
a = np.arange(0,60,5) 
a = a.reshape(3,4)  
for x in np.nditer(a, op_flags=['readwrite']): 
    x[...]=2*x           # 好像必须要写成x[…]，也不知道为什么

b = np.array([1,  2,  3,  4], dtype =  int) 
for x,y in np.nditer([a,b]):  
    print ("%d:%d"  %  (x,y), end=", " )  # 可以与广播结合起来进行迭代
```

**numpy.ndarray.flat**：数组元素迭代器

```python
for element in a.flat:
    print (element)
```

### 函数

#### 字符串函数

* numpy.char.add(arr1,arr2) 函数依次对**两个数组**的元素进行字符串连接。

```python
print (np.char.add(['hello'],[' xyz']))
>>> ['hello xyz']
print (np.char.add(['hello', 'hi'],[' abc', ' xyz']))
>>> ['hello abc' 'hi xyz']
```

* numpy.char.multiply() 函数对**一个数组**或字符串执行多重连接。

```python
print (np.char.multiply('Runoob ',3))
>>> Runoob Runoob Runoob
print (np.char.multiply(['Runoob ','yes'],3))
>>> ['Runoob Runoob Runoob ' 'yesyesyes']
```

* numpy.char.center() 函数用于将一个数组或字符串居中，并使用指定字符在左侧和右侧进行填充。

```python
# np.char.center(str , width,fillchar) ：
# str: 字符串，width: 长度，fillchar: 填充字符
print (np.char.center('Runoob', 20,fillchar = '*'))
```

* numpy.char.capitalize(str) 函数将字符串的第一个字母转换为大写

* numpy.char.title(str) 函数将字符串的每个单词的第一个字母转换为大写

* numpy.char.lower(str) 函数对数组的每个元素转换为小写。

* numpy.char.upper() 函数对数组的每个元素转换为大写。

* numpy.char.split(str[,sep=" "]) 通过指定分隔符对字符串进行分割，并**返回数组**。默认情况下，分隔符为空格。

* numpy.char.splitlines(str) 函数以换行符作为分隔符来分割字符串，并返回数组。

* numpy.char.strip(str,char) 函数用于移除开头或结尾处的特定字符。char指的是特定字符

* numpy.char.join() 函数通过指定分隔符来连接数组中的元素或字符串

```python
print (np.char.join([':','-'],['runoob','google']))
>>> ['r:u:n:o:o:b' 'g-o-o-g-l-e']
```

* numpy.char.replace(str,old,new) 函数使用新字符串替换字符串中的所有子字符串。

* numpy.char.encode(str[,encode]) 函数对数组中的每个元素调用 str.encode 函数。 默认编码是 utf-8，可以使用标准 Python 库中的编解码器。

* numpy.char.decode(str[,decode]) 函数对编码的元素进行 str.decode() 解码。

#### 数学函数

* 基础运算：`add(a,b)，subtract()，multiply() 和 divide()`，需要注意的是数组必须具有相同的形状或符合数组广播规则。

* 倒数：`numpy.reciprocal()` 函数返回参数逐元素的倒数。如 1/4 倒数为 4/1。

* 幂：`numpy.power(a1,a2) `函数将第一个输入数组中的元素作为底数，计算它与第二个输入数组（可以是一个数，即第一个数组相同的幂）中相应元素的幂。

* 余数：`numpy.mod(a1,a2)` 计算输入数组中相应元素的相除后的余数。 函数 numpy.remainder() 也产生相同的结果。

* 三角函数

```python
a = np.array([0,30,45,60,90])
print (np.sin(a*np.pi/180))
>>> [0.         0.5        0.70710678 0.8660254  1.        ]
```

还有arcsin，arccos，和 arctan，以及numpy.degrees() 函数将弧度转换为角度。

* 舍入函数：

    * 四舍五入：`numpy.around(a,decimals)`，decimals: 舍入的小数位数。 默认值为0。 如果为负，整数将四舍五入到小数点左侧的位置

    * 下舍入整数（即取比原数小的最大整数）：`numpy.floor(a)`

    * 上舍入整数（即取比原数大的最小整数）：`numpy.ceil(a)`

#### 统计函数

* 最值：`numpy.amin(arr[,axis]) `和` numpy.amax(arr[,axis])`分别返回沿指定轴的最小值和最大值，不输入axis的话寻找整个数组的最值

* `numpy.ptp(arr[,axis])`函数计算数组中沿指定轴元素最大值与最小值的差，不输入axis的话在整个数组做运算

* `numpy.percentile(a, q[, axis,keepdims=TFalse])`返回数组的百分位，q 是要计算的百分位数，在 0 ~ 100 之间；axis是沿着它计算百分位数的轴，不填则在整个数组中寻找。keepdims是否保持维度不变

> 如果有70%的数小于a，那么a的百分位是70，如果处于中间的恰好有两个数，那么百分位为50时等于这两个数的平均数。

* `numpy.median(a[,axis]) `函数用于计算数组 a 中元素的中位数（中值）

* `numpy.mean(a[,axis])` 函数返回数组中元素的算术平均值。

* `numpy.average(a1,weights = a2[,axis,returned =  False])` 函数根据在另一个数组中给出的各自的权重计算数组中元素的加权平均值。该函数可以接受一个轴参数。 如果没有指定轴，则数组会被展开。如果 returned 参数设为 true，则同时返回权重的和

* `numpy.std()`标准差

* `numpy.var()`方差

### 排序和筛选

|           种类           | 速度 |    最坏情况    | 工作空间 | 稳定性 |
| ------------------------ | --- | ------------- | ------- | ------ |
| `'quicksort'`（快速排序） | 1    | `O(n^2)`      | 0       | 否     |
| `'mergesort'`（归并排序） | 2    | `O(n*log(n))` | ~n/2    | 是     |
| `'heapsort'`（堆排序）    | 3    | `O(n*log(n))` | 0       | 否     |


**numpy.sort() 函数**返回输入数组的排序副本。函数格式如下：

> numpy.sort(a, axis, kind, order)

kind: 默认为'quicksort'（快速排序），order: 如果数组包含字段，则是要排序的字段

```python
import numpy as np  
 
a = np.array([[3,7],[9,1]])  
print (np.sort(a))
print (np.sort(a, axis =  0))  # 按列排序
>>> [[3 1]
    [9 7]]
# 在 sort 函数中排序字段 
dt = np.dtype([('name',  'S10'),('age',  int)]) 
a = np.array([("raju",21),("anil",25),("ravi",  17),  ("amar",27)], dtype = dt)  
print (np.sort(a, order =  'name'))   # 按name排序
```

**numpy.argsort() 函数**返回的是数组值从小到大的索引值。

```python
import numpy as np 
 
x = np.array([3,  1,  2])  
y = np.argsort(x)  
print (y)
>>> [1 2 0]
print (x[y])  # 以排序后的顺序重构原数组
for i in y:  
    print (x[i], end=" ")   # 使用循环重构原数组
```

**numpy.lexsort() **用于对多个序列进行排序，并返回最后一个序列的从小到大的序号。把它想象成对电子表格进行排序，每一列代表一个序列，排序时优先照顾靠后的列。

> 这里举一个应用场景：小升初考试，重点班录取学生按照总成绩录取。在总成绩相同时，数学成绩高的优先录取，在总成绩和数学成绩都相同时，按照英语成绩录取…… 这里，总成绩排在电子表格的最后一列，数学成绩在倒数第二列，英语成绩在倒数第三列。

```python
import numpy as np 
 
nm =  ('raju','anil','ravi','amar') 
dv =  ('f.y.',  's.y.',  's.y.',  'f.y.') 
ind = np.lexsort((dv,nm))  
print (ind)
>>> [3 1 0 2]
print ([nm[i]  +  ", "  + dv[i]  for i in ind])  # 使用这个索引来获取排序后的数据
>>> ['amar, f.y.', 'anil, s.y.', 'raju, f.y.', 'ravi, s.y.']
```

|                    函数                     |                        描述                         |
| ------------------------------------------- | --------------------------------------------------- |
| msort(a)                                    | 数组按第一个轴排序，返回排序后的数组副本。np.msort(a) 相等于 np.sort(a, axis=0)。 |
| sort_complex(a)                             | 对复数按照先实部后虚部的顺序进行排序。                 |
| partition(a, kth\[, axis, kind, order\])    | 指定一个数，对数组进行分区                            |
| argpartition(a, kth\[, axis, kind, order\]) | 可以通过关键字 kind 指定算法沿着指定轴对数组进行分区   |

```python
# partition() 分区排序：
a = np.array([3, 4, 2, 1])
np.partition(a, 3)  # 将数组 a 中所有元素（包括重复元素）从小到大排列，3 表示的是排序数组索引为 3 的数字，比该数字小的排在该数字前面，比该数字大的排在该数字的后面
>>> array([2, 1, 3, 4])
np.partition(a, (1, 3)) # 小于 1 的在前面，大于 3 的在后面，1和3之间的在中间
>>> array([1, 2, 3, 4])

# argpartition()分区排序
# 找到数组的第 3 小（index=2）的值和第 2 大（index=-2）的值
arr = np.array([46, 57, 23, 39, 1, 10, 0, 120])
arr[np.argpartition(arr, 2)[2]]
>>> 10
arr[np.argpartition(arr, -2)[-2]]
>>> 57
# 同时找到第 3 和第 4 小的值。注意这里，用 [2,3] 同时将第 3 和第 4 小的排序好，然后可以分别通过下标 [2] 和 [3] 取得。
arr[np.argpartition(arr, [2,3])[2]]
>>> 10
arr[np.argpartition(arr, [2,3])[3]]
>>> 23
```

**numpy.argmax(arr[,axis]) 和 numpy.argmin()**函数分别沿给定轴返回最大和最小元素的索引。若没有axis则在整个数组中寻找

**numpy.nonzero(arr) **函数返回输入数组中非零元素的索引。

**numpy.where(condition) **函数返回输入数组中满足给定条件的元素的索引。

```python
import numpy as np 
 
x = np.arange(9.).reshape(3,  3)  
y = np.where(x >  3)  
print (y)
>>> (array([1, 1, 2, 2, 2]), array([1, 2, 0, 1, 2]))
print (x[y])  # 使用这些索引来获取满足条件的元素
>>> [4. 5. 6. 7. 8.]
```

**numpy.extract(condition,arr) **函数根据某个条件从数组中抽取元素，返回满条件的元素。

```python
import numpy as np 
 
x = np.arange(9.).reshape(3,  3)  
# 定义条件, 选择偶数元素
condition = np.mod(x,2)  ==  0  
print (condition)
>>> [[ True False  True]
    [False  True False]
    [ True False  True]]
print (np.extract(condition, x))
```

#### 随机函数

和python的`random`函数类似，但是生成的是一个数组

```python
np.random.random(10)  # 生成10个[0,1]区间的随机实数
np.random.normal(0,1,20) # 生成20个服从均值为0，方差为1的正态分布随机数
```

### 矩阵库(Matrix)

NumPy 中包含了一个矩阵库 numpy.matlib，该模块中的函数返回的是一个矩阵，而不是 ndarray 对象。

使用前要先导入`import numpy.matlib `

```python
numpy.matlib.empty(shape[, dtype, order])  # 生成一个指定大小的随机矩阵
# order: C（行序优先） 或者 F（列序优先）

import numpy.matlib 
import numpy as np
print (np.matlib.empty((2,2)))

numpy.matlib.zeros()       # 创建一个以 0 填充的矩阵
numpy.matlib.ones()        # 创建一个以 1 填充的矩阵。
numpy.matlib.eye(n, M,k, dtype)   # 返回一个矩阵，对角线元素为 1，其他位置为零
# n: 返回矩阵的行数，M: 返回矩阵的列数，默认为 n，k: 对角线的索引，不知道啥用
numpy.matlib.identity(n,dtype)    # 返回一个n*n的单位矩阵
numpy.matlib.rand(n,m) 函数创建一个n*m的随机矩阵
```

### 线性代数运算

|     函数      |              描述              |
| ------------- | ------------------------------ |
| `dot`         | 两个数组的点积，即元素对应相乘。 |
| `vdot`        | 两个向量的点积                  |
| `inner`       | 两个数组的内积                  |
| `matmul`      | 两个数组的矩阵积                |
| `determinant` | 数组的行列式                   |
| `solve`       | 求解线性矩阵方程                |
| `inv`         | 计算矩阵的乘法逆矩阵            |

**数组点积**

numpy.dot() 对于两个一维的数组，计算的是这两个数组对应下标元素的乘积和(数学上称之为内积)；对于二维数组，计算的是两个数组的矩阵乘积；对于多维数组，它的通用计算公式如下，即结果数组中的每个元素都是：数组a的最后一维上的所有元素与数组b的倒数第二位上的所有元素的乘积和： `dot(a, b)[i,j,k,m] = sum(a[i,j,:] * b[k,:,m])`。

`numpy.dot(arr1, arr2[, out=None])`，out : ndarray, 可选，用来保存dot()的计算结果

**向量点积**

numpy.vdot() 函数是两个向量的点积。 如果第一个参数是复数，那么它的共轭复数会用于计算。 如果参数是多维数组，它会被展开。

```python
import numpy as np 
 
a = np.array([[1,2],[3,4]]) 
b = np.array([[11,12],[13,14]])
print (np.vdot(a,b))
>>> 130  # 1*11 + 2*12 + 3*13 + 4*14 = 130
```

**向量内积**

numpy.inner() 函数返回一维数组的向量内积。对于更高的维度，它返回最后一个轴上的和的乘积。

```python
print (np.inner(np.array([1,2,3]),np.array([0,1,0])))  
# 等价于 1*0+2*1+3*0

a = np.array([[1,2], [3,4]]) 
b = np.array([[11, 12], [13, 14]]) 
print (np.inner(a,b))

>>> [[35 41]
    [81 95]]
# 1*11+2*12, 1*13+2*14 
# 3*11+4*12, 3*13+4*14
```

**乘积**

numpy.matmul 函数返回两个数组的矩阵乘积。 虽然它返回二维数组的正常乘积，但如果任一参数的维数大于2，则将其视为存在于最后两个索引的矩阵的栈，并进行相应广播。

另一方面，如果任一参数是一维数组，则通过在其维度上附加 1 来将其提升为矩阵（广播），并在乘法之后被去除。

```python
# 二维和一维运算
import numpy.matlib 
import numpy as np 
 
a = [[1,0],[0,1]] 
b = [1,2] 
print (np.matmul(a,b))
print (np.matmul(b,a))
>>> [1  2] 
    [1  2]

# 维度大于二的数组 ：
a = np.arange(8).reshape(2,2,2) 
b = np.arange(4).reshape(2,2) 
print (np.matmul(a,b))
>>> [[[ 2  3]
    [ 6 11]]

    [[10 19]
    [14 27]]]
```

**行列式**

numpy.linalg.det()返回行列式（忘了行列式怎么求的自行百度）

```python
import numpy as np
 
b = np.array([[6,1,1], [4, -2, 5], [2,8,7]]) 
print (b)
print (np.linalg.det(b))  # 6*(-2*7 - 5*8) - 1*(4*7 - 5*2) + 1*(4*8 - -2*2)
```

**线性方程求解**

numpy.linalg.solve(a,b)

$$\left[ \begin{array} { c c c } { 1 } & { 1 } & { 1 } \\ { 0 } & { 2 } & { 5 } \\ { 2 } & { 5 } & { - 1 } \end{array} \right] \left[ \begin{array} { l } { x } \\ { y } \\ { z } \end{array} \right] = \left[ \begin{array} { c } { 6 } \\ { - 4 } \\ { 27 } \end{array} \right]$$

**numpy.linalg.inv() **函数计算矩阵的乘法逆矩阵。

结果也可以使用以下函数获取：x = np.dot(ainv,b)
