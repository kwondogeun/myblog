---
title: machine-learning
date: 2021-12-09 11:33:26
tags: machine-learning
---

## iris 데이터를 통한 머신러닝 학습
### 라이브러리 및 데이터 불러오기
```python
# 독립변수 & 종속변수 데이터 불러오기
# 붓꽃 데이터 세트 불러오기
from sklearn.datasets import load_iris


iris = load_iris()
iris_data = iris.data
iris_label = iris.target
print('iris target 값:', iris_label)
print('iris target 명:', iris.target_names)
```

![irisdata](/img/irisdata.PNG)

### 데이터 시각화
* 종별로 구분이 가능한 변수간 산점도 작성
```python
# pandas 라이브러리 불러오기
# 배열을 데이터 프레임으로 변환
# 0,1,2를 순차적으로 setosa,versicolor,virginica로 변경
import pandas as pd

iris_df = pd.DataFrame(iris_data, columns = ["Sepal_Length", "Sepal_Width", "Petal_Length", "Petal_Width"])
iris_df['Species'] = iris.target
iris_df['Species'] = iris_df['Species'].map({0:"setosa", 1:"versicolor", 2:"virginica"})
iris_df.head()

```

![irisdataframe](/img/irisdataframe.PNG)

### 산점도 시각화 작성
```python
import seaborn as sns
import matplotlib.pyplot as plt 

groups = iris_df.groupby('Species')

fig, ax = plt.subplots()

for name, group in groups:

    ax.plot(group.Sepal_Length, group.Sepal_Width, 
            marker='o', 

            linestyle='',

            label=name)

ax.legend(fontsize=10, loc='lower right') 

plt.xlabel('Sepal Length', fontsize=14)
plt.ylabel('Sepal Width', fontsize=14)

plt.show()

```

![irisplt](/img/irisplt.PNG)

### 데이터셋 분리
* 머신러닝 모형학습을 위해서 훈련 데이터셋과 테스트셋으로 구분

```python

from sklearn.model_selection import train_test_split
# 머신러닝 모형을 학습하기 위해 주어진 데이터를 X_train, X_test, y_train, y_test 분리하는 코드를 작성 
X_train, X_test, y_train, y_test = train_test_split(iris_data,  
                                                    iris_label, 
                                                    test_size = 0.2, 
                                                    random_state = 11)

```

### Decision Tree 객체 생성
* 의사결정 트리 모형 생성

```python
# 분류 모형 객체 생성을 위해 라이브러리 및 객체 생성을 정의
from sklearn.tree import DecisionTreeClassifier
dt_clf = DecisionTreeClassifier(random_state=11)
```

### 학습 수행
* DecisionTreeClassifier 객체를 이용해 예측 수행.

```python
dt_clf.fit(X_train, y_train)
```

### 테스트
* 테스트 데이터 세트로 예측 수행
```python
from sklearn.metrics import accuracy_score
pred=dt_clf.predict(X_test)

```

### 예측 정확도
* 예측 성능 평가
```python
from sklearn.metrics import accuracy_score

print('예측 정확도: {0:.4f}'.format(accuracy_score(y_test,pred)))
```
예측 정확도: 0.9333