---
title: plotly02
date: 2021-11-09 10:13:17
tags: phython
---
필사
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.graph_objects as go
from warnings import filterwarnings
filterwarnings('ignore')

colors = ['#B1EDED','#B1B2ED','#1DE7ED','#1DA5ED','#1D50ED','#16548E']

df = pd.read_csv('../input/kaggle/kaggle_survey_2021_responses.csv')
df.head()
```
```python
fig = go.Figure( data=[go.Pie(labels = df['Q2'][1:].value_counts().index, # 값에 붙일 이름
                              values = df['Q2'][1:].value_counts().values, # 나타낼 값
                              textinfo = 'label+percent')]) # 그래프 항목당 나타낼 텍스트
fig.update_traces(marker=dict(colors=colors[2:])) # 그래프를 어떤 색으로 표현할 것인지
fig.update_layout(title_text='Gender Distribution', showlegend=False) # 그래프의 레이아웃 설정
fig.show()
```
![gender](/img/gender.PNG)

```python
man = df[df['Q2'] == 'Man']['Q1'].value_counts() # 성별이 남성[df['Q2'] == 'Man']인 행에서 나이['Q1']의 값을 카운트하여 시리즈로 만듦.
woman = df[df['Q2'] == 'Woman']['Q1'].value_counts() # 성별이 여성[df['Q2'] == 'WoMan']인 행에서 나이['Q1']의 값을 카운트하여 시리즈로 만듦.
textonbar_man = [
                    round((m/(m+w))*100, 1) 
                    for m, w in zip(man.values, woman.values)]
textonbar_woman = [
                    round((w/(m+w))*100, 1) 
                    for m, w in zip(man.values, woman.values)]

fig = go.Figure(data=[
                        go.Bar(name='Man', # 막대의 항목이름
                               x=man.index, # x축에 man의 인덱스
                               y=man.values, # y축에 man의 값
                               text=textonbar_man, # 막대의 값을 작성해줄 텍스트
                               marker_color=colors[2]), #막대 색
                        go.Bar(name='Woman', 
                               x=woman.index, 
                               y=woman.values, 
                               text=textonbar_woman, 
                               marker_color=colors[3])
])
fig.update_traces(
                    texttemplate='%{text:.3s}%', # 수치가 그래프에서 어느정도 멀어지는지
                    textposition='inside') # 값의 위치
fig.update_layout(
                    barmode='stack', # 막대의 형태
                    title_text='Age distribution by gender', # 제목
                    xaxis_title='Age', # x축 제목
                    yaxis_title='Counts') # y축 제목
fig.show()
```

![age](/img/age.PNG)

### REFERENCE
https://plotly.com/python-api-reference/index.html

