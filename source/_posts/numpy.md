---
title: numpy
date: 2021-11-02 14:21:39
tags: phython
---

## 라이브러리 불러오기


```python
import numpy as np
print(np.__version__)
```

    1.19.5
    
```python
temp = np.array([1, 2, 3])
print(type(temp))
```

    <class 'numpy.ndarray'>
    

## Numpy 배열 생성 및 둘러보기


```python
data1 = [1,2,3]
data1
```




    [1, 2, 3]




```python
data2= [1,1,2,2,3,4]
data2
```




    [1, 1, 2, 2, 3, 4]




```python
my_array1 = np.array(data1)
print(my_array1) 
print(my_array1.shape)
```

    [1 2 3]
    (3,) -->3개들어있기때문
    


```python
my_array2 = np.array(data2)
print(my_array2) 
print(my_array2.shape)
```

    [1 1 2 2 3 4]
    (6,)
    


```python
my_array3 = np.array([3,6,9,12])
print(my_array3)
print(my_array3.shape)
print(my_array3.dtype)
```

    [ 3  6  9 12]
    (4,)
    int64
    


```python
my_array4 = np.array([[2,4,6],[8,10,12],[14,16,18],[20,22,24]])
my_array4
```




    array([[ 2,  4,  6],
           [ 8, 10, 12],
           [14, 16, 18],
           [20, 22, 24]])




```python
my_array4.shape
```




    (4, 3)--> 4개의배열안에 3개가 들어있음




```python
my_array5 = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
my_array5.shape
```




    (2, 2, 2)


## 기본함수
### arange


```python
arrange_array = np.arange(5)
arrange_array
```




    array([0, 1, 2, 3, 4])




```python
arrange_array2 = np.arange(1, 9, 3)
arrange_array2
```




    array([1, 4, 7])
  - [start,stop,step] step의 크기만큼 일정하게 떨어져있는 숫자를 array형태로 반환
  - 기본값은 start=0 step=1 
  - ### zeroes, ones


```python
zeros_array = np.zeros((3,2))
print(zeros_array)
print("Data Type is:", zeros_array.dtype)
print("Data Shape is:", zeros_array.shape)
```

    [[0. 0.]
     [0. 0.]
     [0. 0.]]
    Data Type is: float64
    Data Shape is: (3, 2)
    


```python
ones_array = np.ones((3,4), dtype='int32')
print(ones_array)
print("Data Type is:", ones_array.dtype)
print("Data Shape is:", ones_array.shape)
```

    [[1 1 1 1]
     [1 1 1 1]
     [1 1 1 1]]
    Data Type is: int32
    Data Shape is: (3, 4)

- zeros:0으로 초기화된 shape차원의 ndarray 배열 객체 반환
- ones :1로 초기화된 shape차원의 ndarray 배열 객체 반환
### reshape



```python
after_reshape = ones_array.reshape(6,2)
print(after_reshape)
print("Data Shape is:", after_reshape.shape)
```

    [[1 1]
     [1 1]
     [1 1]
     [1 1]
     [1 1]
     [1 1]]
    Data Shape is: (6, 2)
    


```python
after_reshape = ones_array.reshape(5,3)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-25-94cac763be50> in <module>()
    ----> 1 after_reshape = ones_array.reshape(5,3)
    

    ValueError: cannot reshape array of size 12 into shape (5,3)



```python
after_reshape = ones_array.reshape(2,3,2)
print(after_reshape)
print("Data Shape is:", after_reshape.shape)
```

    [[[1 1]
      [1 1]
      [1 1]]
    
     [[1 1]
      [1 1]
      [1 1]]]
    Data Shape is: (2, 3, 2)
    


```python
after_reshape2= ones_array.reshape(-1,6)
print("reshape(-1,6)? \n")
print(after_reshape2)
```

    reshape(-1,6)? 
    
    [[1 1 1 1 1 1]
     [1 1 1 1 1 1]]
    


```python
after_reshape3= ones_array.reshape(3,-1)
print("reshape(3, -1)? \n")
print(after_reshape3)
print("Data Shape is:", after_reshape3.shape)
```

    reshape(3, -1)? 
    
    [[1 1 1 1]
     [1 1 1 1]
     [1 1 1 1]]
    Data Shape is: (3, 4)
- 현재의 배열 차원(1차원,2차원,3차원)을 변경하여 행렬 반환

## Numpy 정렬 1차원배열정렬 (x)(-x)
### sort()


```python
height_arr = np.array([174, 165, 180, 182, 168])
sorted_height_arr = np.sort(height_arr)

print('Height Matrix: ', height_arr)
print('np.sort() Matrix: ', sorted_height_arr)
```

    Height Matrix:  [174 165 180 182 168]
    np.sort() Matrix:  [165 168 174 180 182]
    


```python
desc_sorted_height_arr = np.sort(height_arr)[::-1]
print('np.sort()[::-1] : ', desc_sorted_height_arr)
```

    np.sort()[::-1] :  [182 180 174 168 165]
    

### argsort()


```python
fives = np.array([10, 5, 15, 20])
fives_order = fives.argsort()

print("The original data", fives)
print("The argsort(): ", fives_order)
print("The asending:", fives[fives_order])
```

    The original data [10  5 15 20]
    The argsort():  [1 0 2 3]
    The asending: [ 5 10 15 20]

