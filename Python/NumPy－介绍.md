##Python NumPy---快速处理数据
><font color=#009ff>@Author : Gust <br>
>@Date : 2016-07-24 <font>

#######Numpy－－－－简介

&emsp;&emsp;NumPy为Python提供了快速的多维数组处理的能力，而SciPy则在NumPy基础上添加了众多的科学计算所需的各种工具包，有了这两个库，Python就有几乎和Matlab一样的处理数据和计算的能力了。

NumPy和SciPy官方网址： [http://www.scipy.org](http://www.scipy.org)

&emsp;&emsp;NumPy为Python带来了真正的多维数组功能，并且提供了丰富的函数库处理这些数组。它将常用的数学函数都进行数组化，使得这些数学函数能够直接对数组进行操作，将本来需要在Python级别进行的循环，放到C语言的运算中，明显地提高了程序的运算速度。

SciPy的核心计算部分都是一些久经考验的Fortran数值计算库，例如：

	*线性代数使用LAPACK库
	*快速傅立叶变换使用FFTPACK库
	*常微分方程求解使用ODEPACK库
	*非线性方程组求解以及最小值求解等使用MINPACK库
	

######1.&emsp;ndarray 对象


>导入```ndarray```对象

```python
	import numpy as np
```

>创建&&基本操作

&emsp;&emsp;首先需要创建数组才能进行操作。
&emsp;&emsp;通过将 array 传递给 Python 对象创建数组（可以是多维数组）

```python
	>>> a = np.array([1, 2, 3, 4])
	>>> b = np.array((5, 6, 7, 8))
	>>> c = np.array([[1, 2, 3, 4],[4, 5, 6, 7], [7, 8, 9, 10]])
	>>> b
	array([5, 6, 7, 8])
	>>> c
	array([[1, 2, 3, 4],
	       [4, 5, 6, 7],
	       [7, 8, 9, 10]])
	>>> c.dtype
	dtype('int32')
``` 

&emsp;&emsp;shape 属性获取数组大小并可以通过修改值从而改变数组大小

```python
	>>> a.shape
	(4,)
	>>> c.shape
	(3, 4)
	
	>>> c.shape = 4,3
	>>> c
	array([[ 1,  2,  3],
	       [ 4,  4,  5],
	       [ 6,  7,  7],
	       [ 8,  9, 10]])
```

&emsp;&emsp;当某一轴的元素为 －1 时，会自动计算数组大小

```python
	>> c.shape = 2,-1
	>>> c
	array([[ 1,  2,  3,  4,  4,  5],
	       [ 6,  7,  7,  8,  9, 10]])
```


&emsp;&emsp;reshape 方法利用原数组，创建一个新的数组，原数组的大小不变

```python
	>>> d = a.reshape((2,2))
	>>> d
	array([[1, 2],
	       [3, 4]])
	>>> a
	array([1, 2, 3, 4])
```

&emsp;&emsp;dtype 属性－设置或获得元素类型

```python
	>>> np.array([[1, 2, 3, 4],[4, 5, 6, 7], [7, 8, 9, 10]], dtype=np.float)
	array([[  1.,   2.,   3.,   4.],
	       [  4.,   5.,   6.,   7.],
	       [  7.,   8.,   9.,  10.]])
	>>> np.array([[1, 2, 3, 4],[4, 5, 6, 7], [7, 8, 9, 10]], dtype=np.complex)
	array([[  1.+0.j,   2.+0.j,   3.+0.j,   4.+0.j],
	       [  4.+0.j,   5.+0.j,   6.+0.j,   7.+0.j],
	       [  7.+0.j,   8.+0.j,   9.+0.j,  10.+0.j]])
```

&emsp;&emsp;size 元素数，ndim 维数,

```python
	>>> print a.size   #数组的元素数
	8
	>>> print a.ndim   #数组的维数
	3
```

&emsp;&emsp;构造特殊矩阵

```python
	>>> print np.zeros((3,4))
	[[ 0.  0.  0.  0.]
	 [ 0.  0.  0.  0.]
	 [ 0.  0.  0.  0.]]
	>>> print np.ones((3,4))
	[[ 1.  1.  1.  1.]
	 [ 1.  1.  1.  1.]
	 [ 1.  1.  1.  1.]]
	>>> print np.eye(3)
	[[ 1.  0.  0.]
	 [ 0.  1.  0.]
	 [ 0.  0.  1.]]
```

&emsp;&emsp;使用 numpy.arange 方法

```python
	>>> print np.arange(15)
	[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14]
	>>> print type(np.arange(15))
	<type 'numpy.ndarray'>
	>>> print np.arange(15).reshape(3,5)
	[[ 0  1  2  3  4]
	 [ 5  6  7  8  9]
	 [10 11 12 13 14]]
	>>> print type(np.arange(15).reshape(3,5))
	<type 'numpy.ndarray'>
```

&emsp;&emsp;使用 numpy.linspace 方法

```python
	>>> print np.linspace(1,3,9)
	[ 1.   	1.25  1.5   1.75  2.    2.25  2.5   2.75  3.  ]
```


&emsp;&emsp;数组索引，切片，赋值

```python
	>>> a = np.array( [[2,3,4],[5,6,7]] )
	>>> print a
	[[2 3 4]
	 [5 6 7]]
	>>> print a[1,2]
	7
	>>> print a[1,:]
	[5 6 7]
	>>> print a[1,1:2]
	[6]
	>>> a[1,:] = [8,9,10]
	>>> print a
	[[ 2  3  4]
	 [ 8  9 10]]
```


&emsp;&emsp;数组的加减乘除

```python
	>>> print a > 2
	[[False False]
	 [False False]]
	>>> print a+b
	[[ 2.  1.]
	 [ 1.  2.]]
	>>> print a-b
	[[ 0.  1.]
	 [ 1.  0.]]
	>>> print b*2
	[[ 2.  0.]
	 [ 0.  2.]]
	>>> print (a*2)*(b*2)
	[[ 4.  0.]
	 [ 0.  4.]]
	>>> print b/(a*2)
	[[ 0.5  0. ]
	 [ 0.   0.5]]
	>>> print (a*2)**4
	[[ 16.  16.]
	 [ 16.  16.]]
```


<br>[关于矩阵的基本操作](http://www.jb51.net/article/49397.htm)

>存取元素

```python

	＃
	>>> a = np.arange(10)
	>>> a[5]    # 用整数作为下标可以获取数组中的某个元素
	5
	>>> a[3:5]  # 用范围作为下标获取数组的一个切片，包括a[3]不包括a[5]
	array([3, 4])
	>>> a[:5]   # 省略开始下标，表示从a[0]开始
	array([0, 1, 2, 3, 4])
	>>> a[:-1]  # 下标可以使用负数，表示从数组后往前数
	array([0, 1, 2, 3, 4, 5, 6, 7, 8])
	>>> a[2:4] = 100,101    # 下标还可以用来修改元素的值
	>>> a
	array([  0,   1, 100, 101,   4,   5,   6,   7,   8,   9])
	>>> a[1:-1:2]   # 范围中的第三个参数表示步长，2表示隔一个元素取一个元素
	array([  1, 101,   5,   7])
	>>> a[::-1] # 省略范围的开始下标和结束下标，步长为-1，整个数组头尾颠倒
	array([  9,   8,   7,   6,   5,   4, 101, 100,   1,   0])
	>>> a[5:1:-2] # 步长为负数时，开始下标必须大于结束下标
	array([  5, 101])
	
	>>> b = a[3:7] # 通过下标范围产生一个新的数组b，b和a共享同一块数据空间
	>>> b
	array([101,   4,   5,   6])
	>>> b[2] = -10 # 将b的第2个元素修改为-10
	>>> b
	array([101,   4, -10,   6])
	>>> a # a的第5个元素也被修改为10
	array([  0,   1, 100, 101,   4, -10,   6,   7,   8,   9])
	
	
	＃使用整数序列
	>>> x = np.arange(10,1,-1)
	>>> x
	array([10,  9,  8,  7,  6,  5,  4,  3,  2])
	>>> x[[3, 3, 1, 8]] # 获取x中的下标为3, 3, 1, 8的4个元素，组成一个新的数组
	array([7, 7, 9, 2])
	>>> b = x[np.array([3,3,-3,8])]  #下标可以是负数
	>>> b[2] = 100
	>>> b
	array([7, 7, 100, 2])
	>>> x   # 由于b和x不共享数据空间，因此x中的值并没有改变
	array([10,  9,  8,  7,  6,  5,  4,  3,  2])
	>>> x[[3,5,1]] = -1, -2, -3 # 整数序列下标也可以用来修改元素的值
	>>> x
	array([10, -3,  8, -1,  6, -2,  4,  3,  2])
	
	
	#布尔数组
	>>> x = np.arange(5,0,-1)
	>>> x
	array([5, 4, 3, 2, 1])
	>>> x[np.array([True, False, True, False, False])]
	>>> # 布尔数组中下标为0，2的元素为True，因此获取x中下标为0,2的元素
	array([5, 3])
	>>> x[[True, False, True, False, False]]
	>>> # 如果是布尔列表，则把True当作1, False当作0，按照整数序列方式获取x中的元素
	array([4, 5, 4, 5, 5])
	>>> x[np.array([True, False, True, True])]
	>>> # 布尔数组的长度不够时，不够的部分都当作False
	array([5, 3, 2])
	>>> x[np.array([True, False, True, True])] = -1, -2, -3
	>>> # 布尔数组下标也可以用来修改元素
	>>> x
	array([-1,  4, -2, -3,  1])
	
	
	>>> x = np.random.rand(10) # 产生一个长度为10，元素值为0-1的随机数的数组
	>>> x
	array([ 0.72223939,  0.921226  ,  0.7770805 ,  0.2055047 ,  0.17567449,
	        0.95799412,  0.12015178,  0.7627083 ,  0.43260184,  0.91379859])
	>>> x>0.5
	>>> # 数组x中的每个元素和0.5进行大小比较，得到一个布尔数组，True表示x中对应的值大于0.5
	array([ True,  True,  True, False, False,  True, False,  True, False,  True], dtype=bool)
	>>> x[x>0.5]
	>>> # 使用x>0.5返回的布尔数组收集x中的元素，因此得到的结果是x中所有大于0.5的元素的数组
	array([ 0.72223939,  0.921226  ,  0.7770805 ,  0.95799412,  0.7627083 ,
	        0.91379859])
```

