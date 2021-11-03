---
title : python numpy 정리
date : 21-11-01-15:00
tags  : python
categories  : python
---


**라이브러리 불러오기**


```python
import numpy as np
print(np.__version__)
```

    1.19.5
    


```python
temp = np.array([1,2,3])
print(type(temp))
```

    <class 'numpy.ndarray'>
    

# Numpy 배열 생성 및 둘러보기


```python
data1 = [1,2,3]
data1
```




    [1, 2, 3]




```python
data2 = [1,1,2,2,3,4]
data2
```




    [1, 1, 2, 2, 3, 4]




```python
my_array1 = np.array(data1)
print(my_array1)
print(my_array1.shape)
```

    [1 2 3]
    (3,)
    


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




    (4, 3)




```python
my_array4.shape
# 4행과 3열
```




    (4, 3)




```python
my_array5=np.array([[ [1,2] ,[3,4] ], [ [5,6] , [7,8] ]])
my_array5.shape
```




    (2, 2, 2)



# Numpy 기본 함수

##arange
arrang()는 함수 이름에서 알수 있듯이 파이썬 표준 함수인 range()와 유사한 기능을 합니다. 쉽게 생각하면 array를 range()로 표현하는 것입니다. 0부터 함수 인자 값 -1까지의 값을 순차적으로 ndarray의 데이터 값으로 변화해 줍니다.


```python
arrange_array = np.arange(5)
arrange_array
```




    array([0, 1, 2, 3, 4])




```python
arrange_array2 =np.arange(1,9,3)
arrange_array2
```




    array([1, 4, 7])



## zeroes, ones


```python
zeroes_array = np.zeros((3,2))
print(zeroes_array)
print("Data Type is : ", zeroes_array.dtype)
print("Data Type is : " , zeroes_array.shape)
```

    [[0. 0.]
     [0. 0.]
     [0. 0.]]
    Data Type is :  float64
    Data Type is :  (3, 2)
    


```python
ones_array = np.ones((3,4), dtype='int32')
print(ones_array)
print("Data Type is : " , ones_array.dtype)
print("Data Type is : ", ones_array.shape)
```

    [[1 1 1 1]
     [1 1 1 1]
     [1 1 1 1]]
    Data Type is :  int32
    Data Type is :  (3, 4)
    

##reshape
reshape() 메서드는 ndarray를 특정 차원 및 크기로 변환합니다. 변환을 원하는 크기를 함수 인자로 부여하면 됩니다. 


```python
after_reshape = ones_array.reshape(6,2)
print(after_reshape)
print("Data Shape is" , after_reshape.shape)
# 단 6*2의 값과 같은 크기로 변환이 가능하다 EX) (1,12), (2,3,2) etc...
```

    [[1 1]
     [1 1]
     [1 1]
     [1 1]
     [1 1]
     [1 1]]
    Data Shape is (6, 2)
    


```python
after_reshape = ones_array.reshape(2,3,2)
print(after_reshape)
print("Data Shape is" , after_reshape.shape)
```

    [[[1 1]
      [1 1]
      [1 1]]
    
     [[1 1]
      [1 1]
      [1 1]]]
    Data Shape is (2, 3, 2)
    


```python
after_reshape3  = ones_array.reshape(3,-1)
print("reshape(3,-1)? \n")
print(after_reshape3)
print("Data Shape is : " , after_reshape3.shape)
```

    reshape(3,-1)? 
    
    [[1 1 1 1]
     [1 1 1 1]
     [1 1 1 1]]
    Data Shape is :  (3, 4)
    
