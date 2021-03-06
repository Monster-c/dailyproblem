# `numpy`使用小记

## `fromfile()方法`

`fromfile()`函数读回数据时需要用户指定元素类型，并对数组的形状进行适当的修改,此外如果指定了`sep`参数，则`fromfile()`和`tofile()`将以文本格式对数组进行输入输出。`sep`参数指定的是文本数据中数值的分隔符。

```python
fromfile(filename='filename', sep=' ')
#其中sep参数指定的是数据之间的分隔符
```

## `max()`、`min()`、`sum()`方法

依次为求最大，求最小，求和方法

```python
ndarray.max(axis=None)

# axis默认为None，返回ndarray中最大或最小的数，

#axis指定为数字时，返回该纬度对应的最值
#如：
arr1 = np.array([[1, 5, 3], [4, 2, 6]])
print(arr1.shape) # (2,3)
返回结果为(2,3)，是一个二维数组，说明axis只能取0或1

下面分别介绍当ndarray为二维，三维，四维时axis的取值和最终结果

#二维
arr1 = np.array([[1, 5, 3], [4, 2, 6]])
#首先先判断出数组的shape值
print(arr1.shape) # (2,3)

#当axis=0时，min的结果返回(3)
#当axis=1时，min的结果返回(2)
print(np.min(arr1, axis=0).shape,end="axis=0\n\n")
print(np.min(arr1, axis=1),end="axis=1\n\n")

#三维
arr1 = np.array([[[1, 2, 3], [4, 5, 6]], [[2, 3, 4], [3, 65, 1]], [[1, 33, 2], [44, 55, 66]],[[21, 12, 17], [3, 11, 43]]])
print(arr1.shape) #(4,2,3)
#每一数值代表的纬度
print(np.min(arr1, axis=0).shape, end="axis=0\n\n") # (2,3)
print(np.min(arr1, axis=1).shape, end="axis=1\n\n") # (4,3)
print(np.min(arr1, axis=2).shape, end="axis=2\n\n") # (4,2)

总结：当axis=k时，维度为n的(n1,n2,n3,...nn-1,nn)数组，min后的结果维度为(n1,n2,n3,...nk-1,nk+1,...,nn-1,nn)

各维度的值如何比对，取值

#三维
arr1 = np.array([[[1, 2, 3], [4, 5, 6]], [[2, 3, 4], [3, 65, 1]], [[1, 33, 2], [44, 55, 66]],[[21, 12, 17], [3, 11, 43]]])
print(arr1)

[[[ 1 2 3]
[ 4 5 6]]

[[ 2 3 4]
[ 3 65 1]]

[[ 1 33 2]
[44 55 66]]

[[21 12 17]
[ 3 11 43]]]

print(np.min(arr1, axis=0), end="axis=0\n\n") 
先根据上面的推算，写出维度格式
[[x1 x2 x3]
[x4 x5 x6]]
再比对取值：

[x1,x2,x3]从[1 2 3],[2 3 4],[1 33 2],[21 12 17]中取各项中最小值
x1=1,x2=2,x3=2
[x4 x5 x6]从[4 5 6],[3 65 1],[44 55 66],[3 11 43]中取各项中最小值
x4=3,x5=5,x6=1
最后结果为

[[1 2 2]

[3 5 1]]

print(np.min(arr1, axis=1), end="axis=1\n\n") 

写出维度格式

[[x1 x2 x3]

[x4 x5 x6]

[x7 x8 x9]

[x10 x11 x12]]

再比对取值：

[x1,x2,x3]从[1 2 3],[4 5 6]中取各项中最小值

 

x1=1,x2=2,x3=3

[x4,x5,x6]从[2 3 4],[3 65 1]中取各项中最小值

x4=2,x5=3,x6=1

[x7,x8,x9]从[1 33 2],[44 55 66]中取各项中最小值

x7=1,x8=33,x9=2

[x10,x11,x12]从[21 12 17],[3 11 43]中取各项中最小值

x10=3,x11=11,x9=17

最后结果为

[[ 1 2 3]
[ 2 3 1]
[ 1 33 2]
[ 3 11 17]]

print(np.min(arr1, axis=2), end="axis=2\n\n") 

写出维度格式

[[x1 x2]

[x3 x4]

[x5 x6]

[x7 x8]]

再比对取值：

[x1,x2]从[1 2 3],[4 5 6]中取各项中最小值

x1=1,x2=4

[x3,x4]从[2 3 4],[3 65 1]中取各项中最小值

x3=2,x4=1

[x5,x6]从[1 33 2],[44 55 66]中取各项中最小值

x5=1,x5=44

[x7,x8]从[21 12 17],[3 11 43]中取各项中最小值

x7=12,x8=3

最后结果为

[[ 1 4]
[ 2 1]
[ 1 44]
[12 3]]

 

以上就介绍完了，下面再以max函数介绍一个四维数组

# 四维

arr1 = np.array([[[[1, 2, 3], [4, 5, 6]], [[2, 3, 4], [3, 65, 1]], [[1, 33, 2], [44, 55, 66]],[[21, 12, 17], [3, 11, 43]]],[[[1, 2, 3], [4, 5, 6]], [[3, 1, 2], [3, 5, 1]], [[1, 3, 2], [4, 5, 7]],[[3, 5, 6], [7, 2, 8]]]])
print(arr1.shape) #(2,4,2,3)
print(arr1)
print(np.max(arr1, axis=0), end="axis=0\n\n") # (4,2,3)

[[[x1 x2 x3]
[x4 x5 x6]]

[[x7 x8 x9]
[x10 x11 x12]]

[[x13 x14 x15]
[x16 x17 x18]]

[[x19 x20 x21]
[x22 x23 x24]]]

再比对取值：

[[x1 x2 x3]
[x4 x5 x6]]

从

[[ 1 2 3]
[ 4 5 6]]

[[ 1 2 3]
[ 4 5 6]]

中取最大值，因为例子中两组值都是一样的，所以结果就为

[[ 1 2 3]
[ 4 5 6]]

再比对取值：

[[x7 x8 x9]
[x10 x11 x12]]

从

[[ 2 3 4]
[ 3 65 1]]

[[ 3 1 2]
[ 3 5 1]]

中取最大值，结果为

[[3 3 4]

[3 65 1]]

再比对取值：

[[x13 x14 x15]
[x16 x17 x18]]

从

[[ 1 33 2]
[44 55 66]]

[[ 1 3 2]
[ 4 5 7]]

中取最大值，结果为

[[1 33 2]

[44 55 66]]

再比对取值：

[[x19 x20 x21]
[x22 x23 x24]]

从

[[21 12 17]
[ 3 11 43]]

[[ 3 5 6]
[ 7 2 8]]

中取最大值，结果为

[[21 12 17]

[7 11 43]]

最终结果为

[[[ 1 2 3]
[ 4 5 6]]

[[ 3 3 4]
[ 3 65 1]]

[[ 1 33 2]
[44 55 66]]

[[21 12 17]
[ 7 11 43]]]
```



```python
arr = numpy.array([[[1,2,3],
                   [4,5,6]],
                  [[7,8,9],
                   [10,11,12]],
                  [[13,14,15],
                   [16,17,18]],
                  [[19,20,21],[22,23,24]]])

arr.shape # (4,2,3)

arr.min(axis=0)
# Out: array([[1, 2, 3],
#       [4, 5, 6]])

arr.min(axis=1)
#Out：array([[ 1,  2,  3],
#       [ 7,  8,  9],
#      [13, 14, 15],
#       [19, 20, 21]])

arr.min(axis=2)
#Out: array([[ 1,  4],
#       [ 7, 10],
#       [13, 16],
#       [19, 22]])
```

