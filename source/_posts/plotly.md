---
title: plotly
date: 2021-11-08 11:55:57
tags: phython
---
## 코드분석 노트북

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.graph_objects as go
from warnings import filterwarnings
filterwarnings('ignore')

colors = ['#B1EDED','#B1B2ED','#1DE7ED','#1DA5ED','#1D50ED','#16548E']
df = pd.read_csv('../input/kwdoku145/kaggle_survey_2021_responses.csv')
df.head()
```
![kaggle](/img/kaggle.PNG)
```python

##fig > go.Figure > data: 그래프가 그려지는 데이터 담기

fig = go.Figure(data=[go.Pie(labels=df['Q4'][1:].value_counts().index,
                             values=df['Q4'][1:].value_counts().values, textinfo='label+percent')]) 
## go.Pie 원형그래프 
## Q4의 데이터 값을 가져옴 index 내용 / valuses 값
## textinfo='label+percent 표안에 퍼센트와 내용기입

fig.update_traces(marker=dict(colors=colors[2:]))
## 형성된 fig에 추가적인 시각적요소 삽입  /색깔입히기


fig.update_layout(title_text='Formal Education attained or plan to attain in next 2 year', showlegend=False)
## fig > go.Figure > layout: 그래프의 부가정보 기입, 그래프 크기 등 조절 
## 형성된 fig에 레이아웃 계속 업데이트 가능
## title_text=''그래프 제목 / showlegend='False' 범례숨기기
fig.show()
```
![pie](/img/pie.PNG)

## Reference Pie

URL:https://plotly.com/python/reference/pie/

URL:https://github.com/plotly/plotly.py/blob/master/doc/python/pie-charts.md