---
title: plotly03
date: 2021-11-09 10:52:25
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
fig = px.funnel_area(names=df['Q6'][1:].value_counts().index,
                     values=df['Q6'][1:].value_counts().values, title='Coding Experince')
# 피규어 모형: funnel_area 깔때기형 차트, 데이터프레임 Q6 불러오기 및 (index)값 출력, [배열순서 1번행부터 시작], 
# 피규어 모형: funnel_area 깔때기형 차트, 데이터프레임 Q6 불러오기 및 (values)값 출력, [배열순서 1번행부터 시작], 제목 'Coding Experince'
fig.update_traces(marker=dict(colors=colors[::-1]))
# 모형 업데이트: 모형 지정, 색 한칸당 -1 단계씩 변하도록 변경
fig.show()
# 모형 작동
```

![aa](/img/aa.PNG)

```python
#퍼센트 표기 예시용코드
df1 = df['Q1'].value_counts()
df2 = df['Q1'].value_counts(normalize = True)
val_pnt_df = pd.DataFrame({"count":df1,"%":df2*100})

fig = go.Figure()
# [str(x) + ' %' for x in np.round(val_pnt_df["%"].values, 1).tolist()]
# Add Traces
fig.add_bar(x = val_pnt_df.index,
            y = val_pnt_df['count'].values, 
            text = [str(x) + ' %' for x in np.round(val_pnt_df["%"].values, 1).tolist()], 
            textposition="auto")

fig.update_layout(title_text = "Q1. questions[1]")
fig.show()
```

![aaa](/img/aaa.PNG)

```python
df_py = df[(df['Q7_Part_1'] == 'Python')]
df_r = df[(df['Q7_Part_2'] == 'R')]
# 데이터프레임 파이썬 Q7_Part_1 불러오기
# 데이터프레임 R Q7_Part_2 불러오기

fig = go.Figure(data=[
    go.Bar(name='Python', x=df_py['Q1'].value_counts().index, y=df_py['Q1'].value_counts().values, marker_color=colors[2]),
    go.Bar(name='R', x=df_r['Q1'].value_counts().index, y=df_r['Q1'].value_counts().values, marker_color=colors[3])])
# 피규어 생성, 바 이름: 파이썬, x축 파이썬 데이터프레임에 Q1 불러오기, index 고유값 출력
# y축 파이썬 데이터프레임에 Q1 불러오기, values 고유값 출력
# 마커색 2번 (하늘색)
# 바 이름: R, x축 R 데이터프레임에 Q1 불러오기, index 고유값 출력
# y축 R 데이터프레임에 Q1 불러오기, values 고유값 출력
# 마커색 3번 (파랑색)

fig.update_layout(barmode='group', title='Kagglers using Python and R on regular basis by Age', xaxis_title='Age', yaxis_title='Counts')
fig.show()

# 그래프 그룹형, 피규어 타이틀 'Kagglers using Python and R on regular basis by Age', X축 소제목 'Age', Y축 소제목 'Counts'
```

![age2](/img/age2.PNG)
