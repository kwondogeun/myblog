---
title: numpy
date: 2021-11-02 14:21:39
tags: phython
---

## 라이브러리 불러오기
- import numpy as np
- print(np.__version__)
- --(출력) 1.19.5

## Numpy 배열 생성
- data1 =[1,2,3]
   - data1
   - (출력)[1,2,3]
- my_array1 = np.array(data1)
  - print(my_array1)
  - print(my_array1.shape)
  - (출력) [1 2 3]
  - (3,) -->3개들어있기때문

- my_array4 = np.array([[2,4,6],[8,10,12],[14,16,18],[20,22,24]])
   - my_array4.shape
   - 실행시 (4,3)--> 4개의배열안에 3개가 들어있음
## 기본함수
- arange
  - [start,stop,step] step의 크기만큼 일정하게 떨어져있는 숫자를 array형태로 반환
  - 기본값은 start=0 step=1
- zeros,ones
  - zeors:0으로 초기화된 shape차원의 ndarray 배열 객체 반환
  - ones :1로 초기화된 "
- reshape
  - 현재의 배열 차원(1차원,2차원,3차원)을 변경하여 행렬 반환

## Numpy 정렬
- sort()
  - 1차원배열정렬 (x)(-x)
- argsort()
  - fives = np.array([10, 5, 15, 20])
  - fives_order = fives.argsort()
  - print("The original data", fives)
  - print("The argsort(): ", fives_order)
  - print("The asending:", fives[fives_order])
     - (출력) 
     - The original data [10  5 15 20]
     - The argsort():  [1 0 2 3]
     - The asending: [ 5 10 15 20]
