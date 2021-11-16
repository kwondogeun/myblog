---
title: graph
date: 2021-11-12 12:43:16
tags: phython
---
```python

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.graph_objects as go
from warnings import filterwarnings
filterwarnings('ignore')
colors = ['#B1EDED','#B1B2ED','#1DE7ED','#1DA5ED','#1D50ED','#16548E']
```
```python
#데이터불러오기
df = pd.read_csv('../input/123123123123/kaggle_survey_2021_responses.csv')
df.head()
```

```python
#불러온 데이터값중 분류하고 하는 데이터프레임으로 나누기
df = df[df.Q3.isin(["Japan","China"])]
print(df.shape)
df.sample(5) #5줄로 샘플표시
```

## Age 막대그래프
```python
# 데이터 프레임 정의
df_ch = df[df.Q3.isin(["China"])]
df_ja = df[df.Q3.isin(["Japan"])]
```
```python
df_ch_sort = df_ch['Q1'].value_counts().sort_index()
df_ja_sort = df_ja['Q1'].value_counts().sort_index()
# sort 명령어로 x축 정리
fig = go.Figure(data=[
    go.Bar(name='Japan', x=df_ja_sort.index, y=df_ja_sort.values, marker_color=colors[3]),
    go.Bar(name='China', x=df_ch_sort.index, y=df_ch_sort.values, marker_color=colors[2])])


fig.update_layout(barmode='group', title='China & Japan Age', xaxis_title='Age', yaxis_title='Counts')
fig.show()
```
![age3](/img/age3.PNG)
## Gender Pie 그래프
```python
# 중국데이터프레임을 가지고 파이그래프 그리기
fig = go.Figure(data=[go.Pie(labels=df_ch['Q2'][1:].value_counts().index, values=df_ch['Q2'][1:].value_counts().values, textinfo='label+percent')])
fig.update_traces(marker=dict(colors=colors[2:]))
fig.update_layout(title_text='China Gender Distribution', showlegend=True)
fig.show()
```
![chinagen](/img/chinagen.PNG)

```python
# 일본데이터 프레임을 가지고 파이그래프 그리기
fig = go.Figure(data=[go.Pie(labels=df_ja['Q2'][1:].value_counts().index, values=df_ja['Q2'][1:].value_counts().values, textinfo='label+percent')])
fig.update_traces(marker=dict(colors=colors[2:]))
fig.update_layout(title_text='Japan Gender Distribution', showlegend=True)
fig.show()
```

![japangen](/img/japangen.PNG)


