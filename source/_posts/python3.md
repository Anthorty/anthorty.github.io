---
title: Python3 IO读写
date: 2017-05-16 00:03:57
tags:
- Python3
description: 'Python3 IO读写'
---
## IO读写（内存读写）
- 内存读写不同于文件读写，内存读取后，内存指针会偏移。

```python
# Example

In [3]: from io import StringIO,BytesIO # 使用前需要先导入模块

In [4]: a = StringIO('Hello,World!')	#创建一个字符串对象

In [5]: a.readline()	#读取内存保存的字符串
Out[5]: 'Hello,World!'

In [6]: a.tell()	#现在的内存地址
Out[6]: 12

In [7]: a.readline()	#返回空字符串，因为内存地址移动了
Out[7]: ''

In [8]: a.seek(0)	#seek函数可以设置内存地址
Out[8]: 0

In [10]: a.readline()		#设置为初始值，可以读出字符串
Out[10]: 'Hello,World!'
```