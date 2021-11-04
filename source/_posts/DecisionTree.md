---
title: DecisionTree
date: 2021-11-04 11:51:53
tags: machineLearning
---

## Decision Tree

### 개념

- 의사결정트리는 일련의 분류 규칙을 통해 데이터를 분류,회귀하는 지도 학습 모델 중 하나
- 결과 모델이 Tree 구조를 가지고 있기때문에 Decision Tree 라는 이름을 가짐
- 예측 변수를 기반으로 결과를 분류하거나 예측

### 대표적인 의사결정트리 예시

![Decision Tree](/img/tree.PNG)

- 두 가지로 나뉘는 부분들을 분기라 부름
- 분기들중 가장 위에 있는 분기를 루트 노드
- (yes,no) 결정 노드
- 맨 밑에 있는 노드를 잎 노드

![ex](/img/tree2.PNG)



### 의사결정트리 모형 만들기
- 크게 성장(growing),가지치기(pruning)단계를 통하여 만들어진다.
- 성장단계에서는 먼저 최적화할 목적함수를 정한다.
- 가지치기단계에서는 과적합(overfitting)을 방지, 해석이 안되는 규칙등 불필요한 가지를 제거한다.
- 출력 변수가 연속형이면 회귀나무(regression tree)
- 출력 변수가 범주형이면 번류나무(classification)

### 의사결정트리 구현하기
![구현](/img/tree3.PNG)

- 먼저 주어진 데이터의 조건을 확인
- 조건을 만족한 노드의 분리를 멈춘다, 만약 해당 노드가 왼쪽(오른쪽)노드라면 오른쪽(왼쪽)데이터에 대해서 동일한 과정을 반복
- 조건을 만족하지 않는경우 모든 설명 변수에 대해 분리기준 후보생성후 불순도 측정을 이용해 최적 분리기준을 찾고 이를 통해 데이터를 분리한다. 이경우 데이터는 왼쪽과 오른쪽 데이터로 나누어지고 이 2개의 데이터에 대해서 동일한 과정을 반복한다.

### [참조]
- Decision Tree 정리글 URL:https://zephyrus1111.tistory.com/124
- 소스 참고: https://scikit-learn.org/stable/modules/tree.html#regression
- 영상 참고: https://www.youtube.com/results?search_query=decision+tree+